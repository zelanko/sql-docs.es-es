---
title: Funciones de XQuery con el tipo de datos xml | Documentos de Microsoft
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- XQuery, functions
- xml data type [SQL Server], XQuery
- functions [SQL Server], XQuery
ms.assetid: 8df0877d-a03f-4ca9-b84e-908c4bb42b5e
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f950e3bbeb239537bc606c38469b9fb79e36837b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="xquery-functions-against-the-xml-data-type"></a>Funciones de XQuery con el tipo de datos xml
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Este tema y sus temas secundarios describen las funciones que puede usar al especificar XQuery en el **xml** tipo de datos. Para las especificaciones de W3C, vea [http://www.w3.org/TR/2004/WD-xpath-functions-20040723](http://go.microsoft.com/fwlink/?LinkId=4873).  
  
 Las funciones de XQuery pertenecen al espacio de nombres http://www.w3.org/2004/07/xpath-functions. Las especificaciones de W3C utilizan el prefijo de espacio de nombres "fn": para describir estas funciones. No es necesario especificar explícitamente el prefijo de espacio de nombres "fn": cuando se utilicen estas funciones. Debido a esto y para facilitar la lectura, los prefijos de espacio de nombres no se suelen usar en esta documentación.  
  
 En la tabla siguiente se enumera las funciones de XQuery que son compatibles con el **xml**tipo de datos.  
  
|Categoría|Nombre de la función|  
|--------------|-------------------|  
|[Funciones en valores numéricos](http://msdn.microsoft.com/library/d5740a32-b174-43b9-b64d-1cc6edc50cff)|[límite superior](../xquery/numeric-values-functions-ceiling.md)|  
||[Floor](../xquery/numeric-values-functions-floor.md)|  
||[redondear](../xquery/numeric-values-functions-round.md)|  
|[Funciones de XQuery en valores de cadena](http://msdn.microsoft.com/library/2dccefef-5d90-4f56-bda7-4c1954d8a730)|[concat](../xquery/functions-on-string-values-concat.md)|  
||[contiene](../xquery/functions-on-string-values-contains.md)|  
||[subcadena](../xquery/functions-on-string-values-substring.md)|  
||[minúsculas Function &#40; XQuery &#41;](../xquery/functions-on-string-values-lower-case.md)|  
||[longitud de la cadena](../xquery/functions-on-string-values-string-length.md)|  
||[mayúsculas Function &#40; XQuery &#41;](../xquery/functions-on-string-values-upper-case.md)|  
|Funciones en valores booleanos|[no](../xquery/functions-on-boolean-values-not-function.md)|  
|[Funciones en nodos](http://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)|[número](../xquery/functions-on-nodes-number.md)|  
||[Función local-name (XQuery)](../xquery/functions-on-nodes-local-name.md)|  
||[Función namespace-uri (XQuery)](../xquery/functions-on-nodes-namespace-uri.md)|  
|[Funciones de contexto](http://msdn.microsoft.com/library/f7d8af33-9de9-450c-a667-23dee3129b5f)|[último](../xquery/context-functions-last-xquery.md)|  
||[posición](../xquery/context-functions-position-xquery.md)|  
|[Funciones utilizadas en secuencias](http://msdn.microsoft.com/library/672d2795-53ab-49c2-bf24-bc81a47ecd3f)|[vacía](../xquery/functions-on-sequences-empty.md)|  
||[valores distintos](../xquery/functions-on-sequences-distinct-values.md)|  
||[Id. de función (XQuery)](../xquery/functions-on-sequences-id.md)|  
|[Las funciones de agregado &#40; XQuery &#41;](http://msdn.microsoft.com/library/be647ef1-291e-4a5d-ab18-07c759efe176)|[Recuento](../xquery/aggregate-functions-count.md)|  
||[AVG](../xquery/aggregate-functions-avg.md)|  
||[min](../xquery/aggregate-functions-min.md)|  
||[max](../xquery/aggregate-functions-max.md)|  
||[suma](../xquery/aggregate-functions-sum.md)|  
|[Funciones constructoras &#40; XQuery &#41;](../xquery/constructor-functions-xquery.md)|[Funciones constructoras](../xquery/constructor-functions-xquery.md)|  
|[Funciones del descriptor de acceso a datos](../xquery/data-accessor-functions.md)|[string](../xquery/data-accessor-functions-string-xquery.md)|  
||[datos](../xquery/data-accessor-functions-data-xquery.md)|  
|[Funciones de Constructor booleano &#40; XQuery &#41;](http://msdn.microsoft.com/library/fa907f39-d4b7-4495-b829-c788928e0f64)|[Función True (XQuery)](../xquery/boolean-constructor-functions-true-xquery.md)|  
||[Función false (XQuery)](../xquery/boolean-constructor-functions-false-xquery.md)|  
|[Funciones relacionadas con QNames &#40; XQuery &#41;](http://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)|[Expanded-QName (XQuery)](../xquery/functions-related-to-qnames-expanded-qname.md)|  
||[local-nombre-de-QName (XQuery)](../xquery/functions-related-to-qnames-local-name-from-qname.md)|  
||[espacio de nombres uri de QName (XQuery)](../xquery/functions-related-to-qnames-namespace-uri-from-qname.md)|  
|[Funciones de extensión de XQuery SQL Server](http://msdn.microsoft.com/library/4bc5d499-5fec-4c3f-b11e-5ab5ef9d8f97)|[función SQL:Column() (XQuery)](../xquery/xquery-extension-functions-sql-column.md)|  
||[función SQL:variable() (XQuery)](../xquery/xquery-extension-functions-sql-variable.md)|  
  
## <a name="see-also"></a>Vea también  
 [métodos del tipo de datos xml](../t-sql/xml/xml-data-type-methods.md)   
 [Referencia del lenguaje XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [Datos XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)  
  
  
