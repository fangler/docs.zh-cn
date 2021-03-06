---
title: 外部函数 (F#)
description: '了解如何为本机代码中调用函数的 F # 语言支持。'
author: cartermp
ms.author: phcart
ms.date: 05/16/2016
ms.topic: language-reference
ms.prod: dotnet-fsharp
ms.devlang: fsharp
ms.openlocfilehash: 28e74258d91ff2d9742caa7a6c06f515cd987c0a
ms.sourcegitcommit: 03ee570f6f528a7d23a4221dcb26a9498edbdf8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2018
---
# <a name="external-functions"></a>外部函数

本主题介绍为本机代码中调用函数的 F # 语言支持。

## <a name="syntax"></a>语法

```fsharp
[<DllImport( arguments )>]
extern declaration
```

## <a name="remarks"></a>备注

在上述语法中，*参数*表示自变量，则提供给`System.Runtime.InteropServices.DllImportAttribute`属性。 第一个参数是一个字符串，表示包含此函数，而无需.dll 扩展名的 DLL 的名称。 可以为任何的公共属性提供其他参数`System.Runtime.InteropServices.DllImportAttribute`类，如的调用约定。

假定你具有本机 c + + DLL，它包含以下导出的函数。

```cpp
#include <stdio.h>
extern "C" void __declspec(dllexport) HelloWorld()
{
    printf("Hello world, invoked by F#!\n");
}
```

可以通过使用下面的代码从 F # 中调用此函数。

```fsharp
open System.Runtime.InteropServices

module InteropWithNative =
    [<DllImport(@"C:\bin\nativedll", CallingConvention = CallingConvention.Cdecl)>]
    extern void HelloWorld()

InteropWithNative.HelloWorld()
```

与本机代码的互操作性称为*平台调用*，并且是 CLR 的功能。 有关详细信息，请参阅[与非托管代码交互操作](../../../../docs/framework/interop/index.md)。 该部分中的信息都适用于 F #。


## <a name="see-also"></a>请参阅

[函数](index.md)
