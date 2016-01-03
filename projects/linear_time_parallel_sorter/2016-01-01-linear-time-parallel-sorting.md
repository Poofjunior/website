---
layout: project_entry
year: 2016
title: Linear-Time Sorter for FPGAs
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

A few head-scratching evenings later--behold--the __Linear-Time-Sorter__ was born!
I'm jazzed to mock this up as an SPI-peripheral for a microcontroller.
Feel free to make use of the [source files](https://github.com/Poofjunior/fpga_fast_serial_sort) as you need.

***

## Behavior

Sorting is performed in linear time _as the unsorted array is being serially clocked into the sorter_.
With this scheme, the sorting is __done__ as soon as the unsorted array has finished being input into the sorting logic. In that sense, it can be read out immediately after it's been clocked in!
The running time on this algorithm is __O(N)__, where __N__ is the number of clock cycles needed before the unsorted array has been sorted.


***

## The Interface

Feel free to interact with the sorting logic directly!
For convenience, though, I've wrapped it up inside an SPI interface.
__N__ unsorted array elements are accepted serially via __N__ sequential spi transfers while the WRITE pin is asserted.
The sorted array can then be immediately clocked out via __N__ more spi transfers while the WRITE pin is released.

For more details on the nuts and bolts behind how the SPI Interface works, check out my [step-by-step guide (PDF)](/projects/linear_time_parallel_sorting/downloads/FPGA_PeripheralExpansion.pdf) that I wrote earler.

***

## The Algorithm

### Questions asked in Parallel

The algorithm boils down to two questions asked in parallel across all cells.
For each cell, we must answer the questions:

1. am I empty or occupied?
2. If occupied, is my current value pushed by either the previous cell value or the new value to be sorted?

Simultaneously, each cell _also_ needs the answer to both of these questions from the previous cell.

Hence, we can build a logical block designed for this specific purpose that answers these questions within a single clock cycle:

### Sorting Cell IOs

![](/projects/linear_time_parallel_sorter/pics/sorting_cell_anatomy.png){: .center-image width="400px"}

Answering the first question involves us keeping track of the cell state as either __empty__ or __occupied__.
Upon reset, the cell state is __empty__, but if data enters the cell it is occupied from that point onward.
Implementation is a simple two-state state machine.

Answering the second question: "am I pushed" is as easy as asking whether or not the new value is strictly less-than the current cell value and the current cell is already occupied:
    
    assign new_data_fits = (new_data < cell_data) || (cell_state == EMPTY);
    assign cell_data_is_pushed = new_data_fits & (cell_state == OCCUPIED);
    

Finally we'll need to make agreements on what happens based on these inputs.

* If the previous cell value is pushed, the input cell _must_ take the previous cell's value.
* If the __previous cell is full__ and the __current cell is empty__ and __previous cell data is pushed__, then the cell must take the previous cell's data.
* If the __previous cell is full__, the __current cell is empty__, and __the previous cell data was not pushed__, then the current cell _must_ take the input data since it is assumed that it is the first empty cell at the bottom of the cell array and the input value is the largest value seen so far since it didn't fit in any of the previous cells.
* In all other cases, the cell keeps its original data.

This logic ends up manifesting itself as a priority decoder:
    
    logic [4:0] priority_vector;
    assign priority_vector [4:0] = {shift_up, new_data_fits, prev_cell_data_pushed,
                              cell_state, prev_cell_state};
    
    /// ... Source File truncated for brevity ...
    
            casez (priority_vector)
                'b0?1??: cell_data <= prev_cell_data;
                'b0101?: cell_data <= new_data;
                'b0?001: cell_data <= new_data;
                'b1????: cell_data <= next_cell_data;
            default: cell_data <= cell_data;
            endcase
    

***

## Example: a "4-sorter" sorting a 4-element array

By setting the SystemVerilog parameters __DATA_WIDTH__ to be 8 and __SIZE__ to be 4, I can generate a "4-sorter" that can sort lists _up to length 4_ in linear time.
Here's a block-diagram of the test setup:

The FPGA logic is wrapped up inside the _sorter_ block, and cells are marked with an _x_ to indicate _empty_.
I've tossed out the SPI interface for now just to highlight the inputs and outputs of the cells to show how they interact with each other.

![](/projects/linear_time_parallel_sorter/pics/test_setup.png){: .center-image width="400px"}

Let's start by following the list behavior as we input unsorted elements in serially.
When we try to insert the first element, each cell compares it to the current stored element in that cell and answer the questions:

* Am I empty or occupied?
* Is my data pushed by the previous cell's value or the new value to be sorted?

Meanwhile it receives the answers to these questions from the previous cell:

* Is the previous cell occupied?
* Is the previous cell pushing its cell value?

The answers to these questions happen within a single clock cycle.
(Senders and receivers of this information, as well as what information was sent, are depicted with arrows below.)

![](/projects/linear_time_parallel_sorter/pics/insert_first_element.png){: .center-image width="400px"}

Upon reset, all elements start off as empty.
To force the first cell to take the first element, I've tied that element's __prev_cell_data_pushed__ input __HIGH__.
In that sense, with an empty list, the first inserted element will always be claimed by the first empty cell.
While other cells are empty, they do not take the first element because each of their respective previous cells are also empty.


On the next clock cycle, we're ready to insert another element and sort it.
Again, each cell asks the same questions and receives the answers to those questions from the previous cell.
Since 3 is less-than 5, the cell holding 5 kicks its data down to the next cell and takes the 3 instead.

![](/projects/linear_time_parallel_sorter/pics/insert_second_element.png){: .center-image width="400px"}

On the next clock cycle we insert a 6. Since all occupied cells contain values less than 6, the 6 goes into the first empty slot.

![](/projects/linear_time_parallel_sorter/pics/insert_third_element.png){: .center-image width="400px"}

On the next clock cycle, we get yet another value, but this time that value forces a "push" on certain elements.

![](/projects/linear_time_parallel_sorter/pics/insert_fourth_element.png){: .center-image width="400px"}



## The Takeaway

It works! If you've got a Teensy and an FPGA floating around your bench, feel free to give it a shot from the [source files](https://github.com/Poofjunior/fpga_fast_serial_sort) and let me know what you think.

Walking in, I tried to nail down the base case of the inputs-and-outputs of a single cell.
Once I could prove that the IOs worked for one, I could prove that they'd work for _N_ and so on!
In the current source code state, I can scale the maximum capacity of the sorter with a single parameter, growing the complexity of the system larger than anything I'd be able to keep track of in my head all at once!
Here lies the beauty of modular design.
If we can solidify the agreements between each of the most fundamental components of our system, we can guarantee and predict their behavior when those same components work together in a largers system.

Even though the problem of fast-sorting seems complicated, the building blocks that form the solution don't have to be.

On the other hand, while this solution saves time with a parallel approach, we're paying a different price in consumed FPGA resources.
Weighing time and space is a game I'll likely need to play in the future.

***