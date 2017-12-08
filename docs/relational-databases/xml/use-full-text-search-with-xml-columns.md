---
title: "Usar la búsqueda de texto completo con columnas XML | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: xml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- xml columns [full-text search]
- indexes [full-text search]
ms.assetid: 8096cfc6-1836-4ed5-a769-a5d63b137171
caps.latest.revision: "14"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 60ab43fc16b75b4031b1f73ba6850dd835d7f2a9
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="use-full-text-search-with-xml-columns"></a>Usar la búsqueda de texto completo con columnas XML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)] Puede crear un índice de texto completo en columnas XML para indizar el contenido de los valores XML, pero omitiendo el marcado XML. Las etiquetas de elemento se usan como límites de token. Los siguientes elementos se indizan:  
  
-   Contenido de los elementos XML.  
  
-   Contenido de los atributos XML del elemento de nivel superior únicamente, a menos que esos valores sean numéricos.  
  
 Si es posible, puede combinar una búsqueda de texto completo con un índice XML como se indica a continuación:  
  
1.  En primer lugar, filtre los valores XML que resulten de interés mediante una búsqueda de texto completo SQL.  
  
2.  A continuación, realice una consulta en los valores XML que usen índice XML en la columna XML.  
  
## <a name="example-combining-full-text-search-with-xml-querying"></a>Ejemplo: combinar una búsqueda de texto completo con consultas XML  
 Una vez creado un índice de texto completo en la columna XML, la siguiente consulta comprueba que un valor XML contiene la palabra "custom" en el título de un libro:  
  
```  
SELECT *   
FROM   T   
WHERE  CONTAINS(xCol,'custom')   
AND    xCol.exist('/book/title/text()[contains(.,"custom")]') =1  
```  
  
 El método **contains()** usa el índice de texto completo para crear un subconjunto con los valores XML que contienen la palabra "custom" en algún lugar del documento. La cláusula **exist()** se asegura de que la palabra "custom" aparezca en el título de un libro.  
  
 Una búsqueda de texto completo que usa **contains()** y la función **contains()** de XQuery tiene semánticas distintas. La última busca una coincidencia de subcadena y la primera busca una coincidencia de token que utilice lematización. Es decir, si se busca la cadena que contiene "run" en el título, las coincidencias incluirán "run", "runs" y "running", puesto que se cumplen los criterios tanto de **contains()** de texto completo como los de la función **contains()** de XQuery. Pero la consulta no coincide con la palabra "customizable" del título, ya que la función **contains()** para la búsqueda de texto completo genera un error, pero la función **contains()** de Xquery sí se cumple. Por lo general, para una coincidencia de subcadena pura, debe quitarse la cláusula **contains()** de la búsqueda de texto completo.  
  
 Además, la búsqueda de texto completo usa lematización de palabras, pero la función **contains()** de XQuery busca una coincidencia literal. Esta diferencia se describe en el siguiente ejemplo.  
  
## <a name="example-full-text-search-on-xml-values-using-stemming"></a>Ejemplo: búsqueda de texto completo en valores XML mediante lematización  
 Por lo general, la comprobación de la función **contains()** de XQuery que se ha efectuado en el ejemplo anterior no se puede eliminar. Considere esta consulta:  
  
```  
SELECT *   
FROM   T   
WHERE  CONTAINS(xCol,'run')   
```  
  
 La palabra "ran" en el documento cumple la condición de búsqueda debido a la lematización. Además, el contexto de búsqueda no se comprueba mediante XQuery.  
  
 Cuando el XML se descompone en columnas relacionales utilizando AXSD y las columnas se incluyen en el índice de texto completo, las consultas XPath que se ejecutan en la vista XML no efectúan búsquedas de texto completo en las tablas subyacentes.  
  
## <a name="see-also"></a>Vea también  
 [Índices XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)  
  
  
