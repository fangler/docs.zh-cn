---
title: "ServicePointManager.s_ServicePointTable 字段"
ms.date: 05/01/2017
ms.prod: .net-framework
ms.technology: 
ms.topic: reference
topic_type:
- apiref
api_name:
- System.Net.ServicePointManager.s_ServicePointTable
api_location:
- System.dll
api_type:
- Assembly
ms.assetid: 24459679-291c-401a-9def-e42b29466fcf
author: guardrex
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 8dfdbab78d8efab13487575218820f8b0455248d
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2017
---
# <a name="servicepointmanagersservicepointtable-field"></a>ServicePointManager.s\_ServicePointTable 字段

`ServicePointManager.s_ServicePointTable`是<xref:System.Collections.Hashtable>其中包含的活动的 HTTP 连接的列表 (<xref:System.Net.ServicePoint>s) 中<xref:System.AppDomain>。

## <a name="syntax"></a>语法
  
```csharp  
private static Hashtable s_ServicePointTable
```

> [!WARNING]
> `ServicePointManager.s_ServicePointTable`字段是私有，且不是在你的代码中直接使用。
> 
> Microsoft 不支持在生产应用程序在任何情况下使用此字段。

## <a name="requirements"></a>惠?

**Namespace:**<xref:System.Net>

**程序集：**系统 （在 System.dll)

**.NET framework 版本：**自 2.0 之后可用。
