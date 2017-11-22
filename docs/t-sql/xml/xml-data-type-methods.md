---
title: "Métodos de tipo de datos XML | Documentos de Microsoft"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- xml data type [SQL Server], methods
- methods [XML in SQL Server]
ms.assetid: d112b9c9-be9f-435c-a9e6-d21b65778fb7
caps.latest.revision: "32"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e607f76007473b0ca53788b2a934221ef68d1e0d
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="xml-data-type-methods"></a>Métodos de tipo de datos xml
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Puede usar el **xml** métodos para consultar una instancia XML almacenada en una variable o columna de tipo de datos **xml** tipo. Los temas de esta sección describen cómo utilizar el **xml** métodos del tipo de datos.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[consulta &#40; &#41; Método &#40; tipo de datos xml &#41;](../../t-sql/xml/query-method-xml-data-type.md)|Describe cómo utilizar el método query() para realizar una consulta en una instancia XML.|  
|[valor &#40; &#41; Método &#40; tipo de datos xml &#41;](../../t-sql/xml/value-method-xml-data-type.md)|Describe cómo utilizar el método value() para recuperar un valor de tipo SQL de una instancia XML.|  
|[Existen &#40; &#41; Método &#40; tipo de datos xml &#41;](../../t-sql/xml/exist-method-xml-data-type.md)|Describe cómo utilizar el método exist() para determinar si una consulta devuelve un resultado no vacío.|  
|[Modificar &#40; &#41; Método &#40; tipo de datos xml &#41;](../../t-sql/xml/modify-method-xml-data-type.md)|Describe cómo utilizar el método modify() para especificar [lenguaje de manipulación de datos XML &#40; XML DML &#41; ](../../t-sql/xml/xml-data-modification-language-xml-dml.md)instrucciones para realizar actualizaciones.|  
|[nodos &#40; &#41; Método &#40; tipo de datos xml &#41;](../../t-sql/xml/nodes-method-xml-data-type.md)|Describe cómo utilizar el método nodes() para dividir XML en varias filas, lo que propaga partes de documentos XML en conjuntos de filas.|  
|[Enlace de datos relacionales dentro de datos XML](../../t-sql/xml/binding-relational-data-inside-xml-data.md)|Describe cómo enlazar datos no XML dentro de XML.|  
|[Directrices para usar los métodos del tipo de datos xml](../../t-sql/xml/guidelines-for-using-xml-data-type-methods.md)|Describe instrucciones para utilizar el **xml** métodos del tipo de datos.|  
  
 Estos métodos se llaman mediante la sintaxis de llamada de métodos de tipo definido por el usuario. Por ejemplo:  
  
```  
SELECT XmlCol.query(' ... ')  
FROM   Table  
```  
  
> [!NOTE]  
>  El **xml** métodos del tipo de datos **query()**, **value()**, y **exist()** devolver NULL si se ejecuta en una instancia NULL XML. Además, **modify()** no devuelve nada, pero **nodes()** devuelve conjuntos de filas y un conjunto de filas vacío con una entrada NULL.  
  
## <a name="see-also"></a>Vea también  
 [Comparar XML con tipo y XML sin tipo](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Crear instancias de datos XML](../../relational-databases/xml/create-instances-of-xml-data.md)  
  
  
