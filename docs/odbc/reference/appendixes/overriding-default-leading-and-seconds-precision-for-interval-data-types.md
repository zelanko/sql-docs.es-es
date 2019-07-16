---
title: Invalidar líderes y precisión en segundos para los tipos de datos Interval | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 13adfb16b772acc5fac30cf3d10c6199f16f479d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100626"
---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>Reemplazar predeterminado inicial y la precisión de segundos para los tipos de datos Interval
Cuando se establece el campo SQL_DESC_TYPE de una descartar a un tipo C de intervalo o datetime, llamando **SQLBindCol** o **SQLSetDescField**, el campo SQL_DESC_PRECISION (que contiene el intervalo (segundos) precisión) se establece en los valores predeterminados siguientes:  
  
-   6 para todos los tipos de datos de intervalo con un segundo componente y marca de tiempo.  
  
-   0 para todos los demás tipos de datos.  
  
 Para todos los tipos de datos de intervalo, el campo descriptor SQL_DESC_DATETIME_INTERVAL_PRECISION, que contiene la precisión del campo intervalo inicial, se establece en un valor predeterminado de 2.  
  
 Cuando se establece el campo SQL_DESC_TYPE en un APD a un tipo C de intervalo o datetime, llamando **SQLBindParameter** o **SQLSetDescField**, el SQL_DESC_PRECISION y SQL_DESC_DATETIME_INTERVAL_ Campos de precisión en el APD se establecen los valores predeterminados indicados anteriormente. Esto es cierto para los parámetros de entrada pero no para los parámetros de entrada y salida o de salida.  
  
 Una llamada a **SQLSetDescRec** establece el intervalo de precisión del principio en el valor predeterminado, pero establece la precisión de segundos de intervalo (en el campo SQL_DESC_PRECISION) en el valor de su *precisión* argumento.  
  
 Si anteriormente cualquiera de los valores predeterminados dada no es aceptable para una aplicación, la aplicación debe establecer el campo SQL_DESC_PRECISION o SQL_DESC_DATETIME_INTERVAL_PRECISION mediante una llamada a **SQLSetDescField**.  
  
 Si la aplicación llama a **SQLGetData** para devolver datos en una hora o un intervalo de tipo C, se utilizan la precisión líderes de intervalo predeterminado y la precisión de segundos del intervalo. Si cualquier valor predeterminado no es aceptable, la aplicación debe llamar a **SQLSetDescField** para establecer el campo descriptor, o **SQLSetDescRec** establecer SQL_DESC_PRECISION. La llamada a **SQLGetData** debe tener un *TargetType* de SQL_ARD_TYPE para usar los valores en los campos de descriptor.  
  
 Cuando **SQLPutData** se denomina el intervalo de líderes de precisión y el intervalo de segundos precisión se leen desde los campos del registro de descriptor que corresponden al parámetro de datos en ejecución o columna, que son campos APD para las llamadas para **SQLExecute** o **SQLExecDirect**, o los campos de Descartar para las llamadas a **SQLBulkOperations** o **SQLSetPos**.
