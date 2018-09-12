---
title: 'Ejemplo: Cambiar el nombre del elemento &lt;row&gt; | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, renaming <row> example
ms.assetid: b042292a-0b6e-40a3-b254-71c06e626706
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 082bbb9ce94b8f3b2625176e27f4c088ffef3b8b
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43888521"
---
# <a name="example-renaming-the-ltrowgt-element"></a>Example: Renaming the &lt;row&gt; Element (Ejemplo: Cambiar el nombre del elemento &lt;row&gt;)
  El modo RAW genera un elemento para cada fila del conjunto de resultados `<row>`. Opcionalmente, se puede indicar otro nombre para este elemento especificando un argumento opcional para el modo RAW, como se muestra en esta consulta. La consulta devuelve un elemento <`ProductModel`> para cada fila del conjunto de filas.  
  
## <a name="example"></a>Ejemplo  
  
```  
SELECT ProductModelID, Name   
FROM Production.ProductModel  
WHERE ProductModelID=122  
FOR XML RAW ('ProductModel'), ELEMENTS  
GO  
```  
  
 Éste es el resultado. Dado que se agrega la directiva `ELEMENTS` en la consulta, el resultado está centrado en elementos.  
  
```  
<ProductModel>  
  <ProductModelID>122</ProductModelID>  
  <Name>All-Purpose Bike Stand</Name>  
</ProductModel>   
```  
  
## <a name="see-also"></a>Vea también  
 [Usar el modo RAW con FOR XML](use-raw-mode-with-for-xml.md)  
  
  
