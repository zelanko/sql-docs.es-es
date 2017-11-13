---
title: Tipo de datos de fecha y hora cambia | Documentos de Microsoft
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
- time data type [ODBC]
- datetime data types [ODBC]
- date data type [ODBC]
- backward compatibility [ODBC], datetime data types
- timestamp data type [ODBC]
- compatibility [ODBC], datetime data types
ms.assetid: c38c79f9-8bb0-4633-ac86-542366c09a95
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b09a6daa19b7a8b22ac5f4b3147e6cefde6ffc60
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="datetime-data-type-changes"></a>Cambia el tipo de datos de fecha y hora
En ODBC 3. *x*, los identificadores de fecha, hora y tipos de datos SQL de marca de tiempo han cambiado desde SQL_DATE, SQL_TIME y SQL_TIMESTAMP (con instancias de **#define** en el archivo de encabezado de 9, 10 y 11) a SQL_TYPE_DATE, SQL_TYPE_TIME y SQL_TYPE_TIMESTAMP (con instancias de **#define** en el archivo de encabezado de 91, 92 y 93), respectivamente. Los identificadores de tipo C correspondientes han cambiado desde SQL_C_DATE, SQL_C_TIME y SQL_C_TIMESTAMP SQL_C_TYPE_DATE, SQL_C_TYPE_TIME y SQL_C_TYPE_TIMESTAMP, respectivamente.  
  
 El tamaño de la columna y los dígitos decimales que se devuelve para los tipos de datos de fecha y hora SQL en ODBC 3. *x* son el mismo que la precisión y escala devueltos para ellos en ODBC 2. *x*. Estos valores son diferentes de los valores de los campos de descriptor SQL_DESC_PRECISION y SQL_DESC_SCALE. (Para obtener más información, consulte [tamaño de la columna, dígitos decimales, transferencia de longitud de bytes y el tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).)  
  
 Estos cambios afectan a **SQLDescribeCol**, **SQLDescribeParam**, y **SQLColAttribute**; **SQLBindCol**, **SQLBindParameter**, y **SQLGetData**; y **SQLColumns**, **SQLGetTypeInfo** , **SQLProcedureColumns**, **SQLStatistics**, y **SQLSpecialColumns**.  
  
 La tabla siguiente muestra cómo ODBC 3*.x* el Administrador de controladores realiza la asignación de los tipos de datos de C de fecha, hora y marca de tiempo que se especificó en el *TargetType* argumentos de **SQLBindCol**y **SQLGetData** o en la *ValueType* argumento de **SQLBindParameter**.  
  
|Tipo de datos<br /><br /> código escrito|2.*x* aplicación<br /><br /> 2.*x* controlador|2.*x* aplicación<br /><br /> 3.*x* controlador|3.*x* aplicación<br /><br /> 2.*x* controlador|3.*x* aplicación<br /><br /> 3.*x* controlador|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_C_DATE (9)|Ninguna asignación|SQL_C_TYPE_DATE (91)|Ninguna asignación [1]|SQL_C_TYPE_DATE (91)|  
|SQL_C_TYPE_DATE (91)|Error (a través de DM)|Error (a través de DM)|SQL_C_DATE (9)|Ninguna asignación [2]|  
|SQL_C_TIME (10)|Ninguna asignación|SQL_C_TYPE_TIME (92)|Ninguna asignación [1]|SQL_C_TYPE_TIME (92)|  
|SQL_C_TYPE_TIME (92)|Error (a través de DM)|Error (a través de DM)|SQL_C_TIME (10)|Ninguna asignación [2]|  
|SQL_C_TIMESTAMP (11)|Ninguna asignación|SQL_C_TYPE_TIMESTAMP (93)|Ninguna asignación [1]|SQL_C_TYPE_TIMESTAMP (93)|  
|SQL_C_TYPE_TIMESTAMP (93)|Error (a través de DM)|Error (a través de DM)|SQL_C_TIMESTAMP (11)|Ninguna asignación [2]|  
  
 [1] como resultado de esto, una aplicación ODBC 3. *x* aplicación trabajar con una API ODBC 2. *x* controlador puede usar los códigos de fecha, hora o marca de tiempo devueltos en los conjuntos de resultados devueltos por las funciones de catálogo.  
  
 [2] como resultado de esto, una aplicación ODBC 3. *x* aplicación trabajar con una aplicación ODBC 3. *x* controlador puede usar los códigos de fecha, hora o marca de tiempo devueltos en los conjuntos de resultados devueltos por las funciones de catálogo.  
  
 La tabla siguiente muestra cómo ODBC 3*.x* el Administrador de controladores realiza la asignación de los tipos de datos SQL de fecha, hora y marca de tiempo que se escribió en el *ParameterType* argumento de **SQLBindParameter**  o en la *DataType* argumento de **SQLGetTypeInfo**.  
  
|Tipo de datos<br /><br /> código escrito|2.*x* aplicación<br /><br /> 2.*x* controlador|2.*x* aplicación<br /><br /> 3.*x* controlador|3.*x* aplicación<br /><br /> 2.*x* controlador|3.*x* aplicación<br /><br /> 3.*x* controlador|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_DATE (9)|Ninguna asignación|SQL_TYPE_DATE (91)|Ninguna asignación [1]|SQL_TYPE_DATE (91)|  
|SQL_TYPE_DATE (91)|Error (a través de DM)|Error (a través de DM)|SQL_DATE (9)|Ninguna asignación [2]|  
|SQL_TIME (10)|Ninguna asignación|SQL_TYPE_TIME (92)|Ninguna asignación [1]|SQL_TYPE_TIME (92)|  
|SQL_TYPE_TIME (92)|Error (a través de DM)|Error (a través de DM)|SQL_TIME (10)|Ninguna asignación [2]|  
|SQL_TIMESTAMP (11)|Ninguna asignación|SQL_TYPE_TIMESTAMP (93)|Ninguna asignación [1]|SQL_TYPE_TIMESTAMP (93)|  
|SQL_TYPE_TIMESTAMP (93)|Error (a través de DM)|Error (a través de DM)|SQL_TIMESTAMP (11)|Ninguna asignación [2]|  
  
 [1] como resultado de esto, una aplicación ODBC 3. *x* aplicación trabajar con una API ODBC 2. *x* controlador puede usar los códigos de fecha, hora o marca de tiempo devueltos en los conjuntos de resultados devueltos por las funciones de catálogo.  
  
 [2] como resultado de esto, una aplicación ODBC 3. *x* aplicación trabajar con una aplicación ODBC 3. *x* controlador puede usar los códigos de fecha, hora o marca de tiempo devueltos en los conjuntos de resultados devueltos por las funciones de catálogo.

