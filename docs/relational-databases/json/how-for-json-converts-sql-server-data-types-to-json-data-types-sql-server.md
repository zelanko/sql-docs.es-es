---
title: "Cómo convierte FOR JSON tipos de datos de SQL Server en tipos de datos JSON (SQL Server) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/07/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR JSON, data type conversion
ms.assetid: da356f06-efd0-4ea3-8157-77395bf790d7
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 527cb99c5caf0bb805e17f3b77b7d5e017e28ace
ms.contentlocale: es-es
ms.lasthandoff: 06/23/2017

---
# <a name="how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server"></a>Conversión por parte de FOR JSON de tipos de datos de SQL Server en tipos de datos JSON (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  La cláusula **FOR JSON** usa las siguientes reglas para convertir tipos de datos SQL Server en tipos JSON en la salida JSON.  
  
|Categoría|Tipo de datos de SQL Server|Tipo de datos JSON|  
|--------------|--------------|---------------|  
|Tipos de carácter y cadena|Char, nchar, varchar, nvarchar|string|  
|Tipos numéricos|int, bigint, float, decimal, numeric|number|  
|Tipo de bit|bit|Booleano (true o false)|  
|Tipos de fecha y hora|date, datetime, datetime2, time, datetimeoffset|string|  
|Tipos binarios|varbinary, binary, image, timestamp, rowversion|Cadena codificada en BASE64|  
|Tipos CLR|Geometry, geography, otros tipos CLR|No compatible. Estos tipos devuelven un error.<br /><br /> En la instrucción SELECT, use CAST o convertir, o usar una propiedad CLR o un método, para convertir los datos de origen a un tipo de datos de SQL Server que se puede convertir correctamente a un tipo JSON. Por ejemplo, utilice **STAsText()** para el tipo de geometría o use **ToString()** para cualquier tipo CLR. El tipo del valor de salida JSON, a continuación, se deriva el tipo de valor devuelto de la conversión que se aplican en la instrucción SELECT.|  
|Otros tipos|uniqueidentifier, money|string|  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Obtener más información sobre la compatibilidad integrada de JSON en SQL Server  
Para una gran cantidad de soluciones específicas, casos de uso y recomendaciones, consulte el [entradas de blog sobre la compatibilidad integrada de JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) en SQL Server y en la base de datos de SQL de Azure mediante el Administrador de programas de Microsoft Jovan Popovic.
  
## <a name="see-also"></a>Vea también  
 [Format Query Results as JSON with FOR JSON &#40;SQL Server&#41; (Dar formato JSON a los resultados de consulta con FOR JSON &#40;SQL Server&#41;)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  

