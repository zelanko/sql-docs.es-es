---
title: Usar el modo RAW con FOR XML | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML RAW mode
- XMLSCHEMA option
- FOR XML clause, RAW mode
- RAW FOR XML mode
- ELEMENTS directive
- RAW mode
- XMLDATA option
ms.assetid: 02c1bc0b-760c-4589-9ab1-6927c6d9c734
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 249bee21bdddacc369a99efe8c31be511e2d305a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47837963"
---
# <a name="use-raw-mode-with-for-xml"></a>Usar el modo RAW con FOR XML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  El modo RAW transforma cada fila del conjunto de resultados de la consulta en un elemento XML que tiene el identificador genérico \<row> o el nombre del elemento, que se proporciona de manera opcional. De forma predeterminada, cada valor de columna del conjunto de filas que no es NULL se asigna a un atributo del elemento \<row>. Si se agrega la directiva ELEMENTS a la cláusula FOR XML, cada valor de columna se asigna a un subelemento del elemento \<row>. Opcionalmente, junto con la directiva ELEMENTS se puede especificar la opción XSINIL para asignar los valores de columna NULL del conjunto de resultados a un elemento que tenga el atributo, xsi:nil=`"`true`"`.  
  
 Se puede solicitar un esquema para el XML resultante. Si se especifica la opción XMLDATA se devuelve un esquema XDR en línea. Si se especifica la opción XMLSCHEMA se devuelve un esquema XSD en línea. El esquema aparece al principio de los datos. En el resultado, la referencia al espacio de nombres del esquema se repite en todos los elementos de nivel superior.  
  
 La opción BINARY BASE64 se debe especificar en la cláusula FOR XML para devolver los datos binarios en formato codificado en base 64. En el modo RAW, si se recuperan los datos binarios sin especificar la opción BINARY BASE64, se produce un error.  
  
## <a name="in-this-section"></a>En esta sección  
 Esta sección contiene los siguientes ejemplos:  
  
-   [Ejemplo: Recuperar información de modelos de productos como XML](../../relational-databases/xml/example-retrieving-product-model-information-as-xml.md)  
  
-   [Ejemplo: Especificar XSINIL con la directiva ELEMENTS](../../relational-databases/xml/example-specifying-xsinil-with-the-elements-directive.md)  
  
-   [Ejemplo: solicitar esquemas como resultados con las opciones XMLDATA y XMLSCHEMA](../../relational-databases/xml/example-requesting-schemas-as-results-with-the-xmldata-and-xmlschema-options.md)  
  
-   [Ejemplo: Recuperar datos binarios](../../relational-databases/xml/example-retrieving-binary-data.md)  
  
-   [Ejemplo: Cambiar el nombre del elemento &#60;row&#62;](../../relational-databases/xml/example-renaming-the-row-element.md)  
  
-   [Ejemplo: Especificar un elemento raíz para el XML generado por FOR XML](../../relational-databases/xml/example-specifying-a-root-element-for-the-xml-generated-by-for-xml.md)  
  
-   [Ejemplo: Consultar columnas de tipo XML](../../relational-databases/xml/example-querying-xmltype-columns.md)  
  
## <a name="see-also"></a>Ver también  
 [Agregar espacios de nombres a consultas con WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Usar el modo AUTO con FOR XML](../../relational-databases/xml/use-auto-mode-with-for-xml.md)   
 [Usar el modo EXPLICIT con FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)   
 [Usar el modo PATH con FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
