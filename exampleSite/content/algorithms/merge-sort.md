---
date: "2020-08-05"
tags: ["algorithm", "algorithms", "programming", "merge", "merge sort", "sort"]
title: "Algorithm of The Day: Merge Sort"
---

There are some approaches when designing an algorithm.
One of them is the **Divide-And-Conquer** approach.

Most of the algorithms are recursive.
They call themselves until the problem is solved, and most of the time they do it by dividing the problem into sub-problems.
Then these sub-problems are solved by the algorithm, finally those results are combined and the main problem is solved.

This is why it is called divide and conquer.

The merge sort is also one of those algorithms that follow this approach.

**Divide**: Divide the n-element set into two sub-sets ( n / 2 )
**Conquer**: Perform the algorithm. Sort the two sub-sets recursively using merge sort.
**Combine**: Merge two sorted sub-sets and produce the result.

Recursion halts when the set to be sorted has 1 element left since it is already sorted, there is no work to be done.