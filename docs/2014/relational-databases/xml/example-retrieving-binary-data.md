---
title: 'Ejemplo: Recuperar datos binarios | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- RAW mode, retrieving binary data example
ms.assetid: 5cea5d49-58ac-403a-a933-c4fd91de400b
caps.latest.revision: 11
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e1449a80aeb3b758658556b080d896089796f66d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107566"
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
  
## <a name="see-also"></a>Vea también  
 [Usar el modo RAW con FOR XML](use-raw-mode-with-for-xml.md)  
  
  