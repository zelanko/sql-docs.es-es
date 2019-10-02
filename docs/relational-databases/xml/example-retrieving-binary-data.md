---
title: 'Ejemplo: Recuperación de datos binarios | Microsoft Docs'
ms.custom: ''
ms.date: 09/23/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, retrieving binary data example
ms.assetid: 5cea5d49-58ac-403a-a933-c4fd91de400b
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||=azuresqldb-mi-current||>=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions
ms.openlocfilehash: c168c76d33ac90bc658fad86404aea45b322d037
ms.sourcegitcommit: 9221a693d4ab7ae0a7e2ddeb03bd0cf740628fd0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/23/2019
ms.locfileid: "71199463"
---
# <a name="example-retrieving-binary-data"></a>Ejemplo: Recuperación de datos binarios

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
