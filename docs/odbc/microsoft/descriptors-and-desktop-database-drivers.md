---
title: Base de datos de descriptores y escritorio controladores | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- desktop database drivers [ODBC], descriptors
- Jet-based ODBC drivers [ODBC], descriptors
- descriptors [ODBC], Jet-supported descriptor fields
- ODBC desktop database drivers [ODBC], descriptors
ms.assetid: 9ae2d9b5-365f-4f0a-9116-defe9498b401
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 136c037cbf6d6d40335350e1c6cb9136d9bf8f0c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="descriptors-and-desktop-database-drivers"></a>Descriptores de y controladores de escritorio de la base de datos
Un descriptor es una estructura de datos que contiene información sobre los datos de las columnas o los parámetros dinámicos. **SQLGetDescField** puede usarse para recuperar los descriptores compatibles enumerados a continuación. Descriptores de parámetros de implementación (IPD) no se rellenan automáticamente porque **SQLDescribeParam** no se admite. Tampoco se admiten campos de descriptor que no están disponibles a través de Jet (por ejemplo, SQL_DESC_BASE_TABLE_NAME).  
  
 Para obtener más información acerca de los campos de descriptor de Jet compatible, consulte la *Guía del programador del motor de base de datos Jet de Microsoft*.  
  
 Para obtener más información acerca de los descriptores, vea los temas de "Descriptores" en la *referencia del programador de ODBC*.  
  
|Campos de descriptor|Nivel de soporte técnico|  
|-----------------------|-------------------|  
|SQL_DESC_ALLOC_TYPE|Admitida|  
|SQL_DESC_ARRAY_SIZE|Solo se admite para descartar|  
|SQL_DESC_ARRAY_STATUS_PTR|Admitida|  
|SQL_DESC_BIND_OFFSET_PTR|Admitida|  
|SQL_DESC_BIND_TYPE|Admitida|  
|SQL_DESC_COUNT|Admitida|  
|SQL_DESC_ROWS_PROCESSED_PTR|Solo se admite para descartar|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Admitida|  
|SQL_DESC_BASE_COLUMN_NAME|Compatible (nuevo)|  
|SQL_DESC_BASE_TABLE_NAME|Compatible (nuevo)|  
|SQL_DESC_CASE_SENSITIVE|Siempre es FALSE|  
|SQL_DESC_CATALOG_NAME|No compatible|  
|SQL_DESC_CONCISE_TYPE|Admitida|  
|SQL_DESC_DATA_PTR|Admitida|  
|SQL_DESC_DATETIME_INTERVAL_CODE|Admitida|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|Admite para los tipos de C de intervalo|  
|SQL_DESC_DISPLAY_SIZE|Admitida|  
|SQL_DESC_FIXED_PREC_SCALE|Compatible (TRUE por dinero)|  
|SQL_DESC_INDICATOR_PTR|Admitida|  
|SQL_DESC_LABEL|Admitida|  
|SQL_DESC_LENGTH|Admitida|  
|SQL_DESC_LITERAL_PREFIX|Admitida|  
|SQL_DESC_LITERAL_SUFFIX|Admitida|  
|SQL_DESC_LOCAL_TYPE_NAME|No se admite (devuelve una cadena vacía)|  
|SQL_DESC_NAME|Admitida|  
|SQL_DESC_NULLABLE|Admitida<br /><br /> **Tenga en cuenta** no se admiten en versiones anteriores de Jet 4.0|  
|SQL_DESC_NUM_PREC_RADIX|Admitida|  
|SQL_DESC_OCTET_LENGTH|Admitida|  
|SQL_DESC_OCTET_LENGTH_PTR|Admitida|  
|SQL_DESC_PARAMETER_TYPE|Parámetros de entrada|  
|SQL_DESC_PRECISION|Admitida|  
|SQL_DESC_SCALE|Admitida|  
|SQL_DESC_SCHEMA_NAME|No compatible|  
|SQL_DESC_SEARCHABLE|Admitida|  
|SQL_DESC_TABLE_NAME|No compatible|  
|SQL_DESC_TYPE|Admitida|  
|SQL_DESC_TYPE_NAME|Admitida|  
|SQL_DESC_UNNAMED|Admitida|  
|SQL_DESC_UNSIGNED|Admitida|  
|SQL_DESC_UPDATABLE|Admitida|
