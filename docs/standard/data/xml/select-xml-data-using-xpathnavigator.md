---
title: "使用 XPathNavigator 选择 XML 数据"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
ms.assetid: c268c49e-32b9-4171-b782-dcb7b065fa73
caps.latest.revision: 
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: b7bd12ff29db2d299833d855daaa5de2a3d9ef24
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/23/2017
---
# <a name="select-xml-data-using-xpathnavigator"></a>使用 XPathNavigator 选择 XML 数据
<xref:System.Xml.XPath.XPathNavigator> 类提供一组方法，用于使用 XPath 表达式在 <xref:System.Xml.XPath.XPathDocument> 或 <xref:System.Xml.XmlDocument> 对象中选择节点集。 选择后，可以循环访问所选的节点集。  
  
## <a name="xpathnavigator-selection-methods"></a>XPathNavigator 选择方法  
 <xref:System.Xml.XPath.XPathNavigator> 类提供一组方法，用于使用 XPath 表达式在 <xref:System.Xml.XPath.XPathDocument> 或 <xref:System.Xml.XmlDocument> 对象中选择节点集。 <xref:System.Xml.XPath.XPathNavigator> 类还提供一组经过优化的方法，选择上级节点、子节点和子代节点的速度比使用 XPath 表达式更快。 如果选择单个节点，所选的节点集将在 <xref:System.Xml.XPath.XPathNodeIterator> 对象或 <xref:System.Xml.XPath.XPathNavigator> 对象中返回。  
  
### <a name="selecting-nodes-using-xpath-expressions"></a>使用 XPath 表达式选择节点  
 要使用 XPath 表达式选择节点集，请使用下列选择方法之一。  
  
-   <xref:System.Xml.XPath.XPathNavigator.Select%2A>  
  
-   <xref:System.Xml.XPath.XPathNavigator.SelectSingleNode%2A>  
  
 在调用时，如果选择单个节点，这些方法将返回一组节点，您可以使用 <xref:System.Xml.XPath.XPathNodeIterator> 对象或 <xref:System.Xml.XPath.XPathNavigator> 对象随意浏览。  
  
 使用 <xref:System.Xml.XPath.XPathNodeIterator> 对象浏览不会影响用于创建该对象的 <xref:System.Xml.XPath.XPathNavigator> 对象的位置。 从 <xref:System.Xml.XPath.XPathNavigator> 方法返回的 <xref:System.Xml.XPath.XPathNavigator.SelectSingleNode%2A> 对象位于单个返回的节点上，同样不会影响用于创建该对象的 <xref:System.Xml.XPath.XPathNavigator> 对象的位置。  
  
 以下示例显示如何通过 <xref:System.Xml.XPath.XPathNavigator> 对象创建 <xref:System.Xml.XPath.XPathDocument> 对象、如何使用 <xref:System.Xml.XPath.XPathNavigator.Select%2A> 方法选择 <xref:System.Xml.XPath.XPathDocument> 对象中的节点以及如何使用 <xref:System.Xml.XPath.XPathNodeIterator> 对象循环访问所选的节点。  
  
```vb  
Dim document As XPathDocument = New XPathDocument("books.xml")  
Dim navigator As XPathNavigator = document.CreateNavigator()  
Dim nodes As XPathNodeIterator = navigator.Select("/bookstore/book")  
  
While nodes.MoveNext()  
    Console.WriteLine(nodes.Current.Name)  
End While  
```  
  
```csharp  
XPathDocument document = new XPathDocument("books.xml");  
XPathNavigator navigator = document.CreateNavigator();  
XPathNodeIterator nodes = navigator.Select("/bookstore/book");  
  
while(nodes.MoveNext())  
{  
    Console.WriteLine(nodes.Current.Name);  
}  
```  
  
 该示例使用 `books.xml` 文件作为输入。  
  
 [!code-xml[XPathXMLExamples#1](../../../../samples/snippets/xml/VS_Snippets_Data/XPathXMLExamples/XML/books.xml#1)]  
  
### <a name="optimized-selection-methods"></a>经过优化的选择方法  
 <xref:System.Xml.XPath.XPathNavigator.SelectChildren%2A> 类的 <xref:System.Xml.XPath.XPathNavigator.SelectAncestors%2A>、<xref:System.Xml.XPath.XPathNavigator.SelectDescendants%2A> 和 <xref:System.Xml.XPath.XPathNavigator> 方法表示通常用于检索子节点、子代节点和上级节点的 XPath 表达式。 这些方法的性能已得到优化，比相应的 XPath 表达式速度更快。 <xref:System.Xml.XPath.XPathNavigator.SelectChildren%2A>、<xref:System.Xml.XPath.XPathNavigator.SelectAncestors%2A> 和 <xref:System.Xml.XPath.XPathNavigator.SelectDescendants%2A> 方法基于 <xref:System.Xml.XPath.XPathNodeType> 值或要选择的节点的本地名称和命名空间 URI 选择上级节点、子节点和子代节点。 所选的上级节点、子节点和子代节点将在 <xref:System.Xml.XPath.XPathNodeIterator> 对象中返回。  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Xml.XmlDocument>  
 <xref:System.Xml.XPath.XPathDocument>  
 <xref:System.Xml.XPath.XPathNavigator>  
 [使用 XPath 数据模型处理 XML 数据](../../../../docs/standard/data/xml/process-xml-data-using-the-xpath-data-model.md)  
 [使用 XPathNavigator 计算 XPath 表达式](../../../../docs/standard/data/xml/evaluate-xpath-expressions-using-xpathnavigator.md)  
 [使用 XPathNavigator 匹配节点](../../../../docs/standard/data/xml/matching-nodes-using-xpathnavigator.md)  
 [XPath 查询识别的节点类型](../../../../docs/standard/data/xml/node-types-recognized-with-xpath-queries.md)  
 [XPath 查询和命名空间](../../../../docs/standard/data/xml/xpath-queries-and-namespaces.md)  
 [已编译的 XPath 表达式](../../../../docs/standard/data/xml/compiled-xpath-expressions.md)
