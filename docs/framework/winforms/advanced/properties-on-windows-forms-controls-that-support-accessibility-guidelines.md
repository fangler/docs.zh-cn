---
title: "支持辅助功能准则的 Windows 窗体控件上的属性"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-winforms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Windows Forms, accessibility properties of controls
- accessibility [Windows Forms], Windows Forms control properties
ms.assetid: ad3567a6-313b-4708-9e15-f487a831f049
caps.latest.revision: "5"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 967b4a0e883338c756aceef37d11edecfb978527
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2017
---
# <a name="properties-on-windows-forms-controls-that-support-accessibility-guidelines"></a>支持辅助功能准则的 Windows 窗体控件上的属性
标准 Windows 窗体的工具箱上的控件都支持许多辅助功能准则，包括公开键盘焦点和公开屏幕元素。  
  
## <a name="planning-ahead-for-accessibility"></a>预先规划辅助功能  
 可以使用的控件的属性，以支持其他辅助功能准则下, 表中所示。 此外，你应使用菜单提供对功能进行编程访问。  
  
|控件属性|有关辅助功能的注意事项|  
|----------------------|--------------------------------------|  
|AccessibleDescription|说明报告给辅助工具，如屏幕读取器。 辅助工具是专用的程序和设备，用于帮助残障人士更加有效地使用计算机。|  
|AccessibleName|将报告给辅助工具的名称。|  
|AccessibleRole|描述如何使用用户界面中的元素。|  
|TabIndex|创建窗体中导航的合理路径。 很重要没有内部函数的标签，例如文本框中，必须立即在它们之前的 tab 键顺序及其关联的标签的控件。|  
|Text|使用"&"符来创建访问键。 使用访问密钥是一部分提供的功能的已记录的键盘访问。|  
|字号|如果不调整字体大小，则应将它设为 10 磅或更大。 窗体的字体大小设置后，所有之后添加到窗体的控件将具有相同的大小。|  
|前景色|如果此属性设置为默认值，然后将窗体上使用用户的颜色首选项。|  
|背景色|如果此属性设置为默认值，然后将窗体上使用用户的颜色首选项。|  
|BackgroundImage|将此属性保留为空，以使文本更具可读性。|  
  
## <a name="see-also"></a>请参阅  
 [演练：创建基于 Windows 的可访问应用程序](../../../../docs/framework/winforms/advanced/walkthrough-creating-an-accessible-windows-based-application.md)
