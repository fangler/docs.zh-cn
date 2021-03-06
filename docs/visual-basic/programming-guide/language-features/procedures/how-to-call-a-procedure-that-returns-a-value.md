---
title: 如何：调用返回值的过程 (Visual Basic)
ms.custom: ''
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- procedure calls [Visual Basic], returning values
- Visual Basic code, procedures
- procedures [Visual Basic], calling
- procedures [Visual Basic], returning a value
ms.assetid: a445127b-0f5f-465a-98fb-3e514b93d115
caps.latest.revision: 15
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: cbaaa5ed17845a7ac8847786fb10111c724015ba
ms.sourcegitcommit: 86adcc06e35390f13c1e372c36d2e044f1fc31ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="how-to-call-a-procedure-that-returns-a-value-visual-basic"></a>如何：调用返回值的过程 (Visual Basic)
A`Function`过程返回到调用代码的一个值。 它通过调用包括其名称和自变量放在右边的赋值语句或表达式中。  
  
### <a name="to-call-a-function-procedure-within-an-expression"></a>调用函数过程在表达式中  
  
1.  使用`Function`过程名称相同的方式将使用变量。 你可以使用`Function`过程调用可以在表达式中使用变量或常量的任何位置。  
  
2.  过程名后面加上括号将自变量列表括起来。 如果不有任何自变量，你可以选择省略括号。 但是，使用括号使得你的代码易于阅读。  
  
3.  将自变量放在括号里，用逗号分隔参数列表中。 请确保你提供的相同顺序的自变量，`Function`过程所定义的相应参数。  
  
     或者，你可以按名称传递一个或多个自变量。 有关详细信息，请参阅[按位置和按名称传递自变量](./passing-arguments-by-position-and-by-name.md)。  
  
4.  从过程返回的值参与值一样的表达式的变量或常数那样。  
  
### <a name="to-call-a-function-procedure-in-an-assignment-statement"></a>在赋值语句中调用函数过程  
  
1.  使用`Function`过程名称之后相等 (`=`) 在赋值语句登录。  
  
2.  过程名后面加上括号将自变量列表括起来。 如果不有任何自变量，你可以选择省略括号。 但是，使用括号使得你的代码易于阅读。  
  
3.  将自变量放在括号里，用逗号分隔参数列表中。 请确保你提供的相同顺序的自变量，`Function`过程所定义的相应参数，除非您要按名称传递它们。  
  
4.  从过程返回的值存储在变量或赋值语句左侧的属性。  
  
## <a name="example"></a>示例  
 下面的示例调用 Visual Basic<xref:Microsoft.VisualBasic.Interaction.Environ%2A>检索操作系统环境变量的值。 第一个行调用`Environ`内一个表达式和第二个行调用它在赋值语句中。 `Environ` 将变量名称作为其唯一的自变量。 它返回到调用代码的变量的值。  
  
 [!code-vb[VbVbcnProcedures#7](./codesnippet/VisualBasic/how-to-call-a-procedure-that-returns-a-value_1.vb)]  
  
## <a name="see-also"></a>请参阅  
 [Function 过程](./function-procedures.md)  
 [过程参数和自变量](./procedure-parameters-and-arguments.md)  
 [Function 语句](../../../../visual-basic/language-reference/statements/function-statement.md)  
 [如何：创建返回值的过程](./how-to-create-a-procedure-that-returns-a-value.md)  
 [如何：从过程返回值](./how-to-return-a-value-from-a-procedure.md)  
 [如何：调用不返回值的过程](./how-to-call-a-procedure-that-does-not-return-a-value.md)
