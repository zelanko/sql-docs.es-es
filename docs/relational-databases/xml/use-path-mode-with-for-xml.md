---
title: Usar el modo PATH con FOR XML | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- PATH FOR XML mode
- characters [SQL Server], XML
- aliases [SQL Server], XML
- FOR XML clause, PATH mode
- FOR XML PATH mode
- column names [SQL Server]
- XPath queries [SQL Server]
ms.assetid: a685a9ad-3d28-4596-aa72-119202df3976
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 468811f8a7d41497157a86e09030a20d6ad35796
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="use-path-mode-with-for-xml"></a>Usar el modo PATH con FOR XML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Tal como se describe en [Generar XML mediante FOR XML](../../relational-databases/xml/for-xml-sql-server.md), el modo PATH facilita la combinación de elementos y atributos. También facilita la especificación de anidación adicional para representar propiedades complejas. Puede utilizar consultas de modo FOR XML EXPLICIT para generar XML a partir de un conjunto de filas, pero el modo PATH supone una alternativa más sencilla a las consultas de modo EXPLICIT potencialmente complicadas. El modo PATH, junto con la posibilidad de escribir consultas FOR XML anidadas y la directiva TYPE para devolver instancias de tipo **xml** , permite escribir consultas de forma más fácil.  
  
 En el modo PATH, los nombres o alias de columna se tratan como expresiones XPath. Estas expresiones indican el modo en el que se asignan los valores a XML. Cada expresión XPath es una expresión relativa que proporciona el tipo de elemento, como el atributo, el elemento y el valor escalar, así como el nombre y la jerarquía del nodo que se generará en relación con el elemento de fila.  
  
 Esta sección describe las columnas de asignación en un conjunto de filas bajo varias condiciones y proporciona los ejemplos.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Columnas sin nombre](../../relational-databases/xml/columns-without-a-name.md)  
  
-   [Columnas con nombre](../../relational-databases/xml/columns-with-a-name.md)  
  
-   [Columnas con un nombre especificado como carácter comodín](../../relational-databases/xml/columns-with-a-name-specified-as-a-wildcard-character.md)  
  
-   [Columnas con el nombre de una prueba de nodo XPath](../../relational-databases/xml/columns-with-the-name-of-an-xpath-node-test.md)  
  
-   [Nombres de columna con la ruta de acceso especificada como data&#40;&#41;](../../relational-databases/xml/column-names-with-the-path-specified-as-data.md)  
  
-   [Columnas que incluyen un valor NULL de forma predeterminada](../../relational-databases/xml/columns-that-contain-a-null-value-by-default.md)  
  
-   [Compatibilidad con elementos de espacio de nombres en el modo PATH](../../relational-databases/xml/namespace-support-in-path-mode.md)  
  
-   [Ejemplos: Usar el modo PATH](../../relational-databases/xml/examples-using-path-mode.md)  
  
## <a name="see-also"></a>Ver también  
 [Agregar espacios de nombres a consultas con WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
