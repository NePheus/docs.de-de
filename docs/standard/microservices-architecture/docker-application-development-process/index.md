---
title: Entwicklungsprozess für auf Docker-basierende Anwendungen
description: .NET Microservices-Architektur für .NET-Containeranwendungen | Entwicklungsprozess für auf Docker-basierende Anwendungen
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 10/18/2017
ms.openlocfilehash: 881817f4f1007edad85eefb9002d56764cbf2a02
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="development-process-for-docker-based-applications"></a>Entwicklungsprozess für auf Docker-basierende Anwendungen

*Entwickeln Sie .NET-Containeranwendungen nach Ihren Wünschen, egal ob mit Fokus auf IDE mit Visual Studio und Visual Studio-Tools für Docker oder mit Fokus auf CLI/Editor mit Docker-CLI und Visual Studio Code.*

## <a name="development-environment-for-docker-apps"></a>Entwicklungsumgebung für Docker-Apps

### <a name="development-tool-choices-ide-or-editor"></a>Auswahlmöglichkeiten für das Entwicklungstool: IDE oder Editor

Egal, ob Sie eine vollständige und leistungsstarke integrierte Entwicklungsumgebung (IDE) oder einen einfachen und agilen Editor bevorzugen: Microsoft bietet Ihnen Tools, die Sie zum Entwickeln von Docker-Anwendungen verwenden können.

**Visual Studio (für Windows)**. Um Docker-basierte Anwendungen zu entwickeln, verwenden Sie Visual Studio 2017 oder höhere Versionen, die Tools für Docker enthalten, die bereits integriert sind. Mit den Tools für Docker können Sie Ihre Anwendungen direkt in der Docker-Zielumgebung entwickeln, ausführen und überprüfen. Sie können F5 drücken, um Ihre Anwendungen (einzelner oder mehrere Container) direkt in einem Docker-Host auszuführen und zu debuggen. Alternativ drücken Sie STRG+F5, um Ihre Anwendungen zu bearbeiten und zu aktualisieren, ohne den Container erneut erstellen zu müssen. Dies ist die leistungsstärkste Entwicklungsoption für Docker-basierte Anwendungen.

**Visual Studio für Mac**. Es handelt sich um eine IDE, eine Weiterentwicklung von Xamarin Studio, die unter macOS ausgeführt wird und die Docker-basierte Anwendungsentwicklung unterstützt. Dies sollte die bevorzugte Wahl für Entwickler sein, die auf Mac-Computern arbeiten und eine leistungsfähige IDE verwenden möchten.

**Visual Studio Code und Docker-CLI** Wenn Sie einen einfachen und plattformübergreifenden Editor bevorzugen, der jede beliebige Entwicklungssprache unterstützt, können Sie Microsoft Visual Studio Code (VS Code) sowie die Docker-CLI verwenden. Dies ist ein plattformübergreifender Entwicklungsansatz für Mac, Linux und Windows.

Durch Installation der Tools der [Docker Community Edition (CE)](https://www.docker.com/community-edition) können Sie eine einzelne Docker-CLI zum Erstellen von Apps für Windows und Linux verwenden. Zusätzlich unterstützt Visual Studio Code Erweiterungen für Docker, z.B. IntelliSense für Docker-Dateien und Verknüpfungsaufgaben, um Docker-Befehle aus dem Editor auszuführen.

### <a name="additional-resources"></a>Zusätzliche Ressourcen

-   **Visual Studio-Tools für Docker**
    [*https://docs.microsoft.com/aspnet/core/publishing/visual-studio-tools-for-docker*](https://docs.microsoft.com/aspnet/core/publishing/visual-studio-tools-for-docker)

-   **Visual Studio Code**. Offizielle Website.
    [*https://code.visualstudio.com/download*](https://code.visualstudio.com/download)

-   **Docker Community Edition (CE) für Macintosh und Windows**
    [*https://www.docker.com/community-editions*](https://www.docker.com/community-edition)

## <a name="net-languages-and-frameworks-for-docker-containers"></a>.NET-Sprachen und -Frameworks für Docker-Container

Wie in vorherigen Abschnitten diese Handbuchs erwähnt, können Sie .NET Framework, .NET Core oder das Open-Source-Mono-Projekt verwenden, wenn Sie .NET-Containeranwendungen für Docker entwickeln. Sie können C\#, F\# oder Visual Studio entwickeln, wenn Sie Linux- oder Windows-Container als Ziel haben, je nachdem, welches .NET-Framework verwendet wird. Weitere Details zu .NET-Sprachen finden Sie im Blogbeitrag [The .NET Language Strategy (Strategie für die .NET-Sprache)](https://blogs.msdn.microsoft.com/dotnet/2017/02/01/the-net-language-strategy/).


>[!div class="step-by-step"]
[Zurück] (../architect-microservice-container-applications/using-azure-service-fabric.md) [Weiter] (docker-app-development-workflow.md)
