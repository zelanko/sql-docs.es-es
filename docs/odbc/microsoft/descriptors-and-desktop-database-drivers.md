---
title: Descriptores y controladores de base de datos de escritorio | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68112047"
---
# <a name="descriptors-and-desktop-database-drivers"></a>Descriptores de y controladores de escritorio de la base de datos
Un descriptor es una estructura de datos que contiene información sobre los datos de columna o los parámetros dinámicos. **SQLGetDescField** se puede usar para recuperar los descriptores admitidos que se enumeran a continuación. Los descriptores de parámetros de implementación (IPD) no se rellenan automáticamente porque no se admite **SQLDescribeParam** . Tampoco se admiten los campos de descriptor que no están disponibles a través de jet (como SQL_DESC_BASE_TABLE_NAME).  
  
 Para obtener más información acerca de los campos de descriptor compatibles con jet, vea la *Guía del programador de Microsoft Jet motor de base de datos*.  
  
 Para obtener más información acerca de los descriptores, vea los temas de "descriptores" en la *Referencia del programador de ODBC*.  
  
|Campos de descriptor|Nivel de compatibilidad|  
|-----------------------|-------------------|  
|SQL_DESC_ALLOC_TYPE|Compatible|  
|SQL_DESC_ARRAY_SIZE|Solo se admite para ARD|  
|SQL_DESC_ARRAY_STATUS_PTR|Compatible|  
|SQL_DESC_BIND_OFFSET_PTR|Compatible|  
|SQL_DESC_BIND_TYPE|Compatible|  
|SQL_DESC_COUNT|Compatible|  
|SQL_DESC_ROWS_PROCESSED_PTR|Solo se admite para ARD|  
|SQL_DESC_AUTO_UNIQUE_VALUE|Compatible|  
|SQL_DESC_BASE_COLUMN_NAME|Compatible (nuevo)|  
|SQL_DESC_BASE_TABLE_NAME|Compatible (nuevo)|  
|SQL_DESC_CASE_SENSITIVE|Siempre FALSE|  
|SQL_DESC_CATALOG_NAME|No compatible|  
|SQL_DESC_CONCISE_TYPE|Compatible|  
|SQL_DESC_DATA_PTR|Compatible|  
|SQL_DESC_DATETIME_INTERVAL_CODE|Compatible|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|Compatible con tipos de intervalo C|  
|SQL_DESC_DISPLAY_SIZE|Compatible|  
|SQL_DESC_FIXED_PREC_SCALE|Compatible (TRUE para Money)|  
|SQL_DESC_INDICATOR_PTR|Compatible|  
|SQL_DESC_LABEL|Compatible|  
|SQL_DESC_LENGTH|Compatible|  
|SQL_DESC_LITERAL_PREFIX|Compatible|  
|SQL_DESC_LITERAL_SUFFIX|Compatible|  
|SQL_DESC_LOCAL_TYPE_NAME|No compatible (devuelve una cadena vacía)|  
|SQL_DESC_NAME|Compatible|  
|SQL_DESC_NULLABLE|Compatible<br /><br /> **Nota:** No se admite en las versiones anteriores a Jet 4,0|  
|SQL_DESC_NUM_PREC_RADIX|Compatible|  
|SQL_DESC_OCTET_LENGTH|Compatible|  
|SQL_DESC_OCTET_LENGTH_PTR|Compatible|  
|SQL_DESC_PARAMETER_TYPE|Solo parámetros de entrada|  
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
