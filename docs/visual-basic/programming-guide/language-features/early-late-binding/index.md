---
title: 早期绑定和后期绑定 (Visual Basic)
ms.custom: ''
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- early binding [Visual Basic]
- objects [Visual Basic], late-bound
- objects [Visual Basic], early-bound
- objects [Visual Basic], late bound
- early binding [Visual Basic], Visual Basic compiler
- binding [Visual Basic], late and early
- objects [Visual Basic], early bound
- Visual Basic compiler, early and late binding
- late binding [Visual Basic]
- late binding [Visual Basic], Visual Basic compiler
ms.assetid: d6ff7f1e-b94f-4205-ab8d-5cfa91758724
caps.latest.revision: 10
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: fa63a250ce6bdf4a8a34d9f1c0284a9d04e75f38
ms.sourcegitcommit: 2042de78fcdceebb6b8ac4b7a292b93e8782cbf5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2018
---
# <a name="early-and-late-binding-visual-basic"></a>早期绑定和后期绑定 (Visual Basic)
Visual Basic 编译器会执行一个过程调用`binding`当一个对象分配给对象变量。 如果对象被分配给声明为特定对象类型的变量，就是*早期绑定*对象。 借助早期绑定对象，编译器可以在应用程序执行前分配内存并执行其他优化。 例如，下面的代码片段将变量声明为类型 <xref:System.IO.FileStream>：  
  
 [!code-vb[VbVbalrOOP#90](../../../../visual-basic/misc/codesnippet/VisualBasic/early-and-late-binding_1.vb)]  
  
 由于 <xref:System.IO.FileStream> 是特定对象类型，因此分配给 `FS` 的实例就是早期绑定对象。  
  
 相反，如果对象被分配给声明为 `Object` 类型的变量，就是*晚期绑定*对象。 虽然这种类型的对象可保留对任何对象的引用，但却没有早期绑定对象的诸多优点。 例如，下面的代码片段将对象变量声明为保留 `CreateObject` 函数返回的对象：  
  
 [!code-vb[VbVbalrOOP#91](../../../../visual-basic/misc/codesnippet/VisualBasic/early-and-late-binding_2.vb)]  
  
## <a name="advantages-of-early-binding"></a>早期绑定的优点  
 应尽量使用早期绑定对象，因为这样编译器可以执行重要优化，从而大大提升应用程序的工作效率。 早期绑定对象的速度远超晚期绑定对象，并明确指出在使用的对象类型，使得代码更易于阅读和维护。 早期绑定到另一个优点是它启用有用的功能，例如自动代码完成和动态帮助，因为 Visual Studio 集成的开发环境 (IDE) 可以确定完全什么类型的对象使用当您编辑代码。 早期绑定降低了运行时错误的数量和严重性，因为它允许编译器在编译程序时报告错误。  
  
> [!NOTE]
>  晚期绑定只能用于访问声明为 `Public` 的类型成员。 访问声明为 `Friend` 或 `Protected Friend` 的成员会导致生成运行时错误。  
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.VisualBasic.Interaction.CreateObject%2A>  
 [对象生存期：如何创建和销毁对象](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)  
 [Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md)
