---
title: Cambia el tipo de datos de fecha y hora | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a5a87a1cbfbdff5eb428e73d74cdd1199955d673
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63267696"
---
# <a name="datetime-data-type-changes"></a>Cambia el tipo de datos de fecha y hora
En ODBC 3. *x*, los identificadores de fecha, hora y tipos de datos SQL de marca de tiempo que han cambiado desde SQL_DATE, SQL_TIME y SQL_TIMESTAMP (con las instancias de **#define** en el archivo de encabezado de 9, 10 y 11) a SQL_TYPE_DATE, SQL_TYPE_TIME y SQL_TYPE_TIMESTAMP (con las instancias de **#define** en el archivo de encabezado de 93, 91 y 92), respectivamente. Los identificadores de tipo C correspondientes han cambiado desde SQL_C_DATE SQL_C_TIME y SQL_C_TIMESTAMP SQL_C_TYPE_DATE, SQL_C_TYPE_TIME y SQL_C_TYPE_TIMESTAMP, respectivamente.  
  
 El tamaño de columna y los dígitos decimales que se devuelven para los tipos de datos datetime SQL de ODBC 3. *x* son el mismo que la precisión y escala devuelto para ellos en ODBC 2. *x*. Estos valores son diferentes de los valores de los campos de descriptor SQL_DESC_PRECISION y SQL_DESC_SCALE. (Para obtener más información, consulte [tamaño de la columna, dígitos decimales, transferir la longitud en octetos y tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).)  
  
 Estos cambios afectan a **SQLDescribeCol**, **SQLDescribeParam**, y **SQLColAttribute**; **SQLBindCol**, **SQLBindParameter**, y **SQLGetData**; y **SQLColumns**, **SQLGetTypeInfo** , **SQLProcedureColumns**, **SQLStatistics**, y **SQLSpecialColumns**.  
  
 La tabla siguiente muestra cómo el ODBC 3 *.x* Driver Manager realiza la asignación de los tipos de datos C fecha, hora y marca de tiempo especificado en el *TargetType* argumentos de **SQLBindCol**y **SQLGetData** o en el *ValueType* argumento de **SQLBindParameter**.  
  
|Tipo de datos<br /><br /> código escrito|2.*x* aplicación<br /><br /> 2.*x* controlador|2.*x* aplicación<br /><br /> 3.*x* controlador|3.*x* aplicación<br /><br /> 2.*x* controlador|3.*x* aplicación<br /><br /> 3.*x* controlador|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_C_DATE (9)|Sin asignación|SQL_C_TYPE_DATE (91)|Ninguna asignación [1]|SQL_C_TYPE_DATE (91)|  
|SQL_C_TYPE_DATE (91)|Error (de DM)|Error (de DM)|SQL_C_DATE (9)|Ninguna asignación [2]|  
|SQL_C_TIME (10)|Sin asignación|SQL_C_TYPE_TIME (92)|Ninguna asignación [1]|SQL_C_TYPE_TIME (92)|  
|SQL_C_TYPE_TIME (92)|Error (de DM)|Error (de DM)|SQL_C_TIME (10)|Ninguna asignación [2]|  
|SQL_C_TIMESTAMP (11)|Sin asignación|SQL_C_TYPE_TIMESTAMP (93)|Ninguna asignación [1]|SQL_C_TYPE_TIMESTAMP (93)|  
|SQL_C_TYPE_TIMESTAMP (93)|Error (de DM)|Error (de DM)|SQL_C_TIMESTAMP (11)|Ninguna asignación [2]|  
  
 [1] como resultado de esto, una aplicación ODBC 3. *x* la aplicación funciona con un ODBC 2. *x* controlador puede usar los códigos de fecha, hora o marca de tiempo devueltos en los conjuntos de resultados devueltos por las funciones de catálogo.  
  
 [2] como resultado de esto, una aplicación ODBC 3. *x* la aplicación funciona con una aplicación ODBC 3. *x* controlador puede usar los códigos de fecha, hora o marca de tiempo devueltos en los conjuntos de resultados devueltos por las funciones de catálogo.  
  
 La tabla siguiente muestra cómo el ODBC 3 *.x* Driver Manager realiza la asignación de los tipos de datos SQL fecha, hora y marca de tiempo especificado en el *ParameterType* argumento de **SQLBindParameter**  o en el *DataType* argumento de **SQLGetTypeInfo**.  
  
|Tipo de datos<br /><br /> código escrito|2.*x* aplicación<br /><br /> 2.*x* controlador|2.*x* aplicación<br /><br /> 3.*x* controlador|3.*x* aplicación<br /><br /> 2.*x* controlador|3.*x* aplicación<br /><br /> 3.*x* controlador|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_DATE (9)|Sin asignación|SQL_TYPE_DATE (91)|Ninguna asignación [1]|SQL_TYPE_DATE (91)|  
|SQL_TYPE_DATE (91)|Error (de DM)|Error (de DM)|SQL_DATE (9)|Ninguna asignación [2]|  
|SQL_TIME (10)|Sin asignación|SQL_TYPE_TIME (92)|Ninguna asignación [1]|SQL_TYPE_TIME (92)|  
|SQL_TYPE_TIME (92)|Error (de DM)|Error (de DM)|SQL_TIME (10)|Ninguna asignación [2]|  
|SQL_TIMESTAMP (11)|Sin asignación|SQL_TYPE_TIMESTAMP (93)|Ninguna asignación [1]|SQL_TYPE_TIMESTAMP (93)|  
|SQL_TYPE_TIMESTAMP (93)|Error (de DM)|Error (de DM)|SQL_TIMESTAMP (11)|Ninguna asignación [2]|  
  
 [1] como resultado de esto, una aplicación ODBC 3. *x* la aplicación funciona con un ODBC 2. *x* controlador puede usar los códigos de fecha, hora o marca de tiempo devueltos en los conjuntos de resultados devueltos por las funciones de catálogo.  
  
 [2] como resultado de esto, una aplicación ODBC 3. *x* la aplicación funciona con una aplicación ODBC 3. *x* controlador puede usar los códigos de fecha, hora o marca de tiempo devueltos en los conjuntos de resultados devueltos por las funciones de catálogo.
