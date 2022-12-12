---
title: cursor_after() - Azure Data Explorer
description: Learn how to use the cursor_after() function to compare the ingestion time of the records of a table against the database cursor time.
ms.reviewer: alexans
ms.topic: reference
ms.date: 11/24/2022
zone_pivot_group_filename: data-explorer/zone-pivot-groups.json
zone_pivot_groups: kql-flavors
---
# cursor_after()

::: zone pivot="azuredataexplorer"

A predicate run over the records of a table to compare their ingestion time against a database cursor.

## Syntax

`cursor_after` `(` *RHS* `)`

## Arguments

* *RHS*: Either an empty string literal, or a valid database cursor value.

## Returns

A scalar value of type `bool` that indicates whether the record was ingested
after the database cursor *RHS* (`true`) or not (`false`).

**Notes**

See [database cursors](../management/databasecursor.md) for additional
details on database cursors.

This function can only be invoked on records of a table which has the
[IngestionTime policy](../management/ingestiontimepolicy.md) enabled.

::: zone-end

::: zone pivot="azuremonitor"

This capability isn't supported in Azure Monitor

::: zone-end
