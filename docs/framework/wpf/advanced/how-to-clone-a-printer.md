---
title: 如何：克隆打印机
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-wpf
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- print queues [WPF]
- cloning printers [WPF]
- printers [WPF], cloning
- print queues [WPF], cloning
- cloning print queues [WPF]
ms.assetid: dd6997c9-fe04-40f8-88a6-92e3ac0889eb
caps.latest.revision: 8
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 9ffb9f5ab8e7b768d888f5f2800fae668e47bfc3
ms.sourcegitcommit: 2042de78fcdceebb6b8ac4b7a292b93e8782cbf5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2018
---
# <a name="how-to-clone-a-printer"></a>如何：克隆打印机
大多数的企业在某些时候，将购买的同一模型的多个打印机。 通常情况下，这些进行所有安装使用几乎相同的配置设置。 安装每个打印机会很耗时，而且容易出错。 <xref:System.Printing.IndexedProperties?displayProperty=nameWithType>命名空间和<xref:System.Printing.PrintServer.InstallPrintQueue%2A>都通过 Microsoft.NET Framework 公开的类，使可以立即安装任意数目的其他已克隆的打印队列，从现有的打印队列。  
  
## <a name="example"></a>示例  
 在下面的示例中，第二个打印队列克隆现有的打印队列中。 第二个与前者区别仅在其名称、 位置、 端口和共享的状态。 用于执行此操作的主要步骤如下所示。  
  
1.  创建<xref:System.Printing.PrintQueue>要克隆的现有打印机的对象。  
  
2.  创建<xref:System.Printing.IndexedProperties.PrintPropertyDictionary>从<xref:System.Printing.PrintSystemObject.PropertiesCollection%2A>的<xref:System.Printing.PrintQueue>。 <xref:System.Collections.DictionaryEntry.Value%2A>此字典中的每个条目的属性是一个派生自的类型的对象<xref:System.Printing.IndexedProperties.PrintProperty>。 有两种方法在此字典中设置的项值。  
  
    -   使用字典的**删除**和<xref:System.Printing.IndexedProperties.PrintPropertyDictionary.Add%2A>方法来删除此项，然后使用所需的值重新添加它。  
  
    -   使用字典的<xref:System.Printing.IndexedProperties.PrintPropertyDictionary.SetProperty%2A>方法。  
  
     下面的示例阐释了这两种方式。  
  
3.  创建<xref:System.Printing.IndexedProperties.PrintBooleanProperty>对象，并将其<xref:System.Printing.IndexedProperties.PrintProperty.Name%2A>到"IsShared"并将其<xref:System.Printing.IndexedProperties.PrintBooleanProperty.Value%2A>到`true`。  
  
4.  使用<xref:System.Printing.IndexedProperties.PrintBooleanProperty>对象的值<xref:System.Printing.IndexedProperties.PrintPropertyDictionary>的"IsShared"条目。  
  
5.  创建<xref:System.Printing.IndexedProperties.PrintStringProperty>对象，并将其<xref:System.Printing.IndexedProperties.PrintProperty.Name%2A>到"共享名"并将其<xref:System.Printing.IndexedProperties.PrintStringProperty.Value%2A>给适当<xref:System.String>。  
  
6.  使用<xref:System.Printing.IndexedProperties.PrintStringProperty>对象的值<xref:System.Printing.IndexedProperties.PrintPropertyDictionary>的"共享名"条目。  
  
7.  创建另一个<xref:System.Printing.IndexedProperties.PrintStringProperty>对象，并将其<xref:System.Printing.IndexedProperties.PrintProperty.Name%2A>到"位置"并将其<xref:System.Printing.IndexedProperties.PrintStringProperty.Value%2A>给适当<xref:System.String>。  
  
8.  使用第二个<xref:System.Printing.IndexedProperties.PrintStringProperty>对象的值<xref:System.Printing.IndexedProperties.PrintPropertyDictionary>的"位置"条目。  
  
9. 创建的数组<xref:System.String>s。 每个项是端口的服务器上的名称。  
  
10. 使用<xref:System.Printing.PrintServer.InstallPrintQueue%2A>新打印机安装使用新值。  
  
 下面是一个示例。  
  
 [!code-csharp[ClonePrinter#ClonePrinter](../../../../samples/snippets/csharp/VS_Snippets_Wpf/ClonePrinter/CSharp/Program.cs#cloneprinter)]
 [!code-vb[ClonePrinter#ClonePrinter](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/ClonePrinter/visualbasic/program.vb#cloneprinter)]  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Printing.IndexedProperties>  
 <xref:System.Printing.IndexedProperties.PrintPropertyDictionary>  
 <xref:System.Printing.LocalPrintServer>  
 <xref:System.Printing.PrintQueue>  
 <xref:System.Collections.DictionaryEntry>  
 [WPF 中的文档](../../../../docs/framework/wpf/advanced/documents-in-wpf.md)  
 [打印概述](../../../../docs/framework/wpf/advanced/printing-overview.md)
