---
title: 'Ejemplo: Especificar XSINIL con la directiva ELEMENTS | Microsoft Docs'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: RAW mode, specifying XSINIL example
ms.assetid: 07c873ff-1f9d-480e-8536-862c39eb8249
caps.latest.revision: "11"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 277d79a76cac65d132c925e4cd91ee1a77ade46f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="example-specifying-xsinil-with-the-elements-directive"></a>Ejemplo: Especificar XSINIL con la directiva ELEMENTS
  En esta consulta se especifica la directiva `ELEMENTS` para generar XML centrado en elementos a partir del resultado de la consulta.  
  
## <a name="example"></a>Ejemplo  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name, Color  
FROM Production.Product  
FOR XML RAW, ELEMENTS;  
GO  
```  
  
 El resultado parcial es el siguiente.  
  
```  
<row>  
  <ProductID>1</ProductID>  
  <Name>Adjustable Race</Name>  
</row>  
...  
<row>  
  <ProductID>317</ProductID>  
  <Name>LL Crankarm</Name>  
  <Color>Black</Color>  
</row>  
```  
  
 Dado que la columna `Color` tiene valores NULL para algunos productos, el XML resultante no generará el elemento <`Color`> correspondiente. Al agregar la directiva `XSINIL` junto con `ELEMENTS`, se puede generar el elemento <`Color`> incluso para los valores de color NULL del conjunto de resultados.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name, Color  
FROM Production.Product  
FOR XML RAW, ELEMENTS XSINIL ;  
```  
  
 Éste es el resultado parcial:  
  
```  
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <ProductID>1</ProductID>  
  <Name>Adjustable Race</Name>  
  <Color xsi:nil="true" />  
</row>  
...  
<row>  
  <ProductID>317</ProductID>  
  <Name>LL Crankarm</Name>  
  <Color>Black</Color>  
</row>  
```  
  
## <a name="see-also"></a>Vea también  
 [Usar el modo RAW con FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  
