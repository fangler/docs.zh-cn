---
title: 如何：在 Windows 窗体内异步加载声音
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
- SoundPlayer class [Windows Forms], loading sounds asynchronously
- sounds [Windows Forms], loading on separate threads
- threading [Windows Forms], sounds
ms.assetid: 3b6a9296-1d5e-4d52-a4ba-94366d6fe302
caps.latest.revision: 18
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: ea84f03088deb7225e90150d9d298f1b64030cc6
ms.sourcegitcommit: 2042de78fcdceebb6b8ac4b7a292b93e8782cbf5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2018
---
# <a name="how-to-load-a-sound-asynchronously-within-a-windows-form"></a>如何：在 Windows 窗体内异步加载声音
以下代码示例从 URL 异步上载了一个声音，然后在新线程中播放。  
  
## <a name="example"></a>示例  
 [!code-csharp[System.Media.SoundPlayer.LoadAsync#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Media.SoundPlayer.LoadAsync/CS/Form1.cs#1)]
 [!code-vb[System.Media.SoundPlayer.LoadAsync#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Media.SoundPlayer.LoadAsync/VB/Form1.vb#1)]  
  
## <a name="compiling-the-code"></a>编译代码  
 此示例需要：  
  
-   对 System 和 System.Windows.Forms 程序集的引用。  
  
-   即，使用有效的文件名替换文件名 `"http://www.tailspintoys.com/sounds/stop.wav"`。  
  
 为 Visual Basic 或 Visual C# 中生成此示例从命令行有关的信息，请参阅[从命令行生成](~/docs/visual-basic/reference/command-line-compiler/building-from-the-command-line.md)或[命令行上使用 csc.exe 生成](~/docs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)。 你也可以通过将代码粘贴到新项目中生成 Visual Studio 中的此示例。  另请参阅 [如何：使用 Visual Studio 编译和运行完整的 Windows 窗体代码示例](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\))。  
  
## <a name="robust-programming"></a>可靠编程  
 文件操作应包含在相应的异常处理块内。  
  
 以下情况可能会导致异常：  
  
-   路径名称格式不正确。 例如，路径名称包含无效的字符或它仅为空白（<xref:System.ArgumentException> 类）。  
  
-   此路径为只读路径（<xref:System.IO.IOException> 类）。  
  
-   此路径名为 `Nothing`（<xref:System.ArgumentNullException> 类）。  
  
-   此路径名过长（<xref:System.IO.PathTooLongException> 类）。  
  
-   此路径无效（<xref:System.IO.DirectoryNotFoundException> 类）。  
  
-   此路径仅为冒号“:”（<xref:System.NotSupportedException> 类）。  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 不要根据文件的名称来判断文件的内容。 例如，文件 `Form1.vb` 可能不是 Visual Basic 源文件。 在应用程序中使用输入的数据之前，需验证所有的输入内容。  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Media.SoundPlayer.LoadAsync%2A>  
 <xref:System.Media.SoundPlayer.LoadCompleted>  
 <xref:System.Media.SoundPlayer.Play%2A>  
 [如何：从 Windows 窗体播放声音](../../../../docs/framework/winforms/controls/how-to-play-a-sound-from-a-windows-form.md)
