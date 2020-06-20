---
title: 'Ejemplo: Recuperar datos binarios | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, retrieving binary data example
ms.assetid: 5cea5d49-58ac-403a-a933-c4fd91de400b
author: rothja
ms.author: jroth
ms.openlocfilehash: ac566b47ff5ec9e1d69d0bdb24e29587aea017ff
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85013399"
---
# <a name="example-retrieving-binary-data"></a>Ejemplo: Recuperar datos binarios
  La consulta siguiente devuelve la fotografía del producto almacenada en una columna de tipo `varbinary(max)`. En la consulta, se especifica la opción `BINARY BASE64` para devolver los datos binarios en formato codificado en base 64.  
  
## <a name="example"></a>Ejemplo  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductPhotoID, ThumbNailPhoto  
FROM Production.ProductPhoto  
WHERE ProductPhotoID=1  
FOR XML RAW, BINARY BASE64 ;  
GO  
```  
  
 El resultado es el siguiente:  
  
```  
<row ProductModelID="1" ThumbNailPhoto="base64 encoded binary data"/>  
```  
  
## <a name="see-also"></a>Consulte también  
 [Usar el modo RAW con FOR XML](use-raw-mode-with-for-xml.md)  
  
  
