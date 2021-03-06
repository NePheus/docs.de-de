---
title: CreateClassEnumWmi-Funktion (Referenz zur nicht verwalteten API)
description: Die CreateClassEnumWmi-Funktion gibt einen Enumerator für alle Klassen, die bestimmte Kriterien erfüllen.
ms.date: 11/06/2017
api_name:
- CreateClassEnumWmi
api_location:
- WMINet_Utils.dll
api_type:
- DLLExport
f1_keywords:
- CreateClassEnumWmi
helpviewer_keywords:
- CreateClassEnumWmi function [.NET WMI and performance counters]
topic_type:
- Reference
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3f84902586a2b940d52eb6365a141af61af802dd
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="createclassenumwmi-function"></a>CreateClassEnumWmi-Funktion
Gibt einen Enumerator für alle Klassen, die die angegebenen Auswahlkriterien entsprechen.  

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT CreateClassEnumWmi (
   [in] BSTR                    strSuperclass,
   [in] long                    lFlags,
   [in] IWbemContext*           pCtx,
   [out] IEnumWbemClassObject** ppEnum,
   [in] DWORD                   authLevel,
   [in] DWORD                   impLevel,
   [in] IWbemServices*          pCurrentNamespace,
   [in] BSTR                    strUser,
   [in] BSTR                    strPassword,
   [in] BSTR                    strAuthority
); 
```  

## <a name="parameters"></a>Parameter

`strSuperclass`    
[in] Wenn dies nicht der `null` oder leer ist, gibt den Namen einer übergeordneten Klasse; der Enumerator gibt nur Unterklassen dieser Klasse zurück. Ist er `null` oder leer und `lFlags` WBEM_FLAG_SHALLOW ist, wird nur auf oberster Ebene Klassen (mit keinen übergeordneten Klasse). Ist er `null` oder leer und `lFlags` ist `WBEM_FLAG_DEEP`, alle Klassen im Namespace zurückgegeben.

`lFlags`   
[in] Eine Kombination von Flags, die das Verhalten dieser Funktion beeinflussen. Die folgenden Werte werden definiert, der *WbemCli.h* Header-Datei, oder Sie können diese definieren als Konstanten in Ihrem Code: 

|Konstante  |Wert  |Beschreibung  |
|---------|---------|---------|
| `WBEM_FLAG_USE_AMENDED_QUALIFIERS` | 0 x 20000 | Wenn festgelegt ist, die Funktion ruft die Qualifizierern in den lokalisierten Namespace des Gebietsschemas für die aktuelle Verbindung gespeichert ab. <br/> Wenn dies nicht festgelegt ist, die Funktion ruft nur die Qualifizierer, die in den unmittelbaren Namespace gespeichert. |
| `WBEM_FLAG_DEEP` | 0 | Die Enumeration enthält alle Unterklassen in der Hierarchie, aber nicht für diese Klasse. |
| `WBEM_FLAG_SHALLOW` | 1 | Die Enumeration schließt nur reine Instanzen dieser Klasse und schließt alle Instanzen von Unterklassen, die Eigenschaften, die nicht in dieser Klasse angeben. |
| `WBEM_FLAG_RETURN_IMMEDIATELY` | 0x10 | Das Flag wird halbsynchrone aufgerufen. |
| `WBEM_FLAG_FORWARD_ONLY` | 0x20 | Die Funktion gibt einen Enumerator Vorwärtscursor. In der Regel nur vorwärts Enumeratoren werden schneller ausgeführt und belegen weniger Speicher als konventionelle Enumeratoren, aber es nicht möglich, dass Aufrufe [Klon](clone.md). |
| `WBEM_FLAG_BIDIRECTIONAL` | 0 | WMI behält Zeiger auf Objekte in der Enumration, bis sie veröffentlicht werden. | 

Die empfohlene Flags sind `WBEM_FLAG_RETURN_IMMEDIATELY` und `WBEM_FLAG_FORWARD_ONLY` für optimale Leistung zu erzielen.

`pCtx`  
[in] In der Regel wird dieser Wert ist `null`. Andernfalls ist ein Zeiger auf ein ["IWbemContext"](https://msdn.microsoft.com/library/aa391465(v=vs.85).aspx) -Instanz, die vom Anbieter verwendet werden kann, das die angeforderte Klassen bereitstellt. 

`ppEnum`  
[out] Erhält der Zeiger auf den Enumerator.

`authLevel`  
[in] Die Autorisierungsebene.

`impLevel` [in] Die Ebene des Identitätswechsels.

`pCurrentNamespace`   
[in] Ein Zeiger auf ein [IWbemServices](https://msdn.microsoft.com/library/aa392093(v=vs.85).aspx) -Objekt, das den aktuellen Namespace darstellt.

`strUser`   
[in] Der Benutzername. Finden Sie unter der [ConnectServerWmi](connectserverwmi.md) -Funktion für Weitere Informationen.

`strPassword`   
[in] Das Kennwort. Finden Sie unter der [ConnectServerWmi](connectserverwmi.md) -Funktion für Weitere Informationen.

`strAuthority`   
[in] Der Domänenname des Benutzers. Finden Sie unter der [ConnectServerWmi](connectserverwmi.md) -Funktion für Weitere Informationen.

## <a name="return-value"></a>Rückgabewert

Die folgenden Werte, die von dieser Funktion zurückgegebenen werden definiert, der *WbemCli.h* Header-Datei, oder Sie können diese definieren als Konstanten in Ihrem Code:

|Konstante  |Wert  |Beschreibung  |
|---------|---------|---------|
| `WBEM_E_ACCESS_DENIED` | 0 x 80041003 | Der Benutzer keine Berechtigung zum Anzeigen, eine oder mehrere Klassen, die die Funktion zurückgeben kann. |
| `WBEM_E_FAILED` | 0 x 80041001 | Nicht angegebener Fehler ist aufgetreten. |
| `WBEM_E_INVALID_CLASS` | 0 x 80041010 | `strSuperClass` existiert nicht. |
| `WBEM_E_INVALID_PARAMETER` | 0 x 80041008 | Ein Parameter ist ungültig. |
| `WBEM_E_OUT_OF_MEMORY` | 0x80041006 | Es ist nicht genügend Arbeitsspeicher verfügbar, um den Vorgang abzuschließen. |
| `WBEM_E_SHUTTING_DOWN` | 0x80041033 | WMI wurde wahrscheinlich beendet und neu gestartet. Rufen Sie [ConnectServerWmi](connectserverwmi.md) erneut aus. |
| `WBEM_E_TRANSPORT_FAILURE` | 0x80041015 | Der Remoteprozeduraufruf (RPC)-Link zwischen dem aktuellen Prozess und die WMI-ausgefallen ist. |
|`WBEM_S_NO_ERROR` | 0 | Der Funktionsaufruf war erfolgreich.  |
  
## <a name="remarks"></a>Hinweise

Diese Funktion dient als Wrapper für einen Aufruf der [IWbemServices::CreateClassEnum](https://msdn.microsoft.com/library/aa392095(v=vs.85).aspx) Methode.

Wenn der Funktionsaufruf fehlschlägt, können Sie zusätzliche Fehlerinformationen abrufen, durch Aufrufen der [GetErrorInfo](geterrorinfo.md) Funktion.

## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** WMINet_Utils.idl  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]  
  
## <a name="see-also"></a>Siehe auch  
[WMI und Leistungsindikatoren (Referenz zur nicht verwalteten API)](index.md)
