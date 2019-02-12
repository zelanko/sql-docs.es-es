---
title: 'Especificar el atributo SQL: Inverse en SQL: Relationship (SQLXML 4.0) | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
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
author: MightyPen
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b925cd3dfde7ff5933e70f550cdafb1a62594e63
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56042896"
---
# <a name="specifying-the-sqlinverse-attribute-on-sqlrelationship-sqlxml-40"></a>Especificar el atributo sql:inverse en sql:relationship (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  El **SQL: Inverse** atributo es útil solo cuando se usa el esquema XSD para la carga masiva o por un diagrama de actualización. El **SQL: Inverse** atributo puede especificarse en el  **\<SQL: Relationship >** elemento. En diagramas de actualización, la lógica del diagrama de actualización interpreta el esquema para determinar las tablas y columnas actualizadas mediante la operación del diagrama de actualización. Las relaciones entre elementos primarios y secundarios que se especifican en el esquema determinan el orden en que se modifican (insertan o eliminan) los registros.  
  
 Si tiene un esquema XSD en el que la relación entre elementos primarios y secundarios se especifica en el orden inverso de la relación de clave principal y clave externa entre las columnas de base de datos correspondientes, se producirán errores en la operación de inserción o eliminación del diagrama de actualización debido a una infracción de clave principal o clave externa. En tales casos, el **SQL: Inverse** se especifica el atributo (**SQL: Inverse = "true"**) en el  **\<SQL: Relationship >** elemento y la lógica del diagrama de actualización interpreta su interpretación de la relación de elementos primarios y secundarios especificada en el esquema.  
  
 El **SQL: Inverse** atributo toma un valor booleano (0 = false, 1 = true). Los valores permitidos son 0, 1, true y false.  
  
 Para obtener un ejemplo de trabajo con el **SQL: Inverse** anotaciones, vea [especificar un esquema de asignación anotado en un diagrama de actualización](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Vea también  
 [Especificar relaciones mediante SQL: Relationship &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
  
  
