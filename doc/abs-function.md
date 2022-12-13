---
title: abs() - Azure Data Explorer
description: Learn how to use the function abs() to calculate the absolute value of an input.
ms.reviewer: alexans
ms.topic: reference
ms.date: 11/20/2022
---
# abs()

Calculates the absolute value of the input.

## Syntax

`abs(`*x*`)`

## Parameters

| Name | Type | Required | Description |
| -- | -- | -- | -- |
| *x* | int, real, or timespan | &check; | The value to make absolute. |

## Returns

Absolute value of x.

## Example

> [!div class="nextstepaction"]
> <a href="https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAAAysoyswrUUhMKtbQNdUEADsyYK4NAAAA" target="_blank">Run the query</a>

```kusto
abs(-5)
```

|Result|
|------|
|5|
