---
title: ICorDebugExceptionObjectCallStackEnum::Next-Methode
ms.date: 03/30/2017
api_name:
- ICorDebugExceptionObjectCallStackEnum::Next
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugExceptionObjectCallStackEnum::Next
helpviewer_keywords:
- ICorDebugExceptionObjectCallStackEnum::Next method [.NET Framework debugging]
- Next method, ICorDebugExceptionObjectCallStackEnum interface [.NET Framework debugging]
ms.assetid: 3328a2c0-1e48-4a54-802a-9b474cf82c21
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 2216ad54c37bcaf62f3ddca6a4d48ef2cb4faf22
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="icordebugexceptionobjectcallstackenumnext-method"></a>ICorDebugExceptionObjectCallStackEnum::Next-Methode
Ruft die angegebene Anzahl von [CorDebugExceptionObjectStackFrame](../../../../docs/framework/unmanaged-api/debugging/cordebugexceptionobjectstackframe-structure.md) Instanzen, die Informationen aus der Aufrufliste eines Ausnahmeobjekts enthalten.  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT Next(  
    [in] ULONG celt,  
    [out, size_is(celt), length_is(*pceltFetched)] CorDebugExceptionObjectStackFrame values[],  
    [out] ULONG *pceltFetched  
);  
```  
  
#### <a name="parameters"></a>Parameter  
 `celt`  
 [in] Die Anzahl der [CorDebugExceptionObjectStackFrame](../../../../docs/framework/unmanaged-api/debugging/cordebugexceptionobjectstackframe-structure.md) Instanzen abgerufen werden sollen.  
  
 `values`  
 [out] Ein Array von Zeigern, die jeweils auf eine [CorDebugExceptionObjectStackFrame](../../../../docs/framework/unmanaged-api/debugging/cordebugexceptionobjectstackframe-structure.md) Objekt.  
  
 `pceltFetched`  
 [out] Ein Zeiger auf die Anzahl der [CorDebugExceptionObjectStackFrame](../../../../docs/framework/unmanaged-api/debugging/cordebugexceptionobjectstackframe-structure.md) Instanzen, die tatsächlich zurückgegeben.  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorDebug.idl, CorDebug.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v45plus](../../../../includes/net-current-v45plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [ICorDebugExceptionObjectCallStackEnum-Schnittstelle](../../../../docs/framework/unmanaged-api/debugging/icordebugexceptionobjectcallstackenum-interface.md)  
 [Debuggen von Schnittstellen](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
