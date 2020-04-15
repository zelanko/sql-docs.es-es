---
title: Cambios en el tipo de datos de fecha y hora ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- time data type [ODBC]
- datetime data types [ODBC]
- date data type [ODBC]
- backward compatibility [ODBC], datetime data types
- timestamp data type [ODBC]
- compatibility [ODBC], datetime data types
ms.assetid: c38c79f9-8bb0-4633-ac86-542366c09a95
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4f186047dd31aa2c4b66ec1ce73c8cb9fae31c04
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304648"
---
# <a name="datetime-data-type-changes"></a>Cambia el tipo de datos de fecha y hora
En ODBC *3.x*, los identificadores de los tipos de datos SQL de fecha, hora y marca de tiempo han cambiado de SQL_DATE, SQL_TIME y SQL_TIMESTAMP (con instancias de **#define** en el archivo de encabezado de 9, 10 y 11) a SQL_TYPE_DATE, SQL_TYPE_TIME y SQL_TYPE_TIMESTAMP (con instancias de **#define** en el archivo de encabezado de 91, 92 y 93), respectivamente. Los identificadores de tipo C correspondientes han cambiado de SQL_C_DATE, SQL_C_TIME y SQL_C_TIMESTAMP a SQL_C_TYPE_DATE, SQL_C_TYPE_TIME y SQL_C_TYPE_TIMESTAMP, respectivamente.  
  
 El tamaño de columna y los dígitos decimales devueltos para los tipos de datos de fecha y hora sql en ODBC *3.x* son los mismos que la precisión y la escala devueltas para ellos en ODBC *2.x*. Estos valores son diferentes de los valores de los campos SQL_DESC_PRECISION y SQL_DESC_SCALE descriptor. (Para obtener más información, consulte Tamaño de [columna, Dígitos decimales, Transferir longitud de octeto y Tamaño](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)de visualización .)  
  
 Estos cambios afectan a **SQLDescribeCol**, **SQLDescribeParam**y **SQLColAttribute**; **SQLBindCol**, **SQLBindParameter**y **SQLGetData**; y **SQLColumns**, **SQLGetTypeInfo**, **SQLProcedureColumns**, **SQLStatistics**y **SQLSpecialColumns**.  
  
 En la tabla siguiente se muestra cómo el Administrador de controladores ODBC *3.x* realiza la asignación de los tipos de datos C de fecha, hora y marca de tiempo especificados en los argumentos *TargetType* de **SQLBindCol** y **SQLGetData** o en el argumento *ValueType* de **SQLBindParameter**.  
  
|Tipo de datos<br /><br /> código introducido|*2.x* aplicación para<br /><br /> *Controlador 2.x*|*2.x* aplicación para<br /><br /> *3.x* conductor|*3.x* aplicación para<br /><br /> *Controlador 2.x*|*3.x* aplicación para<br /><br /> *3.x* conductor|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_C_DATE (9)|Sin mapeo|SQL_C_TYPE_DATE (91)|Sin mapeo[1]|SQL_C_TYPE_DATE (91)|  
|SQL_C_TYPE_DATE (91)|Error (de DM)|Error (de DM)|SQL_C_DATE (9)|Sin mapeo[2]|  
|SQL_C_TIME (10)|Sin mapeo|SQL_C_TYPE_TIME (92)|Sin mapeo[1]|SQL_C_TYPE_TIME (92)|  
|SQL_C_TYPE_TIME (92)|Error (de DM)|Error (de DM)|SQL_C_TIME (10)|Sin mapeo[2]|  
|SQL_C_TIMESTAMP (11)|Sin mapeo|SQL_C_TYPE_TIMESTAMP (93)|Sin mapeo[1]|SQL_C_TYPE_TIMESTAMP (93)|  
|SQL_C_TYPE_TIMESTAMP (93)|Error (de DM)|Error (de DM)|SQL_C_TIMESTAMP (11)|Sin mapeo[2]|  
  
 [1] Como resultado de esto, una aplicación ODBC *3.x* que trabaja con un controlador ODBC *2.x* puede usar los códigos de fecha, hora o marca de tiempo devueltos en los conjuntos de resultados devueltos por las funciones de catálogo.  
  
 [2] Como resultado de esto, una aplicación ODBC *3.x* que trabaja con un controlador ODBC *3.x* puede usar los códigos de fecha, hora o marca de tiempo devueltos en los conjuntos de resultados devueltos por las funciones de catálogo.  
  
 En la tabla siguiente se muestra cómo el Administrador de controladores ODBC *3.x* realiza la asignación de los tipos de datos SQL de fecha, hora y marca de tiempo especificados en el argumento *ParameterType* de **SQLBindParameter** o en el argumento *DataType* de **SQLGetTypeInfo**.  
  
|Tipo de datos<br /><br /> código introducido|*2.x* aplicación para<br /><br /> *Controlador 2.x*|*2.x* aplicación para<br /><br /> *3.x* conductor|*3.x* aplicación para<br /><br /> *Controlador 2.x*|*3.x* aplicación para<br /><br /> *3.x* conductor|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_DATE (9)|Sin mapeo|SQL_TYPE_DATE (91)|Sin mapeo[1]|SQL_TYPE_DATE (91)|  
|SQL_TYPE_DATE (91)|Error (de DM)|Error (de DM)|SQL_DATE (9)|Sin mapeo[2]|  
|SQL_TIME (10)|Sin mapeo|SQL_TYPE_TIME (92)|Sin mapeo[1]|SQL_TYPE_TIME (92)|  
|SQL_TYPE_TIME (92)|Error (de DM)|Error (de DM)|SQL_TIME (10)|Sin mapeo[2]|  
|SQL_TIMESTAMP (11)|Sin mapeo|SQL_TYPE_TIMESTAMP (93)|Sin mapeo[1]|SQL_TYPE_TIMESTAMP (93)|  
|SQL_TYPE_TIMESTAMP (93)|Error (de DM)|Error (de DM)|SQL_TIMESTAMP (11)|Sin mapeo[2]|  
  
 [1] Como resultado de esto, una aplicación ODBC *3.x* que trabaja con un controlador ODBC *2.x* puede usar los códigos de fecha, hora o marca de tiempo devueltos en los conjuntos de resultados devueltos por las funciones de catálogo.  
  
 [2] Como resultado de esto, una aplicación ODBC *3.x* que trabaja con un controlador ODBC *3.x* puede usar los códigos de fecha, hora o marca de tiempo devueltos en los conjuntos de resultados devueltos por las funciones de catálogo.
