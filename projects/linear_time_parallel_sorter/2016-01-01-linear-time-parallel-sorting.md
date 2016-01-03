---
layout: project_entry
year: 2016
title: FPGA Linear-Time Parallel Sorter
top_image_link: "/projects/linear_time_parallel_sorter/pics/linear_time_sorter.png"
tagline: a parallel approach to a familiar problem
---

# {{ page.title }}

<center>
<img src="{{page.top_image_link}}"
vspace="15px">
</center>

Sorting algorithms are an old hat in the comp-sci community.
Running times on the fastest of these algorithms is usually __O(Nlogn)__ on a
single core.
I thought, with an FPGA, why not try a parallel approach in hardare to bring the running time down to __O(N)__?

This project came about in a notebook at the end of an airplane ride.
A few head-scratching hours later--behold--an fpga implementation was born!
My favorite part is that the sorting is done in linear time _as the unsorted array is being serially clocked into the sorting logic_.
With this scheme, the sorting is __done__ as soon as the unsorted array has finished being input into the sorting logic such that it can be read out immediately after it's been clocked in!
The running time on this algorithm is __O(N)__, where __N__ is the number of clock cycles needed before the unsorted array has been sorted.

I'm thrilled to see this project through to the end mocked up as an SPI-peripheral for a microcontroller.

***

## The Interface

Feel free to interact with the sorting logic directly.
For convenience, though, I've wrapped it up inside an SPI interface.
__N__ unsorted array elements are accepted serially via N sequential spi transfers while the WRITE pin is asserted (1).
The sorted array can then be immediately clocked out via N more spi transfers while the WRITE pin is released (0).

For more details on the nuts and bolts behind how the SPI Interface works, check out my [step-by-step guide (PDF)](/projects/linear_time_parallel_sorting/downloads/FPGA_PeripheralExpansion.pdf) that I wrote earler.

***

## The Algorithm

### Simple Questions asked in Parallel

The algorithm boils down to essentially two simple questions asked in parallel asked across all cells.
For each cell, we must answer the questions:

1. am I empty or occupied?
2. If occupied, is my current value pushed by the current value?

In parallel, each cell also needs the answer to these questions from the previous cell.

Hence, we can build a logical block designed for this specific purpose:

![]("/projects/linear_time_parallel_sorter/clb.png"){: .center-image}

Answering the second question: "am I pushed" is as easy as asking whether or not the new value is strictly less-than the current cell value.

We'll also need to make agreements on what happens based on these inputs.

* If the previous cell value is pushed, the input cell _must_ take the previous cell's value.
* If the previous cell is full and the current cell is empty,
* If the previous cell is full, the current cell is full, and the current cell value is pushed,
* If

I'll spare us the combinational logic for now; let's take a look at the power of answering these two questions with an example.

### Example: a "4-sorter" sorting a 4-element array

By setting the SystemVerilog parameters __DATA_WIDTH__ to be 8 and __SIZE__ to be 4, I can generate a "4-sorter" that can sort lists up to length 4 in linear time.
Here's a block-diagram of the test setup:

The FPGA logic is wrapped up inside the _sorter_ block, and cells are marked with an _x_ to indicate _empty_.
I've tossed out the SPI interface for now just to highlight the inputs and outputs of the cells to show how they interact with each other.

![]("/projects/linear_time_parallel_sorter/test_setup.png"){: .center-image}

Let's start by following the list behavior as we input unsorted elements in serially.
When we try to insert the first element, each cell compares it to the current stored element in that cell and answer the questions:
* Is new_cell_data < current_cell_data ?
* Am I empty or occupied?

Meanwhile it receives the answers to these questions from the previous cell:
* Is the previous cell occupied?
* Is the previous cell pushing its cell data because __prev_cell_data < prev_curr_cell_data__?

The answers to these questions happen within a single clock cycle.
(Senders and receivers of this information, as well as what information was sent, are depicted with arrows below.)

![]("/projects/linear_time_parallel_sorter/insert_first_element.png"){: .center-image}

Upon reset, all elements start off as empty.
To force the first cell to take the first element, I've tied that element's __prev_cell_data_pushed__ input __HIGH__.
In that sense, with an empty list, the first inserted element will always be claimed by the first empty cell.
While other cells are empty, they do not take the first element because each of their respective previous cells are also empty.

On the next clock cycle, we're ready to insert another element and sort it.
Again, each cell asks the same questions and receives the answers to those questions from the previous cell.
Since all occupied cells don't satisfy the first condition, since their values are smaller, the value goes in the first empty slot, just like the previous one.

![]("/projects/linear_time_parallel_sorter/insert_second_element.png"){: .center-image}

On the next clock cycle, the same scenario happens for a third time:

![]("/projects/linear_time_parallel_sorter/insert_third_element.png"){: .center-image}

On the next clock cycle, we get yet another value, but this time that value forces a "push" on certain elements.

![]("/projects/linear_time_parallel_sorter/insert_third_element.png"){: .center-image}



Write more here!


***

Let's say we've synthesized a design that can hold arrays up to _M_ elements long.
Hence, our hardware is essentially a linked list of cells of length _M_.
With this architecture, the end-user can achieve __O(N)__ performance for any input array from 0 up to _M_ elements long.
(Any longer, and they'll need to synthesize more hardware.)
At every clock cycle, _M_ comparisons are made, where _M_ is the total number of cells synthesized on the FPGA.

### Cell Unit Logic


***

***
