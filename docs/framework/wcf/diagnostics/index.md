---
title: 管理和诊断
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Windows Communication Foundation, diagnostics
- Windows Communication Foundation, administration
- diagnostics [WCF]
- WCF, diagnostics
- administration [WCF]
- WCF, administration
ms.assetid: 34c81c08-0e0f-4fbc-9ae8-91948640ee43
caps.latest.revision: 19
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: fa5256f543a99618e00dc88e085dfee4ac76ebab
ms.sourcegitcommit: 03ee570f6f528a7d23a4221dcb26a9498edbdf8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2018
---
# <a name="administration-and-diagnostics"></a>管理和诊断
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 提供了一组丰富的功能，可帮助监视应用程序生命周期的不同阶段。 例如，您可以在部署时使用配置来设置服务和客户端。 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 包含一个大型性能计数器集合，可帮助您衡量应用程序的性能。 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 还通过 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] Windows Management Instrumentation (WMI) 提供程序在运行时公开服务的检测数据。 当应用程序出现错误或者开始错误操作时，可使用事件日志来了解是否有重大事件发生。 此外，还可以使用消息日志记录和跟踪来从头至尾查看应用程序中发生了哪些事件。 这些功能有助于开发人员和 IT 专业人员在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序运行不正常时进行故障诊断。  
  
> [!NOTE]
>  如果你收到任何特定详细信息的错误，则应启用`includeExceptionDetailInFaults`属性[ \<serviceDebug >](../../../../docs/framework/configure-apps/file-schema/wcf/servicedebug.md)配置元素。 这会指示 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将异常详细信息发送到客户端，使用这些详细信息，可以检测到很多常见问题，而不必进行更高级的诊断。 有关详细信息，请参阅[发送和接收错误](../../../../docs/framework/wcf/sending-and-receiving-faults.md)。  
  
## <a name="diagnostics-features-provided-by-wcf"></a>WCF 提供的诊断功能  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供了以下诊断功能：  
  
-   端到端跟踪提供的检测数据可用于对应用程序进行故障排除而无需使用调试器。 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 输出跟踪进程的里程碑以及错误消息。 这可能包括打开通道工厂或者通过服务主机发送和接收消息。 可以为运行中的应用程序启用跟踪，以监视其进度。 有关详细信息，请参阅[跟踪](../../../../docs/framework/wcf/diagnostics/tracing/index.md)主题。 若要了解如何使用跟踪来调试你的应用程序，请参阅[解决应用程序中使用跟踪](../../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md)主题。  
  
-   消息日志记录用于查看消息在传输前后的情况。 有关详细信息，请参阅[消息日志记录](../../../../docs/framework/wcf/diagnostics/message-logging.md)主题。  
  
-   事件跟踪针对所有主要问题将事件写入事件日志。 然后，可以使用事件查看器检查任何异常情况。 有关详细信息，请参阅[事件日志记录](../../../../docs/framework/wcf/diagnostics/event-logging/index.md)主题。  
  
-   通过性能监视器公开的性能计数器可用于监视应用程序和系统的运行状况。 有关详细信息，请参阅[性能计数器](../../../../docs/framework/wcf/diagnostics/performance-counters/index.md)主题。  
  
-   <xref:System.ServiceModel.Configuration> 命名空间用于加载配置文件和设置服务或客户端终结点。 如果必须将更新部署到很多计算机，可使用对象模型通过脚本对很多应用程序进行更改。 或者，可以使用[配置编辑器工具 (SvcConfigEditor.exe)](../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md)编辑使用 GUI 向导的配置设置。 有关详细信息，请参阅[配置应用程序](../../../../docs/framework/wcf/diagnostics/configuring-your-application.md)主题。  
  
-   WMI 可用于查找哪些服务正在计算机上进行侦听，以及正在使用哪些绑定。 有关详细信息，请参阅[使用 Windows Management Instrumentation 进行诊断](../../../../docs/framework/wcf/diagnostics/wmi/index.md)主题。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 还提供了多个 GUI 和命令行工具，以使创建、部署和管理 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序更加容易。 有关详细信息，请参阅[Windows Communication Foundation 工具](../../../../docs/framework/wcf/tools.md)。 例如，你可以使用[配置编辑器工具 (SvcConfigEditor.exe)](../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md)创建和编辑[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]使用向导，而不直接编辑 XML 的配置设置。 你还可以使用[服务跟踪查看器工具 (SvcTraceViewer.exe)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)若要查看、 分组和筛选跟踪消息，以便可以诊断、 修复和验证问题[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]服务。  
  
## <a name="see-also"></a>请参阅  
 [配置应用程序](../../../../docs/framework/wcf/diagnostics/configuring-your-application.md)  
 [部署服务](../../../../docs/framework/wcf/diagnostics/deploying-services.md)  
 [关于异常的参考信息](../../../../docs/framework/wcf/diagnostics/exceptions-reference/index.md)  
 [事件日志记录](../../../../docs/framework/wcf/diagnostics/event-logging/index.md)  
 [消息日志记录](../../../../docs/framework/wcf/diagnostics/message-logging.md)  
 [配置编辑器工具 (SvcConfigEditor.exe)](../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md)  
 [服务跟踪查看器工具 (SvcTraceViewer.exe)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)  
 [ServiceModel 注册工具](../../../../docs/framework/wcf/diagnostics/servicemodel-registration-tool.md)  
 [跟踪](../../../../docs/framework/wcf/diagnostics/tracing/index.md)  
 [使用 Windows Management Instrumentation 进行诊断](../../../../docs/framework/wcf/diagnostics/wmi/index.md)  
 [性能计数器](../../../../docs/framework/wcf/diagnostics/performance-counters/index.md)  
 [Windows Communication Foundation 工具](../../../../docs/framework/wcf/tools.md)
