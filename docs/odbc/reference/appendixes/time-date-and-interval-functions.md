---
title: Funciones de intervalo, fecha y hora | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e1303ca724ef6790ae7bcf218ab8ed0e5da4ed38
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62735091"
---
# <a name="time-date-and-interval-functions"></a>Funciones de hora, fecha e intervalo
En la tabla siguiente se enumera las funciones de fecha y hora que se incluyen en el conjunto de funciones escalares de ODBC. Una aplicación puede determinar qué funciones de fecha y hora admitidas por un controlador mediante una llamada a **SQLGetInfo** con un *tipo de información* de SQL_TIMEDATE_FUNCTIONS.  
  
 Argumentos que se indican como *timestamp_exp* puede ser el nombre de una columna, el resultado de otra función escalar, o un *escape de hora ODBC*, *escape de fecha ODBC*, o *Escape de marca de tiempo de ODBC*, donde el tipo de datos subyacente podría representarse como SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME, SQL_TYPE_DATE o SQL_TYPE_TIMESTAMP.  
  
 Argumentos que se indican como *date_exp* puede ser el nombre de una columna, el resultado de otra función escalar, o un *escape de fecha ODBC* o *escape de marca de tiempo de ODBC*, donde el tipo de datos subyacente podría representarse como SQL_CHAR, SQL_VARCHAR, SQL_TYPE_DATE o SQL_TYPE_TIMESTAMP.  
  
 Argumentos que se indican como *time_exp* puede ser el nombre de una columna, el resultado de otra función escalar, o un *escape de hora ODBC* o *escape de marca de tiempo de ODBC*, donde el tipo de datos subyacente podría representarse como SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME y SQL_TYPE_TIMESTAMP.  
  
 El CURRENT_DATE y CURRENT_TIME CURRENT_TIMESTAMP timedate funciones escalares se han agregado en ODBC 3.0 para alinearse con SQL-92.  
  
|Función|Descripción|  
|--------------|-----------------|  
|**() CURRENT_DATE** (ODBC 3.0)|Devuelve la fecha actual.|  
|**CURRENT_TIME [(** *precisión de tiempo* **)]** (ODBC 3.0)|Devuelve la hora local actual. El *precisión de tiempo* argumento determina la precisión de segundos del valor devuelto.|  
|**CURRENT_TIMESTAMP**<br /> **[(** *precisión de la marca de tiempo* **)]** (ODBC 3.0)|Devuelve la fecha local actual y la hora local como un valor de marca de tiempo. El *precisión de la marca de tiempo* argumento determina la precisión de segundos de la marca de tiempo devuelto.|  
|**CURDATE ()** (ODBC 1.0)|Devuelve la fecha actual.|  
|**() CURTIME** (ODBC 1.0)|Devuelve la hora local actual.|  
|**DAYNAME (** *date_exp* **)** (ODBC 2.0)|Devuelve una cadena de caracteres que contiene el nombre específico del origen de datos del día (por ejemplo, Sunday a Saturday o Sun. a Sat. para un origen de datos que utiliza inglés, o bien Sonntag a Samstag para un origen de datos que utiliza alemán) para la parte del día *date_exp*.|  
|**DAYOFMONTH (** *date_exp* **)** (ODBC 1.0)|Devuelve el día del mes en función del campo de mes en *date_exp* como un valor entero en el intervalo de 1 a 31.|  
|**DAYOFWEEK (** *date_exp* **)** (ODBC 1.0)|Devuelve el día de la semana basado en el campo de la semana en *date_exp* como un valor entero en el intervalo de 1 a 7, donde 1 representa el domingo.|  
|**DAYOFYEAR (** *date_exp* **)** (ODBC 1.0)|Devuelve el día del año según el campo año en *date_exp* como un valor entero en el intervalo de 1-366.|  
|**EXTRAER (** *extraer campo FROM* *origen de extracción* **)** (ODBC 3.0)|Devuelve el *extraer campo* parte de la *origen de extracción*. El *origen de extracción* argumento es una expresión de intervalo o datetime. El *extraer campo* argumento puede ser una de las siguientes palabras clave:<br /><br /> AÑO MES DÍA HORA MINUTO SEGUNDO<br /><br /> La precisión del valor devuelto es definido por la implementación. La escala es 0, a menos que se especifica en segundo lugar, en cuyo caso la escala no es menor que la precisión de fracciones de segundos de la *origen de extracción* campo.|  
|**HOUR(** *time_exp* **)** (ODBC 1.0)|Devuelve la hora en función del campo de hora en *time_exp* como un valor entero en el intervalo de 0 a 23.|  
|**MINUTE(** *time_exp* **)** (ODBC 1.0)|Devuelve el minuto basándose en el campo de miuntos en *time_exp* como un valor entero en el intervalo de 0 a 59.|  
|**MONTH(** *date_exp* **)** (ODBC 1.0)|Devuelve el mes según el campo de mes en *date_exp* como un valor entero en el intervalo de 1 a 12.|  
|**MONTHNAME (** *date_exp* **)** (ODBC 2.0)|Devuelve una cadena de caracteres que contiene el nombre específico del origen de datos del mes (por ejemplo, January a December o enero a diciembre de un origen de datos que utiliza a inglés, o bien Januar a Dezember para un origen de datos que utiliza alemán) para la parte del mes *date_exp*.|  
|**AHORA ()** (ODBC 1.0)|Devuelve la fecha y hora como un valor de marca de tiempo actual.|  
|**QUARTER(** *date_exp* **)** (ODBC 1.0)|Devuelve el trimestre en *date_exp* como un valor entero en el intervalo de 1 a 4, donde 1 representa el 1 de enero hasta el 31 de marzo.|  
|**SECOND(** *time_exp* **)** (ODBC 1.0)|Devuelve el segundo basándose en el segundo campo de *time_exp* como un valor entero en el intervalo de 0 a 59.|
|**TIMESTAMPADD(** *interval*, *integer_exp*, *timestamp_exp* **)** (ODBC 2.0)|Devuelve la marca de tiempo que se calcula sumando *integer_exp* intervalos de tipo *intervalo* a *timestamp_exp*. Los valores válidos de *intervalo* son las siguientes palabras clave:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> donde las fracciones de segundo se expresan en milmillonésimas de segundo. Por ejemplo, la siguiente instrucción SQL devuelve el nombre de cada empleado y su fecha de aniversario:<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> Si *timestamp_exp* es un valor de tiempo y *intervalo* especifica los días, semanas, meses, trimestres o años, la parte de fecha de *timestamp_exp* se establece en la fecha actual calcular la marca de tiempo resultante.<br /><br /> Si *timestamp_exp* es un valor de fecha y *intervalo* especifica fracciones segundos, segundos, minutos u horas, la parte de hora *timestamp_exp* se establece en 0 antes de calcular la marca de tiempo resultante.<br /><br /> Una aplicación determina qué intervalos es compatible con un origen de datos mediante una llamada a **SQLGetInfo** con la opción SQL_TIMEDATE_ADD_INTERVALS.|  
|**TIMESTAMPDIFF(** *interval*, *timestamp_exp1*, *timestamp_exp2* **)** (ODBC 2.0)|Devuelve el número entero de intervalos de tipo *intervalo* mediante el cual *timestamp_exp2* es mayor que *timestamp_exp1*. Los valores válidos de *intervalo* son las siguientes palabras clave:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> donde las fracciones de segundo se expresan en milmillonésimas de segundo. Por ejemplo, la siguiente instrucción SQL devuelve el nombre de cada empleado y el número de años que ha sido contratado piensan:<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> Si una de las expresiones de marca de tiempo es un valor de tiempo y *intervalo* especifica los días, semanas, meses, trimestres o años, la parte de la fecha de esa marca de tiempo se establece en la fecha actual antes de calcular la diferencia entre las marcas de tiempo.<br /><br /> Si una de las expresiones de marca de tiempo es un valor de fecha y *intervalo* especifica fracciones segundos, segundos, minutos u horas, la parte de hora de esa marca de tiempo se establece en 0 antes de calcular la diferencia entre las marcas de tiempo.<br /><br /> Una aplicación determina qué intervalos es compatible con un origen de datos mediante una llamada a **SQLGetInfo** con la opción SQL_TIMEDATE_DIFF_INTERVALS.|  
|**WEEK(** *date_exp* **)** (ODBC 1.0)|Devuelve la semana del año según el campo de la semana en *date_exp* como un valor entero en el intervalo de 1-53.|  
|**YEAR(** *date_exp* **)** (ODBC 1.0)|Devuelve el año según el campo año en *date_exp* como un valor entero. El intervalo es depende del origen de datos.|
