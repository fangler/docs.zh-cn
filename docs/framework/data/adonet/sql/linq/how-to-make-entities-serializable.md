---
title: 如何：使实体可序列化
ms.custom: ''
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dotnet-ado
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a6c5bf6e-064a-4f77-b74c-76b3a5dec309
caps.latest.revision: 3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload:
- dotnet
ms.openlocfilehash: b14738e5220810f01b555e54efaad8d8898b7e45
ms.sourcegitcommit: 86adcc06e35390f13c1e372c36d2e044f1fc31ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
---
# <a name="how-to-make-entities-serializable"></a>如何：使实体可序列化
当你生成代码时，可以使实体可序列化。 实体类使用 <xref:System.Runtime.Serialization.DataContractAttribute> 属性修饰，列使用 <xref:System.Runtime.Serialization.DataMemberAttribute> 属性修饰。  
  
 使用 Visual Studio 的开发人员可以使用[!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)]为此目的。  
  
 如果你正在使用 SQLMetal 命令行工具，使用 **/serialization**选项与`unidirectional`自变量。 有关详细信息，请参阅 [SqlMetal.exe（代码生成工具）](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md)。  
  
## <a name="example"></a>示例  
 以下 SQLMetal 命令行会产生包含可序列化实体的文件。  
  
```  
sqlmetal /code:nwserializable.vb /language:vb "c:\northwnd.mdf" /sprocs /functions /pluralize /serialization:unidirectional  
```  
  
```  
sqlmetal /code:nwserializable.cs /language:csharp "c:\northwnd.mdf" /sprocs /functions /pluralize /serialization:unidirectional  
```  
  
## <a name="see-also"></a>请参阅  
 [序列化](../../../../../../docs/framework/data/adonet/sql/linq/serialization.md)  
 [创建对象模型](../../../../../../docs/framework/data/adonet/sql/linq/creating-the-object-model.md)
