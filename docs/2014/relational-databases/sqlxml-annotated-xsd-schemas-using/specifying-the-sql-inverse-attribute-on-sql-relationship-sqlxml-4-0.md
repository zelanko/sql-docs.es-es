---
title: 'Especificar el atributo SQL: Inverse en SQL: Relationship (SQLXML 4.0) | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5bb1d16ef1caf6622a2da1dd1c2c9674cf2b9d0c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48164585"
---
# <a name="specifying-the-sqlinverse-attribute-on-sqlrelationship-sqlxml-40"></a>Especificar el atributo sql:inverse en sql:relationship (SQLXML 4.0)
  El atributo `sql:inverse` solamente resulta útil cuando se utiliza el esquema XSD, ya sea para la carga masiva o por parte de un diagrama de actualización. El `sql:inverse` atributo puede especificarse en el  **\<SQL: Relationship >** elemento. En diagramas de actualización, la lógica del diagrama de actualización interpreta el esquema para determinar las tablas y columnas actualizadas mediante la operación del diagrama de actualización. Las relaciones entre elementos primarios y secundarios que se especifican en el esquema determinan el orden en que se modifican (insertan o eliminan) los registros.  
  
 Si tiene un esquema XSD en el que la relación entre elementos primarios y secundarios se especifica en el orden inverso de la relación de clave principal y clave externa entre las columnas de base de datos correspondientes, se producirán errores en la operación de inserción o eliminación del diagrama de actualización debido a una infracción de clave principal o clave externa. En tales casos, el `sql:inverse` se especifica el atributo (`sql:inverse="true"`) en el  **\<SQL: Relationship >** elemento y los inversos de lógica del diagrama de actualización su interpretación de la relación de elementos primarios y secundarios especificada en el esquema.  
  
 El atributo `sql:inverse` toma un valor booleano (0=false, 1=true). Los valores permitidos son 0, 1, true y false.  
  
 Para obtener un ejemplo de trabajo con el `sql:inverse` anotaciones, vea [especificar un esquema de asignación anotado en un diagrama de actualización](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Vea también  
 [Especificar relaciones mediante SQL: Relationship &#40;SQLXML 4.0&#41;](specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
  
  
