---
title: 什么&#39;s.NET 4.5 中的 Windows Workflow Foundation 中的新增功能
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 195c43a8-e0a8-43d9-aead-d65a9e6751ec
caps.latest.revision: 32
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: d862865057f9978a0b815f3026f2ba67c87eac7d
ms.sourcegitcommit: 94d33cadc5ff81d2ac389bf5f26422c227832052
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2018
---
# <a name="what39s-new-in-windows-workflow-foundation-in-net-45"></a>什么&#39;s.NET 4.5 中的 Windows Workflow Foundation 中的新增功能
中的 Windows Workflow Foundation (WF)[!INCLUDE[net_v45](../../../includes/net-v45-md.md)]引入了许多新功能，如新的活动、 设计器的功能和工作流开发模型。 重新承载的工作流设计器支持 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 中引入的许多（但不是全部）新工作流功能。 有关支持的新功能的详细信息，请参阅[重新承载工作流设计器中新 Workflow Foundation 4.5 功能的支持](../../../docs/framework/windows-workflow-foundation/wf-features-in-the-rehosted-workflow-designer.md)。 有关迁移.NET 3.0 和.NET 3.5 工作流应用程序以使用最新版本的详细信息，请参阅[迁移指南](../../../docs/framework/windows-workflow-foundation/migration-guidance.md)。 本主题概述了 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 中引入的新工作流功能。  
  
> [!WARNING]
>  中引入的新 Windows Workflow Foundation 功能[!INCLUDE[net_v45](../../../includes/net-v45-md.md)]对于面向以前版本的 framework 的项目不可用。 如果面向 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 的项目重新面向以前版本的框架，则可能会发生多个问题。  
>   
>  -   C# 表达式将在设计器中替换为消息**值在 XAML 中设置**。  
> -   将发生许多生成错误，包括以下错误。  
>   
>  **文件格式不兼容与当前目标框架。若要转换文件格式，请显式保存文件。保存该文件并重新打开设计器之后，此错误消息将消失。**  
  
##  <a name="BKMK_Versioning"></a> 工作流版本控制  
 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 引入了几个基于新的 <xref:System.Activities.WorkflowIdentity> 类的工作流版本控制功能。 <xref:System.Activities.WorkflowIdentity> 为工作流应用程序提供了一种通过定义来映射持久化工作流实例的机制。  
  
-   使用 <xref:System.Activities.WorkflowApplication> 承载的开发人员可以使用 <xref:System.Activities.WorkflowIdentity> 来启用并行承载多个版本的工作流。 可以使用新的 <xref:System.Activities.WorkflowApplicationInstance> 类来加载持久化工作流实例，然后，主机可以使用 <xref:System.Activities.WorkflowApplicationInstance.DefinitionIdentity%2A> 在实例化 <xref:System.Activities.WorkflowApplication> 时提供工作流定义的正确版本。 有关详细信息，请参阅[使用 WorkflowIdentity 和版本控制](../../../docs/framework/windows-workflow-foundation/using-workflowidentity-and-versioning.md)和[How to： 主机多个版本的工作流通过并行](../../../docs/framework/windows-workflow-foundation/how-to-host-multiple-versions-of-a-workflow-side-by-side.md)。  
  
-   <xref:System.ServiceModel.WorkflowServiceHost> 现在是多版本主机。 在部署工作流服务的新版本时，将使用新的服务创建新实例，但会使用以前的版本来完成现有实例。 有关详细信息，请参阅[WorkflowServiceHost 中的并行版本控制](../../../docs/framework/wcf/feature-details/side-by-side-versioning-in-workflowservicehost.md)。  
  
-   引入了动态更新，其提供了一种更新持久化工作流实例定义的机制。 有关详细信息，请参阅[动态更新](../../../docs/framework/windows-workflow-foundation/dynamic-update.md)和[如何： 更新运行的工作流实例的定义](../../../docs/framework/windows-workflow-foundation/how-to-update-the-definition-of-a-running-workflow-instance.md)。  
  
-   SqlWorkflowInstanceStoreSchemaUpgrade.sql 数据库脚本旨在用于升级使用 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] 数据库脚本创建的持久性数据库。 此脚本会更新 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] 持久性数据库以支持 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 中引入的版本控制功能。 数据库中的持久化工作流实例将获得默认的版本控制值，然后就可以参与并行执行和动态更新。 有关详细信息，请参阅[升级.NET Framework 4 持久性数据库到支持工作流版本控制](../../../docs/framework/windows-workflow-foundation/using-workflowidentity-and-versioning.md#UpdatingWF4PersistenceDatabases)。  
  
##  <a name="BKMK_NewActivities"></a> 活动  
 内置活动库包含新活动和现有活动的新功能。  
  
###  <a name="BKMK_NoPersistScope"></a> NoPersist 范围  
 <xref:System.Activities.Statements.NoPersistScope> 是一个在执行 NoPersistScope 的子活动时防止工作流持久保存的新容器活动。 此活动在工作流不适合持久保存的方案中十分有用，例如，当工作流使用计算机特定资源（如文件句柄）时或在执行数据库事务期间。 以前，为防止在活动执行期间出现持久性，需要一个使用 <xref:System.Activities.NativeActivity> 的自定义 <xref:System.Activities.NoPersistHandle>。  
  
###  <a name="BKMK_NewFlowchartCapabilities"></a> 新流程图功能  
 流程图将针对 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 进行更新，并具有以下新功能：  
  
-   `DisplayName` 或 <xref:System.Activities.Statements.FlowSwitch%601> 活动的 <xref:System.Activities.Statements.FlowDecision> 属性是可编辑的。 这样，活动设计器就可以显示有关该活动的用途的详细信息。  
  
-   流程图具有一个名为 <xref:System.Activities.Statements.Flowchart.ValidateUnconnectedNodes%2A> 的新属性；此属性的默认值为 `False`。 如果此属性设置为 `True`，则未连接的流程图节点将产生验证错误。  
  
## <a name="support-for-partial-trust"></a>支持部分信任  
 在 [!INCLUDE[netfx40_long](../../../includes/netfx40-long-md.md)] 中的工作流需要完全信任的应用程序域。 在 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 中，工作流可以在部分信任环境中运行。 在部分信任环境中，可以使用第三方组件而无需为其授予主机资源的完全访问权限。 关于在部分信任中运行的工作流，请注意以下几点：  
  
1.  在部分信任下，不支持使用 <xref:System.Activities.Statements.Interop> 活动中包含的旧组件（包括规则）。  
  
2.  不支持 <xref:System.ServiceModel.WorkflowServiceHost> 中在部分信任下运行的工作流。  
  
3.  在部分信任方案中持久保留异常是一种潜在安全威胁。 若要禁用异常的持久保留，必须将扩展类型 <xref:System.Activities.ExceptionPersistenceExtension> 添加至项目，以便取消持久化异常。 下面的代码示例演示如何实现此类型。  
  
    ```  
    public class ExceptionPersistenceExtension   
    {  
        public ExceptionPersistenceExtension()   
        {   
            this.PersistExceptions = false;   
        }   
        public bool PersistExceptions { get; set; }   
    }  
    ```  
  
     如果无需对异常进行序列化，请确保在 <xref:System.Activities.Statements.NoPersistScope> 内使用异常。  
  
4.  活动作者应重写 <xref:System.Activities.Activity.CacheMetadata%2A> 以避免让工作流运行时针对该类型自动执行反射。 参数和子活动必须为非 null，并且 <xref:System.Activities.ActivityMetadata.Bind%2A> 必须被显式调用。 有关详细信息重写<xref:System.Activities.Activity.CacheMetadata%2A>，请参阅[使用 CacheMetadata 公开数据](../../../docs/framework/windows-workflow-foundation/exposing-data-with-cachemetadata.md)。 此外，这些是为类型自变量的实例`internal`或**私有**必须以显式创建<xref:System.Activities.Activity.CacheMetadata%2A>以避免反射的创建。  
  
5.  这些类型不会使用 <xref:System.Runtime.Serialization.ISerializable> 或 <xref:System.SerializableAttribute> 来进行序列化；要进行序列化的类型必须支持 <xref:System.Runtime.Serialization.DataContractSerializer>。  
  
6.  使用 <xref:System.Activities.Expressions.LambdaValue%601> 的表达式需要 <xref:System.Security.Permissions.ReflectionPermissionAttribute.RestrictedMemberAccess%2A>，因此不能在部分信任下使用。 使用 <xref:System.Activities.Expressions.LambdaValue%601> 的工作流应将这些表达式替换为派生自 <xref:System.Activities.CodeActivity%601> 的活动。 .  
  
7.  在部分信任下，不能使用 <xref:System.Activities.XamlIntegration.TextExpressionCompiler> 或 Visual Basic 承载的编译器来编译表达式，但是可以运行以前编译的表达式。  
  
8.  使用的单个程序集[2 级透明度](http://aka.ms/Level2Transparency)不能在[!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)]，[!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)]以完全信任和[!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)]在部分信任环境中。  
  
##  <a name="BKMK_NewDesignerCapabilites"></a> 新设计器功能  
  
###  <a name="BKMK_DesignerSearch"></a> 设计器搜索  
 为了使较大的工作流程更易于管理，现在可以按关键字来搜索工作流。 此功能选项仅适用于 Visual Studio;此功能不可用在重新承载设计器中。 提供了两种搜索：  
  
-   快速查找，使用启动**Ctrl + F**或**编辑**，**查找和替换**，**快速查找**。  
  
-   查找在文件中，使用启动**Ctrl + Shift + F**或**编辑**，**查找和替换**，**在文件中查找**。  
  
 请注意，不支持替换。  
  
####  <a name="BKMK_QuickFind"></a> 快速查找  
 在工作流中搜索的关键字将匹配下列设计器项：  
  
-   <xref:System.Activities.Activity> 对象、<xref:System.Activities.Statements.FlowNode> 对象、<xref:System.Activities.Statements.State> 对象、<xref:System.Activities.Statements.Transition> 对象以及其他自定义流控制项的属性。  
  
-   变量  
  
-   参数  
  
-   表达式  
  
 在设计器上的 <xref:System.Activities.Presentation.Model.ModelItem> 树上执行快速查找。 快速查找不会查找在工作流定义中导入的命名空间。  
  
####  <a name="BKMK_FindInFiles"></a> 在文件中查找  
 在工作流中搜索的关键字将匹配工作流文件的实际内容。 搜索结果将显示在 Visual Studio 查找结果视图窗格中。 双击结果项将会定位到包含工作流设计器中的匹配项的活动。  
  
###  <a name="BKMK_VariableDeleteContextMenu"></a> 删除变量和自变量设计器中的上下文菜单项  
 在 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] 中，只能使用键盘来删除设计器中的变量和参数。 从 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 开始，可以使用上下文菜单来删除变量和参数。  
  
 以下屏幕快照显示了变量和自变量设计器的上下文菜单。  
  
 ![变量和自变量设计器上下文菜单](../../../docs/framework/windows-workflow-foundation/media/designercontextmenu.png "DesignerContextMenu")  
  
###  <a name="BKMK_AutoSurround"></a> 自动包围与序列  
 由于工作流或特定容器活动（如 <xref:System.Activities.Statements.NoPersistScope>）只能包含单个主体活动，因此添加第二个活动需要开发人员删除第一个活动，请添加一个 <xref:System.Activities.Statements.Sequence> 活动，然后将两个活动都添加到该顺序活动中。 从 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 开始，向设计器图面添加第二个活动时，将会自动创建 `Sequence` 活动以包装两个活动。  
  
 以下屏幕快照显示了 `WriteLine` 的 `Body` 中的 `NoPersistScope` 活动。  
  
 ![自动&#45;包围放置位置](../../../docs/framework/windows-workflow-foundation/media/autosurround1.png "AutoSurround1")  
  
 以下屏幕快照显示了在第一个 `Sequence` 下面丢弃第二个时在 `Body` 中自动创建的 `WriteLine` 活动。  
  
 ![自动创建的序列活动](../../../docs/framework/windows-workflow-foundation/media/autosurround2.png "AutoSurround2")  
  
###  <a name="BKMK_PanMode"></a> 平移模式  
 若要更轻松地在设计器中浏览大型工作流，可以启用平移模式；通过此模式，开发人员可以单击并拖动工作流的可见部分将其移动，而无需使用滚动条。 用于激活平移模式的按钮位于设计器的右下角。  
  
 下面的屏幕快照显示了位于工作流设计器右下角的平移按钮。  
  
 ![在工作流设计器中的平移按钮](../../../docs/framework/windows-workflow-foundation/media/panbutton.png "PanButton")  
  
 也可以使用鼠标中键或空格键来平移工作流设计器。  
  
###  <a name="BKMK_MultiSelect"></a> 多重选择  
 通过拖动围绕活动的矩形（未启用平移模式时）或通过按住 Ctrl 键并逐一单击所需的活动，可以一次选择多个活动。  
  
 也可以在设计器中拖动并放置多个选择的活动，并使用上下文菜单与这些活动交互。  
  
###  <a name="BKMK_DocumentOutline"></a> 工作流项的大纲视图  
 为了更加方便地浏览分层工作流，工作流的组件显示在树样式的大纲视图中。 大纲视图将显示在**文档大纲**视图。 若要打开此视图中，从顶部菜单中，选择**视图**，**其他窗口**，**文档大纲**，或按 Ctrl W、 u。 单击大纲视图中的节点将会定位到工作流设计器中的相应活动，并且该大纲视图将会更新以显示在设计器中选择的活动。  
  
 从完成的工作流的以下屏幕截图[入门教程](../../../docs/framework/windows-workflow-foundation/getting-started-tutorial.md)显示大纲视图中的，一个顺序工作流。  
  
 ![大纲视图中工作流设计器](../../../docs/framework/windows-workflow-foundation/media/outlineviewinworkflowdesigner.jpg "OutlineViewinWorkflowDesigner")  
  
###  <a name="BKMK_CSharpExpressions"></a> C# 表达式  
 在 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 之前，工作流中的所有表达式只能用 Visual Basic 来编写。 在 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 中，Visual Basic 表达式仅用于使用 Visual Basic 创建的项目。 Visual C# 项目现在将 C# 用于表达式。 提供了功能完全的 C# 表达式编辑器，包括语法突出显示和 Intellisense 等功能。 在使用 Visual Basic 表达式的以前版本中创建的 C# 工作流项目仍可继续使用。  
  
 将在设计时对 C# 表达式进行验证。 C# 表达式中的错误将标有红色波浪形下划线。  
  
 有关 C# 表达式的详细信息，请参阅[C# 表达式](../../../docs/framework/windows-workflow-foundation/csharp-expressions.md)。  
  
###  <a name="BKMK_Visibility"></a> Shell 栏和标头的可见性的更多控制项  
 在重新承载的设计器中，某些标准 UI 控件可能对于给定的工作流没有意义，并可能已关闭。 在 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] 中，此自定义仅受设计器底部的 shell 栏支持。 在 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 中，可通过用合适的 <xref:System.Activities.Presentation.View.DesignerView.WorkflowShellHeaderItemsVisibility%2A> 值设置 <xref:System.Activities.Presentation.View.ShellHeaderItemsVisibility> 来调整设计器顶部 shell 标头项的可见性。  
  
###  <a name="BKMK_AutoConnect"></a> 自动连接和流程图和状态机工作流中的自动插入  
 在 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] 中，必须手动添加流程图工作流中节点之间的连接。 在 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 中，流程图和状态机节点具有自动连接点，这些自动连接点会在将一个活动从工具箱拖到设计器图面上时变为可见。 将活动放置在这些点中的一个点上会自动添加该活动以及必要的连接。  
  
 下面的屏幕快照显示了从工具箱中拖动活动时变为可见的附属点。  
  
 ![显示自动连接点的流程图起始节点](../../../docs/framework/windows-workflow-foundation/media/autoconnect1.png "Autoconnect1")  
  
 也可以将活动拖动到流程图节点和状态之间的连接上，以在两个其他节点之间自动插入该节点。 以下屏幕快照显示了突出显示的连接线，可在此连接线处从工具箱拖动并放置活动。  
  
 ![自动&#45;插入放置活动的句柄](../../../docs/framework/windows-workflow-foundation/media/autoinsert.png "自动插入")  
  
###  <a name="BKMK_Annotations"></a> 设计器批注  
 为促进开发较大型的工作流，设计器现在支持添加批注以帮助跟踪设计过程。 可以向活动、状态、流程图节点、变量和参数添加批注。 以下屏幕快照显示了用于将批注添加到设计器的上下文菜单。  
  
 ![注释上下文菜单](../../../docs/framework/windows-workflow-foundation/media/annotationdialog.png "annotationdialog")  
  
### <a name="debugging-states"></a>调试状态  
 在 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] 中，非活动元素不支持调试断点，因为这些元素不是执行单位。 此版本提供了一种向 <xref:System.Activities.Statements.State> 对象添加断点的机制。 若在 <xref:System.Activities.Statements.State> 上设置了断点，则执行将在计划了状态入口活动或触发器之前、状态发生转换时中断。  
  
###  <a name="BKMK_ActivityDelegates"></a> 定义和使用 ActivityDelegate 对象在设计器  
 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] 中的活动使用 <xref:System.Activities.ActivityDelegate> 对象来公开执行点，在这些执行点处，工作流的其他部分可与工作流的执行交互；但是，使用这些执行点通常需要数量相当大的代码。 在此版本中，开发人员可以使用工作流设计器来定义和使用活动委托。 有关详细信息，请参阅[如何： 定义和使用工作流设计器中的活动委托](/visualstudio/workflow-designer/how-to-define-and-consume-activity-delegates-in-the-workflow-designer)。  
  
###  <a name="BKMK_BuildTimeValidation"></a> 生成时验证  
 在 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] 中，不会将生成工作流项目期间的工作流验证错误计为生成错误。 这意味着即使存在工作流验证错误，工作流项目的生成也可能成功。 在 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 中，工作流验证错误会导致生成失败。  
  
###  <a name="BKMK_DesignTimeValidation"></a> 设计时后台验证  
 在 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] 中，会把工作流作为前台进程进行验证，这可能会在复杂或耗时的验证过程中将 UI 挂起。 工作流验证现在发生在后台线程上，因此不会阻止 UI。  
  
###  <a name="BKMK_ViewState"></a> 位于 XAML 文件中的单独位置视图状态  
 在 [!INCLUDE[netfx40_short](../../../includes/netfx40-short-md.md)] 中，工作流的视图状态信息存储在 XAML 文件中的许多不同位置。 这对于想直接读取 XAML 或编写用于删除视图状态信息的代码的开发人员来说很不方便。 在[!INCLUDE[net_v45](../../../includes/net-v45-md.md)]，XAML 文件中的视图状态信息序列化为 XAML 文件中的一个单独的元素。  开发人员可以轻松地找到和编辑视图状态信息的一项活动，或完全删除的视图状态。  
  
###  <a name="BKMK_ExpressionExtensibility"></a> 表达式扩展性  
 在 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 中，我们为开发人员提供了一种创建自己的表达式并可将表达式创作体验插入到工作流设计器中的方法。  
  
###  <a name="BKMK_BackwardCompatRehostedDesigner"></a> 重新承载的设计器中 Workflow 4.5 功能的选择性加入  
 为保留向后兼容性，默认情况下，包括在 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 中的一些新功能不会在重新承载的设计器中启用。 这是为了确保使用重新承载的设计器的现有应用程序不会由于更新至最新版本而中断。 若要启用重新承载的设计器中的新功能，可将 <xref:System.Activities.Presentation.DesignerConfigurationService.TargetFrameworkName%2A> 设置为“.NET Framework 4.5”，或设置 <xref:System.Activities.Presentation.DesignerConfigurationService> 的各成员以启用各个功能。  
  
##  <a name="BKMK_NewWFModels"></a> 新工作流开发模型  
 除流程图和顺序工作流开发模型外，此版本还包括状态机工作流和协定优先工作流服务。  
  
###  <a name="BKMK_StateMachine"></a> 状态机工作流  
 状态机工作流已作为.NET Framework 4 中的版本 4.0.1 的一部分引入[Microsoft.NET Framework 4 平台更新 1](http://go.microsoft.com/fwlink/?LinkID=215092)。 此更新包括多个新类和活动，允许开发人员创建状态机工作流。 这些类和活动已针对 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 进行更新。 更新包括：  
  
1.  能够对状态设置断点  
  
2.  能够在工作流设计器中复制和粘贴转换  
  
3.  设计器支持共享触发器转换创建  
  
4.  用于创建状态机工作流的活动，包括：<xref:System.Activities.Statements.StateMachine>、<xref:System.Activities.Statements.State> 和 <xref:System.Activities.Statements.Transition>  
  
 以下屏幕截图显示完成的状态机工作流从[入门教程](../../../docs/framework/windows-workflow-foundation/getting-started-tutorial.md)步骤[如何： 创建状态机工作流](../../../docs/framework/windows-workflow-foundation/how-to-create-a-state-machine-workflow.md)。  
  
 ![已完成状态机工作流](../../../docs/framework/windows-workflow-foundation/media/wfstatemachinegettingstartedtutorialcomplete.JPG "WFStateMachineGettingStartedTutorialComplete")  
  
 有关创建状态机工作流的详细信息，请参阅[状态机工作流](../../../docs/framework/windows-workflow-foundation/state-machine-workflows.md)。  
  
###  <a name="BKMK_ContractFirst"></a> 协定优先工作流开发  
 协定优先工作流开发工具允许开发人员可以先，设计一个协定在代码中的，然后在 Visual Studio 中单击几下，自动生成活动模板在工具箱中表示每个操作。 这些活动随后用于创建实现由该协定定义的操作的工作流。 工作流设计器将对该工作流服务进行验证，以确保实现这些操作并且工作流的签名与协定签名匹配。 开发人员还可以将工作流服务与所实现的协定的集合进行关联。 协定优先工作流服务开发的详细信息，请参阅[如何： 创建使用现有服务协定的工作流服务](../../../docs/framework/windows-workflow-foundation/how-to-create-a-workflow-service-that-consumes-an-existing-service-contract.md)。
