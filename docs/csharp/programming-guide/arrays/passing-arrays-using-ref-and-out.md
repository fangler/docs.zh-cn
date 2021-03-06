---
title: "使用 ref 和 out 传递数组（C# 编程指南）"
ms.date: 07/20/2015
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
helpviewer_keywords:
- arrays [C#], passing using ref and out
ms.assetid: 6a2b261e-a1cc-49a6-b4f0-6cacae385a1e
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: f76f63aee0100c6af6bde73c8543b4e7136b1954
ms.sourcegitcommit: 83dd5ec003e788ccb3e33f3412a7af39ae347646
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/15/2018
---
# <a name="passing-arrays-using-ref-and-out-c-programming-guide"></a>使用 ref 和 out 传递数组（C# 编程指南）
与所有 [out](../../../csharp/language-reference/keywords/out-parameter-modifier.md) 参数一样，在使用数组类型的 `out` 参数前必须先为其赋值；即必须由被调用方为其赋值。 例如:  
  
 [!code-csharp[csProgGuideArrays#39](../../../csharp/programming-guide/arrays/codesnippet/CSharp/passing-arrays-using-ref-and-out_1.cs)]  
  
 与所有 [ref](../../../csharp/language-reference/keywords/ref.md) 参数一样，数组类型的 `ref` 参数必须由调用方明确赋值。 因此，不需要由被调用方明确赋值。 可以将数组类型的 `ref` 参数更改为调用的结果。 例如，可以为数组赋以 [null](../../../csharp/language-reference/keywords/null.md) 值，或将其初始化为另一个数组。 例如:  
  
 [!code-csharp[csProgGuideArrays#40](../../../csharp/programming-guide/arrays/codesnippet/CSharp/passing-arrays-using-ref-and-out_2.cs)]  
  
 下面两个示例演示了 `out` 与 `ref` 在将数组传递给方法时的用法差异。  
  
## <a name="example"></a>示例  
 在此示例中，在调用方（`theArray` 方法）中声明数组 `Main`，并在 `FillArray` 方法中初始化此数组。 然后，数组元素将返回调用方并显示。  
  
 [!code-csharp[csProgGuideArrays#37](../../../csharp/programming-guide/arrays/codesnippet/CSharp/passing-arrays-using-ref-and-out_3.cs)]  
  
## <a name="example"></a>示例  
 在此示例中，在调用方（`theArray` 方法）中初始化数组 `Main`，并通过使用 `FillArray` 参数将其传递给 `ref` 方法。 在 `FillArray` 方法中更新某些数组元素。 然后，数组元素将返回调用方并显示。  
  
 [!code-csharp[csProgGuideArrays#38](../../../csharp/programming-guide/arrays/codesnippet/CSharp/passing-arrays-using-ref-and-out_4.cs)]  
  
## <a name="see-also"></a>请参阅  
 [ref](../../../csharp/language-reference/keywords/ref.md)  
 [out 参数修饰符](../../../csharp/language-reference/keywords/out-parameter-modifier.md)  
 [C# 编程指南](../../../csharp/programming-guide/index.md)  
 [数组](../../../csharp/programming-guide/arrays/index.md)  
 [一维数组](../../../csharp/programming-guide/arrays/single-dimensional-arrays.md)  
 [多维数组](../../../csharp/programming-guide/arrays/multidimensional-arrays.md)  
 [交错数组](../../../csharp/programming-guide/arrays/jagged-arrays.md)
