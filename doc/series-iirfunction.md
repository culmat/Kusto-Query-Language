---
title: series_iir() - Azure Data Explorer
description: This article describes series_iir() in Azure Data Explorer.
ms.reviewer: alexans
ms.topic: reference
ms.date: 08/09/2021
---
# series_iir()

Applies an Infinite Impulse Response filter on a series.  

The function takes an expression containing dynamic numerical array as input, and applies an [Infinite Impulse Response](https://en.wikipedia.org/wiki/Infinite_impulse_response) filter. By specifying the filter coefficients, the function can be used:
* to calculate the cumulative sum of the series
* to apply smoothing operations
* to apply various [high-pass](https://en.wikipedia.org/wiki/High-pass_filter), [band-pass](https://en.wikipedia.org/wiki/Band-pass_filter), and [low-pass](https://en.wikipedia.org/wiki/Low-pass_filter) filters

The function takes as input the column containing the dynamic array and two static dynamic arrays of the filter's *a* and *b* coefficients, and applies the filter on the column. It outputs a new dynamic array column, containing the filtered output.  

## Syntax

`series_iir(`*x*`,` *b* `,` *a*`)`

## Arguments

* *x*: Dynamic array of numeric values, typically the resulting output of [make-series](make-seriesoperator.md) or [make_list](makelist-aggfunction.md) operators.
* *b*: Dynamic array of numeric values, containing the numerator coefficients of the filter.
* *a*: Dynamic array of numeric values, containing the denominator coefficients of the filter.

> [!IMPORTANT]
> The first element of `a` (that is, `a[0]`) mustn't be zero, to avoid division by 0. See the [formula below](#the-filters-recursive-formula).

## The filter's recursive formula

* Consider an input array X, and coefficients arrays a and b of lengths n_a and n_b respectively. The transfer function of the filter that will generate the output array Y, is defined by:

<div align="center">
Y<sub>i</sub> = a<sub>0</sub><sup>-1</sup>(b<sub>0</sub>X<sub>i</sub>
 + b<sub>1</sub>X<sub>i-1</sub> + ... + b<sub>n<sub>b</sub>-1</sub>X<sub>i-n<sub>b</sub>-1</sub>
 - a<sub>1</sub>Y<sub>i-1</sub>-a<sub>2</sub>Y<sub>i-2</sub> - ... - a<sub>n<sub>a</sub>-1</sub>Y<sub>i-n<sub>a</sub>-1</sub>)
</div>

## Example

Calculate a cumulative sum. 
Use the iir filter with coefficients *a*=[1,-1] and *b*=[1]:  

<!-- csl: https://help.kusto.windows.net/Samples -->
```kusto
let x = range(1.0, 10, 1);
print x=x, y = series_iir(x, dynamic([1]), dynamic([1,-1]))
| mv-expand x, y
```

**Output**

| x | y |
|:--|:--|
|1.0|1.0|
|2.0|3.0|
|3.0|6.0|
|4.0|10.0|

Here's how to wrap it in a function:

<!-- csl: https://help.kusto.windows.net/Samples -->
```kusto
let vector_sum=(x:dynamic)
{
  let y=array_length(x) - 1;
  toreal(series_iir(x, dynamic([1]), dynamic([1, -1]))[y])
};
print d=dynamic([0, 1, 2, 3, 4])
| extend dd=vector_sum(d)
```

**Output**

|d            |dd  |
|-------------|----|
|`[0,1,2,3,4]`|`10`|
