---
title: Reemplazar la precisión de los segundos y los ajustes para los tipos de datos de intervalo . Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: 3d65493f-dce7-4d29-9f59-c63a4e47918c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1e60d5d8fc696ad8e2bd4cfb0c082ff214e066d0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303606"
---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>Reemplazar predeterminado inicial y la precisión de segundos para los tipos de datos Interval
Cuando el campo SQL_DESC_TYPE de un ARD se establece en un tipo datetime o interval C, llamando a **SQLBindCol** o **SQLSetDescField**, el campo SQL_DESC_PRECISION (que contiene la precisión de segundos de intervalo) se establece en los siguientes valores predeterminados:  
  
-   6 para la marca de tiempo y todos los tipos de datos de intervalo con un segundo componente.  
  
-   0 para todos los demás tipos de datos.  
  
 Para todos los tipos de datos de intervalo, el campo descriptor de SQL_DESC_DATETIME_INTERVAL_PRECISION, que contiene la precisión del campo inicial del intervalo, se establece en un valor predeterminado de 2.  
  
 Cuando el campo SQL_DESC_TYPE de un APD se establece en un tipo datetime o interval C, llamando a **SQLBindParameter** o **SQLSetDescField**, los campos SQL_DESC_PRECISION y SQL_DESC_DATETIME_INTERVAL_PRECISION del APD se establecen en el valor predeterminado especificado anteriormente. Esto es cierto para los parámetros de entrada, pero no para los parámetros de entrada/salida o salida.  
  
 Una llamada a **SQLSetDescRec** establece la precisión inicial del intervalo en el valor predeterminado, pero establece la precisión de los segundos de intervalo (en el campo SQL_DESC_PRECISION) en el valor de su *Precision* argumento.  
  
 Si cualquiera de los valores predeterminados especificados anteriormente no es aceptable para una aplicación, la aplicación debe establecer el SQL_DESC_PRECISION o SQL_DESC_DATETIME_INTERVAL_PRECISION campo mediante una llamada a **SQLSetDescField**.  
  
 Si la aplicación llama a **SQLGetData** para devolver datos a un tipo datetime o interval C, se usa la precisión inicial del intervalo predeterminado y la precisión de los segundos de intervalo. Si no se acepta ningún valor predeterminado, la aplicación debe llamar a **SQLSetDescField** para establecer el campo descriptor o **SQLSetDescRec** para establecer SQL_DESC_PRECISION. La llamada a **SQLGetData** debe tener un *TargetType* de SQL_ARD_TYPE para usar los valores de los campos descriptores.  
  
 Cuando se llama a **SQLPutData,** la precisión inicial del intervalo y la precisión de los segundos de intervalo se leen de los campos del registro descriptor que corresponden al parámetro o columna de datos en ejecución, que son campos APD para llamadas a **SQLExecute** o **SQLExecDirect,** o campos ARD para llamadas a **SQLBulkOperations** o **SQLSetPos**.
