---
title: Einschränkung der referenziellen Integrität
ms.date: 03/30/2017
ms.assetid: 3d3ba44b-4302-40d8-a7a9-62932e0395e5
ms.openlocfilehash: a4d63e07da0c75b8a0369933fccfc0cc66fcc40b
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2018
---
# <a name="referential-integrity-constraint"></a>Einschränkung der referenziellen Integrität
Ein *Einschränkung der referenziellen Integrität* im Entity Data Model (EDM) ähnelt einer Einschränkung der referenziellen Integrität in einer relationalen Datenbank. Auf die gleiche Weise, dass eine Spalte (oder Spalten) aus einer Datenbanktabelle auf den Primärschlüssel einer anderen Tabelle verweisen können eine [Eigenschaft](../../../../docs/framework/data/adonet/property.md) (oder Eigenschaften) von einem [Entitätstyp](../../../../docs/framework/data/adonet/entity-type.md) verweisen können die [Entitätsschlüssel ](../../../../docs/framework/data/adonet/entity-key.md) eines anderen Entitätstyps. Der Entitätstyp, auf die verwiesen wird, aufgerufen wird die *prinzipalende* der Einschränkung. Der Entitätstyp, der auf das prinzipalende verweist heißt die *abhängiges Ende* der Einschränkung.  
  
 Eine Einschränkung der referenziellen Integrität wird definiert als Teil einer [Zuordnung](../../../../docs/framework/data/adonet/association-type.md) zwischen zwei Entitätstypen. Die Definition für eine Einschränkung der referenziellen Integrität gibt die folgenden Informationen an:  
  
-   Das Prinzipalende der Einschränkung. (Ein Entitätstyp, auf dessen Entitätsschlüssel durch das abhängige Ende verwiesen wird.)  
  
-   Den Entitätsschlüssel des Prinzipalendes.  
  
-   Das abhängige Ende der Einschränkung. (Ein Entitätstyp, der über eine Eigenschaft oder Eigenschaften verfügt, die auf den Entitätsschlüssel des Prinzipalendes verweisen.)  
  
-   Die verweisende Eigenschaft oder Eigenschaften des abhängigen Endes.  
  
 Mit Einschränkungen der referenziellen Integrität im EDM soll sichergestellt werden, dass gültige Zuordnungen immer vorhanden sind. Weitere Informationen finden Sie unter [Fremdschlüsseleigenschaft](../../../../docs/framework/data/adonet/foreign-key-property.md).  
  
## <a name="example"></a>Beispiel  
 Die unten stehende Abbildung zeigt ein konzeptionelles Modell mit zwei Zuordnungen: `WrittenBy` und `PublishedBy`. Der `Book`-Entitätstyp verfügt über die Eigenschaft `PublisherId`, die auf den Entitätsschlüssel des `Publisher`-Entitätstyps verweist, wenn Sie eine Einschränkung der referenziellen Integrität für die `PublishedBy`-Zuordnung definieren.  
  
 ![RefConstraintModel](../../../../docs/framework/data/adonet/media/refconstraintmodel.gif "RefConstraintModel")  
  
 Die [ADO.NET Entity Framework](../../../../docs/framework/data/adonet/ef/index.md) verwendet eine domänenspezifische Sprache (DSL) Bezeichnung konzeptionelle Schemadefinitionssprache ([CSDL](../../../../docs/framework/data/adonet/ef/language-reference/csdl-specification.md)) um konzeptionelle Modelle zu definieren. Die folgende CSDL definiert eine Einschränkung der referenziellen Integrität für die oben im konzeptionellen Modell gezeigte `PublishedBy`-Zuordnung.  
  
 [!code-xml[EDM_Example_Model#RefConstraint](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books4.edmx#refconstraint)]  
  
## <a name="see-also"></a>Siehe auch  
 [Schlüsselkonzepte im Entity Data Model](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)  
 [Entity Data Model](../../../../docs/framework/data/adonet/entity-data-model.md)
