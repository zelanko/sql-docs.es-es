---
title: "Cómo convierte FOR JSON tipos de datos de SQL Server en tipos de datos JSON (SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 07/07/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: json
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: FOR JSON, data type conversion
ms.assetid: da356f06-efd0-4ea3-8157-77395bf790d7
caps.latest.revision: "11"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9d934c3ddaee2d87a0a4afa5f9df900f759a1ed7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server"></a>Conversión por parte de FOR JSON de tipos de datos de SQL Server en tipos de datos JSON (SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  La cláusula **FOR JSON** usa las siguientes reglas para convertir tipos de datos SQL Server en tipos JSON en la salida JSON.  
  
|Categoría|Tipo de datos de SQL Server|Tipo de datos JSON|  
|--------------|--------------|---------------|  
|Tipos de carácter y cadena|char, nchar, varchar, nvarchar|string|  
|Tipos numéricos|int, bigint, float, decimal, numeric|number|  
|Tipo de bit|bit|Booleano (true o false)|  
|Tipos de fecha y hora|date, datetime, datetime2, time, datetimeoffset|string|  
|Tipos binarios|varbinary, binary, image, timestamp, rowversion|Cadena codificada en BASE64|  
|Tipos CLR|geometry, geography, otros tipos CLR|No compatible. Estos tipos devuelven un error.<br /><br /> En la instrucción SELECT, use CAST o CONVERT, o bien use un método o propiedad CLR, para convertir los datos de origen en un tipo de datos SQL Server que pueda convertirse correctamente a un tipo JSON. Por ejemplo, use **STAsText()** para el tipo geometry o **ToString()** para cualquier tipo CLR. El tipo del valor de salida JSON se deriva del tipo de valor devuelto de la conversión aplicada en la instrucción SELECT.|  
|Otros tipos|uniqueidentifier, money|string|  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Más información sobre la compatibilidad integrada de JSON en SQL Server  
Para obtener una gran cantidad de soluciones específicas, casos de uso y recomendaciones, consulte las [entradas de blog sobre la compatibilidad integrada de JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) en SQL Server y en Azure SQL Database ofrecidas por el director de programas de Microsoft Jovan Popovic.
  
## <a name="see-also"></a>Vea también  
 [Format Query Results as JSON with FOR JSON &#40;SQL Server&#41; (Dar formato JSON a los resultados de consulta con FOR JSON &#40;SQL Server&#41;)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md)  
  
  
