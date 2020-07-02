---
title: 'Establecer el atributo SQL: inverso en SQL: Relationship (SQLXML)'
description: 'Aprenda a usar el atributo SQL: inverso en el elemento SQL: Relationship para especificar las relaciones entre las columnas de base de datos en una operación diagrama.'
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0bf9f98482ad83d1cf5104f9379ac294f2064c62
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85725880"
---
# <a name="specifying-the-sqlinverse-attribute-on-sqlrelationship-sqlxml-40"></a>Especificar el atributo sql:inverse en sql:relationship (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  El atributo **SQL: inverso** solo es útil cuando el esquema XSD se usa para la carga masiva o mediante un diagrama. El atributo **SQL: inverso** se puede especificar en el **\<sql:relationship>** elemento. En diagramas de actualización, la lógica del diagrama de actualización interpreta el esquema para determinar las tablas y columnas actualizadas mediante la operación del diagrama de actualización. Las relaciones entre elementos primarios y secundarios que se especifican en el esquema determinan el orden en que se modifican (insertan o eliminan) los registros.  
  
 Si tiene un esquema XSD en el que la relación entre elementos primarios y secundarios se especifica en el orden inverso de la relación de clave principal y clave externa entre las columnas de base de datos correspondientes, se producirán errores en la operación de inserción o eliminación del diagrama de actualización debido a una infracción de clave principal o clave externa. En tales casos, se especifica el atributo **SQL: inverso** (**SQL: inverso = "true"**) en el **\<sql:relationship>** elemento y la lógica diagrama inversa a su interpretación de la relación de elementos primarios y secundarios especificada en el esquema.  
  
 El atributo **SQL: inverso** toma un valor booleano (0 = false, 1 = true). Los valores permitidos son 0, 1, true y false.  
  
 Para obtener un ejemplo funcional del uso de la anotación **SQL: inverso** , vea [especificar un esquema de asignación anotado en un diagrama](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Consulte también  
 [Especificar relaciones mediante SQL: Relationship &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
  
  
