---
title: 病毒消息处理
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 8d1c5e5a-7928-4a80-95ed-d8da211b8595
caps.latest.revision: 29
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 6fa35209b2dafc088605848a0dc96a53a2813dfd
ms.sourcegitcommit: 94d33cadc5ff81d2ac389bf5f26422c227832052
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2018
---
# <a name="poison-message-handling"></a>病毒消息处理
A*病毒消息*是一条消息，已超出向应用程序传递尝试最大数量。 当基于队列的应用程序由于错误而无法处理消息时，可能会引起这种情况。 为符合可靠性要求，排队的应用程序是在事务中接收消息的。 中止已接收某个排队消息的事务时，该消息仍会保留在队列中，这样当开始一个新事务时，将对该消息重试操作。 如果导致事务中止的问题未得到更正，则直到超出最大传递尝试次数并导致产生病毒消息时，接收应用程序才会中断接收和中止同一消息的循环。  
  
 消息变为病毒消息的原因有很多。 最常见的是应用程序特定的原因。 例如，如果某个应用程序从队列中读取消息，并执行某些数据库处理，则该应用程序在获取数据库锁时可能会失败，导致中止事务。 因为数据库事务已中止，所以消息仍保留在队列中，这会导致应用程序再次读取消息，并再次尝试获取数据库锁。 如果消息包含无效信息，则也可能变为病毒消息。 例如，采购订单可能包含无效的客户编号。 这种情况下，应用程序可能会自动中止事务，将该消息强制变为病毒消息。  
  
 有时消息可能无法被调度到应用程序，不过，这种情况比较少见。 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 层可能会找到消息的问题所在，例如消息有错误帧、附加到消息的消息凭据无效或操作标头无效。 在上述情况下，应用程序绝不会收到消息；不过，消息仍可能变为病毒消息，可以对其进行手动处理。  
  
## <a name="handling-poison-messages"></a>处理病毒消息  
 在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中，病毒消息处理提供了一种机制，使接收应用程序可以处理无法调度到应用程序的消息、或那些虽然调度到了应用程序但是由于应用程序特定原因而无法进行处理的消息。 病毒消息处理是由每个可用排队绑定中的下列属性配置的：  
  
-   `ReceiveRetryCount`. 一个整数值，指示将某个消息从应用程序队列传递到应用程序的最大重试次数。 默认值为 5。 对于立即重试就可以修复问题（如数据库出现临时死锁）的情况，这个数值已足够了。  
  
-   `MaxRetryCycles`. 一个整数值，指示最大重试周期数。 一个重试周期包括将消息从应用程序队列传送到重试子队列，在经过可配置的延迟后，从重试子队列将消息传送回应用程序队列以便重新尝试传递。 默认值为 2。 在 [!INCLUDE[wv](../../../../includes/wv-md.md)] 中，消息尝试最多 (`ReceiveRetryCount` +1) * (`MaxRetryCycles` + 1) 次。 对于 `MaxRetryCycles` 和 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)]，将忽略 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]。  
  
-   `RetryCycleDelay`. 重试周期之间的时间延迟。 默认值为 30 分钟。 `MaxRetryCycles` 和 `RetryCycleDelay` 共同提供一个机制，用于解决周期性延迟之后重试可修复问题的问题。 例如，这种机制可以处理 SQL Server 挂起的事务提交中锁定的行集。  
  
-   `ReceiveErrorHandling`. 一个枚举，指示对在已尝试过最大重试次数后仍无法传递的消息所采取的操作。 可能的值包括“错误”、“删除”、“拒绝”和“移动”。 默认选项为“错误”。  
  
-   错误。 此选项会向导致 `ServiceHost` 出现错误的侦听器发送一个错误。 必须利用其他一些外部机制将该消息从应用程序中移除，应用程序才能继续处理队列中的消息。  
  
-   删除。 此选项删除病毒消息，该消息永远不会再传递到应用程序。 如果该消息的 `TimeToLive` 属性在此时已过期，那么此消息可能会显示在发送方的死信队列中。 如果不是这种情况，则该消息将不会显示在任何位置。 此选项指示用户尚未指定丢失消息时该如何处理。  
  
-   拒绝。 此选项仅在 [!INCLUDE[wv](../../../../includes/wv-md.md)] 中可用。 选择此选项会指示消息队列 (MSMQ) 将否定确认发送回发送队列管理器，以说明应用程序无法接收该消息。 该消息会放入发送队列管理器的死信队列中。  
  
-   移动。 此选项仅在 [!INCLUDE[wv](../../../../includes/wv-md.md)] 中可用。 选择此选项会将病毒消息移动到病毒消息队列，以供以后由病毒消息处理应用程序进行处理。 病毒消息队列是应用程序队列的子队列。 病毒消息处理应用程序可以是将消息从病毒队列中读取出来的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务。 病毒队列是应用程序队列的子队列，可以解决作为 net.msmq://\<*计算机名*>/*应用*; poison，其中*计算机名*是队列所驻留的计算机的名称和*应用*是应用程序特定队列的名称。  
  
 下面是对消息尝试传递的最大次数：  
  
-   对于 [!INCLUDE[wv](../../../../includes/wv-md.md)]，请用 ((ReceiveRetryCount+1) * (MaxRetryCycles + 1)) 计算。  
  
-   对于 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 和 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]，请用 (ReceiveRetryCount + 1) 计算。  
  
> [!NOTE]
>  对于成功传递的消息，不会再重试传递。  
  
 为了跟踪尝试读取消息的次数，[!INCLUDE[wv](../../../../includes/wv-md.md)] 保留了一个持久性消息属性（用于对中止次数进行计数）和一个移动计数属性（用于对消息在应用程序队列和子队列之间移动的次数进行计数）。 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 通道使用上述属性计算接收重试计数和重试周期计数。 在 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 和 [!INCLUDE[wxp](../../../../includes/wxp-md.md)] 上，中止计数是由 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 通道在内存中维护的，如果应用程序失败，会重置此计数。 另外，在任意时候，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 通道最多只为 256 条消息保留中止计数。 如果读取了第 257 条消息，则时间最早的消息中止计数会被重置。  
  
 中止计数和移动计数属性均可用于通过操作上下文进行的服务操作。 下面的代码示例演示如何访问上述两个属性。  
  
 [!code-csharp[S_UE_MSMQ_Poison#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ue_msmq_poison/cs/service.cs#1)]  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供两种标准排队绑定：  
  
-   <xref:System.ServiceModel.NetMsmqBinding>. 这种 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 绑定适用于执行与其他 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 终结点之间的基于队列的通信。  
  
-   <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>. 这种绑定适用于与现有消息队列应用程序之间的通信。  
  
> [!NOTE]
>  您可以根据 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的要求更改上述绑定中的属性。 对于接收应用程序来说，整个病毒消息处理机制都是本地的。 处理过程对于发送应用程序是不可见的，除非接收应用程序最终停止接收并将否定确认发送回发送方。 这种情况下，该消息会移动到发送方的死信队列中。  
  
## <a name="best-practice-handling-msmqpoisonmessageexception"></a>最佳方案：处理 MsmqPoisonMessageException  
 当服务确定某个消息是病毒消息时，排队传输会引发一个 <xref:System.ServiceModel.MsmqPoisonMessageException>，其中包含病毒消息的 `LookupId`。  
  
 接收应用程序可以实现 <xref:System.ServiceModel.Dispatcher.IErrorHandler> 接口，以处理应用程序要求处理的任何错误。 有关详细信息，请参阅[扩展控件通过错误处理和报表](../../../../docs/framework/wcf/samples/extending-control-over-error-handling-and-reporting.md)。  
  
 应用程序可能要求对病毒消息能进行某种自动处理，也就是将病毒消息移动至病毒消息队列，以便服务可以访问队列中的其他消息。 唯一需要使用错误处理程序机制来侦听病毒消息异常情况的情形是 <xref:System.ServiceModel.Configuration.MsmqBindingElementBase.ReceiveErrorHandling%2A> 设置被设置为 <xref:System.ServiceModel.ReceiveErrorHandling.Fault> 时。 Message Queuing 3.0 的病毒消息示例阐释了这一行为。 下面说明了处理病毒消息应执行的步骤，包括最佳方案：  
  
1.  确保您的病毒消息设置可以反映您的应用程序需要。 在进行设置时，确保您对 [!INCLUDE[wv](../../../../includes/wv-md.md)]、[!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 和 [!INCLUDE[wxp](../../../../includes/wxp-md.md)] 之间消息队列功能的差异有所了解。  
  
2.  如果需要，请实现 `IErrorHandler` 以处理病毒消息错误。 由于将 `ReceiveErrorHandling` 设置为 `Fault` 需要一个手动机制以便将病毒消息移出队列或更正外部相关问题，因此当 `IErrorHandler` 设置为 `ReceiveErrorHandling` 时，该机制的典型用法就是实现 `Fault`，如下面的代码中所示。  
  
     [!code-csharp[S_UE_MSMQ_Poison#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ue_msmq_poison/cs/poisonerrorhandler.cs#2)]  
  
3.  创建服务行为可以使用的 `PoisonBehaviorAttribute`。 该行为会在调度程序上安装 `IErrorHandler`。 请参见下面的代码示例。  
  
     [!code-csharp[S_UE_MSMQ_Poison#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_ue_msmq_poison/cs/poisonbehaviorattribute.cs#3)]  
  
4.  确保您的服务已使用病毒行为属性批注过。  
  
  
  
 另外，如果 `ReceiveErrorHandling` 设置为 `Fault`，则 `ServiceHost` 会在遇到病毒消息时出现错误。 您可以挂钩出错的事件，并关闭服务，采取更正措施，然后重新启动。 例如，可以记下传播到 `LookupId` 的 <xref:System.ServiceModel.MsmqPoisonMessageException> 中的 `IErrorHandler`，当服务主机出错时，您可以使用 `System.Messaging` API 从队列接收消息，同时使用 `LookupId` 从队列中移除该消息，并将该消息存储在外部存储区或其他队列中。 然后，您可以重新启动 `ServiceHost` 以继续正常处理。 [病毒消息处理在 MSMQ 4.0 中](../../../../docs/framework/wcf/samples/poison-message-handling-in-msmq-4-0.md)演示此行为。  
  
## <a name="transaction-time-out-and-poison-messages"></a>事务超时和病毒消息  
 在排队传输通道和用户代码之间可能会出现一类错误。 这类错误可以在中间层（如消息安全层）或服务调度逻辑中检测到。 例如，无论是在 SOAP 安全层中检测到缺少 X.509 证书，还是缺少操作，都会导致不将消息调度到应用程序。 出现这种情况时，服务模型会删除该消息。 因为该消息是在事务中读取的，并且无法提供此事务的结果，所以事务最终会超时、中止，同时该消息会传送回队列中。 也就是说，对于某一类错误，事务不会立即中止，而是一直等待，直到事务超时。您可以使用 <xref:System.ServiceModel.ServiceBehaviorAttribute> 修改服务的事务超时时间。  
  
 若要在计算机范围内更改事务超时时间，请修改 machine.config 文件并设置适当的事务超时时间。需要特别注意，根据在事务中设置的超时时间，事务最终会中止并返回到队列，其中止计数会递增。 最后，消息变为病毒消息，并按照用户的设置进行正确处理。  
  
## <a name="sessions-and-poison-messages"></a>会话和病毒消息  
 会话所经历的重试和病毒消息处理过程与单个消息的经历是一样的。 前面列出的病毒消息属性适用于整个会话。 这意味着整个会话将会重试，并前进到最终病毒消息队列或发送方的死信队列（如果消息被拒绝）。  
  
## <a name="batching-and-poison-messages"></a>批处理和病毒消息  
 如果某条消息变为病毒消息，并且是某个批处理的一部分，则整个批处理将回滚，通道会返回到一次读取一条消息的状态。 有关批处理的详细信息，请参阅[在事务中对消息进行批处理](../../../../docs/framework/wcf/feature-details/batching-messages-in-a-transaction.md)  
  
## <a name="poison-message-handling-for-messages-in-a-poison-queue"></a>对病毒队列中的消息进行病毒消息处理  
 只要有消息放入病毒消息队列中，病毒消息处理就不会结束。 还必须读取和处理病毒消息队列中的消息。 当从最终病毒子队列读取消息时，可以使用病毒消息处理设置的子集。 适用的设置有 `ReceiveRetryCount` 和 `ReceiveErrorHandling`。 您可以将 `ReceiveErrorHandling` 设置为“删除”、“拒绝”或“错误”。 如果 `MaxRetryCycles` 设置为“移动”，`ReceiveErrorHandling` 将被忽略并引发异常。  
  
## <a name="windows-vista-windows-server-2003-and-windows-xp-differences"></a>Windows Vista、Windows Server 2003 和 Windows XP 之间的差异  
 如上所述，并非所有病毒消息处理设置均适用于 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 和 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]。 下面列出了 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)]、[!INCLUDE[wxp](../../../../includes/wxp-md.md)] 和 [!INCLUDE[wv](../../../../includes/wv-md.md)] 上的消息队列在病毒消息处理方面的主要差异：  
  
-   [!INCLUDE[wv](../../../../includes/wv-md.md)] 中的消息队列支持子队列，而 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 和 [!INCLUDE[wxp](../../../../includes/wxp-md.md)] 中的消息队列不支持子队列。 子队列用于病毒消息处理。 重试队列和病毒队列是应用程序队列的子队列，是基于病毒消息处理设置创建的。 `MaxRetryCycles` 用于指示要创建的重试子队列的数量。 因此，当在 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 或 [!INCLUDE[wxp](../../../../includes/wxp-md.md)] 上运行时，`MaxRetryCycles` 会被忽略，并且不允许 `ReceiveErrorHandling.Move`。  
  
-   [!INCLUDE[wv](../../../../includes/wv-md.md)] 中的消息队列支持否定确认，而 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 和 [!INCLUDE[wxp](../../../../includes/wxp-md.md)] 中的消息队列不支持。 来自接收队列管理器的否定确认会致使发送队列管理器将被拒绝的消息放入死信队列。 因此，在 `ReceiveErrorHandling.Reject` 和 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 中不允许 [!INCLUDE[wxp](../../../../includes/wxp-md.md)]。  
  
-   [!INCLUDE[wv](../../../../includes/wv-md.md)] 中的消息队列支持用于记录消息传递尝试次数的消息属性。 此中止计数属性在 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 和 [!INCLUDE[wxp](../../../../includes/wxp-md.md)] 中不可用。 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 会在内存中维护中止计数，所以当场中的多个 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务读取同一消息时，此属性包含的值可能不精确。  
  
## <a name="see-also"></a>请参阅  
 [队列概述](../../../../docs/framework/wcf/feature-details/queues-overview.md)  
 [Windows Vista、Windows Server 2003 和 Windows XP 在排队功能方面的差异](../../../../docs/framework/wcf/feature-details/diff-in-queue-in-vista-server-2003-windows-xp.md)  
 [在协定和服务中指定并处理错误](../../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md)
