---
title: 'Ejemplo: Cambiar el nombre del elemento &lt;row&gt; | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, renaming <row> example
ms.assetid: b042292a-0b6e-40a3-b254-71c06e626706
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4ae1003318f8514973cdbb8e3c5bce098cda581d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="example-renaming-the-ltrowgt-element"></a>Example: Renaming the &lt;row&gt; Element (Ejemplo: Cambiar el nombre del elemento &lt;row&gt;)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
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
  
## <a name="see-also"></a>Ver también  
 [Usar el modo RAW con FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  
