---
title: Convertir datos de C a tipos de datos SQL | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: "9"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bb1d1c07f1453886fd91159eabad97dc90b9b191
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="converting-data-from-c-to-sql-data-types"></a>Convertir datos de C a tipos de datos SQL
Cuando una aplicación llama **SQLExecute** o **SQLExecDirect**, el controlador JDBC recupera los datos para los parámetros enlazados con **SQLBindParameter** desde ubicaciones de almacenamiento en la aplicación. Cuando una aplicación llama **SQLSetPos**, el controlador recupera los datos de una actualización o agregar operación de columnas enlazadas con **SQLBindCol**. Para los parámetros de datos en ejecución, la aplicación envía los datos del parámetro con **SQLPutData**. Si es necesario, el controlador convierte los datos del tipo de datos especificado por la *ValueType* argumento en **SQLBindParameter** al tipo de datos especificado por el *ParameterType*argumento en **SQLBindParameter**y, a continuación, envía los datos al origen de datos.  
  
 En la tabla siguiente muestra las conversiones compatibles de C de ODBC tipos de datos a tipos de datos SQL de ODBC. Un círculo relleno indica la conversión de valor predeterminado para un tipo de datos SQL (el tipo de datos de C desde el que los datos se convertirá cuando el valor de *ValueType* o el campo de descriptor SQL_DESC_CONCISE_TYPE es SQL_C_DEFAULT). Un círculo vacío indica una conversión compatible.  
  
 El formato de los datos convertidos no se ve afectado por el valor de país Windows®.  
  
 ![Conversiones admitidas: tipos de datos SQL ODBC C a](../../../odbc/reference/appendixes/media/apd1b.gif "apd1b")  
  
 Las tablas en las secciones siguientes describe cómo el controlador o el origen de datos convierte datos que se envían al origen de datos; se requieren controladores para admitir las conversiones de todos los tipos de datos ODBC C a los tipos de datos SQL de ODBC que admite. Para un determinado tipo de datos C de ODBC, la primera columna de la tabla enumera los valores de entrada válidos de la *ParameterType* argumento en **SQLBindParameter**. La segunda columna muestra los resultados de una prueba de que el controlador se realiza para determinar si puede convertir los datos. La tercera columna muestra el valor de SQLSTATE devuelto para cada resultado por **SQLExecDirect**, **SQLExecute**, **SQLBulkOperations**, **SQLSetPos**, o **SQLPutData**. Datos se envían al origen de datos solo si se devuelve SQL_SUCCESS.  
  
 Si el *ParameterType* argumento en **SQLBindParameter** contiene el identificador de un tipo de datos SQL de ODBC que no se muestra en la tabla para un determinado tipo de datos de C, **SQLBindParameter**devuelve SQLSTATE 07006 (infracción del atributo de tipo de datos restringido). Si el *ParameterType* argumento contiene un identificador específico del controlador y el controlador no admite la conversión del tipo de datos C de ODBC específico para ese tipo de datos SQL específico del controlador, **SQLBindParameter** devuelve SQLSTATE HYC00 (característica opcional no implementada).  
  
 Si el *ParameterValuePtr* y *StrLen_or_IndPtr* argumentos especificados en **SQLBindParameter** son ambos punteros nulos, que la función devuelve SQLSTATE HY009 (no válido uso del puntero null). Aunque no se muestra en las tablas, una aplicación establece el valor del búfer de longitud/indicador que señala el *StrLen_or_IndPtr* argumento de **SQLBindParameter** o el valor de la  *StrLen_or_IndPtr* argumento de **SQLPutData** en SQL_NULL_DATA para especificar un valor de datos de SQL NULL. (El *StrLen_or_IndPtr* argumento corresponde al campo SQL_DESC_OCTET_LENGTH_PTR de la APD.) La aplicación establece estos valores para SQL_NTS para especificar que el valor de \* *ParameterValuePtr* en **SQLBindParameter** o \* *DataPtr*en **SQLPutData** (indicado por el campo SQL_DESC_DATA_PTR de la APD) es una cadena terminada en null.  
  
 Los siguientes términos se usan en las tablas:  
  
-   **Longitud de bytes de datos** : número de bytes de datos SQL disponibles para que se envíen al origen de datos, si no se truncarán los datos antes de que se envíe al origen de datos. Para los datos de cadena, esto no incluye espacio para el carácter de terminación null.  
  
-   **Longitud de bytes de la columna** : número de bytes necesarios para almacenar los datos en el origen de datos.  
  
-   **Longitud de bytes de caracteres** : número máximo de bytes necesario para mostrar datos en formato de carácter. Se trata como se define para cada tipo de datos SQL en [Mostrar tamaño](../../../odbc/reference/appendixes/display-size.md), excepto en que es de longitud de bytes de caracteres en bytes, mientras que el tamaño de pantalla es en caracteres.  
  
-   **Número de dígitos** : número de caracteres que se utilizan para representar un número, incluido el signo menos, decimal y exponente (si es necesario).  
  
-   **Palabras en**   
     ***italics*** : elementos de la gramática SQL. Para obtener la sintaxis de elementos de la gramática, vea [Apéndice C: SQL gramática](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [C a SQL: caracteres](../../../odbc/reference/appendixes/c-to-sql-character.md)  
  
-   [C a SQL: numérico](../../../odbc/reference/appendixes/c-to-sql-numeric.md)  
  
-   [C a SQL: bits](../../../odbc/reference/appendixes/c-to-sql-bit.md)  
  
-   [C a SQL: binario](../../../odbc/reference/appendixes/c-to-sql-binary.md)  
  
-   [C a SQL: fecha](../../../odbc/reference/appendixes/c-to-sql-date.md)  
  
-   [C a SQL: GUID](../../../odbc/reference/appendixes/c-to-sql-guid.md)  
  
-   [C a SQL: hora](../../../odbc/reference/appendixes/c-to-sql-time.md)  
  
-   [C a SQL: marca de tiempo](../../../odbc/reference/appendixes/c-to-sql-timestamp.md)  
  
-   [C a SQL: intervalos de mes del año](../../../odbc/reference/appendixes/c-to-sql-year-month-intervals.md)  
  
-   [C a SQL: intervalos de tiempo del día](../../../odbc/reference/appendixes/c-to-sql-day-time-intervals.md)  
  
-   [Ejemplos de conversión de datos de C en SQL](../../../odbc/reference/appendixes/c-to-sql-data-conversion-examples.md)
