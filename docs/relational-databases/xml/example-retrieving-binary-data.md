---
title: 'Ejemplo: Recuperar datos binarios | Microsoft Docs'
ms.custom: ''
ms.date: 04/03/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, retrieving binary data example
ms.assetid: 5cea5d49-58ac-403a-a933-c4fd91de400b
author: RothJa
ms.author: jroth
ms.openlocfilehash: 8d66e1ec9c580030f1f65f030cdb0367d8f4f430
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664503"
---
# <a name="example-retrieving-binary-data"></a>Ejemplo: Recuperar datos binarios

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

La consulta siguiente devuelve la fotografía del producto almacenada en una columna de tipo **varbinary(max)** . En la consulta, se especifica la opción `BINARY BASE64` para devolver los datos binarios en formato codificado en base 64.

## <a name="example"></a>Ejemplo

```sql
USE AdventureWorks2012;
GO
SELECT ProductPhotoID, ThumbNailPhoto
FROM Production.ProductPhoto
WHERE ProductPhotoID=1
FOR XML RAW, BINARY BASE64 ;
GO
```

Espere el siguiente resultado:

```console
<row ProductModelID="1" ThumbNailPhoto="base64 encoded binary data"/>
```

## <a name="see-also"></a>Consulte también

[Usar el modo RAW con FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)
