---
title: ICorProfilerInfo4::EnumJITedFunctions2-Methode
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo4.EnumJITedFunctions2
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo4::EnumJITedFunctions2
helpviewer_keywords:
- EnumJITedFunctions2 method, ICorProfilerInfo4 interface [.NET Framework profiling]
- ICorProfilerInfo4::EnumJITedFunctions2 method [.NET Framework profiling]
ms.assetid: 40e9a1be-9bd2-4fad-9921-34a84b61c1e3
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: b11c70fa7d423575b2dd1d2cc676908885a0fd4c
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="icorprofilerinfo4enumjitedfunctions2-method"></a>ICorProfilerInfo4::EnumJITedFunctions2-Methode
Gibt einen Enumerator für alle Funktionen, die bereits JIT-kompiliert und JIT-kompiliert wurden. Diese Methode ersetzt die [ICorProfilerInfo3:: EnumJITedFunctions](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-enumjitedfunctions-method.md) -Methode, die nicht erneut JIT-kompilierten IDs aufgelistet ist.  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT EnumJITedFunctions([out] ICorProfilerFunctionEnum** ppEnum);  
```  
  
#### <a name="parameters"></a>Parameter  
 `ppEnum`  
 [out] Ein Zeiger auf die [ICorProfilerFunctionEnum](../../../../docs/framework/unmanaged-api/profiling/icorprofilerfunctionenum-interface.md) Enumerator.  
  
## <a name="remarks"></a>Hinweise  
 Diese Methode möglicherweise überschneiden sich mit `JITCompilation` Rückrufe, z. B. die [ICorProfilerCallback:: JITCompilationStarted](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-jitcompilationstarted-method.md) Methode. Die zurückgegebene-Enumeration enthält Werte für die `COR_PRF_FUNCTION::reJitId` Feld. Die [ICorProfilerInfo3:: EnumJITedFunctions](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-enumjitedfunctions-method.md) -Methode, die diese Methode ersetzt wird, nicht erneut JIT-kompilierten IDs aufgelistet, da die `COR_PRF_FUNCTION::reJitId` Feld immer auf 0 festgelegt ist. Die `ICorProfilerInfo4::EnumJITedFunctions` Methode JIT-kompilierten-IDs aufgelistet werden, da die `COR_PRF_FUNCTION::reJitId` Feld ordnungsgemäß festgelegt ist. Beachten Sie, dass die [icorprofilerinfo4:: Enumjitedfunctions2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-enumjitedfunctions2-method.md) Methode kann eine Garbagecollection auslösen, wohingegen [ICorProfilerInfo3:: EnumJITedFunctions-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-enumjitedfunctions-method.md) geschieht dies nicht.  Weitere Informationen finden Sie unter [CORPROF_E_UNSUPPORTED_CALL_SEQUENCE HRESULT](../../../../docs/framework/unmanaged-api/profiling/corprof-e-unsupported-call-sequence-hresult.md).  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorProf.idl, CorProf.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [EnumJITedFunctions-Methode](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-enumjitedfunctions-method.md)  
 [ICorProfilerInfo4-Schnittstelle](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo4-interface.md)  
 [Profilerstellungsschnittstellen](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)  
 [Profilerstellung](../../../../docs/framework/unmanaged-api/profiling/index.md)
