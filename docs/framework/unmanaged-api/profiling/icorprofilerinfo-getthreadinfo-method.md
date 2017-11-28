---
title: "ICorProfilerInfo::GetThreadInfo 方法"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorProfilerInfo.GetThreadInfo
api_location: mscorwks.dll
api_type: COM
f1_keywords: ICorProfilerInfo::GetThreadInfo
helpviewer_keywords:
- ICorProfilerInfo::GetThreadInfo method [.NET Framework profiling]
- GetThreadInfo method [.NET Framework profiling]
ms.assetid: fc994fef-65c9-432a-84cb-66c8141147e7
topic_type: apiref
caps.latest.revision: "11"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 4c4657279e145dbb923c339ed0114723620e7aa7
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2017
---
# <a name="icorprofilerinfogetthreadinfo-method"></a><span data-ttu-id="75ea0-102">ICorProfilerInfo::GetThreadInfo 方法</span><span class="sxs-lookup"><span data-stu-id="75ea0-102">ICorProfilerInfo::GetThreadInfo Method</span></span>
<span data-ttu-id="75ea0-103">获取指定线程的当前的 Win32 线程标识。</span><span class="sxs-lookup"><span data-stu-id="75ea0-103">Gets the current Win32 thread identity for the specified thread.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="75ea0-104">语法</span><span class="sxs-lookup"><span data-stu-id="75ea0-104">Syntax</span></span>  
  
```  
HRESULT GetThreadInfo(  
    [in]  ThreadID threadId,  
    [out] DWORD    *pdwWin32ThreadId);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="75ea0-105">参数</span><span class="sxs-lookup"><span data-stu-id="75ea0-105">Parameters</span></span>  
 `threadId`  
 <span data-ttu-id="75ea0-106">[in]要为其获取当前 Win32 id。 线程的 ID</span><span class="sxs-lookup"><span data-stu-id="75ea0-106">[in] The ID of the thread for which to get the current Win32 ID.</span></span>  
  
 `pdwWin32ThreadId`  
 <span data-ttu-id="75ea0-107">[out]指向指定的线程的当前 Win32 线程的 id。</span><span class="sxs-lookup"><span data-stu-id="75ea0-107">[out] A pointer to the specified thread's current Win32 thread ID.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="75ea0-108">要求</span><span class="sxs-lookup"><span data-stu-id="75ea0-108">Requirements</span></span>  
 <span data-ttu-id="75ea0-109">**平台：**请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="75ea0-109">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="75ea0-110">**头文件：** CorProf.idl、CorProf.h</span><span class="sxs-lookup"><span data-stu-id="75ea0-110">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="75ea0-111">**库：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="75ea0-111">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="75ea0-112">**.NET framework 版本：**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="75ea0-112">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="75ea0-113">另请参阅</span><span class="sxs-lookup"><span data-stu-id="75ea0-113">See Also</span></span>  
 [<span data-ttu-id="75ea0-114">ICorProfilerInfo 接口</span><span class="sxs-lookup"><span data-stu-id="75ea0-114">ICorProfilerInfo Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-interface.md)