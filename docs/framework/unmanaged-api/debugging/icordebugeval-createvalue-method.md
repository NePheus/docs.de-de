---
title: ICorDebugEval::CreateValue-Methode
ms.date: 03/30/2017
api_name:
- ICorDebugEval.CreateValue
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval::CreateValue
helpviewer_keywords:
- ICorDebugEval::CreateValue method [.NET Framework debugging]
- CreateValue method [.NET Framework debugging]
ms.assetid: 9a1c0b47-6f10-4fcb-844a-4ab2d7990140
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 6d67784daee055106f104d74d098b9926c6de2ec
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="icordebugevalcreatevalue-method"></a>ICorDebugEval::CreateValue-Methode
Erstellt einen Wert des angegebenen Typs mit einem Anfangswert von 0 (null) oder Null.  
  
 Diese Methode ist veraltet in .NET Framework, Version 2.0. Verwendung [ICorDebugEval2:: CreateValueForType](../../../../docs/framework/unmanaged-api/debugging/icordebugeval2-createvaluefortype-method.md) stattdessen.  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT CreateValue (  
    [in] CorElementType     elementType,  
    [in] ICorDebugClass     *pElementClass,  
    [out] ICorDebugValue    **ppValue  
);  
```  
  
#### <a name="parameters"></a>Parameter  
 `elementType`  
 [in] Der Wert der [CorElementType](../../../../docs/framework/unmanaged-api/metadata/corelementtype-enumeration.md) -Enumeration, der den Typ des Werts angibt.  
  
 `pElementClass`  
 [in] Zeiger auf eine [ICorDebugClass](../../../../docs/framework/unmanaged-api/debugging/icordebugclass-interface.md) -Objekt, das die Klasse der der Wert gibt an, wenn der Typ kein primitiver Typ ist.  
  
 `ppValue`  
 [out] Zeiger auf die Adresse eines Objekts "ICorDebugValue", das den Wert darstellt.  
  
## <a name="remarks"></a>Hinweise  
 `CreateValue` erstellt ein `ICorDebugValue` Objekt des angegebenen Typs für der einzige Zweck der Verwendung in einer funktionsauswertung. Dieser Wertobjekt kann verwendet werden, Benutzerkonstanten als Parameter übergeben.  
  
 Wenn der Typ des Werts ein primitiver Typ ist, ist der Anfangswert 0 (null) oder null. Verwendung [ICorDebugGenericValue:: SetValue](../../../../docs/framework/unmanaged-api/debugging/icordebuggenericvalue-setvalue-method.md) zum Festlegen des Werts eines primitiven Typs.  
  
 Wenn der Wert der `elementType` ELEMENT_TYPE_CLASS lautet, erhalten Sie eine "ICorDebugReferenceValue" (im zurückgegebenen `ppValue`), die null-Objektverweis darstellt. Dieses Objekt können Sie null für eine funktionsauswertung übergeben, die Objektverweisparameter verfügt. Kann nicht festgelegt werden die `ICorDebugValue` anderer Wert; er bleibt immer null.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** CorDebug.idl, CorDebug.h  
  
 **Bibliothek:** CorGuids.lib  
  
 **.NET Framework-Versionen:** 1.1, 1.0  
  
## <a name="see-also"></a>Siehe auch  
    
 [CreateValueForType-Methode](../../../../docs/framework/unmanaged-api/debugging/icordebugeval2-createvaluefortype-method.md)  
 ICorDebugValue
