---
title: 如何：设置 Windows 窗体 DataGridView 控件的大小调整模式
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-winforms
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data grids [Windows Forms], setting sizing modes
- DataGridView control [Windows Forms], sizing modes
ms.assetid: e9ad15e6-b4bb-44aa-a767-3738e9db1651
caps.latest.revision: 16
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 62eb5c9dde5686bf2734e445b9c2a25477a5876f
ms.sourcegitcommit: 2042de78fcdceebb6b8ac4b7a292b93e8782cbf5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2018
---
# <a name="how-to-set-the-sizing-modes-of-the-windows-forms-datagridview-control"></a>如何：设置 Windows 窗体 DataGridView 控件的大小调整模式
以下步骤演示了自定义或组合用于 <xref:System.Windows.Forms.DataGridView> 控件和控件中特定列的调整大小选项的一些常见方案。  
  
### <a name="to-create-a-fixed-width-column"></a>若要创建固定宽度的列  
  
-   将 <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> 属性设置为 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode.None>，<xref:System.Windows.Forms.DataGridViewColumn.Resizable%2A> 属性设置为 <xref:System.Windows.Forms.DataGridViewTriState.False>，<xref:System.Windows.Forms.DataGridViewColumn.ReadOnly%2A> 属性设置为 `true`，并将 <xref:System.Windows.Forms.DataGridViewColumn.Width%2A> 属性设置为适当值。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSizingScenarios#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSizingScenarios/CS/sizingscenarios.cs#10)]
     [!code-vb[System.Windows.Forms.DataGridViewSizingScenarios#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSizingScenarios/vb/sizingscenarios.vb#10)]  
  
### <a name="to-create-a-column-that-adjusts-its-size-to-fit-its-content"></a>若要创建可调整自身大小以完整显示内容的列  
  
-   将 <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A> 属性设置为基于内容调整大小的模式。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSizingScenarios#20](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSizingScenarios/CS/sizingscenarios.cs#20)]
     [!code-vb[System.Windows.Forms.DataGridViewSizingScenarios#20](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSizingScenarios/vb/sizingscenarios.vb#20)]  
  
### <a name="to-create-fill-mode-columns-for-values-of-varying-size-and-importance"></a>若要为其大小和重要性不同的值创建填充模式列  
  
-   将 <xref:System.Windows.Forms.DataGridView.AutoSizeColumnsMode%2A?displayProperty=nameWithType> 属性设置为 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnsMode.Fill>，从而为不会重写此值的所有列设置调整大小模式。 将列的 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 属性设置为与其平均内容宽度成正比的值。 设置重要列的 <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A> 属性以确保显示部分内容。  
  
     [!code-csharp[System.Windows.Forms.DataGridViewSizingScenarios#30](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSizingScenarios/CS/sizingscenarios.cs#30)]
     [!code-vb[System.Windows.Forms.DataGridViewSizingScenarios#30](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSizingScenarios/vb/sizingscenarios.vb#30)]  
  
## <a name="example"></a>示例  
 以下完整的代码示例演示了应用程序，可帮助你了解本主题所描述的调整大小选项。  
  
 [!code-csharp[System.Windows.Forms.DataGridViewSizingScenarios#00](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSizingScenarios/CS/sizingscenarios.cs#00)]
 [!code-vb[System.Windows.Forms.DataGridViewSizingScenarios#00](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.DataGridViewSizingScenarios/vb/sizingscenarios.vb#00)]  
  
 使用此演示应用程序：  
  
-   更改窗体大小。 观察填充模式列如何更改宽度并同时保留 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A> 属性值指示的比例。 观察窗体过小时列的 <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A> 如何防止其进行更改。  
  
-   通过使用鼠标拖动列分隔线，更改列的大小。 观察某些列如何无法调整大小，以及可调整大小的列如何无法比自身最小宽度更窄。  
  
## <a name="compiling-the-code"></a>编译代码  
 此示例需要：  
  
-   对 System 和 System.Windows.Forms 程序集的引用。  
  
 为 Visual Basic 或 Visual C# 中生成此示例从命令行有关的信息，请参阅[从命令行生成](~/docs/visual-basic/reference/command-line-compiler/building-from-the-command-line.md)或[命令行上使用 csc.exe 生成](~/docs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)。 你也可以通过将代码粘贴到新项目中生成 Visual Studio 中的此示例。  另请参阅 [如何：使用 Visual Studio 编译和运行完整的 Windows 窗体代码示例](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\))。  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Windows.Forms.DataGridView>  
 <xref:System.Windows.Forms.DataGridViewColumn.AutoSizeMode%2A?displayProperty=nameWithType>  
 <xref:System.Windows.Forms.DataGridViewAutoSizeColumnMode>  
 <xref:System.Windows.Forms.DataGridViewColumn.Resizable%2A?displayProperty=nameWithType>  
 <xref:System.Windows.Forms.DataGridViewColumn.ReadOnly%2A?displayProperty=nameWithType>  
 <xref:System.Windows.Forms.DataGridViewColumn.Width%2A?displayProperty=nameWithType>  
 <xref:System.Windows.Forms.DataGridViewColumn.FillWeight%2A?displayProperty=nameWithType>  
 <xref:System.Windows.Forms.DataGridViewColumn.MinimumWidth%2A?displayProperty=nameWithType>
