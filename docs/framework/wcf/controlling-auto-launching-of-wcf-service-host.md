---
title: 控制 WCF 服务主机的自动启动
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- WcfOptions
ms.assetid: 6abe5d34-519b-4cef-8f02-3c0a7f125585
caps.latest.revision: 8
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 5bb6356ba4698cad00d443fdb80b1a45d35e2175
ms.sourcegitcommit: 2042de78fcdceebb6b8ac4b7a292b93e8782cbf5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2018
---
# <a name="controlling-auto-launching-of-wcf-service-host"></a>控制 WCF 服务主机的自动启动
你可以控制的自动启动功能[!INCLUDE[indigo1](../../../includes/indigo1-md.md)]服务主机 (WcfSvcHost.exe)[!INCLUDE[indigo2](../../../includes/indigo2-md.md)]服务库项目，在调试包含多个项目的同一个 Visual Studio 解决方案中另一个项目时。  
  
 为此，请右键单击[!INCLUDE[indigo2](../../../includes/indigo2-md.md)]中的服务项目**解决方案资源管理器**，选择**属性**，然后单击**WCF 选项**选项卡。**时启动 WCF 服务主机调试同一解决方案中的另一个项目**复选框默认处于启用状态。 您可以清除此复选框，这样，在同一解决方案中调试另一个项目时，此特定项目的 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务主机就不会启动。  
  
 此行为不会影响 F5 调试或此项目的“添加服务引用”功能。  
  
 该选项可用于以下项目：  
  
-   [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务库项目。  
  
-   顺序工作流服务库项目。  
  
-   状态机工作流服务库项目。  
  
-   联合服务库项目。  
  
## <a name="see-also"></a>请参阅  
 [WCF 服务主机 (WcfSvcHost.exe)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)
