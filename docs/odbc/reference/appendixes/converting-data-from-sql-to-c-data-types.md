---
title: Convertir datos de SQL a tipos de datos de C | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 553596f474cd8e7c4f4c91911b0167d5b1bc0b4a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224482"
---
# <a name="converting-data-from-sql-to-c-data-types"></a>Convertir datos de SQL a tipos de datos C
Cuando una aplicación llama **SQLFetch**, **SQLFetchScroll**, o **SQLGetData**, el controlador recupera los datos del origen de datos. Si es necesario, convierte los datos del tipo de datos en el que el controlador recupera para el tipo de datos especificado por el *TargetType* argumento en **SQLBindCol** o **SQLGetData.** Por último, almacena los datos en la ubicación señalada por el *TargetValuePtr* argumento en **SQLBindCol** o **SQLGetData** (y el campo SQL_DESC_DATA_PTR de la descartar).  
  
 La siguiente tabla muestra las conversiones compatibles de SQL de ODBC a tipos de datos ODBC C los tipos de datos. Un círculo relleno indica la conversión predeterminada para un tipo de datos SQL (el tipo de datos C a la que los datos se convertirá cuando el valor de *TargetType* es SQL_C_DEFAULT). Un círculo hueco indica una conversión compatible.  
  
 Para una aplicación ODBC 3 *.x* la aplicación funciona con un ODBC 2. *x* controlador, conversión de datos específicos del controlador podrían no admitir tipos.  
  
 El formato de los datos convertidos no se ve afectado por la configuración de país Windows®.  
  
 Las tablas en las secciones siguientes describen cómo el controlador o el origen de datos convierte los datos recuperados del origen de datos; se requieren controladores para admitir las conversiones a todos los tipos de datos C de ODBC de los tipos de datos SQL de ODBC que admiten. Para un tipo determinado de datos SQL de ODBC, la primera columna de la tabla enumera los valores de entrada válidos de la *TargetType* argumento en **SQLBindCol** y **SQLGetData**. La segunda columna muestra los resultados de una prueba, a menudo mediante el *BufferLength* argumento especificado en **SQLBindCol** o **SQLGetData**, que lleva a cabo en el controlador determinar si pueden convertir los datos. Para cada resultado, las columnas de la terceros y cuarta lista de los valores situados en los búferes especificados por el *TargetValuePtr* y *StrLen_or_IndPtr* argumentos especificados en **SQLBindCol** o **SQLGetData** después de que el controlador ha intentado convertir los datos. (El *StrLen_or_IndPtr* argumento corresponde al campo de la descartar SQL_DESC_OCTET_LENGTH_PTR.) La última columna muestra el valor de SQLSTATE devuelto para cada resultado por **SQLFetch**, **SQLFetchScroll**, o **SQLGetData**.  
  
 Si el *TargetType* argumento en **SQLBindCol** o **SQLGetData** contiene un identificador para un tipo de datos C de ODBC no se muestra en la tabla para un tipo determinado de datos SQL de ODBC,  **SQLFetch**, **SQLFetchScroll**, o **SQLGetData** devuelve SQLSTATE 07006 (infracción del atributo de tipo de datos restringido). Si el *TargetType* argumento contiene un identificador que especifica una conversión de un tipo de datos específicos del controlador SQL para un tipo de datos ODBC C y esta conversión no es compatible con el controlador, **SQLFetch**, **SQLFetchScroll**, o **SQLGetData** devuelve SQLSTATE HYC00 (característica opcional no implementada).  
  
 Aunque no se muestra en las tablas, el controlador devuelve SQL_NULL_DATA en el búfer especificado por el *StrLen_or_IndPtr* argumento cuando el valor de datos SQL es NULL. Para obtener una explicación del uso de *StrLen_or_IndPtr* cuando se realizan varias llamadas para recuperar los datos, vea el [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md)descripción de la función. Cuando los datos SQL se convierten en datos de caracteres de C, el recuento de caracteres se devuelve en \* *StrLen_or_IndPtr* no incluye los bytes de terminación null. Si *TargetValuePtr* es un puntero nulo, **SQLGetData** devuelve SQLSTATE HY009 (uso no válido del puntero null); en **SQLBindCol**, esto desenlaza la columna.  
  
 En las tablas se utilizan los siguientes términos y convenciones:  
  
-   **Longitud de bytes de datos** es el número de bytes de datos de C disponibles para devolver en **TargetValuePtr*, o no se truncarán los datos antes de devolverlos a la aplicación. Para los datos de cadena, esto no incluye el espacio para el carácter de terminación null.  
  
-   **Longitud de bytes de caracteres** es el número total de bytes necesarios para mostrar los datos en formato de caracteres. Esto es como se define para cada tipo de datos C en la sección [Mostrar tamaño](../../../odbc/reference/appendixes/display-size.md), salvo que la longitud de bytes del carácter está en bytes, mientras que el tamaño de pantalla es en caracteres.  
  
-   Es decir, en *cursiva* representan los argumentos de función o elementos de la gramática de SQL. Para obtener la sintaxis de elementos de gramática, consulte [Apéndice C: Gramática de SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [SQL a C: Carácter](../../../odbc/reference/appendixes/sql-to-c-character.md)  
  
-   [SQL a C: Numérico](../../../odbc/reference/appendixes/sql-to-c-numeric.md)  
  
-   [SQL a C: Bit](../../../odbc/reference/appendixes/sql-to-c-bit.md)  
  
-   [SQL a C: archivo binario](../../../odbc/reference/appendixes/sql-to-c-binary.md)  
  
-   [SQL a C: Fecha](../../../odbc/reference/appendixes/sql-to-c-date.md)  
  
-   [SQL a C: GUID](../../../odbc/reference/appendixes/sql-to-c-guid.md)  
  
-   [SQL a C: Tiempo](../../../odbc/reference/appendixes/sql-to-c-time.md)  
  
-   [SQL a C: marca de tiempo](../../../odbc/reference/appendixes/sql-to-c-timestamp.md)  
  
-   [SQL a C: Intervalos de mes del año](../../../odbc/reference/appendixes/sql-to-c-year-month-intervals.md)  
  
-   [SQL a C: Intervalos de tiempo del día](../../../odbc/reference/appendixes/sql-to-c-day-time-intervals.md)  
  
-   [SQL a los ejemplos de conversión de datos de C](../../../odbc/reference/appendixes/sql-to-c-data-conversion-examples.md)
