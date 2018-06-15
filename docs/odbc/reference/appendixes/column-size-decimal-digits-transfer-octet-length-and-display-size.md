---
title: Tamaño de la columna, dígitos decimales, longitud de bytes de transferencia, el tamaño de presentación | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- display size of data types [ODBC]
- data types [ODBC], column size
- transfer octet length of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- decimal digits of data types [ODBC]
- data types [ODBC], decimal digits
- SQL data types [ODBC], column characteristics
- column size of data types [ODBC]
- data types [ODBC], transfer octet length
ms.assetid: 723107a1-be08-4ea3-a8c0-b2c45d38d1aa
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f4a63c37dae0e8cbb06f00f5d043576028dd0508
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32907770"
---
# <a name="column-size-decimal-digits-transfer-octet-length-and-display-size---odbc"></a>Tamaño de la columna, dígitos decimales, transferir la longitud en octetos y mostrar tamaño - ODBC
Tipos de datos se caracterizan por su tamaño de columna (o parámetro), dígitos decimales, longitud y tamaño de presentación. Las siguientes funciones ODBC devuelven estos atributos para un parámetro en una instrucción SQL o para un tipo de datos SQL en un origen de datos. Cada función ODBC devuelve un conjunto diferente de estos atributos, como se indica a continuación:  
  
-   **SQLDescribeCol** devuelve dígitos decimales y tamaño de las columnas se describe de la columna.  
  
-   **SQLDescribeParam** devuelve el parámetro de dígitos decimales y tamaño de los parámetros se describen. **SQLBindParameter** establece el parámetro de dígitos decimales y tamaño para un parámetro en una instrucción SQL.  
  
-   Las funciones de catálogo **SQLColumns**, **SQLProcedureColumns**, y **SQLGetTypeInfo** devolver atributos para una columna en una tabla, conjunto de resultados o un parámetro de procedimiento y los atributos de catálogo de los tipos de datos del origen de datos. **SQLColumns** devuelve el tamaño de la columna, dígitos decimales y longitud de una columna en las tablas especificadas (por ejemplo, la tabla base, vista o una tabla del sistema). **SQLProcedureColumns** devuelve el tamaño de la columna, dígitos decimales y longitud de una columna en un procedimiento. **SQLGetTypeInfo** devuelve el tamaño máximo de las columnas y los dígitos decimales de mínimos y máximo de un tipo de datos SQL en un origen de datos.  
  
 Los valores devueltos por estas funciones para la columna o el tamaño del parámetro que se corresponde con "precisión" como definido en ODBC 2. *x*. Sin embargo, los valores no corresponden necesariamente a los valores devueltos en SQL_DESC_PRECISION o cualquier otro campo descriptor uno. Lo mismo puede decirse de dígitos decimales, que se corresponden con "escala" como definidas en ODBC 2. *x*. No se corresponde necesariamente con los valores devueltos en SQL_DESC_SCALE o cualquier otro campo descriptor uno, pero proceden de campos de descriptor diferentes según el tipo de datos. Para obtener más información, consulte [tamaño de la columna](../../../odbc/reference/appendixes/column-size.md) y [dígitos decimales](../../../odbc/reference/appendixes/decimal-digits.md).  
  
 De igual forma, los valores de longitud de bytes de transferencia no proceden de SQL_DESC_LENGTH. Provienen de la SQL_DESC_OCTET_LENGTH de un campo de un descriptor para todos los tipos de caracteres y binarios. No hay ningún campo de descriptor que contiene esta información para otros tipos.  
  
 El valor de tamaño de presentación para todos los tipos de datos corresponde al valor de un campo de descriptor único, SQL_DESC_DISPLAY_SIZE.  
  
 Campos de descriptor describen las características de un conjunto de resultados. Campos de descriptor no contienen valores válidos acerca de los datos antes de ejecutar la instrucción. Los valores de columna, dígitos decimales, visualización y el tamaño devuelto por el tamaño **SQLColumns**, **SQLProcedureColumns**, y **SQLGetTypeInfo**por otra parte, devolver características de los objetos de base de datos, como columnas de la tabla y tipos de datos, que se encuentren en el catálogo del origen de datos. Del mismo modo, en su conjunto de resultados, **SQLColAttribute** devuelve el tamaño de la columna, dígitos decimales y longitud de bytes de transferencia de las columnas del origen de datos; estos valores no son necesariamente el mismo que los valores de la SQL_DESC_PRECISION, SQL_ DESC_SCALE y campos de descriptor SQL_DESC_OCTET_LENGTH.  
  
 Para obtener más información acerca de estos campos de descriptor, consulte [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Temas relacionados:  
  
-   [Tamaño de columna](../../../odbc/reference/appendixes/column-size.md)  
-   [Dígitos decimales](../../../odbc/reference/appendixes/decimal-digits.md)  
-   [Transferir la longitud en octetos](../../../odbc/reference/appendixes/transfer-octet-length.md)  
-   [Tamaño de presentación](../../../odbc/reference/appendixes/display-size.md)
