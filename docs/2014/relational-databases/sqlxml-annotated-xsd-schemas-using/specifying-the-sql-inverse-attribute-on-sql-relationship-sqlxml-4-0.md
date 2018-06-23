---
title: 'Especificar el atributo SQL: Inverse en SQL: Relationship (SQLXML 4.0) | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- sql:relationship
- bulk load [SQLXML]
- inverse attribute
- relationships [SQLXML], inverse orders
- relationship annotation
- XSD schemas [SQLXML], relationships
- annotated XSD schemas, relationships
- updategrams [SQLXML], relationships
- sql:inverse
ms.assetid: 08904cbd-9c86-493d-90c3-f5e1d13ce59d
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 66cbeee228a5f186317eb69d4b0dad899c9c1252
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199309"
---
# <a name="specifying-the-sqlinverse-attribute-on-sqlrelationship-sqlxml-40"></a>Especificar el atributo sql:inverse en sql:relationship (SQLXML 4.0)
  El atributo `sql:inverse` solamente resulta útil cuando se utiliza el esquema XSD, ya sea para la carga masiva o por parte de un diagrama de actualización. El `sql:inverse` atributo puede especificarse en el  **\<SQL: Relationship >** elemento. En diagramas de actualización, la lógica del diagrama de actualización interpreta el esquema para determinar las tablas y columnas actualizadas mediante la operación del diagrama de actualización. Las relaciones entre elementos primarios y secundarios que se especifican en el esquema determinan el orden en que se modifican (insertan o eliminan) los registros.  
  
 Si tiene un esquema XSD en el que la relación entre elementos primarios y secundarios se especifica en el orden inverso de la relación de clave principal y clave externa entre las columnas de base de datos correspondientes, se producirán errores en la operación de inserción o eliminación del diagrama de actualización debido a una infracción de clave principal o clave externa. En tales casos, la `sql:inverse` se especifica el atributo (`sql:inverse="true"`) en el  **\<SQL: Relationship >** elemento y los inversos de lógica de updategram su interpretación de la relación de elementos primarios y secundarios especificada en el esquema.  
  
 El atributo `sql:inverse` toma un valor booleano (0=false, 1=true). Los valores permitidos son 0, 1, true y false.  
  
 Para un ejemplo funcional del uso del `sql:inverse` anotación, consulte [especificar un esquema de asignación anotados en un diagrama de actualización](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Vea también  
 [Especificar relaciones mediante SQL: Relationship &#40;SQLXML 4.0&#41;](specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
  
  