---
title: 协定
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
- WCF [WCF], contracts
- contracts [WCF]
- Windows Communication Foundation [WCF], contracts
ms.assetid: c8364183-4ac1-480b-804a-c5e6c59a5d7d
caps.latest.revision: 7
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: adfa43e411a3b4b71edcac8938851b3abfcda2f8
ms.sourcegitcommit: 94d33cadc5ff81d2ac389bf5f26422c227832052
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2018
---
# <a name="contracts"></a>协定
本节向您演示如何定义和实现 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 协定。 服务协定指定终结点与外界通信的内容。 更具体地说，它是有关一组特定消息的声明，这些消息被组织成基本消息交换模式 (MEP)，如请求/答复、单向和双工。 如果说服务协定是一组在逻辑上相关的消息交换，那么服务操作就是单个消息交换。 例如，`Hello` 操作显然必须接受一条消息（以便调用方能够发出问候），并可能返回也可能不返回一条消息（具体取决于操作的礼节性）。  
  
 有关协定和其他核心更多信息[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]概念，请参阅[基本 Windows Communication Foundation 概念](../../../../docs/framework/wcf/fundamental-concepts.md)。 本主题重点介绍对服务协定的理解。 有关如何构建使用服务协定使用连接到服务的客户端的详细信息，请参阅[WCF 客户端概述](../../../../docs/framework/wcf/wcf-client-overview.md)。 有关客户端通道、 客户端体系结构，以及其他客户端问题的详细信息，请参阅[客户端](../../../../docs/framework/wcf/feature-details/clients.md)。  
  
## <a name="overview"></a>概述  
 本主题对 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的设计和实现提供了高级概念性介绍。 各个子主题提供了有关具体设计和实现细节的更多详细信息。 在设计和实现 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序之前，建议您：  
  
-   了解什么是服务协定、服务协定的工作原理以及如何创建服务协定。  
  
-   了解运行时配置或承载环境可能不支持的协定状态最低要求。  
  
## <a name="service-contracts"></a>服务协定  
 服务协定是一个声明，它提供了有关以下方面的信息：  
  
-   服务中操作的分组方式。  
  
-   针对交换的消息所进行的各种操作的签名。  
  
-   这些消息的数据类型。  
  
-   操作的位置。  
  
-   用于支持与服务成功通信的特定协议和序列化格式。  
  
 例如，采购订单协定可能具有一个 `CreateOrder` 操作，该操作接受订单信息类型输入并返回成功或失败信息，包括一个订单标识符。 它还可能具有一个 `GetOrderStatus` 操作，该操作接受一个订单标识符并返回订单状态信息。 此类服务协定需要指定：  
  
-   采购订单协定由 `CreateOrder` 和 `GetOrderStatus` 操作组成。  
  
-   这些操作指定了输入消息和输出消息。  
  
-   这些消息可以携带的数据。  
  
-   有关成功处理消息所必需的通信基础结构的分类声明。 例如，这些详细信息包括建立成功通信是否需要安全以及需要哪些形式的安全。  
  
 若要表达这种应用程序在其他平台 （包括非 Microsoft 平台） 上的信息，XML 服务协定公开以表示标准 XML 格式，如[Web 服务描述语言 (WSDL)](http://go.microsoft.com/fwlink/?LinkId=87004)和[XML 架构 (XSD)](http://go.microsoft.com/fwlink/?LinkId=87005)，等等。 许多平台的开发人员都可以使用此公共协定信息创建可与该服务通信的应用程序，既因为开发人员理解规范的语言，又因为这些语言通过描述服务支持的公共形式、格式和协议，支持互操作。 详细了解如何[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]句柄这类的信息，请参阅[元数据](../../../../docs/framework/wcf/feature-details/metadata.md)。  
  
 然而，协定可以用多种方式表示，并且尽管 WSDL 和 XSD 语言非常适合以可理解的方式描述服务，但这些语言很难直接使用 — 无论如何，这些语言只能描述服务，而不能描述服务协定实现。 因此，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序使用托管属性、接口和类来定义服务的结构，并且实现服务。  
  
 可以转换得到的在托管类型中定义的协定 (也称为*导出*) 作为元数据 — WSDL 和 XSD-需要时通过客户端或其他服务实施者，尤其是在其他平台上的。 结果可以得到一个简单的编程模型，可以使用公共元数据向任何客户端应用程序描述该模型。 基础 SOAP 消息的详细信息（例如与传输和安全相关的信息）可以留给 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 进行处理，它可以在服务协定类型系统和 XML 类型系统之间自动执行必要的转换。  
  
 有关设计协定的详细信息，请参阅[设计服务协定](../../../../docs/framework/wcf/designing-service-contracts.md)。 有关实现协定的详细信息，请参阅[实现服务协定](../../../../docs/framework/wcf/implementing-service-contracts.md)。  
  
 此外，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 还提供完全在消息级别开发服务协定的功能。 有关开发在消息级别的服务协定的详细信息，请参阅[使用消息协定](../../../../docs/framework/wcf/feature-details/using-message-contracts.md)。 有关开发服务非 SOAP XML 的详细信息，请参阅[与 POX 应用程序互操作性](../../../../docs/framework/wcf/feature-details/interoperability-with-pox-applications.md)。  
  
### <a name="understanding-the-hierarchy-of-requirements"></a>了解需求的层次结构  
 服务协定对操作进行分组；指定消息交换模式 (MEP)、消息类型和这些消息携带的数据类型；并指示某个实现为了支持协定而必须具有的运行时行为的类别（例如，它可能要求对消息进行加密和签名）。 但是，服务协定本身并未明确指定如何满足这些要求，而只是指定这些要求必须得到满足。 加密的类型或消息的签名方式取决于满足这些要求的服务的实现和配置。  
  
 请注意协定为添加行为而对服务协定实现和运行时配置提出特定要求的方式。 为了公开某一服务以供使用而必须满足的这组要求建立于前一组要求之上。 如果协定对实现提出要求，那么实现可能会对配置和绑定提出更多的要求，以便使服务能够运行。 最后，主机应用程序还必须支持服务配置和绑定所添加的任何要求。  
  
 在设计、实现、配置和承载 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务应用程序时，牢记这一累积性要求过程是很重要的。 例如，协定可能会指定需要支持某一会话。 如果是这样，您必须配置绑定以支持该协定性要求，否则服务实现将无法正常工作。 或者，如果你的服务要求集成 Windows 身份验证并在 Internet Information Services (IIS) 中承载，则服务所在的 Web 应用程序必须启用集成 Windows 身份验证并禁用匿名支持。 有关功能和不同的服务主机应用程序类型的影响的详细信息，请参阅[宿主](../../../../docs/framework/wcf/feature-details/hosting.md)。  
  
## <a name="see-also"></a>请参阅  
 [终结点：地址、绑定和协定](../../../../docs/framework/wcf/feature-details/endpoints-addresses-bindings-and-contracts.md)  
 [设计服务协定](../../../../docs/framework/wcf/designing-service-contracts.md)  
 [实现服务协定](../../../../docs/framework/wcf/implementing-service-contracts.md)
