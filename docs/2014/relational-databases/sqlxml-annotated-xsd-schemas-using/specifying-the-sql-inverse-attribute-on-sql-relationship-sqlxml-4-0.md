---
title: 'Especificar el atributo SQL: inverso en SQL: Relationship (SQLXML 4,0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 5b0781102371b98cced72a5a0edee70c9567c372
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85003071"
---
# <a name="specifying-the-sqlinverse-attribute-on-sqlrelationship-sqlxml-40"></a>Especificar el atributo sql:inverse en sql:relationship (SQLXML 4.0)
  El atributo `sql:inverse` solamente resulta útil cuando se utiliza el esquema XSD, ya sea para la carga masiva o por parte de un diagrama de actualización. El `sql:inverse` atributo se puede especificar en el **\<sql:relationship>** elemento. En diagramas de actualización, la lógica del diagrama de actualización interpreta el esquema para determinar las tablas y columnas actualizadas mediante la operación del diagrama de actualización. Las relaciones entre elementos primarios y secundarios que se especifican en el esquema determinan el orden en que se modifican (insertan o eliminan) los registros.  
  
 Si tiene un esquema XSD en el que la relación entre elementos primarios y secundarios se especifica en el orden inverso de la relación de clave principal y clave externa entre las columnas de base de datos correspondientes, se producirán errores en la operación de inserción o eliminación del diagrama de actualización debido a una infracción de clave principal o clave externa. En tales casos, el `sql:inverse` atributo se especifica ( `sql:inverse="true"` ) en el **\<sql:relationship>** elemento y la lógica diagrama inversa su interpretación de la relación de elementos primarios y secundarios especificada en el esquema.  
  
 El atributo `sql:inverse` toma un valor booleano (0=false, 1=true). Los valores permitidos son 0, 1, true y false.  
  
 Para obtener un ejemplo funcional del uso de la `sql:inverse` anotación, vea [especificar un esquema de asignación anotado en un diagrama](../sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
## <a name="see-also"></a>Consulte también  
 [Especificar relaciones mediante SQL: Relationship &#40;SQLXML 4,0&#41;](specifying-relationships-using-sql-relationship-sqlxml-4-0.md)  
  
  
