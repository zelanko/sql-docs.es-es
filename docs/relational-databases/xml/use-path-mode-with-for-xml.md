---
title: "Usar el modo PATH con FOR XML | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "PATH FOR XML [modo]"
  - "caracteres [SQL Server], XML"
  - "alias [SQL Server], XML"
  - "cláusula FOR XML, modo PATH"
  - "FOR XML PATH [modo]"
  - "nombres de columna [SQL Server]"
  - "consultas XPath [SQL Server]"
ms.assetid: a685a9ad-3d28-4596-aa72-119202df3976
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# Usar el modo PATH con FOR XML
  Tal como se describe en [Generar XML mediante FOR XML](../../relational-databases/xml/for-xml-sql-server.md), el modo PATH facilita la combinación de elementos y atributos. También facilita la especificación de anidación adicional para representar propiedades complejas. Puede utilizar consultas de modo FOR XML EXPLICIT para generar XML a partir de un conjunto de filas, pero el modo PATH supone una alternativa más sencilla a las consultas de modo EXPLICIT potencialmente complicadas. El modo PATH, junto con la posibilidad de escribir consultas FOR XML anidadas y la directiva TYPE para devolver instancias de tipo **xml** , permite escribir consultas de forma más fácil.  
  
 En el modo PATH, los nombres o alias de columna se tratan como expresiones XPath. Estas expresiones indican el modo en el que se asignan los valores a XML. Cada expresión XPath es una expresión relativa que proporciona el tipo de elemento, como el atributo, el elemento y el valor escalar, así como el nombre y la jerarquía del nodo que se generará en relación con el elemento de fila.  
  
 Esta sección describe las columnas de asignación en un conjunto de filas bajo varias condiciones y proporciona los ejemplos.  
  
## En esta sección  
  
-   [Columnas sin nombre](../../relational-databases/xml/columns-without-a-name.md)  
  
-   [Columnas con nombre](../../relational-databases/xml/columns-with-a-name.md)  
  
-   [Columnas con un nombre especificado como carácter comodín](../../relational-databases/xml/columns-with-a-name-specified-as-a-wildcard-character.md)  
  
-   [Columnas con el nombre de una prueba de nodo XPath](../../relational-databases/xml/columns-with-the-name-of-an-xpath-node-test.md)  
  
-   [Nombres de columna con la ruta de acceso especificada como data&#40;&#41;](../../relational-databases/xml/column-names-with-the-path-specified-as-data.md)  
  
-   [Columnas que incluyen un valor NULL de forma predeterminada](../../relational-databases/xml/columns-that-contain-a-null-value-by-default.md)  
  
-   [Compatibilidad con elementos de espacio de nombres en el modo PATH](../../relational-databases/xml/namespace-support-in-path-mode.md)  
  
-   [Ejemplos: Usar el modo PATH](../../relational-databases/xml/examples-using-path-mode.md)  
  
## Vea también  
 [Agregar espacios de nombres a consultas con WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  