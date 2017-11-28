---
title: "FunctionTailcall3 函数"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: FunctionTailcall3
api_location: mscorwks.dll
api_type: COM
f1_keywords: FunctionTailcall3
helpviewer_keywords: FunctionTailcall3 function [.NET Framework profiling]
ms.assetid: 1e48243f-5de6-4bd6-a1d0-e1d248bca4b8
topic_type: apiref
caps.latest.revision: "13"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: c5d274c966a345e0e2984018bcd8aa1e2dade03b
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="functiontailcall3-function"></a><span data-ttu-id="cd366-102">FunctionTailcall3 函数</span><span class="sxs-lookup"><span data-stu-id="cd366-102">FunctionTailcall3 Function</span></span>
<span data-ttu-id="cd366-103">通知探查器当前正在执行的函数来执行对另一个函数的结尾调用。</span><span class="sxs-lookup"><span data-stu-id="cd366-103">Notifies the profiler that the currently executing function is about to perform a tail call to another function.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="cd366-104">语法</span><span class="sxs-lookup"><span data-stu-id="cd366-104">Syntax</span></span>  
  
```  
void __stdcall FunctionTailcall3 (FunctionOrRemappedID functionOrRemappedID);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="cd366-105">参数</span><span class="sxs-lookup"><span data-stu-id="cd366-105">Parameters</span></span>  
 `functionOrRemappedID`  
 <span data-ttu-id="cd366-106">[in]当前正在执行即将进行的尾调用的函数的标识符。</span><span class="sxs-lookup"><span data-stu-id="cd366-106">[in] The identifier of the currently executing function that is about to make a tail call.</span></span>  
  
## <a name="remarks"></a><span data-ttu-id="cd366-107">备注</span><span class="sxs-lookup"><span data-stu-id="cd366-107">Remarks</span></span>  
 <span data-ttu-id="cd366-108">`FunctionTailcall3`回调函数向发出你通知探查器正被调用函数。</span><span class="sxs-lookup"><span data-stu-id="cd366-108">The `FunctionTailcall3` callback function notifies the profiler as functions are being called.</span></span> <span data-ttu-id="cd366-109">使用[icorprofilerinfo3:: Setenterleavefunctionhooks3 方法](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-setenterleavefunctionhooks3-method.md)注册此函数的实现。</span><span class="sxs-lookup"><span data-stu-id="cd366-109">Use the [ICorProfilerInfo3::SetEnterLeaveFunctionHooks3 method](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-setenterleavefunctionhooks3-method.md) to register your implementation of this function.</span></span>  
  
 <span data-ttu-id="cd366-110">`FunctionTailcall3`函数为回调; 你必须实现它。</span><span class="sxs-lookup"><span data-stu-id="cd366-110">The `FunctionTailcall3` function is a callback; you must implement it.</span></span> <span data-ttu-id="cd366-111">实现必须使用`__declspec(naked)`存储类特性。</span><span class="sxs-lookup"><span data-stu-id="cd366-111">The implementation must use the `__declspec(naked)` storage-class attribute.</span></span>  
  
 <span data-ttu-id="cd366-112">调用此函数之前，执行引擎不保存任何寄存器。</span><span class="sxs-lookup"><span data-stu-id="cd366-112">The execution engine does not save any registers before calling this function.</span></span>  
  
-   <span data-ttu-id="cd366-113">在进入时，必须保存所有使用，包括浮点单位 (FPU) 中的寄存器。</span><span class="sxs-lookup"><span data-stu-id="cd366-113">On entry, you must save all registers that you use, including those in the floating-point unit (FPU).</span></span>  
  
-   <span data-ttu-id="cd366-114">在退出时，你必须通过弹出已推送由其调用方的所有参数由还原堆栈。</span><span class="sxs-lookup"><span data-stu-id="cd366-114">On exit, you must restore the stack by popping off all the parameters that were pushed by its caller.</span></span>  
  
 <span data-ttu-id="cd366-115">实现`FunctionTailcall3`不应阻止，因为它会将延迟垃圾回收。</span><span class="sxs-lookup"><span data-stu-id="cd366-115">The implementation of `FunctionTailcall3` should not block, because it will delay garbage collection.</span></span> <span data-ttu-id="cd366-116">实现不应尝试的垃圾回收，因为堆栈可能不是在垃圾收集友好状态中。</span><span class="sxs-lookup"><span data-stu-id="cd366-116">The implementation should not attempt a garbage collection, because the stack may not be in a garbage collection-friendly state.</span></span> <span data-ttu-id="cd366-117">如果尝试执行垃圾回收，则运行时将阻塞直到`FunctionTailcall3`返回。</span><span class="sxs-lookup"><span data-stu-id="cd366-117">If a garbage collection is attempted, the runtime will block until `FunctionTailcall3` returns.</span></span>  
  
 <span data-ttu-id="cd366-118">`FunctionTailcall3`函数不得调入托管代码或以任何方式导致托管的内存分配。</span><span class="sxs-lookup"><span data-stu-id="cd366-118">The `FunctionTailcall3` function must not call into managed code or cause a managed memory allocation in any way.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="cd366-119">要求</span><span class="sxs-lookup"><span data-stu-id="cd366-119">Requirements</span></span>  
 <span data-ttu-id="cd366-120">**平台：**请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。</span><span class="sxs-lookup"><span data-stu-id="cd366-120">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="cd366-121">**标头：** CorProf.idl</span><span class="sxs-lookup"><span data-stu-id="cd366-121">**Header:** CorProf.idl</span></span>  
  
 <span data-ttu-id="cd366-122">**库：** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="cd366-122">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="cd366-123">**.NET framework 版本：**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="cd366-123">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="cd366-124">另请参阅</span><span class="sxs-lookup"><span data-stu-id="cd366-124">See Also</span></span>  
 [<span data-ttu-id="cd366-125">FunctionEnter3</span><span class="sxs-lookup"><span data-stu-id="cd366-125">FunctionEnter3</span></span>](../../../../docs/framework/unmanaged-api/profiling/functionenter3-function.md)  
 [<span data-ttu-id="cd366-126">FunctionLeave3</span><span class="sxs-lookup"><span data-stu-id="cd366-126">FunctionLeave3</span></span>](../../../../docs/framework/unmanaged-api/profiling/functionleave3-function.md)  
 [<span data-ttu-id="cd366-127">FunctionEnter3WithInfo</span><span class="sxs-lookup"><span data-stu-id="cd366-127">FunctionEnter3WithInfo</span></span>](../../../../docs/framework/unmanaged-api/profiling/functionenter3withinfo-function.md)  
 [<span data-ttu-id="cd366-128">FunctionLeave3WithInfo</span><span class="sxs-lookup"><span data-stu-id="cd366-128">FunctionLeave3WithInfo</span></span>](../../../../docs/framework/unmanaged-api/profiling/functionleave3withinfo-function.md)  
 [<span data-ttu-id="cd366-129">FunctionTailcall3WithInfo 函数</span><span class="sxs-lookup"><span data-stu-id="cd366-129">FunctionTailcall3WithInfo Function</span></span>](../../../../docs/framework/unmanaged-api/profiling/functiontailcall3withinfo-function.md)  
 [<span data-ttu-id="cd366-130">SetEnterLeaveFunctionHooks3</span><span class="sxs-lookup"><span data-stu-id="cd366-130">SetEnterLeaveFunctionHooks3</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-setenterleavefunctionhooks3-method.md)  
 [<span data-ttu-id="cd366-131">SetEnterLeaveFunctionHooks3WithInfo</span><span class="sxs-lookup"><span data-stu-id="cd366-131">SetEnterLeaveFunctionHooks3WithInfo</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-setenterleavefunctionhooks3withinfo-method.md)  
 [<span data-ttu-id="cd366-132">SetFunctionIDMapper</span><span class="sxs-lookup"><span data-stu-id="cd366-132">SetFunctionIDMapper</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setfunctionidmapper-method.md)  
 [<span data-ttu-id="cd366-133">SetFunctionIDMapper2</span><span class="sxs-lookup"><span data-stu-id="cd366-133">SetFunctionIDMapper2</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-setfunctionidmapper2-method.md)  
 [<span data-ttu-id="cd366-134">分析全局静态函数</span><span class="sxs-lookup"><span data-stu-id="cd366-134">Profiling Global Static Functions</span></span>](../../../../docs/framework/unmanaged-api/profiling/profiling-global-static-functions.md)