---
title: Establecer el atributo sql:inverse en sql:relationship (SQLXML)
description: Aprenda a usar el atributo sql:inverse en el elemento sql:relationship para especificar relaciones entre columnas de base de datos en una operación de diagrama de actualización.
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
ms.openlocfilehash: fe5409120a3d0c5df3cf05318b0b85fd22d07bdf
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388092"
---
# <a name="specifying-the-sqlinverse-attribute-on-sqlrelationship-sqlxml-40"></a>Especificar el atributo sql:inverse en sql:relationship (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  El atributo **sql:inverse** solo es útil cuando el esquema XSD se utiliza para la carga masiva o mediante un diagrama de actualización. El atributo **sql:inverse** se puede especificar en el ** \<elemento sql:relationship>.** En diagramas de actualización, la lógica del diagrama de actualización interpreta el esquema para determinar las tablas y columnas actualizadas mediante la operación del diagrama de actualización. Las relaciones entre elementos primarios y secundarios que se especifican en el esquema determinan el orden en que se modifican (insertan o eliminan) los registros.  
  
 Si tiene un esquema XSD en el que la relación entre elementos primarios y secundarios se especifica en el orden inverso de la relación de clave principal y clave externa entre las columnas de base de datos correspondientes, se producirán errores en la operación de inserción o eliminación del diagrama de actualización debido a una infracción de clave principal o clave externa. En tales casos, el atributo **sql:inverse** se especifica (**sql:inverse-"true"**) en el ** \<elemento sql:relationship>** y la lógica de diagrama de actualización inversa su interpretación de la relación primario-secundario especificada en el esquema.  
  
 El atributo **sql:inverse** toma un valor booleano (0-false, 1-true). Los valores permitidos son 0, 1, true y false.  
  
 Para obtener un ejemplo de trabajo mediante la anotación **sql:inverse,** vea Especificar un esquema de [asignación anotado en un diagrama](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)de actualización .  
  
## <a name="see-also"></a>Consulte también  
 [Especificación de relaciones mediante sql:relationship &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
  
  
