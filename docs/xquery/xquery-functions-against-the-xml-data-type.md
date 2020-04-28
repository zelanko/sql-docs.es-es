---
title: Funciones de XQuery con el tipo de datos XML | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, functions
- xml data type [SQL Server], XQuery
- functions [SQL Server], XQuery
ms.assetid: 8df0877d-a03f-4ca9-b84e-908c4bb42b5e
author: rothja
ms.author: jroth
ms.openlocfilehash: e885b537fbc86f3b70a8142c5513dbf16cb1c158
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67945995"
---
# <a name="xquery-functions-against-the-xml-data-type"></a>Funciones de XQuery con el tipo de datos xml
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  En este tema y sus temas secundarios se describen las funciones que se pueden utilizar al especificar XQuery con el tipo de datos **XML** . Para conocer las especificaciones del W3C [http://www.w3.org/TR/2004/WD-xpath-functions-20040723](https://go.microsoft.com/fwlink/?LinkId=4873), vea.  
  
 Las funciones XQuery pertenecen al espacio http://www.w3.org/2004/07/xpath-functions de nombres. Las especificaciones de W3C utilizan el prefijo de espacio de nombres "fn": para describir estas funciones. No es necesario especificar explícitamente el prefijo de espacio de nombres "fn": cuando se utilicen estas funciones. Debido a esto y para facilitar la lectura, los prefijos de espacio de nombres no se suelen usar en esta documentación.  
  
 En la tabla siguiente se enumeran las funciones de XQuery que se admiten con el tipo de datos **XML**.  
  
|Category|Nombre de la función|  
|--------------|-------------------|  
|[Funciones en valores numéricos](https://msdn.microsoft.com/library/d5740a32-b174-43b9-b64d-1cc6edc50cff)|[umbral](../xquery/numeric-values-functions-ceiling.md)|  
||[palabra](../xquery/numeric-values-functions-floor.md)|  
||[retorno](../xquery/numeric-values-functions-round.md)|  
|[Funciones XQuery en valores de cadena](https://msdn.microsoft.com/library/2dccefef-5d90-4f56-bda7-4c1954d8a730)|[concat](../xquery/functions-on-string-values-concat.md)|  
||[contains](../xquery/functions-on-string-values-contains.md)|  
||[substring](../xquery/functions-on-string-values-substring.md)|  
||[Función en minúsculas &#40;XQuery&#41;](../xquery/functions-on-string-values-lower-case.md)|  
||[longitud de cadena](../xquery/functions-on-string-values-string-length.md)|  
||[Función en mayúsculas &#40;XQuery&#41;](../xquery/functions-on-string-values-upper-case.md)|  
|Funciones en valores booleanos|[not](../xquery/functions-on-boolean-values-not-function.md)|  
|[Funciones en nodos](https://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)|[número](../xquery/functions-on-nodes-number.md)|  
||[local-name (función de XQuery)](../xquery/functions-on-nodes-local-name.md)|  
||[namespace-uri (función de XQuery)](../xquery/functions-on-nodes-namespace-uri.md)|  
|[Funciones de contexto](https://msdn.microsoft.com/library/f7d8af33-9de9-450c-a667-23dee3129b5f)|[last](../xquery/context-functions-last-xquery.md)|  
||[localización](../xquery/context-functions-position-xquery.md)|  
|[Funciones utilizadas en secuencias](https://msdn.microsoft.com/library/672d2795-53ab-49c2-bf24-bc81a47ecd3f)|[empty](../xquery/functions-on-sequences-empty.md)|  
||[distinct-values](../xquery/functions-on-sequences-distinct-values.md)|  
||[id. (función de XQuery)](../xquery/functions-on-sequences-id.md)|  
|[Funciones de agregado &#40;XQuery&#41;](https://msdn.microsoft.com/library/be647ef1-291e-4a5d-ab18-07c759efe176)|[count](../xquery/aggregate-functions-count.md)|  
||[latencia](../xquery/aggregate-functions-avg.md)|  
||[min](../xquery/aggregate-functions-min.md)|  
||[max](../xquery/aggregate-functions-max.md)|  
||[Sume](../xquery/aggregate-functions-sum.md)|  
|[Funciones de constructor &#40;XQuery&#41;](../xquery/constructor-functions-xquery.md)|[Funciones de constructor](../xquery/constructor-functions-xquery.md)|  
|[Funciones del descriptor de acceso a datos](../xquery/data-accessor-functions.md)|[string](../xquery/data-accessor-functions-string-xquery.md)|  
||[datos](../xquery/data-accessor-functions-data-xquery.md)|  
|[Funciones de constructor booleano &#40;XQuery&#41;](https://msdn.microsoft.com/library/fa907f39-d4b7-4495-b829-c788928e0f64)|[true (función de XQuery)](../xquery/boolean-constructor-functions-true-xquery.md)|  
||[false (función de XQuery)](../xquery/boolean-constructor-functions-false-xquery.md)|  
|[Funciones relacionadas con QNames &#40;XQuery&#41;](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)|[expanded-QName (XQuery)](../xquery/functions-related-to-qnames-expanded-qname.md)|  
||[local-name-from-QName (XQuery)](../xquery/functions-related-to-qnames-local-name-from-qname.md)|  
||[namespace-uri-from-QName (XQuery)](../xquery/functions-related-to-qnames-namespace-uri-from-qname.md)|  
|[Funciones de extensión de XQuery en SQL Server](https://msdn.microsoft.com/library/4bc5d499-5fec-4c3f-b11e-5ab5ef9d8f97)|[SQL: column () (función de XQuery)](../xquery/xquery-extension-functions-sql-column.md)|  
||[sql:variable() (función de XQuery)](../xquery/xquery-extension-functions-sql-variable.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Métodos de tipo de datos XML](../t-sql/xml/xml-data-type-methods.md)   
 [&#40;de referencia del lenguaje XQuery SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [Datos XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)  
  
  
