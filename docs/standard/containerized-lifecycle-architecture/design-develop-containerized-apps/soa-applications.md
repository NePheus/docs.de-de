---
title: SOA-Anwendungen
description: Lebenszyklus von Docker-Containeranwendungen mit der Microsoft-Plattform und Tools
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 09/22/2017
ms.openlocfilehash: 37313c4eb437b6b7a362456a7d1ee3b3aecb6020
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="soa-applications"></a>SOA-Anwendungen

SOA wurde ein Überbelastung Begriff und so viele verschiedene Bedeutungen für verschiedene Benutzer vorgesehen. Aber zumindest und als gemeinsame Nenner, SOA oder dienstausrichtung, Mittelwert Struktur die Architektur der Anwendung durch zerlegen es in mehreren Diensten (meist als HTTP-Dienste), die in verschiedenen Arten klassifiziert werden können Subsysteme oder in anderen Fällen wie leisten.

Heute können Sie diese Dienste als Docker-Containern bereitstellen, löst die Probleme in Bezug auf Bereitstellung, da alle Abhängigkeiten in Container-Abbild enthalten sind. Jedoch wenn dienstorientierter Architekturen mit horizontaler Skalierung Sie müssen, möglicherweise Probleme auftreten, wenn Sie basierend auf einzelne Instanzen bereitstellen. Dies ist, bei denen ein clustering-Software oder Orchestrator Docker Sie beitragen. Betrachten wir dies im nächsten Abschnitt ausführlich beim Untersuchen wir Microservices Ansätze.

Am Ende des Tages eignen sich die Container-clustering-Lösungen für beide eine herkömmliche SOA-Architektur oder für eine erweiterte Microservices-Architektur, in der jede Microservice seine Datenmodell besitzt. Und Dank mehrere Datenbanken Sie auch können mit horizontaler Skalierung die Datenebene statt arbeiten mit monolithisch Datenbanken, die von der SOA-Diensten gemeinsam genutzt. Ist jedoch die Erläuterung zum Teilen der Daten ausschließlich über die Architektur und Entwurf.


>[!div class="step-by-step"]
[Vorherigen] (State-and-data-in-docker-applications.md) [weiter] (orchestrieren-High-Skalierbarkeit-availability.md)
