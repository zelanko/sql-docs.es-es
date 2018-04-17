---
title: Tipos de datos SQL | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL data types [ODBC]
- SQL data types [ODBC], about SQL data types
- data types [ODBC], SQL data types
ms.assetid: 1b22f985-f5e4-4779-87eb-e43329a442b1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 2c1bb7ad5ce2523f4ee4e5404608e1359b216178
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sql-data-types"></a>Tipos de datos SQL
Cada DBMS define sus propios tipos SQL. Cada controlador ODBC expone solo esos tipos de datos SQL que define el DBMS asociado. Obtener información acerca de cómo se asigna un controlador de DBMS SQL tipos a los identificadores de tipo SQL definidas por ODBC y cómo asigna un controlador de tipos de DBMS SQL a sus propios identificadores de tipo específicos del controlador SQL se devuelve a través de una llamada a **SQLGetTypeInfo**. Un controlador también devuelve los tipos de datos SQL para describir los tipos de datos de columnas y parámetros a través de llamadas a **SQLColAttribute**, **SQLColumns**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLProcedureColumns**, y **SQLSpecialColumns**.  
  
> [!NOTE]  
>  Los tipos de datos SQL se encuentran en los campos SQL_DESC_ CONCISE_TYPE, SQL_DESC_TYPE y SQL_DESC_DATETIME_INTERVAL_CODE de los descriptores de implementación. Características de los tipos de datos SQL se encuentran en los campos SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_LENGTH y SQL_DESC_OCTET_LENGTH de los descriptores de implementación. Para obtener más información, consulte [identificadores de tipo de datos y los descriptores de](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) más adelante en este apéndice.  
  
 Un origen de datos y el controlador determinado no admiten necesariamente todos los tipos de datos SQL que se definen en este apéndice. Compatibilidad del controlador para tipos de datos SQL depende del nivel de SQL-92 que cumple el controlador. Para determinar el nivel de gramática de SQL-92 compatible con el controlador, una aplicación llama **SQLGetInfo** con el tipo de información de SQL_SQL_CONFORMANCE. Además, un determinado controlador y origen de datos puede admitir tipos de datos SQL adicionales, específicos del controlador. Para determinar qué tipos de datos un controlador admite, llama a una aplicación **SQLGetTypeInfo**. Para obtener información acerca de los tipos de datos SQL específico del controlador, consulte la documentación del controlador. Para obtener información acerca de los tipos de datos en un origen de datos específico, consulte la documentación de ese origen de datos.  
  
> [!IMPORTANT]  
>  Las tablas a lo largo de este apéndice son sólo directrices y mostrar suelen usar los nombres, intervalos y límites de tipos de datos SQL. Un origen de datos determinado puede admitir solo algunas de los tipos de datos enumerados y las características de los tipos de datos admitidos pueden diferir de los que aparecen.  
  
 La tabla siguiente enumera los identificadores de tipo SQL válidos para todos los tipos de datos SQL. La tabla también muestra el nombre y la descripción del tipo de datos correspondiente de SQL-92 (si existe).  
  
|Identificador de tipo SQL [1]|Típico de los datos de SQL<br /><br /> tipo [2]|Descripción del tipo típico|  
|------------------------------|------------------------------------|------------------------------|  
|SQL_CHAR|CHAR (*n*)|Cadena de longitud fija la cadena de caracteres *n*.|  
|SQL_VARCHAR|VARCHAR (*n*)|Cadena de caracteres de longitud variable con una longitud máxima de la cadena *n*.|  
|SQL_LONGVARCHAR|LONG VARCHAR|Datos de caracteres de longitud variable. Longitud máxima es depende del origen de datos. [9]|  
|SQL_WCHAR|WCHAR (*n*)|Cadena de caracteres Unicode de longitud de cadena fija *n*|  
|SQL_WVARCHAR|VARWCHAR (*n*)|Cadena de caracteres de longitud variable de Unicode con una longitud máxima de la cadena *n*|  
|SQL_WLONGVARCHAR|LONGWVARCHAR|Datos Unicode de caracteres de longitud variable. Longitud máxima es de – depende del origen de datos|  
|SQL_DECIMAL|DECIMAL (*p*,*s*)|Firmado, valor numérico exacto con una precisión de al menos *p* y escala *s.* (La precisión máxima es definido por el controlador). (1 < = *p* < = 15; *s* <= *p*). [ 4]|  
|SQL_NUMERIC|NUMÉRICO (*p*,*s*)|Firmado, valor numérico exacto con una precisión *p* y escala *s* (1 < = *p* < = 15; *s* <= *p*). [ 4]|  
|SQL_SMALLINT|SMALLINT|Valor numérico exacto con precisión 5 y escala 0 (firmado: -32.768 < = *n* < = 32.767, sin signo: 0 < = *n* < = 65.535) [3].|  
_INTEGER|INTEGER|Valor numérico exacto con precisión 10 y escala 0 (firmado: – 2 [31] < = *n* < = 2 [31] – 1, sin signo: 0 < = *n* < = 2 [32] – 1) [3].|  
|SQL_REAL|REAL|Valor con signo, aproximado, numeric con una precisión binaria de 24 (cero o valor absoluto 10 [– 38] para 10[38]).|  
|SQL_FLOAT|FLOAT (*p*)|Valor con signo, aproximado, numeric con una precisión binaria de al menos *p*. (La precisión máxima es definido por el controlador). [5]|  
|SQL_DOUBLE|DOUBLE PRECISION|Valor con signo, aproximado, numeric con una precisión binaria de 53 (cero o valor absoluto entre 10 [–308] y 10[308]).|  
|SQL_BIT|BIT|Datos binarios de bit único. [8]|  
|SQL_TINYINT|TINYINT|Valor numérico exacto con precisión 3 y escala 0 (firmado: – 128 < = *n* < = 127, sin signo: 0 < = *n* < = 255) [3].|  
_BIGINT|bigint|Exacto valor numérico con precisión 19 (si tiene signo) o 20 (si sin signo) y escala 0 (firmado: – 2 [63] < = *n* < = 2 [63] – 1, sin signo: 0 < = *n* < = 2 [64] – 1) [3], [9].|  
|SQL_BINARY|BINARIO (*n*)|Datos binarios de longitud fija *n*. [ 9]|  
|SQL_VARBINARY|VARBINARY (*n*)|Datos binarios de longitud variable de longitud máxima *n*. El máximo establecido por el usuario. [9]|  
|SQL_LONGVARBINARY|VARBINARY LARGO|Datos binarios de longitud variable. Longitud máxima es depende del origen de datos. [9]|  
|SQL_TYPE_DATE [6]|DATE|Año, mes y día campos, conforme a las reglas del calendario gregoriano. (Consulte [restricciones del calendario gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md), más adelante en este apéndice.)|  
|SQL_TYPE_TIME [6]|TIEMPO (*p*)|Hora, minuto y segundo campos, con los valores válidos para horas de 00 a 23, los valores válidos de minutos de 00 a 59 y los valores válidos de segundos de 00 a 61. Precisión *p* indica la precisión de segundos.|  
|SQL_TYPE_TIMESTAMP [6]|Marca de tiempo (*p*)|Año, mes, día, hora, minuto y segundo campos, con los valores válidos según se define para los tipos de datos de fecha y hora.|  
_TYPE_UTCDATETIME|UTCDATETIME|Campos de año, mes, día, hora, minuto, segundo, utchour y utcminute. Los campos utchour y utcminute tienen precisión de 1/10 microsegundos.|  
|SQL_TYPE_UTCTIME|UTCTIME|Campos de hora, minuto, segundo, utchour y utcminute. Los campos utchour y utcminute con precisión de 1/10 microsegundos...|  
|SQL_INTERVAL_MONTH [7]|MES de intervalo (*p*)|Número de meses entre dos fechas; *p* es el intervalo de precisión del principio.|  
|SQL_INTERVAL_YEAR [7]|AÑO de intervalo (*p*)|Número de años entre dos fechas; *p* es el intervalo de precisión del principio.|  
|SQL_INTERVAL_YEAR_TO_MONTH [7]|AÑO de intervalo (*p*) al mes|Número de años y meses entre dos fechas; *p* es el intervalo de precisión del principio.|  
|SQL_INTERVAL_DAY [7]|DÍAS de intervalo (*p*)|Número de días entre dos fechas; *p* es el intervalo de precisión del principio.|  
|SQL_INTERVAL_HOUR [7]|HORA de intervalo (*p*)|Número de horas entre dos fechas/horas; *p* es el intervalo de precisión del principio.|  
|SQL_INTERVAL_MINUTE [7]|MINUTO de intervalo (*p*)|Número de minutos entre dos fechas/horas; *p* es el intervalo de precisión del principio.|  
|SQL_INTERVAL_SECOND [7]|INTERVALO de segundo (*p*,*preguntas*)|Número de segundos entre dos fechas/horas; *p* es el intervalo de precisión del principio y *preguntas* es la precisión de segundos del intervalo.|  
_INTERVAL_DAY_TO_HOUR [7]|DÍAS de intervalo (*p*) a la hora|Número de días/horas entre dos fechas/horas; *p* es el intervalo de precisión del principio.|  
|SQL_INTERVAL_DAY_TO_MINUTE [7]|DÍAS de intervalo (*p*) minuto|Número de días, horas o minutos entre dos fechas/horas; *p* es el intervalo de precisión del principio.|  
|SQL_INTERVAL_DAY_TO_SECOND [7]|INTERVAL DAY (*p*) al segundo (*preguntas*)|Número de días/horas/minutos/segundos entre dos fechas/horas; *p* es el intervalo de precisión del principio y *preguntas* es la precisión de segundos del intervalo.|  
|SQL_INTERVAL_HOUR_TO_MINUTE [7]|HORA de intervalo (*p*) minuto|Número de horas o minutos entre dos fechas/horas; *p* es el intervalo de precisión del principio.|  
|SQL_INTERVAL_HOUR_TO_SECOND [7]|HORA de intervalo (*p*) al segundo (*preguntas*)|Número de horas, minutos y segundos entre dos fechas/horas; *p* es el intervalo de precisión del principio y *preguntas* es la precisión de segundos del intervalo.|  
_INTERVAL_MINUTE_TO_SECOND [7]|MINUTO de intervalo (*p*) al segundo (*preguntas*)|Número de minutos/segundos entre dos fechas/horas; *p* es el intervalo de precisión del principio y *preguntas* es la precisión de segundos del intervalo.|  
|SQL_GUID|GUID|GUID de longitud fija.|  
  
 [1] es el valor devuelto en la columna DATA_TYPE mediante una llamada a **SQLGetTypeInfo**.  
  
 [2] es el valor devuelto en la columna nombre y crear parámetros mediante una llamada a **SQLGetTypeInfo**. La columna nombre devuelve la designación: por ejemplo, CHAR, mientras que la columna crear PARAMS devuelve una lista separada por comas de los parámetros de creación como la precisión, escala y longitud.  
  
 [3] en una aplicación usa **SQLGetTypeInfo** o **SQLColAttribute** para determinar si un tipo de datos determinado o una columna en particular en un conjunto de resultados es sin signo.  
  
 [4] tipos de datos SQL_DECIMAL de ODBC y SQL_NUMERIC solo difieren en su precisión. La precisión de un DECIMAL (*p*,*s*) es una precisión decimal definido por la implementación que es no menos de *p*, mientras que la precisión de un valor numérico (*p* ,*s*) es exactamente igual que *p*.  
  
 [5] en función de la implementación, puede ser la precisión de SQL_FLOAT 24 o 53: si es 24, el tipo de datos SQL_FLOAT es el mismo que SQL_REAL; Si es 53, el tipo de datos SQL_FLOAT es el mismo que SQL_DOUBLE.  
  
 [6] en ODBC 3*.x*, los tipos de datos de fecha, hora y marca de tiempo SQL son SQL_TYPE_DATE, SQL_TYPE_TIME y SQL_TYPE_TIMESTAMP, respectivamente; en ODBC 2. *x*, los tipos de datos son SQL_DATE, SQL_TIME y SQL_TIMESTAMP.  
  
 [7] para obtener más información acerca de los tipos de datos SQL de intervalo, consulte el [tipos de datos Interval](../../../odbc/reference/appendixes/interval-data-types.md) sección, más adelante en este apéndice.  
  
 [8], el tipo de datos SQL_BIT tiene características diferentes de las que el tipo de BIT en SQL-92.  
  
 [9] este tipo de datos no tiene ningún tipo de datos correspondiente en SQL-92.  
  
 Esta sección proporciona en el ejemplo siguiente.  
  
-   [Conjunto de resultados de SQLGetTypeInfo de ejemplo](../../../odbc/reference/appendixes/example-sqlgettypeinfo-result-set.md)
