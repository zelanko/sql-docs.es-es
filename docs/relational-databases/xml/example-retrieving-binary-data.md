---
title: 'Ejemplo: Recuperación de datos binarios | Microsoft Docs'
description: Vea un ejemplo de una consulta SQL que recupera datos binarios mediante las opciones RAW y BINARY BASE64 con la cláusula FOR XML.
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
ms.openlocfilehash: fedec9e351b9c8910db0bee51c1e2c5dc8569655
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97402988"
---
# <a name="example-retrieving-binary-data"></a>Ejemplo: Recuperación de datos binarios

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

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
