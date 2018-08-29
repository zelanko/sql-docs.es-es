---
title: Interpretación de anotaciones (SQLXML 4.0) | Microsoft Docs
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
- annotated XSD schemas, XML Bulk Load
- XML Bulk Load [SQLXML], annotation intepretations
- annotations [SQLXML]
- bulk load [SQLXML], annotation interpretations
- annotated XDR schemas, XML Bulk Load
ms.assetid: 1c46bdb6-2812-4a13-b60b-7101c04b299f
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 68d956bb6c35adbf7df32becf539f0965f904955
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43089550"
---
# <a name="annotation-interpretation-sqlxml-40"></a>Interpretación de anotaciones (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Los temas de esta sección describen la forma en que la carga masiva XML interpreta las anotaciones del esquema XSD. El comportamiento que aquí se describe también se aplica a las anotaciones del esquema XDR.  
  
> [!NOTE]  
>  La información de estos temas describe únicamente las anotaciones que la carga masiva XML utiliza en su procesamiento. Para obtener una lista completa de anotaciones para el esquema XSD que son compatibles con SQLXML 4.0, consulte [utilizar anotaciones en esquemas XSD &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/using-annotations-in-xsd-schemas-sqlxml-4-0.md). Para obtener una lista de anotaciones compatibles para los esquemas XDR, vea [esquemas XDR anotados &#40;desusado en SQLXML 4.0&#41;](../../../relational-databases/sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
## <a name="in-this-section"></a>En esta sección  
 [SQL: Relationship y regla de orden de clave &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-relationship-and-key-ordering-rule.md)  
 Describe cómo el **SQL: Relationship** anotación se interpreta en la carga masiva XML.  
  
 [SQL: asigna &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-mapped.md)  
 Describe cómo el **sql: asigna** anotación se interpreta en la carga masiva XML.  
  
 [SQL: limit-campo y SQL: limit-valor &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-limit-field-and-sql-limit-value.md)  
 Describe cómo el **SQL: limit-campo** y **SQL: limit-valor** se interpretan las anotaciones en la carga masiva XML.  
  
 [Overflow-campo &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-sql-overflow-field.md)  
 Describe cómo el **Overflow** anotación se interpreta en la carga masiva XML.  
  
 [Otras anotaciones &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/annotation-interpretation-other-annotations.md)  
 Describe cómo se interpretan las siguientes anotaciones en la carga masiva XML: **SQL: ID-prefijo**, **SQL: use-cdata**, **SQL: url-encode**, **sql: esquema de asignación es**, **SQL: Key-campos**.  
  
  
