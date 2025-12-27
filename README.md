# benchmark_push_swap

This project is a small personal tool written in C++ to compute the **average number of moves** produced by my `push_swap` program.

It was created for a very simple reason:  
I wanted to know how my algorithm behaved on average, without manually running `push_swap` dozens of times with different inputs.

In short, this project started out of laziness and turned into a useful benchmarking tool.

---

## Purpose

When working on `push_swap`, performance is evaluated based on the number of operations generated for a given input size.

Manually testing random inputs is:
- time-consuming
- error-prone
- not representative of real averages

This program automates that process and provides a clear numerical result.

---

## General Idea

The program repeatedly executes `push_swap` with randomly shuffled inputs and counts how many operations are printed.

For each run:
- a list of numbers is generated
- the list is shuffled
- a subset of numbers is passed to `push_swap`
- the output is captured
- the number of moves is counted by counting newline characters (`'\n'`)

The process is repeated multiple times to compute an average.

---

## Input Generation

A large sequence of integers is generated once (100 000 numbers).

This sequence is shuffled, and depending on the benchmark:
- chunks of **100 numbers**
- or chunks of **500 numbers**

are extracted and passed to `push_swap`.

This allows:
- fast generation of varied inputs
- consistent randomness
- realistic test cases without manual work

---

## Execution

`push_swap` is executed as an external program using `execve`.

A pipe is used to capture its standard output, which contains the list of operations.  
Each newline corresponds to one operation, making the move count trivial to compute.

This keeps the benchmark simple and close to real usage.

---

## Benchmarking

Two benchmarks are performed:
- sorting **100 numbers**
- sorting **500 numbers**

For each case, `push_swap` is executed **100 times** with different shuffled inputs.

At the end of each benchmark, the average number of moves is computed.

---

## Output

The program outputs the average number of operations for each input size.

This information was mainly used to:
- write an accurate README for `push_swap`
- get a concrete idea of the algorithm’s behavior on average

No further optimization was driven by this tool.

---

## Why This Exists

This project does not introduce a new algorithm or technique.

It simply reflects:
- curiosity about actual performance
- willingness to automate repetitive tasks
- the habit of writing small tools to answer concrete questions

---

## Usage

```bash
make
./benchmark_push_swap /path/to/push_swap
```

---

## Author

**Anthony Goldberg** ***agoldber***

42 student – core curriculum completed
