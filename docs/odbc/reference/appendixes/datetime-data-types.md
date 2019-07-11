---
title: Los tipos de datos de fecha y hora | Microsoft Docs
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
- data types [ODBC], date
- backward compatibility [ODBC], datetime data types
- timestamp data type [ODBC]
- data types [ODBC], timestamp
- data types [ODBC], backward compatibility
- compatibility [ODBC], datetime data types
- data types [ODBC], time
ms.assetid: 6b9363c9-04bf-4492-a210-7aa15dea4af8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 13cb433da64b78a8b5e70f28642fd576f6803ed5
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792594"
---
# <a name="datetime-data-types"></a>Tipos de datos de fecha y hora
En ODBC *3.x*, los identificadores de fecha, hora y tipos de datos SQL de marca de tiempo que han cambiado desde SQL_DATE, SQL_TIME y SQL_TIMESTAMP (con las instancias de **#define** en el archivo de encabezado de 9, 10 y 11) a SQL_ TYPE_DATE, SQL_TYPE_TIME y SQL_TYPE_TIMESTAMP (con las instancias de **#define** en el archivo de encabezado de 93, 91 y 92), respectivamente. El tipo C correspondiente identificadores han cambiado desde SQL_C_DATE SQL_C_TIME y SQL_C_TIMESTAMP SQL_C_TYPE_DATE, SQL_C_TYPE_TIME y SQL_C_TYPE_TIMESTAMP, respectivamente y las instancias de **#define** han cambiado en consecuencia.  
  
 El tamaño de la columna y los dígitos decimales que se devuelven para los tipos de datos datetime SQL de ODBC *3.x* son el mismo que la precisión y escala devuelto para ellos en ODBC *2.x*. Estos valores son diferentes de los valores de los campos de descriptor SQL_DESC_PRECISION y SQL_DESC_SCALE. (Para obtener más información, consulte [tamaño de la columna, dígitos decimales, transferir la longitud en octetos y tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) en el apéndice D: Tipos de datos).  
  
 Estos cambios afectan a **SQLDescribeCol**, **SQLDescribeParam**, y **SQLColAttributes**; **SQLBindCol**, **SQLBindParameter**, y **SQLGetData**; y **SQLColumns**, **SQLGetTypeInfo** , **SQLProcedureColumns**, **SQLStatistics**, y **SQLSpecialColumns**.  
  
 Un ODBC *3.x* controlador procesa las llamadas de función aparece en el párrafo anterior según la configuración del atributo entorno SQL_ATTR_ODBC_VERSION. Para **SQLColumns**, **SQLGetTypeInfo**, **SQLProcedureColumns**, **SQLSpecialColumns**, y **SQLStatistics** si SQL_ATTR_ODBC_VERSION está establecido en SQL_OV_ODBC3, las funciones de devolución SQL_TYPE_DATE, SQL_TYPE_TIME y SQL_TYPE_TIMESTAMP en el campo DATA_TYPE. La columna COLUMN_SIZE (en el conjunto de resultados devuelto por **SQLColumns**, **SQLGetTypeInfo**, **SQLProcedureColumns**, y **SQLSpecialColumns**) contiene la precisión binaria para el tipo numérico aproximado. La columna NUM_PREC_RADIX (en el conjunto de resultados devuelto por **SQLColumns**, **SQLGetTypeInfo**, y **SQLProcedureColumns**) contiene un valor de 2. Si se establece SQL_ATTR_ODBC_VERSION SQL_OV_ODBC2 y, después, las funciones de devolución SQL_DATE, SQL_TIME y SQL_TIMESTAMP en el campo DATA_TYPE, la columna COLUMN_SIZE contiene la precisión decimal para el tipo numérico aproximado y la columna NUM_PREC_RADIX contiene un valor de 10.  
  
 Cuando se solicitan todos los tipos de datos en una llamada a **SQLGetTypeInfo**, el conjunto de resultados devuelto por la función contendrá tanto SQL_TYPE_DATE, SQL_TYPE_TIME y SQL_TYPE_TIMESTAMP tal como se define en ODBC *3.x*, y SQL_DATE, SQL_TIME y SQL_TIMESTAMP tal como se define en ODBC *2.x*.  
  
 Debido a cómo ODBC *3.x* Driver Manager realiza la asignación de los tipos de datos de fecha, hora y marca de tiempo, ODBC *3.x* controladores deben reconocer solo **#defines** de 91, 92, y 93 para la fecha, hora y los tipos de datos C de la marca de tiempo especificado en el *TargetType* argumentos de **SQLBindCol** y **SQLGetData** o  *ValueType* argumento de **SQLBindParameter**y solo debe reconocer **#defines** de 91, 92 y 93 para la fecha, hora y tipos de datos SQL de marca de tiempo especifican en el *ParameterType* argumento de **SQLBindParameter** o *DataType* argumento de **SQLGetTypeInfo**. Para obtener más información, consulte [cambios de tipos de datos de fecha y hora](../../../odbc/reference/develop-app/datetime-data-type-changes.md).
