---
title: 'Ejemplo: Cambiar el nombre del elemento &lt;row&gt; | Microsoft Docs'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RAW mode, renaming <row> example
ms.assetid: b042292a-0b6e-40a3-b254-71c06e626706
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0c907cb5e9ac3f4cd7535bea384068b08298e8b9
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

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
 [Usar el modo RAW con FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  
