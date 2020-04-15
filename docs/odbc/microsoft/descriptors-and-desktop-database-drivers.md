---
title: Descriptores y controladores de base de datos de escritorio ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ef79855f71d23e5a884822371f1894eb83442a9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303517"
---
# <a name="descriptors-and-desktop-database-drivers"></a>Descriptores de y controladores de escritorio de la base de datos
Un descriptor es una estructura de datos que contiene información sobre datos de columna o parámetros dinámicos. **SQLGetDescField** se puede utilizar para recuperar los descriptores admitidos que se enumeran a continuación. Los descriptores de parámetros de implementación (IPD) no se rellenan automáticamente porque no se admite **SQLDescribeParam.** Tampoco se admiten los campos de descriptor que no están disponibles a través de Jet (como SQL_DESC_BASE_TABLE_NAME).  
  
 Para obtener más información acerca de los campos descriptores compatibles con Jet, consulte la Guía del programador del motor de base de *datos de Microsoft Jet*.  
  
 Para obtener más información acerca de los descriptores, vea los temas en "Descriptores" en la *referencia del programador ODBC*.  
  
|Campos descriptores|Nivel de compatibilidad|  
|-----------------------|-------------------|  
|SQL_DESC_ALLOC_TYPE|Compatible|  
|SQL_DESC_ARRAY_SIZE|Soportado sólo para ARD|  
|SQL_DESC_ARRAY_STATUS_PTR|Compatible|  
|SQL_DESC_BIND_OFFSET_PTR|Compatible|  
|SQL_DESC_BIND_TYPE|Compatible|  
|SQL_DESC_COUNT|Compatible|  
|SQL_DESC_ROWS_PROCESSED_PTR|Soportado sólo para ARD|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Compatible|  
|SQL_DESC_BASE_COLUMN_NAME|Compatible (NUEVO)|  
|SQL_DESC_BASE_TABLE_NAME|Compatible (NUEVO)|  
|SQL_DESC_CASE_SENSITIVE|Siempre FALSO|  
|SQL_DESC_CATALOG_NAME|No compatible|  
|SQL_DESC_CONCISE_TYPE|Compatible|  
|SQL_DESC_DATA_PTR|Compatible|  
|SQL_DESC_DATETIME_INTERVAL_CODE|Compatible|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|Compatible con los tipos INTERVAL C|  
|SQL_DESC_DISPLAY_SIZE|Compatible|  
|SQL_DESC_FIXED_PREC_SCALE|Compatible (TRUE por dinero)|  
|SQL_DESC_INDICATOR_PTR|Compatible|  
|SQL_DESC_LABEL|Compatible|  
|SQL_DESC_LENGTH|Compatible|  
|SQL_DESC_LITERAL_PREFIX|Compatible|  
|SQL_DESC_LITERAL_SUFFIX|Compatible|  
|SQL_DESC_LOCAL_TYPE_NAME|No admitido (devuelve la cadena EMPTY)|  
|SQL_DESC_NAME|Compatible|  
|SQL_DESC_NULLABLE|Compatible<br /><br /> **Nota** No compatible con versiones anteriores a Jet 4.0|  
|SQL_DESC_NUM_PREC_RADIX|Compatible|  
|SQL_DESC_OCTET_LENGTH|Compatible|  
|SQL_DESC_OCTET_LENGTH_PTR|Compatible|  
|SQL_DESC_PARAMETER_TYPE|Sólo parámetros de entrada|  
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
