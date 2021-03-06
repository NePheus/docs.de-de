---
title: CorBindToCurrentRuntime-Funktion
ms.date: 03/30/2017
api_name:
- CorBindToCurrentRuntime
api_location:
- mscoree.dll
- mscoreei.dll
api_type:
- HeaderDef
f1_keywords:
- CorBindToCurrentRuntime
helpviewer_keywords:
- CorBindToCurrentRuntime function [.NET Framework hosting]
ms.assetid: 6105c13e-d9cd-44d2-a95a-924e042830c7
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 3667ac5a19664507b767ee6c5421a5e93f6cdfe0
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="corbindtocurrentruntime-function"></a>CorBindToCurrentRuntime-Funktion
Lädt die Common Language Runtime (CLR) in einen Prozess, indem in einer XML-Datei gespeicherte Versionsinformationen verwendet werden. Das Format der XML-Datei ist der standard-Anwendungskonfigurationsdatei nachgebildet. Weitere Informationen zu Konfigurationsdateien finden Sie unter [Konfigurationsdateienschema](../../../../docs/framework/configure-apps/file-schema/index.md).  
  
 Diese Funktion ist in [!INCLUDE[net_v40_long](../../../../includes/net-v40-long-md.md)] veraltet. Finden Sie unter [Laden der Common Language Runtime in einen Prozess](http://msdn.microsoft.com/library/1e2d6dc1-6aab-43e2-bbc0-aae40756d24f).  
  
## <a name="syntax"></a>Syntax  
  
```  
HRESULT CorBindToCurrentRuntime (  
    [in]  LPCWSTR   pwszFileName,  
    [in]  REFCLSID  rclsid,  
    [in]  REFIID    riid,  
    [out] LPVOID    *ppv  
);  
```  
  
#### <a name="parameters"></a>Parameter  
 `pwszFileName`  
 [in] Der Name von einer Anwendungskonfigurationsdatei, die angibt, die Version der CLR geladen. Wenn der Dateiname nicht vollständig qualifiziert ist, wird davon ausgegangen werden im gleichen Verzeichnis wie die ausführbare Datei, die den Aufruf.  
  
 Die Version der Laufzeit geladen werden, wird durch das Versionsattribut in beschrieben die [ \<RequiredRuntime >](../../../../docs/framework/configure-apps/file-schema/startup/requiredruntime-element.md) Element der Konfigurationsdatei.  
  
 Wenn keine Version angegeben ist, oder wenn die `<requiredRuntime>` Element kann nicht gefunden werden, die neueste Version der CLR, die auf dem Computer installiert ist, wird geladen.  
  
 `rclsid`  
 [in] Die `CLSID` der Co-Klasse, die entweder implementiert die [ICorRuntimeHost](../../../../docs/framework/unmanaged-api/hosting/icorruntimehost-interface.md) oder [ICLRRuntimeHost](../../../../docs/framework/unmanaged-api/hosting/iclrruntimehost-interface.md) Schnittstelle. Unterstützte Werte sind "CLSID_CorRuntimeHost" oder "CLSID_CLRRuntimeHost".  
  
 `riid`  
 [in] Die `IID` der angeforderten Schnittstelle. Unterstützte Werte sind "IID_ICorRuntimeHost" oder "IID_ICLRRuntimeHost".  
  
 `ppv`  
 [out] Der zurückgegebene Schnittstellenzeiger.  
  
## <a name="requirements"></a>Anforderungen  
 **Plattformen:** finden Sie unter [Systemanforderungen](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Header:** MSCorEE.h  
  
 **Bibliothek:** "Mscoree.dll"  
  
 **.NET Framework-Versionen:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Siehe auch  
 [CorBindToRuntime-Funktion](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntime-function.md)  
 [CorBindToRuntimeByCfg-Funktion](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimebycfg-function.md)  
 [CorBindToRuntimeEx-Funktion](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimeex-function.md)  
 [CorBindToRuntimeHost-Funktion](../../../../docs/framework/unmanaged-api/hosting/corbindtoruntimehost-function.md)  
 [ICorRuntimeHost-Schnittstelle](../../../../docs/framework/unmanaged-api/hosting/icorruntimehost-interface.md)  
 [Veraltete CLR-Hostingfunktionen](../../../../docs/framework/unmanaged-api/hosting/deprecated-clr-hosting-functions.md)
