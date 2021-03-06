---
title: "Anwenden von CQRS- und CQS-Ansätzen in einem DDD-Microservice in eShopOnContainers"
description: ".NET-Microservicesarchitektur für .NET-Containeranwendungen | Anwenden von CQRS- und CQS-Ansätzen in einem DDD-Microservice in eShopOnContainers"
keywords: Docker, Microservices, ASP.NET, Container
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.topic: article
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 63e61a93aa2a162d7b48e0d423dab99dcea9d020
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/23/2017
---
# <a name="applying-cqrs-and-cqs-approaches-in-a-ddd-microservice-in-eshoponcontainers"></a>Anwenden von CQRS- und CQS-Ansätzen in einem DDD-Microservice in eShopOnContainers

Die Struktur des Microservices für Bestellungen in der Referenzanwendung „eShopOnContainers“ basiert auf CQRS-Prinzipien. Allerdings wird darin der einfachste Ansatz verwendet, bei dem Abfragen von Befehlen getrennt werden und dieselbe Datenbank für beide Aktionen dient.

Das Wichtigste daran ist, dass Abfragen idempotent sind: Egal wie oft Sie ein System abfragen, der Zustand des Systems ändert sich nicht, selbst wenn Sie ein anderes Datenmodell für Lesevorgänge verwenden als das Domänenmodell für Schreibvorgänge der Transaktionslogik, obwohl der Microservice für Bestellungen dieselbe Datenbank verwendet. Daher ist es ein vereinfachter CQRS-Ansatz.

Befehle, die Transaktionen und Datenupdates auslösen, ändern wiederum den Zustand im System. Mit Befehlen müssen Sie im Zusammenhang mit Komplexität und sich kontinuierlich ändernden Geschäftsregeln sorgfältig umgehen. An dieser Stelle können Sie DDD-Techniken anwenden, um das System besser zu modellieren.

Die in diesem Leitfaden vorgestellten DDD-Muster sollten nicht universell angewendet werden, denn sie wirken sich negativ auf Ihren Entwurf aus. Diese Einschränkungen haben zwar Vorteile wie höhere Qualität im Laufe der Zeit, vor allem bei Befehlen und anderen Codezeilen, die den Systemstatus ändern, erhöhen jedoch auch die Komplexität, was Nachteile für das Lesen und Abfragen von Daten hat.

Ein solches Muster ist das Aggregatmuster, das wir in späteren Abschnitten kennenlernen. Beim Aggregatmuster werden viele Domänenobjekte aufgrund ihrer Beziehung zur Domäne als eine einzelne Einheit behandelt. In Abfragen ist dieses Muster nicht immer vorteilhaft, da es die Komplexität der Abfragelogik verkomplizieren kann. Bei schreibgeschützten Abfragen werden viele Objekte nicht als einzelnes Aggregat behandelt. In diesem Fall erhöht sich nur die Komplexität.

Wie in Abbildung 9-2 dargestellt, empfiehlt dieser Leitfaden, DDD-Muster nur im Bereich der Transaktionen/Updates Ihres Microservices zu verwenden, d.h. in dem Bereich, in dem Befehle ausgelöst werden. Abfragen können einem einfacheren Ansatz folgen und sollten im Sinne des CQRS-Ansatzes von Befehlen getrennt werden.

Bei der Implementierung der Abfrageseite können Sie zwischen vielen Ansätzen wählen, z.B. ein vollständiger ORM wie EF Core, AutoMapper-Projektionen, gespeicherte Prozeduren, Ansichten, materialisierte Sichten oder ein Mikro-ORM.

In diesem Leitfaden und in eShopOnContainers (insbesondere beim Microservice für Bestellungen) implementieren wir direkte Abfragen mit dem Mikro-ORM [Dapper](https://github.com/StackExchange/dapper-dot-net). So können Sie jede Abfrage auf SQL-Anweisungen basierend implementieren, um aufgrund des schlanken Frameworks mit äußerst wenig Mehraufwand eine optimale Leistung zu erzielen.

Hinweis: Wenn Sie so vorgehen, erfordern alle Updates für das Modell, die in einer SQL-Datenbank aufbewahrt werden, auch separate Updates für SQL-Abfragen, die von Dapper oder anderen Abfrageansätzen (nicht EF) verwendet werden.

## <a name="cqrs-and-ddd-patterns-are-not-top-level-architectures"></a>CQRS und DDD-Muster sind keine Architekturen oberster Ebene

CQRS und die meisten DDD-Muster (z.B. DDD-Ebenen oder ein Domänenmodell mit Aggregaten) sind keine Architekturstile, sondern nur Architekturmuster. Microservices, SOA und ereignisgesteuerte Architekturen (Event-Driven Architecture, EDA) sind Beispiele für Architekturstile, denn Sie beschreiben ein System mit vielen Komponenten, z.B. viele Microservices. CQRS und DDD-Muster beschreiben etwas innerhalb eines einzelnen Systems oder einer einzelnen Komponente, in diesem Fall etwas in einem Microservice.

Unterschiedliche Kontextgrenzen (Bounded Contexts, BCs) wenden außerdem verschiedene Muster an. Sie haben unterschiedliche Aufgaben, und das führt häufig zu unterschiedlichen Lösungen. Wenn überall dasselbe Muster erzwungen wird, führt das jedoch zu einem Fehler. Daher sollten Sie dies auf keinen Fall tun. Viele Teilsysteme, BCs oder Microservices sind einfacher und können leichter mithilfe einfacher CRUD-Dienste oder einer anderen Lösung implementiert werden kann.

Es gibt nur eine Anwendungsarchitektur: die Architektur der System- oder der End-to-End-Anwendung, die Sie gerade entwerfen (z.B. die Microservicesarchitektur). Der Entwurf der einzelnen Kontextgrenzen oder Microservices in dieser Anwendung spiegelt die eigenen Vor-und Nachteile und die interne Entwurfsentscheidungen auf Ebene der Musterarchitektur wider. Wenden Sie auf keinen Fall überall dieselben Architekturmuster wie CQRS oder DDD an.

####  <a name="additional-resources"></a>Zusätzliche Ressourcen

-   **Martin Fowler. CQRS**
    [*https://martinfowler.com/bliki/CQRS.html*](https://martinfowler.com/bliki/CQRS.html)

-   **Greg Young. CQS vs. CQRS**
    [*http://codebetter.com/gregyoung/2009/08/13/command-query-separation/*](http://codebetter.com/gregyoung/2009/08/13/command-query-separation/)

-   **Greg Young. CQRS Documents (CQRS-Dokumente)**
    [*https://cqrs.files.wordpress.com/2010/11/cqrs\_documents.pdf*](https://cqrs.files.wordpress.com/2010/11/cqrs_documents.pdf)

-   **Greg Young. CQRS, Task Based UIs and Event Sourcing (CQRS, auf Aufgaben basierende Benutzeroberflächen und Ereignis-Sourcing)**
    [*http://codebetter.com/gregyoung/2010/02/16/cqrs-task-based-uis-event-sourcing-agh/*](http://codebetter.com/gregyoung/2010/02/16/cqrs-task-based-uis-event-sourcing-agh/)

-   **Udi Dahan. Clarified CQRS (Erläuterung zu CQRS)**
    [*http://udidahan.com/2009/12/09/clarified-cqrs/*](http://udidahan.com/2009/12/09/clarified-cqrs/)

-   **CQRS**
    [*http://udidahan.com/2009/12/09/clarified-cqrs/*](http://udidahan.com/2009/12/09/clarified-cqrs/)

-   **Event-Sourcing (ES)**
    [*http://codebetter.com/gregyoung/2010/02/20/why-use-event-sourcing/*](http://codebetter.com/gregyoung/2010/02/20/why-use-event-sourcing/)


>[!div class="step-by-step"]
[Zurück] (apply-simplified-microservice-cqrs-ddd-patterns.md) [Weiter] (cqrs-microservice-reads.md)
