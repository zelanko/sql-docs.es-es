---
title: Escritorio y los descriptores de controladores de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- desktop database drivers [ODBC], descriptors
- Jet-based ODBC drivers [ODBC], descriptors
- descriptors [ODBC], Jet-supported descriptor fields
- ODBC desktop database drivers [ODBC], descriptors
ms.assetid: 9ae2d9b5-365f-4f0a-9116-defe9498b401
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c0096dad8fbb4cf9847385759702e39ac074c4c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68112047"
---
# <a name="descriptors-and-desktop-database-drivers"></a>Descriptores de y controladores de escritorio de la base de datos
Un descriptor es una estructura de datos que contiene información sobre los datos de las columnas o parámetros dinámicos. **SQLGetDescField** puede usarse para recuperar los descriptores compatibles enumerados a continuación. Los descriptores de parámetros de implementación (IPD) no se rellenan automáticamente porque **SQLDescribeParam** no se admite. Tampoco se admiten campos de descriptor que no están disponibles a través de Jet (por ejemplo, SQL_DESC_BASE_TABLE_NAME).  
  
 Para obtener más información acerca de los campos de descriptor de Jet compatible, consulte el *Guía del programador del motor de base de datos Jet de Microsoft*.  
  
 Para obtener más información acerca de los descriptores, vea los temas en los descriptores de"" en el *referencia del programador de ODBC*.  
  
|Campos de descriptor|Nivel de compatibilidad|  
|-----------------------|-------------------|  
|SQL_DESC_ALLOC_TYPE|Compatible|  
|SQL_DESC_ARRAY_SIZE|Solo se admite para descartar|  
|SQL_DESC_ARRAY_STATUS_PTR|Compatible|  
|SQL_DESC_BIND_OFFSET_PTR|Compatible|  
|SQL_DESC_BIND_TYPE|Compatible|  
|SQL_DESC_COUNT|Compatible|  
|SQL_DESC_ROWS_PROCESSED_PTR|Solo se admite para descartar|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Compatible|  
|SQL_DESC_BASE_COLUMN_NAME|Compatible (nuevo)|  
|SQL_DESC_BASE_TABLE_NAME|Compatible (nuevo)|  
|SQL_DESC_CASE_SENSITIVE|Siempre es FALSE|  
|SQL_DESC_CATALOG_NAME|No compatible|  
|SQL_DESC_CONCISE_TYPE|Compatible|  
|SQL_DESC_DATA_PTR|Compatible|  
|SQL_DESC_DATETIME_INTERVAL_CODE|Compatible|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|Admite para los tipos de C de intervalo|  
|SQL_DESC_DISPLAY_SIZE|Compatible|  
|SQL_DESC_FIXED_PREC_SCALE|Compatible (TRUE por dinero)|  
|SQL_DESC_INDICATOR_PTR|Compatible|  
|SQL_DESC_LABEL|Compatible|  
|SQL_DESC_LENGTH|Compatible|  
|SQL_DESC_LITERAL_PREFIX|Compatible|  
|SQL_DESC_LITERAL_SUFFIX|Compatible|  
|SQL_DESC_LOCAL_TYPE_NAME|No se admite (devuelve una cadena vacía)|  
|SQL_DESC_NAME|Compatible|  
|SQL_DESC_NULLABLE|Compatible<br /><br /> **Tenga en cuenta** no admitidas en versiones anteriores de Jet 4.0|  
|SQL_DESC_NUM_PREC_RADIX|Compatible|  
|SQL_DESC_OCTET_LENGTH|Compatible|  
|SQL_DESC_OCTET_LENGTH_PTR|Compatible|  
|SQL_DESC_PARAMETER_TYPE|Solo los parámetros de entrada|  
|SQL_DESC_PRECISION|Compatible|  
|SQL_DESC_SCALE|Compatible|  
|SQL_DESC_SCHEMA_NAME|No compatible|  
|SQL_DESC_SEARCHABLE|Compatible|  
|SQL_DESC_TABLE_NAME|No compatible|  
|SQL_DESC_TYPE|Compatible|  
|SQL_DESC_TYPE_NAME|Compatible|  
|SQL_DESC_UNNAMED|Compatible|  
|SQL_DESC_UNSIGNED|Compatible|  
|SQL_DESC_UPDATABLE|Compatible|
