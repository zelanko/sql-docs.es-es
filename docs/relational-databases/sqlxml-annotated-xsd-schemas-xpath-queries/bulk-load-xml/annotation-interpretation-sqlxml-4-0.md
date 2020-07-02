---
title: Interpretación de anotaciones (SQLXML)
description: Obtenga información sobre cómo la carga masiva XML en SQLXML 4,0 interpreta las anotaciones en los esquemas XSD y XDR.
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, XML Bulk Load
- XML Bulk Load [SQLXML], annotation intepretations
- annotations [SQLXML]
- bulk load [SQLXML], annotation interpretations
- annotated XDR schemas, XML Bulk Load
ms.assetid: 1c46bdb6-2812-4a13-b60b-7101c04b299f
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 41cb1a0e65b7e453f408a43b71b1cad831b0cba4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85790888"
---
# <a name="annotation-interpretation-sqlxml-40"></a>Interpretación de anotaciones (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Los temas de esta sección describen la forma en que la carga masiva XML interpreta las anotaciones del esquema XSD. El comportamiento que aquí se describe también se aplica a las anotaciones del esquema XDR.  
  
> [!NOTE]  
>  La información de estos temas describe únicamente las anotaciones que la carga masiva XML utiliza en su procesamiento. Para obtener una lista completa de anotaciones para el esquema XSD que son compatibles con SQLXML 4,0, vea [utilizar anotaciones en esquemas xsd &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-annotations-in-xsd-schemas-sqlxml-4-0.md). Para obtener una lista de las anotaciones admitidas para los esquemas XDR, consulte [esquemas XDR anotados &#40;en desuso en SQLXML 4,0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
## <a name="in-this-section"></a>En esta sección  
 [SQL: Relationship y la regla de ordenación de claves &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-relationship-and-key-ordering-rule.md)  
 Describe cómo se interpreta la anotación **SQL: Relationship** en la carga masiva XML.  
  
 [SQL: asignado &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-mapped.md)  
 Describe cómo se interpreta la anotación **SQL: asignada** en la carga masiva XML.  
  
 [SQL: Limit-Field y SQL: Limit-Value &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-limit-field-and-sql-limit-value.md)  
 Describe cómo se interpretan las anotaciones **SQL: limit-field** y **SQL: Limit-Value** en la carga masiva XML.  
  
 [SQL: Overflow-Field &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)  
 Describe cómo se interpreta la anotación **SQL: Overflow** en la carga masiva XML.  
  
 [Otras anotaciones &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-other-annotations.md)  
 Describe cómo se interpretan las anotaciones siguientes en la carga masiva XML: **SQL: id-prefix**, **SQL: Use-CDATA**, **SQL: URL-encode**, **SQL: is-mapping-schema**, **SQL: Key-Fields**.  
  
  
