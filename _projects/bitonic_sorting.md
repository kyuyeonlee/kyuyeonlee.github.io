---
layout: page
title: Sorting with GPUs
description: Implementing bitonic sorting using CUDA
img: assets/img/BitonicSort1.svg
importance: 1
category: GATech
---

The following is a bitonic sorting algorithm (<a href="https://en.wikipedia.org/wiki/Bitonic_sorter">source: Wikipedia</a>)with time complexity $$O(n log^2 n)$$ when executed by CPUs. GPUs can take advantage of the innermost loop, where it greatly improves the amortized time complexity.

``` c
// given an array arr of length n, this code sorts it in place
// all indices run from 0 to n-1
for (k = 2; k <= n; k *= 2) // k is doubled every iteration
    for (j = k/2; j > 0; j /= 2) // j is halved at every iteration, with truncation of fractional parts
        for (i = 0; i < n; i++)
            l = bitwiseXOR (i, j); // in C-like languages this is "i ^ j"
            if (l > i)
                if (  (bitwiseAND (i, k) == 0) AND (arr[i] > arr[l])
                   OR (bitwiseAND (i, k) != 0) AND (arr[i] < arr[l]) )
                      swap the elements arr[i] and arr[l]
```

The goal of this project is to implement an efficient CUDA kernel that accelerates bitonic sorting with optimization techniques such as shared memory and pinned memory usage. Check out the report (<a href="https://kyuyeonlee.github.io/">here</a>).