---
title: Funciones de hora, fecha e intervalo ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], time functions
- functions [ODBC], date functions
- interval functions [ODBC]
- functions [ODBC], interval functions
- time functions [ODBC]
- date functions [ODBC]
ms.assetid: bdf054a0-7aba-4e99-a34a-799917376fd5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aec3d6b23383edcc9659ff884e8cd71b0595dae1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302826"
---
# <a name="time-date-and-interval-functions"></a>Funciones de hora, fecha e intervalo
En la tabla siguiente se enumeran las funciones de hora y fecha que se incluyen en el conjunto de funciones escalares ODBC. Una aplicación puede determinar qué funciones de fecha y hora es compatible con un controlador mediante una llamada a **SQLGetInfo** con un tipo de *información* de SQL_TIMEDATE_FUNCTIONS.  
  
 Los argumentos que se indican como *timestamp_exp* pueden ser el nombre de una columna, el resultado de otra función escalar o un escape en *tiempo ODBC,* *ODBC-date- escape*o *ODBC-timestamp-escape*, donde el tipo de datos subyacente podría representarse como SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME, SQL_TYPE_DATE o SQL_TYPE_TIMESTAMP.  
  
 Los argumentos que se indican como *date_exp* pueden ser el nombre de una columna, el resultado de otra función escalar o un *ODBC-date- escape* o *ODBC-timestamp-escape*, donde el tipo de datos subyacente podría representarse como SQL_CHAR, SQL_VARCHAR, SQL_TYPE_DATE o SQL_TYPE_TIMESTAMP.  
  
 Los argumentos que se indican como *time_exp* pueden ser el nombre de una columna, el resultado de otra función escalar o un escape en *tiempo ODBC* o de escape de marca de *tiempo ODBC,* donde el tipo de datos subyacente se podría representar como SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME o SQL_TYPE_TIMESTAMP.  
  
 Las funciones escalares CURRENT_DATE, CURRENT_TIME y CURRENT_TIMESTAMP fecha de tiempo se han agregado en ODBC 3.0 para alinearse con SQL-92.  
  
|Función|Descripción|  
|--------------|-----------------|  
|**CURRENT_DATE( )** (ODBC 3.0)|Devuelve la fecha actual.|  
|**CURRENT_TIME[(** *precisión de tiempo* **)]** (ODBC 3.0)|Devuelve la hora local actual. El argumento *de precisión* de tiempo determina la precisión de segundos del valor devuelto.|  
|**CURRENT_TIMESTAMP**<br /> **[(** *precisión de marca de tiempo* **)]** (ODBC 3.0)|Devuelve la fecha local actual y la hora local como un valor de marca de tiempo. El argumento *timestamp-precision* determina la precisión de segundos de la marca de tiempo devuelta.|  
|**CURDATE( )** (ODBC 1.0)|Devuelve la fecha actual.|  
|**CURTIME( )** (ODBC 1.0)|Devuelve la hora local actual.|  
|**DAYNAME(** *date_exp* **)** (ODBC 2.0)|Devuelve una cadena de caracteres que contiene el nombre específico del origen de datos del día (por ejemplo, de domingo a sábado o sun. a Sat. para un origen de datos que usa inglés o Sonntag a través de Samstag para un origen de datos que usa alemán) para la parte del día de *date_exp*.|  
|**DAYOFMONTH(** *date_exp* **)** (ODBC 1.0)|Devuelve el día del mes en función del campo de mes en *date_exp* como un valor entero en el intervalo de 1 a 31.|  
|**DAYOFWEEK(** *date_exp* **)** (ODBC 1.0)|Devuelve el día de la semana en función del campo de semana en *date_exp* como un valor entero en el intervalo de 1-7, donde 1 representa el domingo.|  
|**DAYOFYEAR(** *date_exp* **)** (ODBC 1.0)|Devuelve el día del año en función del campo de año de *date_exp* como un valor entero en el intervalo de 1 a 366.|  
|**EXTRACT(** *extraer-campo DE* *extraer-fuente* **)** (ODBC 3.0)|Devuelve la parte del campo de *extracción* del origen *de extracción*. El argumento *extract-source* es una expresión datetime o interval. El argumento *extract-field* puede ser una de las siguientes palabras clave:<br /><br /> AÑO MES DÍA HORA MINUTO SEGUNDO<br /><br /> La precisión del valor devuelto está definida por la implementación. La escala es 0 a menos que se especifique SECOND, en cuyo caso la escala no es inferior a la precisión de fracciones de segundo del campo *de origen de extracción.*|  
|**HOUR(** *time_exp* **)** (ODBC 1.0)|Devuelve la hora en función del campo de hora *de time_exp* como un valor entero en el intervalo de 0 a 23.|  
|**MINUTE(** *time_exp* **)** (ODBC 1.0)|Devuelve el minuto en función del campo de minuto de *time_exp* como un valor entero en el intervalo de 0 a 59.|  
|**MONTH(** *date_exp* **)** (ODBC 1.0)|Devuelve el mes en función del campo de mes *en date_exp* como un valor entero en el intervalo de 1-12.|  
|**MONTHNAME(** *date_exp* **)** (ODBC 2.0)|Devuelve una cadena de caracteres que contiene el nombre específico del origen de datos del mes (por ejemplo, de enero a diciembre o de enero a través de diciembre para un origen de datos que usa inglés o Januar a través de Dezember para un origen de datos que usa alemán) para la parte del mes de *date_exp*.|  
|**NOW( )** (ODBC 1.0)|Devuelve la fecha y hora actuales como un valor de marca de tiempo.|  
|**QUARTER(** *date_exp* **)** (ODBC 1.0)|Devuelve el trimestre en *date_exp* como un valor entero en el intervalo de 1-4, donde 1 representa el 1 de enero al 31 de marzo.|  
|**SEGUNDO(** *time_exp* **)** (ODBC 1.0)|Devuelve el segundo en función del segundo campo *de time_exp* como un valor entero en el intervalo de 0 a 59.|
|**TIMESTAMPADD(** *interval*, *integer_exp*, *timestamp_exp* **)** (ODBC 2.0)|Devuelve la marca de tiempo calculada agregando *integer_exp* intervalos de *intervalo* de tipo para *timestamp_exp*. Los valores válidos de *intervalo* son las siguientes palabras clave:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> donde las fracciones de segundo se expresan en milmillonésimas de segundo. Por ejemplo, la siguiente instrucción SQL devuelve el nombre de cada empleado y su fecha de aniversario de un año:<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> Si *timestamp_exp* es un valor de tiempo y *el intervalo* especifica días, semanas, meses, trimestres o años, la parte de fecha de *timestamp_exp* se establece en la fecha actual antes de calcular la marca de tiempo resultante.<br /><br /> Si *timestamp_exp* es un valor de fecha y *el intervalo* especifica fracciones de segundos, segundos, minutos u horas, la parte de tiempo de *timestamp_exp* se establece en 0 antes de calcular la marca de tiempo resultante.<br /><br /> Una aplicación determina qué intervalos admite un origen de datos llamando a **SQLGetInfo** con la opción SQL_TIMEDATE_ADD_INTERVALS.|  
|**TIMESTAMPDIFF(** *interval*, *timestamp_exp1*, *timestamp_exp2* **)** (ODBC 2.0)|Devuelve el número entero de intervalos de *tipo interval* por el cual *timestamp_exp2* es mayor que *timestamp_exp1*. Los valores válidos de *intervalo* son las siguientes palabras clave:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> donde las fracciones de segundo se expresan en milmillonésimas de segundo. Por ejemplo, la siguiente instrucción SQL devuelve el nombre de cada empleado y el número de años que ha estado empleado:<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> Si cualquiera de las expresiones de marca de tiempo es un valor de hora y *el intervalo* especifica días, semanas, meses, trimestres o años, la parte de fecha de esa marca de tiempo se establece en la fecha actual antes de calcular la diferencia entre las marcas de tiempo.<br /><br /> Si cualquiera de las expresiones de marca de tiempo es un valor de fecha y *el intervalo* especifica fracciones de segundos, segundos, minutos u horas, la parte de tiempo de esa marca de tiempo se establece en 0 antes de calcular la diferencia entre las marcas de tiempo.<br /><br /> Una aplicación determina qué intervalos admite un origen de datos llamando a **SQLGetInfo** con la opción SQL_TIMEDATE_DIFF_INTERVALS.|  
|**WEEK(** *date_exp* **)** (ODBC 1.0)|Devuelve la semana del año en función del campo de semana *de date_exp* como un valor entero en el intervalo de 1 a 53.|  
|**YEAR(** *date_exp* **)** (ODBC 1.0)|Devuelve el año en función del campo de año *de date_exp* como un valor entero. El intervalo depende del origen de datos.|
