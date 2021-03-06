---
title: 如何：从属性获取值 (Visual Basic)
ms.custom: ''
ms.date: 07/20/2015
ms.prod: .net
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- property values [Visual Basic]
- Visual Basic code, procedures
- values [Visual Basic], properties
- Visual Basic code, properties
- properties [Visual Basic], values
ms.assetid: 3954423e-6ab7-4a4c-b55c-a8d27be47891
caps.latest.revision: 11
author: dotnet-bot
ms.author: dotnetcontent
ms.openlocfilehash: 7161052b9d9b388d8da8bd421c3b220f15037805
ms.sourcegitcommit: 86adcc06e35390f13c1e372c36d2e044f1fc31ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="how-to-get-a-value-from-a-property-visual-basic"></a>如何：从属性获取值 (Visual Basic)
通过将属性名称包含在表达式中检索属性的值。  
  
 该属性的`Get`过程将检索值，但并不按名称显式调用它。 就像你将使用变量，你可以使用该属性。 Visual Basic 使对该属性的过程的调用。  
  
### <a name="to-retrieve-a-value-from-a-property"></a>若要检索属性的值  
  
1.  你将使用的变量的名称相同的方式的表达式中使用的属性名称。 你可以使用属性任意位置，你可以使用变量或常量。  
  
     -或-  
  
     使用以下等的属性名称 (`=`) 在赋值语句登录。  
  
     下面的示例读取的值的 Visual Basic`Now`属性，隐式调用其`Get`过程。  
  
     [!code-vb[VbVbalrDateProperties#4](./codesnippet/VisualBasic/how-to-get-a-value-from-a-property_1.vb)]  
  
2.  如果该属性接受参数，请按照用括号将自变量列表括起来的属性名称。 如果不有任何自变量，你可以选择省略括号。  
  
3.  将自变量放在括号里，用逗号分隔参数列表中。 请确保你提供属性定义的相应参数的相同顺序的自变量。  
  
 属性的值参与像变量表达式或常数那样，或存储在变量或赋值语句左侧的属性。  
  
## <a name="see-also"></a>请参阅  
 [过程](./index.md)  
 [属性过程](./property-procedures.md)  
 [过程参数和自变量](./procedure-parameters-and-arguments.md)  
 [Property 语句](../../../../visual-basic/language-reference/statements/property-statement.md)  
 [在 Visual Basic 中属性和变量之间的差异](./differences-between-properties-and-variables.md)  
 [如何：创建属性](./how-to-create-a-property.md)  
 [如何：声明具有混合访问级别的属性](./how-to-declare-a-property-with-mixed-access-levels.md)  
 [如何：调用 Property 过程](./how-to-call-a-property-procedure.md)  
 [如何： 声明和 Visual Basic 中调用默认属性](./how-to-declare-and-call-a-default-property.md)  
 [如何：在属性中放置值](./how-to-put-a-value-in-a-property.md)
