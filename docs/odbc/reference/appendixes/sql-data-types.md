---
title: Tipos de datos SQL (SQL Data Types) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC]
- SQL data types [ODBC], about SQL data types
- data types [ODBC], SQL data types
ms.assetid: 1b22f985-f5e4-4779-87eb-e43329a442b1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3cc91213533aa39f30be1bc838cc014c20e70884
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305009"
---
# <a name="sql-data-types"></a>Tipos de datos SQL
Cada DBMS define sus propios tipos SQL. Cada controlador ODBC expone solo los tipos de datos SQL que define el DBMS asociado. La información sobre cómo un controlador asigna los tipos SQL de DBMS a los identificadores de tipo SQL definidos por ODBC y cómo un controlador asigna tipos SQL de DBMS a sus propios identificadores de tipo SQL específicos del controlador se devuelve mediante una llamada a **SQLGetTypeInfo**. Un controlador también devuelve los tipos de datos SQL al describir los tipos de datos de columnas y parámetros a través de llamadas a **SQLColAttribute**, **SQLColumns**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLProcedureColumns**y **SQLSpecialColumns**.  
  
> [!NOTE]  
>  Los tipos de datos SQL se encuentran en los campos SQL_DESC_ CONCISE_TYPE, SQL_DESC_TYPE y SQL_DESC_DATETIME_INTERVAL_CODE de los descriptores de implementación. Las características de los tipos de datos SQL se encuentran en los campos SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_LENGTH y SQL_DESC_OCTET_LENGTH de los descriptores de implementación. Para obtener más información, vea [Identificadores y descriptores](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) de tipo de datos más adelante en este apéndice.  
  
 Un controlador y un origen de datos determinados no admiten necesariamente todos los tipos de datos SQL definidos en este apéndice. La compatibilidad de un controlador con tipos de datos SQL depende del nivel de SQL-92 que cumpla el controlador. Para determinar el nivel de gramática SQL-92 admitido por el controlador, una aplicación llama a **SQLGetInfo** con el tipo de información SQL_SQL_CONFORMANCE. Además, un controlador y un origen de datos determinados pueden admitir tipos de datos SQL adicionales específicos del controlador. Para determinar qué tipos de datos admite un controlador, una aplicación llama a **SQLGetTypeInfo**. Para obtener información acerca de los tipos de datos SQL específicos del controlador, consulte la documentación del controlador. Para obtener información acerca de los tipos de datos de un origen de datos específico, consulte la documentación de ese origen de datos.  
  
> [!IMPORTANT]  
>  Las tablas de este apéndice son solo directrices y muestran los nombres, rangos y límites de tipos de datos SQL que se usan normalmente. Un origen de datos determinado puede admitir solo algunos de los tipos de datos enumerados y las características de los tipos de datos admitidos pueden diferir de las enumeradas.  
  
 En la tabla siguiente se enumeran identificadores de tipo SQL válidos para todos los tipos de datos SQL. La tabla también enumera el nombre y la descripción del tipo de datos correspondiente de SQL-92 (si existe).  
  
|Identificador de tipo SQL[1]|Datos SQL típicos<br /><br /> tipo[2]|Descripción típica del tipo|  
|------------------------------|------------------------------------|------------------------------|  
|SQL_CHAR|CHAR(*n*)|Cadena de caracteres de longitud de cadena fija *n*.|  
|SQL_VARCHAR|VARCHAR(*n*)|Cadena de caracteres de longitud variable con una longitud de cadena máxima *n*.|  
|SQL_LONGVARCHAR|LONG VARCHAR|Datos de caracteres de longitud variable. La longitud máxima depende del origen de datos. [9]|  
|SQL_WCHAR|WCHAR(*n*)|Cadena de caracteres Unicode de longitud de cadena fija *n*|  
|SQL_WVARCHAR|VARWCHAR(*n*)|Cadena de caracteres de longitud variable Unicode con una longitud de cadena máxima *n*|  
|SQL_WLONGVARCHAR|LONGWVARCHAR|Datos de caracteres Unicode de longitud variable. La longitud máxima depende del origen de datos|  
|SQL_DECIMAL|DECIMAL(*p*,*s*)|Valor numérico firmado, exacto, con una precisión de al menos *p* y escala *s.* (La precisión máxima está definida por el conductor.) (1 <*a p* <15; *s* <= *p*). [4]|  
|SQL_NUMERIC|NUMERIC(*p*,*s*)|Valor numérico, exacto y con una precisión *p* y escala *s* (1 <a *p* <a 15; *s* <= *p*). [4]|  
|SQL_SMALLINT|SMALLINT|Valor numérico exacto con precisión 5 y escala 0 (firmado: -32.768 <a *n <* a 32.767, sin signo: 0 <a *n* <a 65.535)[3].|  
|SQL_INTEGER|INTEGER|Valor numérico exacto con precisión 10 y escala 0 (firmado: -2[31] <á *n* <2[31] - 1, sin signo: 0 <n *n* <2[32] - 1)[3].|  
|SQL_REAL|real|Valor numérico firmado, aproximado, con una precisión binaria 24 (valor cero o absoluto 10[-38] a 10[38]).|  
|SQL_FLOAT|FLOAT(*p*)|Valor numérico firmado, aproximado, con una precisión binaria de al menos *p*. (La precisión máxima está definida por el conductor.) [5]|  
|SQL_DOUBLE|DOUBLE PRECISION|Valor numérico firmado, aproximado, con una precisión binaria 53 (valor cero o absoluto 10[-308] a 10[308]).|  
|SQL_BIT|BIT|Datos binarios de un solo bit. [8]|  
|SQL_TINYINT|TINYINT|Valor numérico exacto con precisión 3 y escala 0 (firmado: -128 <a *n* <a 127, sin signo: 0 <a *n n* <a 255)[3].|  
|SQL_BIGINT|bigint|Valor numérico exacto con precisión 19 (si está firmado) o 20 (si no está firmado) y escala 0 (firmada: -2[63] <n *n* <á 2[63] - 1, sin signo: 0 <n *<* 2[64] - 1)[3],[9].|  
|SQL_BINARY|BINARY(*n*)|Datos binarios de longitud fija *n*. [9]|  
|SQL_VARBINARY|VARBINARY(*n*)|Datos binarios de longitud variable de longitud máxima *n*. El usuario establece el máximo. [9]|  
|SQL_LONGVARBINARY|LONG VARBINARY|Datos binarios de longitud variable. La longitud máxima depende del origen de datos. [9]|  
|SQL_TYPE_DATE[6]|DATE|Campos de año, mes y día, conforme a las reglas del calendario gregoriano. (Consulte [Restricciones del calendario gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md), más adelante en este apéndice.)|  
|SQL_TYPE_TIME[6]|TIME(*p*)|Campos de hora, minuto y segundo, con valores válidos para horas de 00 a 23, valores válidos para minutos de 00 a 59 y valores válidos para segundos de 00 a 61. Precisión *p* indica la precisión de los segundos.|  
|SQL_TYPE_TIMESTAMP[6]|TIMESTAMP(*p*)|Campos de año, mes, día, hora, minuto y segundo, con valores válidos definidos para los tipos de datos DATE y TIME.|  
|SQL_TYPE_UTCDATETIME|UTCDATETIME|Campos de año, mes, día, hora, minuto, segundo, utchour y utcminute. Los campos utchour y utcminute tienen una precisión de 1/10 microsegundos.|  
|SQL_TYPE_UTCTIME|UTCTIME|Campos de hora, minuto, segundo, utchour y utcminute. Los campos utchour y utcminute tienen 1/10 de precisión de microsegundos.|  
|SQL_INTERVAL_MONTH[7]|MES DE INTERVALO(*p*)|Número de meses entre dos fechas; *p* es la precisión de interlineado del intervalo.|  
|SQL_INTERVAL_YEAR[7]|INTERVAL YEAR(*p*)|Número de años entre dos fechas; *p* es la precisión de interlineado del intervalo.|  
|SQL_INTERVAL_YEAR_TO_MONTH[7]|INTERVAL YEAR(*p*) A MES|Número de años y meses entre dos fechas; *p* es la precisión de interlineado del intervalo.|  
|SQL_INTERVAL_DAY[7]|DIA DE INTERVALO(*p*)|Número de días entre dos fechas; *p* es la precisión de interlineado del intervalo.|  
|SQL_INTERVAL_HOUR[7]|HORA DE INTERVALO(*p*)|Número de horas entre dos fechas/horas; *p* es la precisión de interlineado del intervalo.|  
|SQL_INTERVAL_MINUTE[7]|MINUTO DE INTERVALO(*p*)|Número de minutos entre dos fechas/horas; *p* es la precisión de interlineado del intervalo.|  
|SQL_INTERVAL_SECOND[7]|INTERVALO SEGUNDO(*p*,*q*)|Número de segundos entre dos fechas/horas; *p* es la precisión inicial del intervalo y *q* es la precisión de los segundos del intervalo.|  
|SQL_INTERVAL_DAY_TO_HOUR[7]|INTERVAL DAY(*p*) TO HOUR|Número de días/horas entre dos fechas/horas; *p* es la precisión de interlineado del intervalo.|  
|SQL_INTERVAL_DAY_TO_MINUTE[7]|INTERVAL DAY(*p*) TO MINUTE|Número de días/horas/minutos entre dos fechas/horas; *p* es la precisión de interlineado del intervalo.|  
|SQL_INTERVAL_DAY_TO_SECOND[7]|INTERVAL DAY(*p*) TO SECOND(*q*)|Número de días/horas/minutos/segundos entre dos fechas/horas; *p* es la precisión inicial del intervalo y *q* es la precisión de los segundos del intervalo.|  
|SQL_INTERVAL_HOUR_TO_MINUTE[7]|INTERVALO HORA(*p*) A MINUTO|Número de horas/minutos entre dos fechas/horas; *p* es la precisión de interlineado del intervalo.|  
|SQL_INTERVAL_HOUR_TO_SECOND[7]|INTERVALO HORA(*p*) A SEGUNDO(*q*)|Número de horas/minutos/segundos entre dos fechas/horas; *p* es la precisión inicial del intervalo y *q* es la precisión de los segundos del intervalo.|  
|SQL_INTERVAL_MINUTE_TO_SECOND[7]|INTERVAL MINUTE(*p*) TO SECOND(*q*)|Número de minutos/segundos entre dos fechas/horas; *p* es la precisión inicial del intervalo y *q* es la precisión de los segundos del intervalo.|  
|SQL_GUID|GUID|GUID de longitud fija.|  
  
 [1] Este es el valor devuelto en la columna DATA_TYPE mediante una llamada a **SQLGetTypeInfo**.  
  
 [2] Este es el valor devuelto en la columna NAME y CREATE PARAMS mediante una llamada a **SQLGetTypeInfo**. La columna NAME devuelve la designación, por ejemplo, CHAR-mientras que la columna CREATE PARAMS devuelve una lista separada por comas de parámetros de creación como precisión, escala y longitud.  
  
 [3] Una aplicación usa **SQLGetTypeInfo** o **SQLColAttribute** para determinar si un tipo de datos determinado o una columna determinada de un conjunto de resultados no está firmado.  
  
 [4] SQL_DECIMAL y SQL_NUMERIC tipos de datos difieren solo en su precisión. La precisión de un DECIMAL(*p*,*s*) es una precisión decimal definida por la implementación que no es menor que *p*, mientras que la precisión de un NUMERIC(*p*,*s*) es exactamente igual a *p*.  
  
 [5] Dependiendo de la implementación, la precisión de SQL_FLOAT puede ser 24 o 53: si es 24, el tipo de datos SQL_FLOAT es el mismo que SQL_REAL; si es 53, el tipo de datos SQL_FLOAT es el mismo que SQL_DOUBLE.  
  
 [6] En ODBC *3.x*, los tipos de datos de fecha, hora y marca de tiempo SQL se SQL_TYPE_DATE, SQL_TYPE_TIME y SQL_TYPE_TIMESTAMP, respectivamente; en ODBC *2.x*, los tipos de datos se SQL_DATE, SQL_TIME y SQL_TIMESTAMP.  
  
 [7] Para obtener más información sobre los tipos de datos SQL de intervalo, consulte la sección Tipos de [datos](../../../odbc/reference/appendixes/interval-data-types.md) de intervalo, más adelante en este apéndice.  
  
 [8] El tipo de datos SQL_BIT tiene características diferentes que el tipo BIT en SQL-92.  
  
 [9] Este tipo de datos no tiene ningún tipo de datos correspondiente en SQL-92.  
  
 En esta sección se proporciona el siguiente ejemplo.  
  
-   [Conjunto de resultados de SQLGetTypeInfo de ejemplo](../../../odbc/reference/appendixes/example-sqlgettypeinfo-result-set.md)
