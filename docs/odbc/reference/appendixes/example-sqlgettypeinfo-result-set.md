---
title: Ejemplo de conjunto de resultados SQLGetTypeInfo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC], examples
- SQLGetTypeInfo function [ODBC], examples
- data types [ODBC], SQL data types
ms.assetid: dc1952cc-7581-4d69-9c72-7dc1cd370836
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5cf62f8a95f4c91095c21a6d603317fe1f73500
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307016"
---
# <a name="example-sqlgettypeinfo-result-set"></a>Conjunto de resultados de SQLGetTypeInfo de ejemplo
Una aplicación llama a **SQLGetTypeInfo** para determinar qué tipos de datos se admiten en un origen de datos y las características de esos tipos de datos. En las tablas siguientes se muestra un conjunto de resultados de ejemplo devuelto por **SQLGetTypeInfo** para un origen de datos que admite SQL_CHAR, SQL_LONGVARCHAR, SQL_DECIMAL, SQL_REAL, SQL_DATETIME, SQL_INTERVAL_YEAR y SQL_INTERVAL_DAY_TO_SECOND.  
  
|TYPE_NAME|DATA_TYPE|COLUMN_SIZE|LITERAL_PREFIX|LITERAL_SUFFIX|CREATE_PARAMS|NULLABLE|  
|----------------|----------------|------------------|---------------------|---------------------|--------------------|--------------|  
|Juegos|SQL_CHAR|255|"'"|"'"|longitud|SQL_TRUE|  
|"text"|SQL_LONGVARCHAR|2147483647|"'"|"'"|\<> null|SQL_TRUE|  
|decimal|SQL_DECIMAL|28|\<> null|\<> null|precisión<br />escala|SQL_TRUE|  
|impuestos|SQL_REAL|7|\<> null|\<> null|\<> null|SQL_TRUE|  
|DateTime|SQL_TYPE_TIMESTAMP|23|"'"|"'"|\<> null|SQL_TRUE|  
|"INTERVALO AÑO () A AÑO"|SQL_INTERVAL_YEAR|9|"'"|"'"|precisión|SQL_TRUE|  
|"INTERVAL DAY () TO FRACCIÓN (5)"|SQL_INTERVAL_DAY_TO_SECOND|24|"'"|"'"|precisión|SQL_TRUE|  
  
|DATA_TYPE|CASE_SENSITIVE|SEARCHABLE|UNSIGNED_ATTRIBUTE|FIXED_PREC_SCALE|AUTO_UNIQUE_VALUE|LOCAL_TYPE_NAME|  
|----------------|---------------------|----------------|-------------------------|------------------------|-------------------------|-----------------------|  
|**SQL_CHAR**|SQL_FALSE|SQL_SEARCHABLE|\<> null|SQL_FALSE|\<> null|Juegos|  
|**SQL_LONGVARCHAR**|SQL_FALSE|SQL_PRED_CHAR|\<> null|SQL_FALSE|\<> null|"text"|  
|**SQL_DECIMAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|decimal|  
|**SQL_REAL**|SQL_FALSE|SQL_PRED_BASIC|SQL_FALSE|SQL_FALSE|SQL_FALSE|impuestos|  
|**SQL_TYPE_TIMESTAMP**|SQL_FALSE|SQL_SEARCHABLE|\<> null|SQL_FALSE|\<> null|DateTime|  
|**SQL_INTERVAL_YEAR**|SQL_FALSE|SQL_SEARCHABLE|\<> null|SQL_FALSE|\<> null|"INTERVALO AÑO () A AÑO"|  
|**SQL_INTERVAL_DAY_TO_SECOND**|SQL_FALSE|SQL_PRED_BASIC|\<> null|SQL_FALSE|\<> null|"INTERVAL DAY () TO FRACCIÓN (5)"|  
  
|DATA_TYPE|MINIMUM_SCALE|MAXIMUM_SCALE|SQL_DATA_TYPE|SQL_DATETIME_SUB|NUM_PREC_RADIX|INTERVAL_PRECISION|  
|----------------|--------------------|--------------------|---------------------|------------------------|----------------------|-------------------------|  
|**SQL_CHAR**|\<> null|\<> null|SQL_CHAR|\<> null|\<> null|\<> null|  
|**SQL_LONGVARCHAR**|\<> null|\<> null|SQL_LONGVARCHAR|\<> null|\<> null|\<> null|  
|**SQL_DECIMAL**|0|28|SQL_DECIMAL|\<> null|10|\<> null|  
|**SQL_REAL**|\<> null|\<> null|SQL_REAL|\<> null|10|\<> null|  
|**SQL_TYPE_TIMESTAMP**|3|3|SQL_DATETIME|SQL_CODE_TIMESTAMP|\<> null|12|  
|**SQL_INTERVAL_YEAR**|0|0|SQL_INTERVAL|SQL_CODE_INTERVALYEAR|\<> null|9|  
|**SQL_INTERVAL_DAY_TO_SECOND**|5|5|SQL_INTERVAL|SQL_CODE_INTERVALDAY_TO_SECOND|\<> null|9|
