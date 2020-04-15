---
title: Conversión de datos de SQL a tipos de datos de C ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1a10730cb3910c55679c264583801cd57c83bfc3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284755"
---
# <a name="converting-data-from-sql-to-c-data-types"></a>Convertir datos de SQL a tipos de datos C
Cuando una aplicación llama a **SQLFetch**, **SQLFetchScroll**o **SQLGetData**, el controlador recupera los datos del origen de datos. Si es necesario, convierte los datos del tipo de datos en el que el controlador los recuperó al tipo de datos especificado por el *TargetType* argumento en **SQLBindCol** o **SQLGetData.** Por último, almacena los datos en la ubicación señalada por el *TargetValuePtr* argumento en **SQLBindCol** o **SQLGetData** (y el SQL_DESC_DATA_PTR campo de la ARD).  
  
 En la tabla siguiente se muestran las conversiones admitidas de tipos de datos SQL ODBC a tipos de datos ODBC C. Un círculo rellenado indica la conversión predeterminada para un tipo de datos SQL (el tipo de datos C al que se convertirán los datos cuando se SQL_C_DEFAULT el valor de *TargetType).* Un círculo hueco indica una conversión admitida.  
  
 Para una aplicación ODBC *3.x* que trabaja con un controlador ODBC *2.x,* es posible que no se admita la conversión de tipos de datos específicos del controlador.  
  
 El formato de los datos convertidos no se ve afectado por la configuración de país ® Windows.  
  
 Las tablas de las secciones siguientes describen cómo el controlador o el origen de datos convierte los datos recuperados del origen de datos; Los controladores son necesarios para admitir conversiones a todos los tipos de datos ODBC C de los tipos de datos SQL ODBC que admiten. Para un tipo de datos SQL ODBC determinado, la primera columna de la tabla enumera los valores de entrada legales del argumento *TargetType* en **SQLBindCol** y **SQLGetData**. La segunda columna enumera los resultados de una prueba, a menudo mediante el *BufferLength* argumento especificado en **SQLBindCol** o **SQLGetData**, que el controlador realiza para determinar si puede convertir los datos. Para cada resultado, la tercera y cuarta columnas enumeran los valores colocados en los búferes especificados por el *TargetValuePtr* y *StrLen_or_IndPtr* argumentos especificados en **SQLBindCol** o **SQLGetData** después de que el controlador ha intentado convertir los datos. (El argumento *StrLen_or_IndPtr* corresponde al campo SQL_DESC_OCTET_LENGTH_PTR de la ARD.) La última columna enumera el SQLSTATE devuelto para cada resultado por **SQLFetch**, **SQLFetchScroll**o **SQLGetData**.  
  
 Si el *TargetType* argumento en **SQLBindCol** o **SQLGetData** contiene un identificador para un tipo de datos ODBC C no se muestra en la tabla para un tipo de datos SQL ODBC determinado, **SQLFetch**, **SQLFetchScroll**o **SQLGetData** devuelve SQLSTATE 07006 (infracción de atributo de tipo de datos restringido). Si el *TargetType* argumento contiene un identificador que especifica una conversión de un tipo de datos SQL específico del controlador a un tipo de datos ODBC C y esta conversión no es compatible con el controlador, **SQLFetch**, **SQLFetchScroll**, o **SQLGetData** devuelve SQLSTATE HYC00 (característica opcional no implementada).  
  
 Aunque no se muestra en las tablas, el controlador devuelve SQL_NULL_DATA en el búfer especificado por el *StrLen_or_IndPtr* argumento cuando el valor de datos SQL es NULL. Para obtener una explicación del uso de *StrLen_or_IndPtr* cuando se realizan varias llamadas para recuperar datos, vea la descripción de la función [SQLGetData.](../../../odbc/reference/syntax/sqlgetdata-function.md) Cuando los datos SQL se convierten en \*datos de caracteres C, el recuento de caracteres devuelto en *StrLen_or_IndPtr* no incluye el byte de terminación nula. Si *TargetValuePtr* es un puntero nulo, **SQLGetData** devuelve SQLSTATE HY009 (uso no válido del puntero nulo); en **SQLBindCol**, esto desenlaza la columna.  
  
 En las tablas se utilizan los siguientes términos y convenciones:  
  
-   **La longitud de bytes de datos** es el número de bytes de datos de C disponibles para devolver en **TargetValuePtr*, independientemente de si los datos se truncarán antes de que se devuelvan a la aplicación. Para los datos de cadena, esto no incluye el espacio para el carácter de terminación nula.  
  
-   La longitud de bytes de **caracteres** es el número total de bytes necesarios para mostrar los datos en formato de caracteres. Esto es como se define para cada tipo de datos C en la sección Tamaño de [visualización](../../../odbc/reference/appendixes/display-size.md), excepto que la longitud de byte de caracteres está en bytes mientras el tamaño de visualización está en caracteres.  
  
-   Las *palabras* en cursiva representan argumentos de función o elementos de la gramática SQL. Para obtener la sintaxis de los elementos gramaticales, vea [Apéndice C: Gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [SQL a C: Carácter](../../../odbc/reference/appendixes/sql-to-c-character.md)  
  
-   [SQL a C: Numeric](../../../odbc/reference/appendixes/sql-to-c-numeric.md)  
  
-   [SQL a C: bit](../../../odbc/reference/appendixes/sql-to-c-bit.md)  
  
-   [SQL a C: Binary](../../../odbc/reference/appendixes/sql-to-c-binary.md)  
  
-   [SQL a C: Date](../../../odbc/reference/appendixes/sql-to-c-date.md)  
  
-   [SQL a C: GUID](../../../odbc/reference/appendixes/sql-to-c-guid.md)  
  
-   [SQL a C: Time](../../../odbc/reference/appendixes/sql-to-c-time.md)  
  
-   [SQL a C: Timestamp](../../../odbc/reference/appendixes/sql-to-c-timestamp.md)  
  
-   [SQL a C: Intervalos de mes y año](../../../odbc/reference/appendixes/sql-to-c-year-month-intervals.md)  
  
-   [SQL a C: Intervalos de día y hora](../../../odbc/reference/appendixes/sql-to-c-day-time-intervals.md)  
  
-   [SQL a los ejemplos de conversión de datos de C](../../../odbc/reference/appendixes/sql-to-c-data-conversion-examples.md)
