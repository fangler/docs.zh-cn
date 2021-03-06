---
title: .NET Framework 对 Windows 应用商店应用程序和 Windows 运行时的支持情况
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: ''
ms.suite: ''
ms.technology: dotnet-standard
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Windows Store apps, .NET Framework support for
- Windows Runtime, .NET Framework support for
- .NET for Windows Store apps
- .NET Framework, and Windows Store apps
- .NET Framework, and Windows Runtime
ms.assetid: 6fa7d044-ae12-4c54-b8ee-50915607a565
caps.latest.revision: 20
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: dc6c1a31adb0c41225c39a186f876d43f7fb3e4b
ms.sourcegitcommit: 68b60d38043e50104ccc90c76f8599b1ffe18346
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/20/2018
---
# <a name="net-framework-support-for-windows-store-apps-and-windows-runtime"></a>.NET Framework 对 Windows 应用商店应用程序和 Windows 运行时的支持情况
[!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 支持基于 [!INCLUDE[wrt](../../../includes/wrt-md.md)]的许多软件开发方案。 这些方案分为三类：  
  
-   开发[!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]使用 XAML 控件，如中所述应用[路线图 for Windows Store 应用使用 C# 或 Visual Basic](/previous-versions/windows/apps/br229583(v=win.10))，[如何 tos (XAML)](/previous-versions/windows/apps/br229566(v=win.10))，和[.NET for Windows Store 应用概述](https://msdn.microsoft.com/library/windows/apps/br230302%28v=VS.110%29.aspx).  
  
-   开发类库以用于通过 .NET Framework 开发的 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用。  
  
-   开发以 .WinMD 文件打包的 [!INCLUDE[wrt](../../../includes/wrt-md.md)]组件，这类文件可由任何支持 [!INCLUDE[wrt](../../../includes/wrt-md.md)]的编程语言使用。 有关示例，请参阅[以 C# 和 Visual Basic 创建 Windows 运行时组件](https://msdn.microsoft.com/library/windows/apps/br230301(v=VS.110).aspx)。  
  
 本主题概述 .NET Framework 为所有这三个类别提供的支持，并描述用于 [!INCLUDE[wrt](../../../includes/wrt-md.md)]组件的方案。 第一部分包括有关 .NET Framework 和 [!INCLUDE[wrt](../../../includes/wrt-md.md)]之间的关系的基本信息，并阐释了在帮助系统和 IDE 时可能遇到的一些问题。 [第二个部分](#WindowsRuntimeComponents)讨论了的开发方案[!INCLUDE[wrt](../../../includes/wrt-md.md)]组件。  
  
## <a name="the-basics"></a>基本知识  
 .NET Framework 提供[!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)]并支持 [!INCLUDE[wrt](../../../includes/wrt-md.md)]本身，因此支持对前面列出的三个开发方案。  
  
-   [.NET for Windows Store 应用](https://msdn.microsoft.com/library/windows/apps/br230232(v=vs.110).aspx)提供.NET Framework 类库的简化的视图，包括类型和成员可用于创建[!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用和[!INCLUDE[wrt](../../../includes/wrt-md.md)]组件。  
  
    -   当您使用 Visual Studio（[!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)] 或更高版本）来开发 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用或 [!INCLUDE[wrt](../../../includes/wrt-md.md)]组件时，有一组引用程序集可确保只显示相关类型和成员。  
  
    -   通过移除 .NET Framework 中的重复功能或移除重复的 [!INCLUDE[wrt](../../../includes/wrt-md.md)]功能，这个简化的 API 集得到进一步简化。 例如，它仅包含集合类型的泛型版本，并且 XML 文档对象模型被消除以支持 [!INCLUDE[wrt](../../../includes/wrt-md.md)] XML API 集。  
  
    -   只包装操作系统 API 的功能也会被移除，因为 [!INCLUDE[wrt](../../../includes/wrt-md.md)]易于从托管代码调用。  
  
     若要阅读更多有关[!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)]，请参阅[.NET for Windows Store 应用概述](https://msdn.microsoft.com/library/windows/apps/br230302(v=VS.110).aspx)。 若要阅读有关 API 的选择过程信息，请参阅[为 Metro 风格应用的.NET](https://blogs.msdn.microsoft.com/dotnet/2012/04/17/net-for-metro-style-apps/) .NET 博客中的条目。  
  
-   [Windows 运行时](/uwp/api/)提供用户界面元素以便生成[!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用，并提供对操作系统功能的访问权限。 与 .NET Framework相似，[!INCLUDE[wrt](../../../includes/wrt-md.md)]有一些可以让 C# 和 Visual Basic 编译器按照它们使用 .NET Framework 类库的方式来使用 [!INCLUDE[wrt](../../../includes/wrt-md.md)]的元数据。 .NET Framework 将某些差异隐藏起来，令使用 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 变得更简单：  
  
    -   隐藏 .NET Framework 和 [!INCLUDE[wrt](../../../includes/wrt-md.md)]之间在编程模式方面的一些差异，如添加和移除事件处理程序的模式。 只需使用 .NET Framework 模式即可。  
  
    -   隐藏在常用类型上存在一些差异（例如，基元类型和集合）。 你只需使用.NET Framework 类型，如中所述[可见的差异在 IDE 中](#DifferencesVisibleInIDE)，本文稍后的。  
  
 大多数情况下，.NET Framework 对 [!INCLUDE[wrt](../../../includes/wrt-md.md)]的支持是透明的。 下一部分讨论托管代码和 [!INCLUDE[wrt](../../../includes/wrt-md.md)]之间的一些明显差异。  
  
<a name="AboutReferenceDocumentation"></a>   
### <a name="the-net-framework-and-the-includewrtincludeswrt-mdmd-reference-documentation"></a>.NET Framework 和 [!INCLUDE[wrt](../../../includes/wrt-md.md)]参考文档  
 Windows 运行时和.NET Framework 文档集相互独立。 如果按 F1 显示关于类型或成员的帮助，将显示相应集合中的参考文档。 但是，如果你浏览[Windows 运行时引用](/uwp/api/)可能会遇到看起来让令人费解的示例：  
  
-   如主题<xref:Windows.Foundation.Collections.IIterable%601>接口不具有 Visual Basic 或 C# 的声明语法。 相反，将注释显示在语法部分上方 (在这种情况下，".NET： 此接口显示为如\<T >")。 这是因为，.NET Framework 和 [!INCLUDE[wrt](../../../includes/wrt-md.md)]以不同的接口提供类似的功能。 此外，它们还有下列行为差异：`IIterable` 有一个 `First` 方法，而没有返回枚举器的 <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> 方法。 .NET Framework 并不强制您了解执行常规任务的另一种方法，而是通过让托管代码看上去是在使用您熟悉的类型来支持 [!INCLUDE[wrt](../../../includes/wrt-md.md)]。 在 IDE 中，您将看不到 `IIterable` 接口，因此您在 [!INCLUDE[wrt](../../../includes/wrt-md.md)]参考中遇到它的唯一方式是直接浏览该文档。  
  
-   <xref:Windows.Web.Syndication.SyndicationFeed.%23ctor(System.String,System.String,Windows.Foundation.Uri)>文档揭示了密切相关的问题： 其参数类型显示为不同的语言不同。 对于 C# 和 Visual Basic，参数类型为 <xref:System.String?displayProperty=nameWithType> 和 <xref:System.Uri?displayProperty=nameWithType>。 同样，这是因为 .NET Framework 具有自己的 `String` 和 `Uri` 类型，并且，对于这种常用的类型，不宜强制 .NET Framework 用户了解执行操作的不同方式。 在 IDE 中，.NET Framework 隐藏相应的 [!INCLUDE[wrt](../../../includes/wrt-md.md)]类型。  
  
-   在少数情况下，如<xref:Windows.UI.Xaml.GridLength>结构，.NET Framework 提供了具有相同名称但更多的功能的类型。 例如，有些构造函数和属性主题与 `GridLength` 相关，但是其语法部分仅适用于 Visual Basic 和 C#，因为成员仅在托管代码时是可用的。 在 [!INCLUDE[wrt](../../../includes/wrt-md.md)]中，结构只有字段。 [!INCLUDE[wrt](../../../includes/wrt-md.md)]结构都需要一个帮助器类， <xref:Windows.UI.Xaml.GridLengthHelper>，若要提供等效的功能。 当你在编写托管代码时，不会在 IDE 中看到该帮助器类。  
  
-   在 IDE 中，[!INCLUDE[wrt](../../../includes/wrt-md.md)]类型看上去是从 <xref:System.Object?displayProperty=nameWithType> 派生的。 它们看上去拥有从 <xref:System.Object> 继承的成员，例如 <xref:System.Object.ToString%2A?displayProperty=nameWithType>。 如果这些类型的确继承自 <xref:System.Object> 并且 [!INCLUDE[wrt](../../../includes/wrt-md.md)]类型可强制转换为 <xref:System.Object>，则这些成员可正常工作。 此功能是 .NET Framework 为 [!INCLUDE[wrt](../../../includes/wrt-md.md)]提供的支持中的一部分。 但是，如果您在 [!INCLUDE[wrt](../../../includes/wrt-md.md)]参考文档中查看该类型，则不会出现此类成员。 <xref:System.Object?displayProperty=nameWithType> 参考文档为这些明显继承的成员提供了文档。  
  
<a name="DifferencesVisibleInIDE"></a>   
### <a name="differences-that-are-visible-in-the-ide"></a>可在 IDE 中看到的差异  
 在更高级的编程方案中，如使用由 C# 编写的 [!INCLUDE[wrt](../../../includes/wrt-md.md)]组件为使用 JavaScript 面向 Windows 生成的 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用提供应用程序逻辑，这种差异在 IDE 中以及文档中都是一目了然的。 当组件返回 `IDictionary<int, string>` 至 JavaScript 时，如果在 JavaScript 调试器中查看它，将会看到 `IMap<int, string>` 方法，因为 JavaScript 使用 [!INCLUDE[wrt](../../../includes/wrt-md.md)]类型。 下表显示了这两种语言中以不同方式显示的一些常用的集合类型：  
  
|[!INCLUDE[wrt](../../../includes/wrt-md.md)] 类型|对应的 .NET Framework 类型|  
|--------------------------------------------------------------|---------------------------------------|  
|`IIterable<T>`|`IEnumerable<T>`|  
|`IIterator<T>`|`IEnumerator<T>`|  
|`IVector<T>`|`IList<T>`|  
|`IVectorView<T>`|`IReadOnlyList<T>`|  
|`IMap<K, V>`|`IDictionary<TKey, TValue>`|  
|`IMapView<K, V>`|`IReadOnlyDictionary<TKey, TValue>`|  
|`IBindableIterable`|`IEnumerable`|  
|`IBindableVector`|`IList`|  
|`Windows.UI.Xaml.Data.INotifyPropertyChanged`|`System.ComponentModel.INotifyPropertyChanged`|  
|`Windows.UI.Xaml.Data.PropertyChangedEventHandler`|`System.ComponentModel.PropertyChangedEventHandler`|  
|`Windows.UI.Xaml.Data.PropertyChangedEventArgs`|`System.ComponentModel.PropertyChangedEventArgs`|  
  
 在 [!INCLUDE[wrt](../../../includes/wrt-md.md)]中，利用 `IMap<K, V>` 来循环访问 `IMapView<K, V>` 和 `IKeyValuePair`。 在将它们传递给托管代码时，它们显示为 `IDictionary<TKey, TValue>` 和 `IReadOnlyDictionary<TKey, TValue>`，因此自然要使用 `System.Collections.Generic.KeyValuePair<TKey, TValue>` 来枚举它们。  
  
 接口在托管代码中的显示方式将影响实现这些接口的类型的显示方式。 例如， `PropertySet` 类实现 `IMap<K, V>`，后者在托管代码中显示为 `IDictionary<TKey, TValue>`。 `PropertySet` 显示为已实现 `IDictionary<TKey, TValue>` 而不是 `IMap<K, V>`，因此在托管代码中，它显示为具有 `Add` 方法，其行为类似于 .NET Framework 字典中的 `Add` 方法。 它不会显示为具有 `Insert` 方法。  
  
 有关使用.NET Framework 创建[!INCLUDE[wrt](../../../includes/wrt-md.md)]组件，以及一个演练，演示如何使用此类组件，使用 JavaScript，请参阅[以 C# 和 Visual Basic 创建 Windows 运行时组件](https://msdn.microsoft.com/library/windows/apps/br230301%28v=VS.110%29.aspx)。  
  
### <a name="primitive-types"></a>基元类型  
 为了能够在托管代码中自然使用 [!INCLUDE[wrt](../../../includes/wrt-md.md)]，代码中显示 .NET Framework 基元类型而非 [!INCLUDE[wrt](../../../includes/wrt-md.md)]基元类型。 在 .NET Framework 中，诸如 `Int32` 结构等基元类型具有许多有用的属性和方法，如 `Int32.TryParse` 方法。 相反，[!INCLUDE[wrt](../../../includes/wrt-md.md)]中的基元类型和结构只有字段。 在托管代码中使用基元时，它们将显示为 .NET Framework 类型，你可以如往常一样使用 .NET Framework 类型的属性和方法。 以下列表提供了一个摘要：  
  
-   对于 [!INCLUDE[wrt](../../../includes/wrt-md.md)]基元 `Int32`、`Int64`、`Single`、`Double`、`Boolean`、`String`（Unicode 字符的不可变集合）、`Enum`、`UInt32`、`UInt64` 和 `Guid`，请使用 `System` 命名空间中的同名类型。  
  
-   对于 `UInt8`，使用 `System.Byte`。  
  
-   对于 `Char16`，使用 `System.Char`。  
  
-   对于 `IInspectable` 接口，使用 `System.Object`。  
  
-   对于 `HRESULT`，使用包含一个 `System.Int32` 成员的结构。  
  
 与接口类型一样，若要看到此表示形式的证据，唯一的情形可能是，.NET Framework 项目是一个 [!INCLUDE[wrt](../../../includes/wrt-md.md)]组件，该组件由使用 JavaScript 生成的 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用使用。  
  
 在托管代码和 .NET Framework 中显示相同的其他基本常用 [!INCLUDE[wrt](../../../includes/wrt-md.md)]类型包括 `Windows.Foundation.DateTime` 结构（在托管代码显示为 <xref:System.DateTimeOffset?displayProperty=nameWithType> 结构）和 `Windows.Foundation.TimeSpan` 结构（在托管代码显示为 <xref:System.TimeSpan?displayProperty=nameWithType> 结构）。  
  
### <a name="other-differences"></a>其他差异  
 在少数情况下，由于代码中显示 .NET Framework 类型而非 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 类型，某些操作需要由您来执行。 例如，<xref:Windows.Foundation.Uri?displayProperty=nameWithType>类显示为<xref:System.Uri?displayProperty=nameWithType>在.NET Framework 代码中。 <xref:System.Uri?displayProperty=nameWithType> 允许相对的 URI，但<xref:Windows.Foundation.Uri?displayProperty=nameWithType>需要绝对 URI。 因此，在将 URI 传递给 [!INCLUDE[wrt](../../../includes/wrt-md.md)]方法时，必须确保它是绝对 URI。 (请参阅[向 Windows 运行时传递 URI](../../../docs/standard/cross-platform/passing-a-uri-to-the-windows-runtime.md)。)  
  
<a name="WindowsRuntimeComponents"></a>   
## <a name="scenarios-for-developing-windows-runtime-components"></a>开发的 Windows 运行时组件的方案  
 托管 [!INCLUDE[wrt](../../../includes/wrt-md.md)]组件支持的方案取决于下列一般原则：  
  
-   使用 .NET Framework 生成的 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 组件与其他 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 库没有明显的差异。 例如，如果使用托管代码重新实现一个本机 [!INCLUDE[wrt](../../../includes/wrt-md.md)]组件，这两个组件表面上是无法区分的。 在托管代码中编写的组件对使用它的代码来说是不可见的，即使该代码本身是托管代码。 但是，在内部，组件是真正的托管代码并运行在公共语言运行时 (CLR) 上。  
  
-   组件可以包含实现应用程序逻辑和/或 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] UI 控件的类型。  
  
    > [!NOTE]
    >  最好将 UI 元素与应用程序逻辑分离开来。 此外，在使用 JavaScript 和 HTML 为 Windows 编写的 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用中，不能使用 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] UI 控件。  
  
-   组件可以是用于 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用的 Visual Studio 解决方案中的一个项目，也可以是一个可添加到多个解决方案中的可重用组件。  
  
    > [!NOTE]
    >  如果您的组件将仅用于 C# 或 Visual Basic，那么没有必要使其成为 [!INCLUDE[wrt](../../../includes/wrt-md.md)]组件。 如果要使其成为一个普通的 .NET Framework 类库，不必将其公共 API 图面限制为 [!INCLUDE[wrt](../../../includes/wrt-md.md)]类型。  
  
-   你可以通过使用释放的可重用组件版本[!INCLUDE[wrt](../../../includes/wrt-md.md)]<xref:Windows.Foundation.Metadata.VersionAttribute>属性用于标识哪些类型 （和在类型的成员） 已添加了不同的版本。  
  
-   组件中的类型可以从 [!INCLUDE[wrt](../../../includes/wrt-md.md)]类型派生。 可以从中的基元的控件类型派生控件<xref:Windows.UI.Xaml.Controls.Primitives>命名空间，或者从较完成控件如<xref:Windows.UI.Xaml.Controls.Button>。  
  
    > [!IMPORTANT]
    >  从 [!INCLUDE[win8](../../../includes/win8-md.md)] 和 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 开始，托管 [!INCLUDE[wrt](../../../includes/wrt-md.md)]组件中的所有公共类型必须是密封的。 另一个 [!INCLUDE[wrt](../../../includes/wrt-md.md)]组件中的类型无法从它们派生。 如果要在组件中提供多态行为，可以创建一个接口并在多态类型中实现它。  
  
-   组件中所有公共类型的参数和返回类型必须是 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 类型（包括组件定义的 [!INCLUDE[wrt](../../../includes/wrt-md.md)]类型）。  
  
 以下部分提供常见方案的示例。  
  
### <a name="application-logic-for-a-includewin8appnamelongincludeswin8-appname-long-mdmd-app-with-javascript"></a>使用 JavaScript 生成的 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用的应用程序逻辑  
 在使用 JavaScript 为 Windows 开发 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用时，您可能会发现，应用程序逻辑的某些部分在托管代码中性能更佳或更易于开发。 JavaScript 不能直接使用 .NET Framework 类库，但是，您可以使将类库包装为 .WinMD 文件。 在此方案中，[!INCLUDE[wrt](../../../includes/wrt-md.md)]组件是应用中不可分割的组成部分，因此，不宜提供版本特性。  
  
### <a name="reusable-includewin8appnamelongincludeswin8-appname-long-mdmd-ui-controls"></a>可重用的 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] UI 控件  
 对于一组相关的 UI 控件，可打包为可重用的 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 组件。 该组件可以独立销售，或作为您创建的应用元素使用。 在此方案中，因此最好使用[!INCLUDE[wrt](../../../includes/wrt-md.md)]<xref:Windows.Foundation.Metadata.VersionAttribute>属性为了提高兼容性。  
  
### <a name="reusable-application-logic-from-existing-net-framework-apps"></a>来自现有 .NET Framework 应用的可重用的应用程序逻辑  
 对于现有桌面应用中的托管代码，可打包为一个独立的 [!INCLUDE[wrt](../../../includes/wrt-md.md)]组件。 这样即可将该组件用于由 C++ 或 JavaScript 生成的 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用以及由 C# 或 Visual Basic 生成的 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用。 如果代码有多个可重用的方案，可选择进行版本控制。  
  
## <a name="related-topics"></a>相关主题  
  
|标题|描述|  
|-----------|-----------------|  
|[适用于 Microsoft Store 应用的 .NET 概述](https://msdn.microsoft.com/library/windows/apps/br230302(v=VS.110).aspx)|描述可用于创建 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] 应用和 [!INCLUDE[wrt](../../../includes/wrt-md.md)] 组件的 .NET Framework 类型和成员。 （位于 Windows 开发中心。）|  
|[使用 C# 或 Visual Basic 的 Windows 应用商店应用的路线图](/previous-versions/windows/apps/br229583(v=win.10))|提供关键资源来帮助您开始使用 C# 或 Visual Basic 开发 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用，这些资源包括许多快速入门主题、教程和最佳做法。 （位于 Windows 开发中心。）|  
|[如何 tos (XAML)](/previous-versions/windows/apps/br229566(v=win.10))|提供关键资源来帮助您开始使用 C# 或 Visual Basic 开发 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用，这些资源包括许多快速入门主题、教程和最佳做法。 （位于 Windows 开发中心。）|  
|[用 C# 和 Visual Basic 创建 Windows 运行时组件](https://msdn.microsoft.com/library/windows/apps/br230301%28v=VS.110%29.aspx)|描述如何使用 .NET Framework 创建 [!INCLUDE[wrt](../../../includes/wrt-md.md)]组件，说明如何在使用 JavaScript 为 Windows 生成的 [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]应用中使用该组件，并描述如何使用 Visual Studio 调试这一组合。 （位于 Windows 开发中心。）|  
|[Windows 运行时引用](/uwp/api/)|[!INCLUDE[wrt](../../../includes/wrt-md.md)]的参考文档。 （位于 Windows 开发中心。）|  
|[向 Windows 运行时传递 URI](../../../docs/standard/cross-platform/passing-a-uri-to-the-windows-runtime.md)|描述将托管代码的 URI 传递给 [!INCLUDE[wrt](../../../includes/wrt-md.md)]时可能出现的问题，以及如何避免这一问题。|
