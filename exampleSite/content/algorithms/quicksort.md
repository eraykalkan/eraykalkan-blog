---
date: "2020-08-06"
tags: ["algorithm", "algorithms", "programming", "quick", "quicksort", "sort"]
title: "Algorithm of The Day: Quick Sort"
---

Quick sort also follows the divide-and-conquer approach like merge sort.

It divides the problem into sub-problems and combines the result.

Typical flow for quicksort algorithm is like:

1) Select a value as pivot.
2) Find elements that are greater than pivot and find elements less than pivot.
    -   In this case, we can say we have two arrays. One is to find elements greater than, and the other is to find elements greater less pivot.
    -   When you find an element that is greater than pivot store it and then when you find an element less than pivot store it.
    -   Next, exchange those values in two arrays.
    (Increase i until you find an element greater than pivot, decrease j until you find element that is less than pivot. When i became greater than j, stop because j is now in the position of pivot. swap jth value and pivot in array)
    -   Now, the elements on the left side of pivot is less than pivot and elements on the right side of the pivot are greater than pivot.
    -   If left hand side and right and side is still not sorted, continue.
    -   Pivot is sorted, we have found the position of the pivot. Now for the left hand side and right hand side, perform quick sort again recursively.
    -   Repeat procedure until the array is sorted.
3) Combine results and display result.