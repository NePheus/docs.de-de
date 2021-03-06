---
title: 'Portieren auf .NET Core: Verwenden von Windows Compatibility Pack'
description: Erfahren Sie mehr über Windows Compatibility Pack und die Verwendungsmöglichkeiten, um vorhandenen .NET Framework-Code auf .NET Core zu portieren
author: terrajobst
ms.author: mairaw
ms.date: 11/13/2017
ms.openlocfilehash: 6b25a2d5c197a6c9b0a7ead18370870ddc091e1c
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="using-the-windows-compatibility-pack"></a>Verwenden von Windows Compatibility Pack

Zu den häufigsten Problemen, auf die Entwickler beim Portieren von vorhandenem Code zu .NET Core stoßen, zählt die Abhängigkeit von APIs und Technologien, die nur in .NET Framework vorhanden sind. Durch *Windows Compatibility Pack* werden viele dieser Technologien bereitgestellt, sodass das Erstellen von .NET Core-Anwendungen und .NET Standard-Bibliotheken für vorhandenen Code besser umsetzbar ist.

Bei diesem Paket handelt es sich um eine logische [Erweiterung von .NET Standard 2.0](../whats-new/index.md#api-changes-and-library-support), durch die der API-Satz erheblich erhöht wird und vorhandener Code nahezu ohne Änderungen kompiliert wird. Damit das Versprechen von .NET Standard („der API-Satz, den alle .NET-Implementierungen bereitstellen“) eingehalten werden kann, gilt dies nicht für Technologien, die nicht auf allen Plattformen funktionieren können, z.B. die Registrierung, Windows-Verwaltungsinstrumentation (WMI) oder APIs für die Reflektionsausgabe.

*Windows Compatibility Pack* basiert auf .NET Standard und stellt Technologien bereit, die nur unter Windows verfügbar sind. Für Kunden, die zu .NET Core wechseln, aber Windows beibehalten möchten, ist dies ein nützlicher erster Schritt. In diesem Szenario stellt es bei der Migration eine Hürde ohne architektonische Vorteile dar, wenn Windows-Technologien nicht verwendet werden können.

## <a name="package-contents"></a>Paketinhalt

*Windows Compatibility Pack* wird über das NuGet-Paket [Microsoft.Windows.Compatibility](https://www.nuget.org/packages/Microsoft.Windows.Compatibility) bereitgestellt werden, und Projekte, die .NET Core oder .NET Standard anzielen, können darauf verweisen.

Es werden über 20.000 APIs aus folgenden Technologiebereichen bereitgestellt, darunter befinden sich sowohl Windows-APIs als auch plattformübergreifende APIs:

* Codepages
* CodeDom
* Konfiguration
* Verzeichnisdienste
* Zeichnung
* ODBC
* Berechtigungen
* Ports
* Windows-Zugriffssteuerungslisten (Access Control List, ACL)
* Windows Communication Foundation (WCF)
* Windows-Kryptografie
* Windows-EventLog
* Windows Management Instrumentation (WMI)
* Windows-Leistungsindikatoren
* Windows-Registrierung
* Zwischenspeichern von Windows-Runtime
* Windows-Dienste

Weitere Informationen finden Sie unter [Windows Compatibility Pack](https://github.com/dotnet/designs/blob/master/accepted/compat-pack/compat-pack.md).

## <a name="get-started"></a>Erste Schritte

1. Machen Sie sich vor dem Portieren mit dem [Portiervorgang](index.md) vertraut.

2. Wenn Sie vorhandenen Code zu .NET Core oder .NET Standard portieren, installieren Sie das NuGet-Paket [Microsoft.Windows.Compatibility](https://www.nuget.org/packages/Microsoft.Windows.Compatibility).

3. Wenn Sie Windows beibehalten möchten, können Sie sofort beginnen.

4. Wenn Sie die .NET Core-Anwendung oder die .NET Standard-Bibliothek unter Linux oder macOS ausführen möchten, verwenden Sie [API Analyzer](https://blogs.msdn.microsoft.com/dotnet/2017/10/31/introducing-api-analyzer/), um die Verwendungen der APIs zu ermitteln, die nicht plattformübergreifend funktionieren.

5. Entfernen Sie die Verwendungen dieser APIs, ersetzen Sie diese durch plattformübergreifende Alternativen, oder schützen Sie diese folgendermaßen mithilfe einer Plattformüberprüfung:

    ```csharp
    private static string GetLoggingPath()
    {
        // Verify the code is running on Windows.
        if (RuntimeInformation.IsOSPlatform(OSPlatform.Windows))
        {
            using (var key = Registry.CurrentUser.OpenSubKey(@"Software\Fabrikam\AssetManagement"))
            {
                if (key?.GetValue("LoggingDirectoryPath") is string configuredPath)
                    return configuredPath;
            }
        }

        // This is either not running on Windows or no logging path was configured,
        // so just use the path for non-roaming user-specific data files.
        var appDataPath = Environment.GetFolderPath(Environment.SpecialFolder.LocalApplicationData);
        return Path.Combine(appDataPath, "Fabrikam", "AssetManagement", "Logging");
    }
    ```

Eine Demo finden Sie in diesem [Channel 9 video of the Windows Compatibility Pack (Video von Channel 9 über Windows Compatibility Pack)](https://channel9.msdn.com/Events/Connect/2017/T123).

