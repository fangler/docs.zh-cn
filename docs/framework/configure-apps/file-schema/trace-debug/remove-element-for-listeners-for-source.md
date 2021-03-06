---
title: '&lt;删除&gt;元素&lt;侦听器&gt;为&lt;源&gt;'
ms.date: 03/30/2017
f1_keywords:
- http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.diagnostics/sources/source/listeners/remove
helpviewer_keywords:
- remove element for <listeners> for <source>
- <remove> element for <listeners> for <source>
ms.assetid: 3ff6b578-273d-407f-b07f-8251f1f9f5d0
author: mcleblanc
ms.author: markl
manager: markl
ms.openlocfilehash: cc6772e7a9b98f09df21fd1acf24f578b66ae51e
ms.sourcegitcommit: 11f11ca6cefe555972b3a5c99729d1a7523d8f50
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="ltremovegt-element-for-ltlistenersgt-for-ltsourcegt"></a>&lt;删除&gt;元素&lt;侦听器&gt;为&lt;源&gt;
从跟踪源的 `Listeners` 集合中删除侦听器。  
  
 \<configuration>  
\<system.diagnostics >  
\<源 >  
\<源 >  
\<侦听器 >  
\<remove>  
  
## <a name="syntax"></a>语法  
  
```xml  
<remove name="listenerName" />  
```  
  
## <a name="attributes-and-elements"></a>特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### <a name="attributes"></a>特性  
  
|特性|描述|  
|---------------|-----------------|  
|`name`|必需的特性。<br /><br /> 从删除的侦听器名称`Listeners`集合。|  
  
### <a name="child-elements"></a>子元素  
 无。  
  
### <a name="parent-elements"></a>父元素  
  
|元素|描述|  
|-------------|-----------------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`system.diagnostics`|指定用于收集、存储和路由消息的跟踪侦听器以及对跟踪开关设置的级别。|  
|`sources`|包含用于启动跟踪消息的跟踪源。|  
|`source`|指定用于启动跟踪消息的跟踪源。|  
|`listeners`|指定收集、 存储和将消息路由的侦听器。|  
  
## <a name="remarks"></a>备注  
 `<remove>`元素中移除指定的侦听器从`Listeners`跟踪源的集合。  
  
 你可以删除从元素`Listeners`以编程方式通过调用跟踪源集合<xref:System.Diagnostics.TraceListenerCollection.Remove%2A>方法<xref:System.Diagnostics.TraceSource.Listeners%2A>属性<xref:System.Diagnostics.TraceSource>实例。  
  
 计算机配置文件 (Machine.config) 和应用程序配置文件中，可以使用此元素。  
  
## <a name="example"></a>示例  
 下面的示例演示如何使用`<remove>`元素之前使用`<add>`元素添加侦听器`console`到`Listeners`跟踪源集合`TraceSourceApp`。  
  
```xml  
<configuration>  
  <system.diagnostics>  
    <sources>  
      <source name="TraceSourceApp" switchName="sourceSwitch"   
         switchType="System.Diagnostics.SourceSwitch" >  
         <listeners>  
           <remove name="Default"/>  
           <add name="console"   
             type="System.Diagnostics.ConsoleTraceListener" />  
         </listeners>  
      </source>  
    </sources>  
  </system.diagnostics>  
</configuration>   
```  
  
## <a name="see-also"></a>请参阅  
 <xref:System.Diagnostics.TraceSource.Listeners%2A>  
 <xref:System.Diagnostics.TraceSource>  
 [跟踪和调试设置架构](../../../../../docs/framework/configure-apps/file-schema/trace-debug/index.md)  
 [\<clear>](../../../../../docs/framework/configure-apps/file-schema/trace-debug/clear-element-for-listeners-for-source.md)  
 [跟踪侦听器](../../../../../docs/framework/debug-trace-profile/trace-listeners.md)
