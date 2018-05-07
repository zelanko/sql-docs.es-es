---
title: 'Especificar el atributo SQL: Inverse en SQL: Relationship (SQLXML 4.0) | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
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
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: fc17770157758286731f31922daded8f74acc152
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="specifying-the-sqlinverse-attribute-on-sqlrelationship-sqlxml-40"></a>Especificar el atributo sql:inverse en sql:relationship (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  El **SQL: Inverse** atributo es útil solo cuando se usa el esquema XSD para la carga masiva o un diagrama de actualización. El **SQL: Inverse** atributo puede especificarse en el  **\<SQL: Relationship >** elemento. En diagramas de actualización, la lógica del diagrama de actualización interpreta el esquema para determinar las tablas y columnas actualizadas mediante la operación del diagrama de actualización. Las relaciones entre elementos primarios y secundarios que se especifican en el esquema determinan el orden en que se modifican (insertan o eliminan) los registros.  
  
 Si tiene un esquema XSD en el que la relación entre elementos primarios y secundarios se especifica en el orden inverso de la relación de clave principal y clave externa entre las columnas de base de datos correspondientes, se producirán errores en la operación de inserción o eliminación del diagrama de actualización debido a una infracción de clave principal o clave externa. En tales casos, la **SQL: Inverse** se especifica el atributo (**SQL: Inverse = "true"**) en el  **\<SQL: Relationship >** elemento y la lógica del diagrama de actualización inversos su interpretación de la relación de elementos primarios y secundarios especificados en el esquema.  
  
 El **SQL: Inverse** atributo toma un valor booleano (0 = false, 1 = true). Los valores permitidos son 0, 1, true y false.  
  
 Para un ejemplo funcional del uso del **SQL: Inverse** anotación, consulte [especificar un esquema de asignación anotados en un diagrama de actualización](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Vea también  
 [Especificar relaciones mediante SQL: Relationship &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
  
  
