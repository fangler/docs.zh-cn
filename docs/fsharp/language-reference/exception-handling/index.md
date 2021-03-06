---
title: 异常处理 (F#)
description: '了解在 F # 中处理的异常的基础知识和查找异常处理表达式和函数的链接。'
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: dotnet-fsharp
ms.devlang: fsharp
ms.openlocfilehash: 37b33f9387956ee462ff4977dd4ba34a82e89ec6
ms.sourcegitcommit: 03ee570f6f528a7d23a4221dcb26a9498edbdf8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2018
---
# <a name="exception-handling"></a>异常处理

此部分包含 F# 语言中的异常处理支持信息。


## <a name="exception-handling-basics"></a>异常处理基本知识
异常处理是在 .NET Framework 中处理错误条件的标准方法。 因此，任何 .NET 语言都必须支持此机制，包括 F# 在内。 异常是一个封装了有关错误的信息的对象。 发生错误时，将引发异常，并停止常规执行。 而运行时将搜索适当的处理程序来处理异常。 运行时先从当前函数开始搜索，然后在堆栈中向上搜索调用程序的各个层，直至找到匹配的处理程序。 然后，执行找到的处理程序。

此外，随着堆栈的展开，运行时会执行 `finally` 块中的任何代码，从而保证在展开过程中正确地清理对象。


## <a name="related-topics"></a>相关主题

|标题|描述|
|-----|-----------|
|[异常类型](exception-types.md)|介绍如何声明异常类型。|
|[异常：`try...with` 表达式](the-try-with-expression.md)|介绍支持异常处理的语言构造。|
|[异常：`try...finally` 表达式](the-try-finally-expression.md)|介绍一种语言构造，如果在堆栈展开的过程中出现异常，可以通过这种语言构造执行清理代码。|
|[异常：`raise` 函数](the-raise-Function.md)|介绍如何引发异常对象。|
|[异常：`failwith` 函数](the-failwith-function.md)|介绍如何生成常规的 F# 异常。|
|[异常：`invalidArg` 函数](the-invalidArg-function.md)|介绍如何生成无效的参数异常。|
