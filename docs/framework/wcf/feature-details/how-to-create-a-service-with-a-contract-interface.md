---
title: 如何：使用协定接口创建服务
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- csharp
- vb
ms.assetid: 7b6803f6-d6f9-4cc2-9f1b-6f4c920475d5
caps.latest.revision: 9
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: b4af593edd355ed89da8c5b2c79a4c029b966fe4
ms.sourcegitcommit: 94d33cadc5ff81d2ac389bf5f26422c227832052
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2018
---
# <a name="how-to-create-a-service-with-a-contract-interface"></a>如何：使用协定接口创建服务
创建 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 协定的首选方式是使用接口。 此协定指定访问服务提供的操作所必需的消息的集合和结构。 此接口通过将 <xref:System.ServiceModel.ServiceContractAttribute> 类应用到该接口并将 <xref:System.ServiceModel.OperationContractAttribute> 类应用到要公开的方法来定义输入和输出类型。  
  
 有关服务协定的详细信息，请参阅[设计服务协定](../../../../docs/framework/wcf/designing-service-contracts.md)。  
  
### <a name="creating-a-wcf-contract-with-an-interface"></a>使用接口创建 WCF 协定  
  
1.  创建一个新的接口，使用 Visual Basic、 C# 中，或任何将其他公共语言运行时语言。  
  
2.  将 <xref:System.ServiceModel.ServiceContractAttribute> 类应用到该接口。  
  
3.  定义该接口中的方法。  
  
4.  对必须作为公共 <xref:System.ServiceModel.OperationContractAttribute> 协定的一部分公开的每个方法应用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 类。  
  
## <a name="example"></a>示例  
 下面的代码示例演示一个定义服务协定的接口。  
  
 [!code-csharp[c_HowTo_CreateContractWithInterface#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_createcontractwithinterface/cs/source.cs#1)]
 [!code-vb[c_HowTo_CreateContractWithInterface#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_createcontractwithinterface/vb/source.vb#1)]  
  
 默认情况下，应用了 <xref:System.ServiceModel.OperationContractAttribute> 类的方法使用请求-答复消息模式。 有关此消息模式的详细信息，请参阅[如何： 创建请求-答复协定](../../../../docs/framework/wcf/feature-details/how-to-create-a-request-reply-contract.md)。 您还可以通过设置属性 (Attribute) 的属性 (Property) 来创建和使用其他消息模式。 有关更多示例，请参阅[如何： 创建单向协定](../../../../docs/framework/wcf/feature-details/how-to-create-a-one-way-contract.md)和[如何： 创建双工协定](../../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md)。  
  
## <a name="see-also"></a>请参阅  
 <xref:System.ServiceModel.ServiceContractAttribute>  
 <xref:System.ServiceModel.OperationContractAttribute>
