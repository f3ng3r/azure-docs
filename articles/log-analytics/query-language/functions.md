---
title: Functions Azure Log Analytics | Microsoft Docs
description: This article describes how to use functions to call a query from another query in Log Analytics.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: ''
ms.assetid: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 11/15/2018
ms.author: bwren
ms.component: na
---


# Using functions in Azure Monitor Log Analytics

> [!NOTE]
> You should complete [Get started with the Analytics portal](get-started-analytics-portal.md) and [Getting started with queries](get-started-queries.md) before completing this lesson.

[!INCLUDE [log-analytics-demo-environment](../../../includes/log-analytics-demo-environment.md)]


To use a Log Analytics query with another query you can save it as a function. This allows you to simplify complex queries by breaking them into parts and allows you to reuse common code with multiple queries.

## Create a function

Create a function in the Azure portal by clicking **Save** and then providing the information in the following table.

| Setting | Description |
|:---|:---|
| Name           | Display name for the query in **Query explorer**. |
| Save as        | Function |
| Function Alias | Short name to use the function in other queries. May not contain spaces and must be unique. |
| Category       | A category to organize saved queries and functions in **Query explorer**. |

> [!NOTE]
> A function in Log Analytics cannot contain another function.

> [!NOTE]
> Saving a function is possible in Log Analytics queries, but currently not for Application Insights queries.



## Use a function
Use a function by including its alias in another query. It can be used like any other table.

## Example
The following sample query returns all missing security updates reported in the last day. Save this query as a function with the alias _security_updates_last_day_. 

```Kusto
Update
| where TimeGenerated > ago(1d) 
| where Classification == "Security Updates" 
| where UpdateState == "Needed"
```

Create another query and reference the _security_updates_last_day_ function to search for SQL-related needed security updates.

```Kusto
security_updates_last_day | where Title contains "SQL"
```

## Next steps
See other lessons for using the Log Analytics query language:

- [String operations](string-operations.md)
- [Date and time operations](datetime-operations.md)
- [Aggregation functions](aggregations.md)
- [Advanced aggregations](advanced-aggregations.md)
- [JSON and data structures](json-data-structures.md)
- [Joins](joins.md)
- [Charts](charts.md)
