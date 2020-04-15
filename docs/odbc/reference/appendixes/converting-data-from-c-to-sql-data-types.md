---
title: Conversión de datos de C a tipos de datos SQL ( Sql Data Types) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], about converting
- converting data from c to SQL types [ODBC]
- data conversions from C to SQL types [ODBC], about converting
- data types [ODBC], C data types
- data types [ODBC], converting data
- SQL data types [ODBC], converting from C types
- data types [ODBC], SQL data types
- data conversions from C to SQL types [ODBC]
- C data types [ODBC], converting to SQL types
ms.assetid: ee0afe78-b58f-4d34-ad9b-616bb23653bd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8fb707e77df7d793277d4a23146adc980eede6fd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304664"
---
# <a name="converting-data-from-c-to-sql-data-types"></a>Convertir datos de C en tipos de datos SQL
Cuando una aplicación llama a **SQLExecute** o **SQLExecDirect**, el controlador recupera los datos de los parámetros enlazados con **SQLBindParameter** desde las ubicaciones de almacenamiento de la aplicación. Cuando una aplicación llama a **SQLSetPos**, el controlador recupera los datos de una operación de actualización o adición de columnas enlazadas con **SQLBindCol**. Para los parámetros de datos en ejecución, la aplicación envía los datos de parámetro con **SQLPutData**. Si es necesario, el controlador convierte los datos del tipo de datos especificado por el *ValueType* argumento en **SQLBindParameter** al tipo de datos especificado por el *ParameterType* argumento en **SQLBindParameter**y, a continuación, envía los datos al origen de datos.  
  
 En la tabla siguiente se muestran las conversiones admitidas de tipos de datos ODBC C a tipos de datos SQL ODBC. Un círculo rellenado indica la conversión predeterminada para un tipo de datos SQL (el tipo de datos C desde el que se convertirán los datos cuando se SQL_C_DEFAULT el valor de *ValueType* o el campo descriptor de SQL_DESC_CONCISE_TYPE). Un círculo hueco indica una conversión admitida.  
  
 El formato de los datos convertidos no se ve afectado por la configuración de país ® Windows.  
  
 ![Conversiones admitidas: de tipos de datos ODBC C a SQL](../../../odbc/reference/appendixes/media/apd1b.gif "apd1b")  
  
 Las tablas de las secciones siguientes describen cómo el controlador o el origen de datos convierte los datos enviados al origen de datos; Los controladores son necesarios para admitir conversiones de todos los tipos de datos ODBC C a los tipos de datos SQL ODBC que admiten. Para un tipo de datos ODBC C determinado, la primera columna de la tabla enumera los valores de entrada legales del argumento *ParameterType* en **SQLBindParameter**. La segunda columna enumera los resultados de una prueba que realiza el controlador para determinar si puede convertir los datos. La tercera columna enumera el SQLSTATE devuelto para cada resultado por **SQLExecDirect**, **SQLExecute**, **SQLBulkOperations**, **SQLSetPos**o **SQLPutData**. Los datos se envían al origen de datos solo si se devuelve SQL_SUCCESS.  
  
 Si el *ParameterType* argumento en **SQLBindParameter** contiene el identificador de un tipo de datos SQL ODBC que no se muestra en la tabla para un tipo de datos C determinado, **SQLBindParameter** devuelve SQLSTATE 07006 (infracción de atributo de tipo de datos restringido). Si el *ParameterType* argumento contiene un identificador específico del controlador y el controlador no admite la conversión del tipo de datos ODBC C específico a ese tipo de datos SQL específico del controlador, **SQLBindParameter** devuelve SQLSTATE HYC00 (característica opcional no implementada).  
  
 Si el *ParameterValuePtr* y *StrLen_or_IndPtr* argumentos especificados en **SQLBindParameter** son punteros nulos, esa función devuelve SQLSTATE HY009 (uso no válido de puntero nulo). Aunque no se muestra en las tablas, una aplicación establece el valor del búfer de longitud/indicador al que apunta el *argumento StrLen_or_IndPtr* de **SQLBindParameter** o el valor del argumento *StrLen_or_IndPtr* de **SQLPutData** en SQL_NULL_DATA para especificar un valor de datos SQL NULL. (El argumento *StrLen_or_IndPtr* corresponde al campo SQL_DESC_OCTET_LENGTH_PTR del APD.) La aplicación establece estos valores en SQL_NTS \*especificar que el valor \*de *ParameterValuePtr* en **SQLBindParameter** o *DataPtr* en **SQLPutData** (señalado por el campo de SQL_DESC_DATA_PTR de la APD) es una cadena terminada en null.  
  
 En las tablas se utilizan los siguientes términos:  
  
-   **Longitud de bytes de datos:** número de bytes de datos SQL disponibles para enviar al origen de datos, independientemente de si los datos se truncarán antes de enviarlos al origen de datos. Para los datos de cadena, esto no incluye espacio para el carácter de terminación nula.  
  
-   Longitud de bytes de **columna:** número de bytes necesarios para almacenar los datos en el origen de datos.  
  
-   **Longitud** de bytes de caracteres: número máximo de bytes necesarios para mostrar los datos en forma de carácter. Esto es como se define para cada tipo de datos SQL en Tamaño de [visualización](../../../odbc/reference/appendixes/display-size.md), excepto que la longitud de byte de caracteres está en bytes, mientras que el tamaño de visualización está en caracteres.  
  
-   **Número de dígitos:** número de caracteres utilizados para representar un número, incluido el signo menos, el punto decimal y el exponente (si es necesario).  
  
-   **Palabras en**   
     ***cursiva*** - Elementos de la gramática SQL. Para obtener la sintaxis de los elementos gramaticales, vea [Apéndice C: Gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [C a SQL: Carácter](../../../odbc/reference/appendixes/c-to-sql-character.md)  
  
-   [C a SQL: Numeric](../../../odbc/reference/appendixes/c-to-sql-numeric.md)  
  
-   [C a SQL: bit](../../../odbc/reference/appendixes/c-to-sql-bit.md)  
  
-   [C a SQL: Binary](../../../odbc/reference/appendixes/c-to-sql-binary.md)  
  
-   [C a SQL: Date](../../../odbc/reference/appendixes/c-to-sql-date.md)  
  
-   [C a SQL: GUID](../../../odbc/reference/appendixes/c-to-sql-guid.md)  
  
-   [C a SQL: Time](../../../odbc/reference/appendixes/c-to-sql-time.md)  
  
-   [C a SQL: Timestamp](../../../odbc/reference/appendixes/c-to-sql-timestamp.md)  
  
-   [C a SQL: Intervalos de mes y año](../../../odbc/reference/appendixes/c-to-sql-year-month-intervals.md)  
  
-   [C a SQL: Intervalos de día y hora](../../../odbc/reference/appendixes/c-to-sql-day-time-intervals.md)  
  
-   [Ejemplos de conversión de datos de C en SQL](../../../odbc/reference/appendixes/c-to-sql-data-conversion-examples.md)
