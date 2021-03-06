---
title: Hello World 自定义活动
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 72b1dd0a-9aad-47d5-95a9-a1024ee1d0a1
caps.latest.revision: 12
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: fa441a3019b0ef6df31dc0a46be7ea7e8e00a4b8
ms.sourcegitcommit: 2042de78fcdceebb6b8ac4b7a292b93e8782cbf5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2018
---
# <a name="hello-world-custom-activity"></a>Hello World 自定义活动
此示例演示几个重要功能的 Windows Workflow Foundation (WF)，包括如何创建一个简单的自定义活动。 此示例中演示的一些功能使用 C# 创建自定义活动并使用 `in` 和 `out` 参数（<xref:System.Activities.InArgument> 和 <xref:System.Activities.OutArgument>）。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。 在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问 [针对 .NET Framework 4 的 Windows Communication Foundation (WCF) 和 Windows Workflow Foundation (WF) 示例](http://go.microsoft.com/fwlink/?LinkId=150780) 以下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。 此示例位于以下目录：  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Basic\CustomActivities\Code-Bodied\HelloWorld`  
  
## <a name="creating-a-workflow-in-code"></a>使用代码创建工作流  
 在此示例中，使用 C# 代码创建两个自定义活动。 这两个自定义活动直接或间接继承自 <xref:System.Activities.Activity%601> 以返回单个值。 使用泛型返回值（而不是继承自非泛型 <xref:System.Activities.Activity> 类）的好处是：一些活动（例如，<xref:System.Activities.Statements.Assign>）在用作组合活动的一部分时能够访问返回值。  
  
 AppendString  
 此活动继承自 <xref:System.Activities.Activity%601>，并使用一个可将两个字符串连接在一起的 <xref:System.Activities.Statements.Assign> 活动。  
  
 Prepend String  
 此活动直接继承自 <xref:System.Activities.CodeActivity%601>，并且创建与 `AppendString` 活动类似的功能。 活动使用通过代码实现的而不是由预先存在的活动构成的逻辑。  
  
 此项目中包括以下文件。  
  
 AppendString.cs  
 将字符串追加在一起的自定义活动。 它接收一个字符串，并将它组合与文字文本字符串"says 你好 world"，向窗体输出完整的消息。  
  
 PrependString.cs  
 此活动将一个预定义字符串添加到一个输入字符串的前面。  
  
 Sequence1.xaml  
 一个使用 `AppendString` 和 `PrependString` 自定义活动的工作流。  
  
 Program.cs  
 一个运行工作流的程序。  
  
#### <a name="to-use-this-sample"></a>使用此示例  
  
1.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 HelloWorld.sln 解决方案文件。  
  
2.  要生成解决方案，按 Ctrl+Shift+B。  
  
3.  若要运行解决方案，请按 F5。