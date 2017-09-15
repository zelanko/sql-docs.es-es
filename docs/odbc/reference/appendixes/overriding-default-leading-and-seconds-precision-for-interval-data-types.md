---
title: "Invalidar inicial y la precisión de segundos para los tipos de datos Interval | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: 3d65493f-dce7-4d29-9f59-c63a4e47918c
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1ce549be1e3222f41615e5935418cf3e02e767a4
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="overriding-default-leading-and-seconds-precision-for-interval-data-types"></a>Reemplazar predeterminado inicial y la precisión de segundos para los tipos de datos Interval
Cuando se establece el campo SQL_DESC_TYPE de una descartar a un tipo C de intervalo o datetime, llamar a **SQLBindCol** o **SQLSetDescField**, el campo SQL_DESC_PRECISION (que contiene el intervalo (segundos) precisión) se establece en los valores predeterminados siguientes:  
  
-   6 para todos los tipos de datos de intervalo con un segundo componente y marca de tiempo.  
  
-   0 para todos los demás tipos de datos.  
  
 Para todos los tipos de datos de intervalo, el campo de descriptor SQL_DESC_DATETIME_INTERVAL_PRECISION, que contiene la precisión del campo intervalo inicial, se establece en un valor predeterminado de 2.  
  
 Cuando se establece el campo SQL_DESC_TYPE en un APD a un tipo C de intervalo o datetime, llamar a **SQLBindParameter** o **SQLSetDescField**, los SQL_DESC_PRECISION y SQL_DESC_DATETIME_INTERVAL_ Campos de precisión en el APD se establecen en el valor predeterminado proporcionado previamente. Esto es cierto para parámetros de entrada, pero no para los parámetros de entrada/salida o de salida.  
  
 Una llamada a **SQLSetDescRec** establece el intervalo de precisión del principio en el valor predeterminado, sino que establece la precisión de segundos de intervalo (en el campo SQL_DESC_PRECISION) en el valor de su *precisión* argumento.  
  
 Si previamente cualquiera de los valores predeterminados dados no es aceptable para una aplicación, la aplicación debe establecer el campo SQL_DESC_PRECISION o SQL_DESC_DATETIME_INTERVAL_PRECISION mediante una llamada a **SQLSetDescField**.  
  
 Si la aplicación llama **SQLGetData** para devolver datos en una fecha y hora o un intervalo de tipo C, se usan el valor predeterminado inicial de precisión de intervalo y precisión de segundos del intervalo. Si cualquier valor predeterminado no es aceptable, la aplicación debe llamar a **SQLSetDescField** para establecer uno de los campos descriptor, o **SQLSetDescRec** establecer SQL_DESC_PRECISION. La llamada a **SQLGetData** debe tener un *TargetType* de SQL_ARD_TYPE para usar los valores en los campos de descriptor.  
  
 Cuando **SQLPutData** se llama, el intervalo a la precisión y el intervalo de segundos precisión se leen de los campos del registro de descriptor que corresponden a los parámetro de datos en ejecución o una columna, que son campos APD de llamadas para **SQLExecute** o **SQLExecDirect**, o campos de Descartar para las llamadas a **SQLBulkOperations** o **SQLSetPos**.
