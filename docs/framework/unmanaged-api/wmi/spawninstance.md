---
title: "SpawnInstance 函数 （非托管 API 参考）"
description: "SpawnInstance 函数将创建一个类的新实例。"
ms.date: 11/06/2017
ms.prod: .net-framework
ms.technology:
- dotnet-clr
ms.topic: reference
api_name:
- SpawnInstance
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- SpawnInstance
helpviewer_keywords:
- SpawnInstance function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 68508f3000e7f4ac481f940ef4c715366c37125c
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/22/2017
---
# <a name="spawninstance-function"></a>SpawnInstance 函数
创建一个类的新实例。    
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>语法  
  
```  
HRESULT SpawnInstance (
   [in] int                  vFunc, 
   [in] IWbemClassObject*    ptr, 
   [in] LONG                 lFlags,
   [out] IWbemClassObject**  ppNewInstance); 
```  

## <a name="parameters"></a>参数

`vFunc`  
[in]未使用此参数。

`ptr`  
[in]指向的指针[IWbemClassObject](https://msdn.microsoft.com/library/aa391433%28v=vs.85%29.aspx)实例。

`lFlags`  
[in]保留。 此参数必须为 0。

`ppNewInstance`  
[out]接收到类的新实例的指针。 如果发生错误，新的对象不是返回，和`ppNewInstance`左未修改形式。

## <a name="return-value"></a>返回值

此函数返回以下值中定义*WbemCli.h*标头文件，或者你可以定义它们常量作为在代码中：

|返回的常量  |“值”  |描述  |
|---------|---------|---------|
| `WBEM_E_INCOMPLETE_CLASS` | 0x80041020 | `ptr`不是有效的类定义，无法生成新实例。 不完整，或者它具有不已注册到 Windows 管理中调用[PutClassWmi](putclasswmi.md)。 |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | 没有足够的内存是可用于完成该操作。 |
| `WBEM_E_INVALID_PARAMETER` | 0x80041008 | `ppNewClass` 为 `null`。 |
| `WBEM_S_NO_ERROR` | 0 | 函数调用成功。  |
  
## <a name="remarks"></a>备注

此函数包装对的调用[IWbemClassObject::SpawnInstance](https://msdn.microsoft.com/library/aa391458(v=vs.85).aspx)方法。

`ptr`必须是类定义从获取 Windows 管理。 （请注意，支持生成实例中的实例，但返回的实例为空。）然后可以使用此类定义来创建新实例。 调用[PutInstanceWmi](putinstancewmi.md)函数是必需的如果你想要将该实例写入到 Windows 管理。




新的对象中返回`ppNewClass`自动成为当前对象的一个子类。 不能重写此行为。 不没有可以用来创建子类 （派生类） 的任何其他方法。

## <a name="requirements"></a>惠?  
 **平台：**请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** WMINet_Utils.idl  
  
 **.NET framework 版本：**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>请参阅  
[WMI 和性能计数器 （非托管 API 参考）](index.md)
