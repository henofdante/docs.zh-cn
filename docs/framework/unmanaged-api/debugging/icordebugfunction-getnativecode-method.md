---
title: "ICorDebugFunction::GetNativeCode 方法"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugFunction.GetNativeCode
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugFunction::GetNativeCode
helpviewer_keywords:
- GetNativeCode method [.NET Framework debugging]
- ICorDebugFunction::GetNativeCode method [.NET Framework debugging]
ms.assetid: c8a34916-0eef-4987-8d29-c8bcb4be9cf6
topic_type: apiref
caps.latest.revision: "10"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 2fccfaeb346d59f5cf565f47a9a64e732706adad
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2017
---
# <a name="icordebugfunctiongetnativecode-method"></a><span data-ttu-id="c9313-102">ICorDebugFunction::GetNativeCode 方法</span><span class="sxs-lookup"><span data-stu-id="c9313-102">ICorDebugFunction::GetNativeCode Method</span></span>
<span data-ttu-id="c9313-103">获取此 ICorDebugFunction 实例表示的函数的本机代码。</span><span class="sxs-lookup"><span data-stu-id="c9313-103">Gets the native code for the function that is represented by this ICorDebugFunction instance.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="c9313-104">语法</span><span class="sxs-lookup"><span data-stu-id="c9313-104">Syntax</span></span>  
  
```  
HRESULT GetNativeCode (  
    [out] ICorDebugCode **ppCode  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="c9313-105">参数</span><span class="sxs-lookup"><span data-stu-id="c9313-105">Parameters</span></span>  
 `ppCode`  
 <span data-ttu-id="c9313-106">[out]指向 ICorDebugCode 实例，表示此函数，则为 null，本机代码，如果此函数是尚未实时 (JIT) 编译的 Microsoft 中间语言 (MSIL) 代码的指针。</span><span class="sxs-lookup"><span data-stu-id="c9313-106">[out] A pointer to the ICorDebugCode instance that represents the native code for this function, or null, if this function is Microsoft intermediate language (MSIL) code that has not been just-in-time (JIT) compiled.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="c9313-107">备注</span><span class="sxs-lookup"><span data-stu-id="c9313-107">Remarks</span></span>  
 <span data-ttu-id="c9313-108">如果表示由此函数`ICorDebugFunction`实例已进行 JIT 编译一次以上，对于泛型类型，如`GetNativeCode`返回一个随机的本机代码。</span><span class="sxs-lookup"><span data-stu-id="c9313-108">If the function that is represented by this `ICorDebugFunction` instance has been JIT-compiled more than once, as in the case of generic types, `GetNativeCode` returns a random native code object.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="c9313-109">要求</span><span class="sxs-lookup"><span data-stu-id="c9313-109">Requirements</span></span>  
 <span data-ttu-id="c9313-110">**平台：**请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="c9313-110">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="c9313-111">**标头：** CorDebug.idl、 CorDebug.h</span><span class="sxs-lookup"><span data-stu-id="c9313-111">**Header:** CorDebug.idl, CorDebug.h</span></span>  
  
 <span data-ttu-id="c9313-112">**库：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="c9313-112">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="c9313-113">**.NET framework 版本：**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="c9313-113">**.NET Framework Versions:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]</span></span>