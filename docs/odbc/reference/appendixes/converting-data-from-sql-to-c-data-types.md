---
title: Convertir datos de SQL a tipos de datos C | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data conversions from SQL to C types [ODBC]
- data conversions from SQL to C types [ODBC], about converting
- data types [ODBC], C data types
- data types [ODBC], converting data
- data types [ODBC], SQL data types
- SQL data types [ODBC], converting to C types
- converting data from SQL to c types [ODBC]
- converting data from SQL to c types [ODBC], about converting
- C data types [ODBC], converting from SQL types
ms.assetid: 029727f6-d3f0-499a-911c-bcaf9714e43b
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0fef5a663ecbb3ec1f162dcf453691f04183d732
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="converting-data-from-sql-to-c-data-types"></a>Convertir datos de SQL a tipos de datos C
Cuando una aplicación llama **SQLFetch**, **SQLFetchScroll**, o **SQLGetData**, el controlador recupera los datos del origen de datos. Si es necesario, convierte los datos del tipo de datos en el que el controlador recuperado para el tipo de datos especificado por la *TargetType* argumento en **SQLBindCol** o **SQLGetData.** Por último, almacena los datos en la ubicación señalada por la *TargetValuePtr* argumento en **SQLBindCol** o **SQLGetData** (y el campo SQL_DESC_DATA_PTR de la descartar).  
  
 En la tabla siguiente muestra las conversiones no admitidas de SQL de ODBC tipos de datos a tipos de datos C de ODBC. Un círculo relleno indica la conversión de valor predeterminado para un tipo de datos SQL (el tipo de datos C a la que los datos se convertirá cuando el valor de *TargetType* es SQL_C_DEFAULT). Un círculo vacío indica una conversión compatible.  
  
 Para una aplicación ODBC 3*.x* aplicación trabajar con una API ODBC 2. *x* controlador, conversión de datos específico del controlador podrían no admitir tipos.  
  
 El formato de los datos convertidos no se ve afectado por el valor de país Windows®.  
  
 Las tablas en las secciones siguientes describe cómo el controlador o el origen de datos convierte los datos recuperados del origen de datos; se requieren controladores para admitir las conversiones a todos los tipos de datos C de ODBC de los tipos de datos SQL de ODBC que admite. Para un tipo determinado de datos SQL de ODBC, la primera columna de la tabla enumera los valores de entrada válidos de la *TargetType* argumento en **SQLBindCol** y **SQLGetData**. La segunda columna muestra los resultados de una prueba, a menudo usando el *BufferLength* argumento especificado en **SQLBindCol** o **SQLGetData**, que lleva a cabo en el controlador determinar si pueden convertir los datos. Para cada resultado, las columnas terceros y cuarta enumeran los valores que se coloca en los búferes especificados por el *TargetValuePtr* y *StrLen_or_IndPtr* argumentos especificados en **SQLBindCol** o **SQLGetData** después de que el controlador ha intentado convertir los datos. (El *StrLen_or_IndPtr* argumento corresponde al campo de la descartar SQL_DESC_OCTET_LENGTH_PTR.) La última columna muestra el valor de SQLSTATE devuelto para cada resultado por **SQLFetch**, **SQLFetchScroll**, o **SQLGetData**.  
  
 Si el *TargetType* argumento en **SQLBindCol** o **SQLGetData** contiene un identificador para un tipo de datos C de ODBC no se muestra en la tabla para un tipo determinado de datos SQL de ODBC,  **SQLFetch**, **SQLFetchScroll**, o **SQLGetData** devuelve SQLSTATE 07006 (infracción del atributo de tipo de datos restringido). Si el *TargetType* argumento contiene un identificador que especifica una conversión de un tipo de datos específicos del controlador SQL para un tipo de datos C de ODBC y el controlador no admite esta conversión **SQLFetch**, **SQLFetchScroll**, o **SQLGetData** devuelve SQLSTATE HYC00 (característica opcional no implementada).  
  
 Aunque no se muestra en las tablas, el controlador devuelve SQL_NULL_DATA en el búfer especificado por el *StrLen_or_IndPtr* argumento cuando el valor de datos SQL es NULL. Para obtener una explicación del uso de *StrLen_or_IndPtr* cuando se realizan varias llamadas para recuperar los datos, vea el [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)descripción de la función. Cuando los datos SQL se convierten en datos de caracteres C, el número de caracteres devuelto en \* *StrLen_or_IndPtr* no incluye los bytes de terminación null. Si *TargetValuePtr* es un puntero nulo, **SQLGetData** devuelve SQLSTATE HY009 (uso no válido del puntero null); en **SQLBindCol**, este modo desenlaza la columna.  
  
 En las tablas se utilizan los siguientes términos y convenciones:  
  
-   **Longitud de bytes de datos** es el número de bytes de datos de C disponibles para devolver en **TargetValuePtr*, si no se truncarán los datos antes de que se devuelva a la aplicación. Para los datos de cadena, esto no incluye el espacio para el carácter de terminación null.  
  
-   **Longitud de bytes de caracteres** es el número total de bytes necesarios para mostrar los datos en el formato de caracteres. Se trata como se define para cada tipo de datos C en la sección [Mostrar tamaño](../../../odbc/reference/appendixes/display-size.md), salvo que la longitud de bytes de caracteres se muestra en bytes, mientras que el tamaño de pantalla es en caracteres.  
  
-   Palabras en *cursiva* representan los argumentos de función o elementos de la gramática SQL. Para obtener la sintaxis de elementos de la gramática, vea [Apéndice C: SQL gramática](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [SQL a C: caracteres](../../../odbc/reference/appendixes/sql-to-c-character.md)  
  
-   [SQL a C: numérico](../../../odbc/reference/appendixes/sql-to-c-numeric.md)  
  
-   [SQL a C: bit](../../../odbc/reference/appendixes/sql-to-c-bit.md)  
  
-   [SQL a C: binario](../../../odbc/reference/appendixes/sql-to-c-binary.md)  
  
-   [SQL a C: fecha](../../../odbc/reference/appendixes/sql-to-c-date.md)  
  
-   [SQL a C: GUID](../../../odbc/reference/appendixes/sql-to-c-guid.md)  
  
-   [SQL a C: hora](../../../odbc/reference/appendixes/sql-to-c-time.md)  
  
-   [SQL a C: marca de tiempo](../../../odbc/reference/appendixes/sql-to-c-timestamp.md)  
  
-   [SQL a C: intervalos de año y mes](../../../odbc/reference/appendixes/sql-to-c-year-month-intervals.md)  
  
-   [SQL a C: intervalos de día y hora](../../../odbc/reference/appendixes/sql-to-c-day-time-intervals.md)  
  
-   [SQL a los ejemplos de conversión de datos de C](../../../odbc/reference/appendixes/sql-to-c-data-conversion-examples.md)
