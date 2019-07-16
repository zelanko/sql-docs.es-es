---
title: Tipos de datos SQL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4be0e017988670d740067011f775f8477037aa18
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057029"
---
# <a name="sql-data-types"></a>Tipos de datos SQL
Cada DBMS define sus propios tipos SQL. Cada controlador ODBC expone solo esos tipos de datos SQL que define el DBMS asociado. Información acerca de cómo se asigna un controlador de DBMS SQL tipos a los identificadores de tipo definido por el ODBC SQL y cómo asigna un controlador de tipos de DBMS SQL a su propio identificadores específicos del controlador de tipo SQL se devuelve a través de una llamada a **SQLGetTypeInfo**. Un controlador también devuelve los tipos de datos SQL al describir los tipos de datos de columnas y parámetros a través de las llamadas a **SQLColAttribute**, **SQLColumns**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLProcedureColumns**, y **SQLSpecialColumns**.  
  
> [!NOTE]  
>  Los tipos de datos SQL están contenidos en los campos SQL_DESC_ CONCISE_TYPE SQL_DESC_TYPE y SQL_DESC_DATETIME_INTERVAL_CODE de los descriptores de implementación. Características de los tipos de datos SQL están contenidas en los campos SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_LENGTH y SQL_DESC_OCTET_LENGTH de los descriptores de implementación. Para obtener más información, consulte [identificadores de tipo de datos y los descriptores de](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) más adelante en este apéndice.  
  
 Un origen de datos y el controlador determinado no admiten necesariamente todos los tipos de datos SQL que se definen en este apéndice. Soporte técnico de un controlador para los tipos de datos SQL depende del nivel de SQL-92 que obedece el controlador. Para determinar el nivel de gramática de SQL-92 compatible con el controlador, una aplicación llama a **SQLGetInfo** con el tipo de información SQL_SQL_CONFORMANCE. Además, un origen de datos y el controlador determinado puede admitir tipos de datos SQL adicionales, específicos del controlador. Para determinar qué tipos de datos un controlador admite, llama una aplicación **SQLGetTypeInfo**. Para obtener información acerca de los tipos de datos SQL específicas del controlador, consulte la documentación del controlador. Para obtener información sobre los tipos de datos en un origen de datos específico, consulte la documentación para ese origen de datos.  
  
> [!IMPORTANT]  
>  Las tablas a lo largo de este apéndice son sólo directrices y mostrar suelen usado nombres, intervalos y los límites de los tipos de datos SQL. Un origen de datos determinado puede admitir solo algunas de los tipos de datos indicados, y las características de los tipos de datos admitidos pueden diferir de los que aparecen.  
  
 En la tabla siguiente se enumera los identificadores de tipo SQL válidos para todos los tipos de datos SQL. La tabla también enumera el nombre y la descripción del tipo de datos correspondiente de SQL-92 (si existe).  
  
|Identificador de tipo SQL [1]|Datos SQL típica<br /><br /> tipo [2]|Descripción del tipo típico|  
|------------------------------|------------------------------------|------------------------------|  
|SQL_CHAR|CHAR(*n*)|Cadena de longitud fija de caracteres *n*.|  
|SQL_VARCHAR|VARCHAR(*n*)|Cadena de caracteres de longitud variable con una longitud máxima de cadena *n*.|  
|SQL_LONGVARCHAR|LONG VARCHAR|Datos de caracteres de longitud variable. Longitud máxima es depende del origen de datos. [9]|  
|SQL_WCHAR|WCHAR(*n*)|Cadena de caracteres Unicode de longitud fija *n*|  
|SQL_WVARCHAR|VARWCHAR(*n*)|Cadena de caracteres de longitud variable de Unicode con una longitud máxima de cadena *n*|  
|SQL_WLONGVARCHAR|LONGWVARCHAR|Datos Unicode de caracteres de longitud variable. Longitud máxima es depende del origen de datos|  
|SQL_DECIMAL|DECIMAL (*p*,*s*)|Valor con signo, numérico, exacto con una precisión de al menos *p* y escala *s.* (La precisión máxima es definido por el controlador). (1 < = *p* < = 15; *s* <= *p*). [ 4]|  
|SQL_NUMERIC|NUMÉRICO (*p*,*s*)|Iniciado, el valor numérico exacto con una precisión *p* y escala *s* (1 < = *p* < = 15; *s* <= *p*). [ 4]|  
|SQL_SMALLINT|SMALLINT|Valor numérico exacto con precisión de 5 y escala de 0 (firmado: entre-32.768 y < = *n* < = 32 767; sin signo:  0 <= *n* <= 65,535)[3].|  
|SQL_INTEGER|INTEGER|Valor numérico exacto con precisión de 10 y escala de 0 (firmado: -2 [31] < = *n* < = 2 [31] - 1; sin signo:  0 <= *n* <= 2[32] - 1)[3].|  
|SQL_REAL|REAL|Valor con signo, aproximado, numeric con una precisión binaria de 24 (cero o valor absoluto 10 [-38] a 10[38]).|  
|SQL_FLOAT|FLOAT (*p*)|Valor con signo, aproximado, numeric con una precisión binaria de al menos *p*. (La precisión máxima es definido por el controlador). [5]|  
|SQL_DOUBLE|DOUBLE PRECISION|Valor con signo, aproximado, numeric con una precisión binaria de 53 (cero o valor absoluto 10 [-308] a 10[308]).|  
|SQL_BIT|BIT|Datos binarios de bits única. [8]|  
|SQL_TINYINT|TINYINT|Valor numérico exacto con precisión 3 y escala de 0 (firmado: -128 < = *n* < = 127; sin signo:  0 <= *n* <= 255)[3].|  
|SQL_BIGINT|BIGINT|Exacto de un valor numérico con una precisión de 19 (si tiene signo) o 20 (si no tiene signo) y una escala de 0 (firmado: -2 [63] < = *n* < = 2 [63] - 1; sin signo: 0 <= *n* <= 2[64] - 1)[3],[9].|  
|SQL_BINARY|BINARY(*n*)|Datos binarios de longitud fija *n*. [ 9]|  
|SQL_VARBINARY|VARBINARY(*n*)|Datos binarios de longitud variable de longitud máxima *n*. El máximo se establece por el usuario. [9]|  
|SQL_LONGVARBINARY|VARBINARY LARGO|Datos binarios de longitud variable. Longitud máxima es depende del origen de datos. [9]|  
|SQL_TYPE_DATE[6]|DATE|Año, mes y día campos, conforme a las reglas del calendario gregoriano. (Consulte [restricciones del calendario gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md), más adelante en este apéndice.)|  
|SQL_TYPE_TIME[6]|TIEMPO (*p*)|Hora, minuto y segundo campos, con los valores válidos para las horas de 00 a 23, los valores válidos de 00 a 59 minutos y los valores válidos para los segundos de 00 a 61. Precisión *p* indica la precisión de segundos.|  
|SQL_TYPE_TIMESTAMP[6]|Marca de tiempo (*p*)|Año, mes, día, hora, minuto y segundo campos, con los valores válidos según se define para los tipos de datos de fecha y hora.|  
|SQL_TYPE_UTCDATETIME|UTCDATETIME|Campos de año, mes, día, hora, minuto, segundo, utchour y utcminute. Los campos utchour y utcminute tienen precisión de 1/10 microsegundo.|  
|SQL_TYPE_UTCTIME|UTCTIME|Campos de hora, minuto, segundo, utchour y utcminute. Los campos utchour y utcminute tienen precisión de 1/10 microsegundo...|  
|SQL_INTERVAL_MONTH[7]|MES de intervalo (*p*)|Número de meses entre dos fechas; *p* es el intervalo de precisión del principio.|  
|SQL_INTERVAL_YEAR[7]|AÑO del intervalo (*p*)|Número de años entre dos fechas; *p* es el intervalo de precisión del principio.|  
|SQL_INTERVAL_YEAR_TO_MONTH[7]|AÑO del intervalo (*p*) al mes|Número de años y meses entre dos fechas; *p* es el intervalo de precisión del principio.|  
|SQL_INTERVAL_DAY[7]|DÍA del intervalo (*p*)|Número de días entre dos fechas; *p* es el intervalo de precisión del principio.|  
|SQL_INTERVAL_HOUR[7]|HORA del intervalo (*p*)|Número de horas entre dos fechas/horas; *p* es el intervalo de precisión del principio.|  
|SQL_INTERVAL_MINUTE[7]|MINUTOS de intervalo (*p*)|Número de minutos entre dos fechas/horas; *p* es el intervalo de precisión del principio.|  
|SQL_INTERVAL_SECOND[7]|INTERVALO de segundo (*p*,*q*)|Número de segundos entre dos fechas/horas; *p* es el intervalo de precisión del principio y *q* es la precisión de segundos del intervalo.|  
|SQL_INTERVAL_DAY_TO_HOUR[7]|DÍA del intervalo (*p*) a la hora|Número de días y horas entre dos fechas/horas; *p* es el intervalo de precisión del principio.|  
|SQL_INTERVAL_DAY_TO_MINUTE[7]|DÍA del intervalo (*p*) al minuto|Número de días, horas o minutos entre dos fechas/horas; *p* es el intervalo de precisión del principio.|  
|SQL_INTERVAL_DAY_TO_SECOND[7]|INTERVAL DAY (*p*) al segundo (*q*)|Número de días/horas/minutos/segundos entre dos fechas/horas; *p* es el intervalo de precisión del principio y *q* es la precisión de segundos del intervalo.|  
|SQL_INTERVAL_HOUR_TO_MINUTE[7]|HORA del intervalo (*p*) al minuto|Número de horas o minutos entre dos fechas/horas; *p* es el intervalo de precisión del principio.|  
|SQL_INTERVAL_HOUR_TO_SECOND[7]|HORA del intervalo (*p*) al segundo (*q*)|Número de horas/minutos/segundos entre dos fechas/horas; *p* es el intervalo de precisión del principio y *q* es la precisión de segundos del intervalo.|  
|SQL_INTERVAL_MINUTE_TO_SECOND[7]|MINUTOS de intervalo (*p*) al segundo (*q*)|Número de minutos/segundos entre dos fechas/horas; *p* es el intervalo de precisión del principio y *q* es la precisión de segundos del intervalo.|  
|SQL_GUID|GUID|GUID de longitud fija.|  
  
 [1] se trata el valor devuelto en la columna DATA_TYPE mediante una llamada a **SQLGetTypeInfo**.  
  
 [2] es el valor devuelto en la columna nombre y crear PARAMS mediante una llamada a **SQLGetTypeInfo**. La columna nombre devuelve la designación-CHAR, por ejemplo,-, mientras que la columna crear PARAMS devuelve una lista separada por comas de parámetros de creación como la precisión, escala y longitud.  
  
 [3] en una aplicación usa **SQLGetTypeInfo** o **SQLColAttribute** para determinar si un tipo de datos determinado o una columna en particular en un conjunto de resultados es sin signo.  
  
 [4] tipos de datos SQL_DECIMAL y SQL_NUMERIC solo difieren en su precisión. La precisión de un DECIMAL (*p*,*s*) es la precisión decimal definido por la implementación que es no menos de *p*, mientras que la precisión de un valor numérico (*p* ,*s*) es exactamente igual que *p*.  
  
 [5] en función de la implementación, puede ser la precisión de SQL_FLOAT 24 o 53: si es 24, el tipo de datos SQL_FLOAT es el mismo que SQL_REAL; Si es 53, el tipo de datos SQL_FLOAT es igual a SQL_DOUBLE.  
  
 [6] en ODBC *3.x*, los tipos de datos de fecha, hora y marca de tiempo SQL son SQL_TYPE_DATE, SQL_TYPE_TIME y SQL_TYPE_TIMESTAMP, respectivamente; en ODBC *2.x*, los tipos de datos son SQL_DATE, SQL_TIME y SQL_ MARCA DE TIEMPO.  
  
 [7] para obtener más información acerca de los tipos de datos SQL de intervalo, vea el [tipos de datos Interval](../../../odbc/reference/appendixes/interval-data-types.md) sección más adelante en este apéndice.  
  
 [8], el tipo de datos SQL_BIT tiene características diferentes del tipo de BIT en SQL-92.  
  
 [9] este tipo de datos no tiene ningún tipo de datos correspondiente en SQL-92.  
  
 Esta sección proporciona en el ejemplo siguiente.  
  
-   [Conjunto de resultados de SQLGetTypeInfo de ejemplo](../../../odbc/reference/appendixes/example-sqlgettypeinfo-result-set.md)
