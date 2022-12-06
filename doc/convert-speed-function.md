---
title: convert_speed() - Azure Data Explorer
description: Learn how to use the convert_speed() function to convert a speed input value from one unit to another.
ms.reviewer: itsagui
ms.topic: reference
ms.date: 11/27/2022
---
# convert_speed

Convert a speed value from one unit to another.

## Syntax

`convert_speed(`*value*`,`*from*`,`*to*`)`

## Parameters

| Name | Type | Required | Description |
|--|--|--|--|
| *value* | real | &check; | The value to be converted. |
| *from* | string | &check; | The unit to convert from. For possible values, see [Conversion units](#conversion-units).|
| *to* | string | &check; | The unit to convert to. For possible values, see [Conversion units](#conversion-units). |

### Conversion units

* CentimeterPerHour
* CentimeterPerMinute
* CentimeterPerSecond
* DecimeterPerMinute
* DecimeterPerSecond
* FootPerHour
* FootPerMinute
* FootPerSecond
* InchPerHour
* InchPerMinute
* InchPerSecond
* KilometerPerHour
* KilometerPerMinute
* KilometerPerSecond
* Knot
* MeterPerHour
* MeterPerMinute
* MeterPerSecond
* MicrometerPerMinute
* MicrometerPerSecond
* MilePerHour
* MillimeterPerHour
* MillimeterPerMinute
* MillimeterPerSecond
* NanometerPerMinute
* NanometerPerSecond
* UsSurveyFootPerHour
* UsSurveyFootPerMinute
* UsSurveyFootPerSecond
* YardPerHour
* YardPerMinute
* YardPerSecond

## Returns

Returns the input value converted from one speed unit to another.

## Example

[**Run the query**](https://dataexplorer.azure.com/clusters/help/databases/Samples?query=H4sIAAAAAAAAAysoyswrUShKLS7NKVGwVUjOzytLLSqJLy5ITU3RMNQz0lFQ900tSS0KSC0KTgXKpqgDRZxT80oyc6HCHvmlReqaAK/HOJBIAAAA)

```kusto
print result = convert_speed(1.2, 'MeterPerSecond', 'CentimeterPerHour')
```

|result|
|---|
|432000|
