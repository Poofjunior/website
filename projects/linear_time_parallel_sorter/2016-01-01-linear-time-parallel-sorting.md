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
