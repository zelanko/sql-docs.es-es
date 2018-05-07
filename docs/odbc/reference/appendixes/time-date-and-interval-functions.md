---
title: Funciones de intervalo de hora, fecha e | Documentos de Microsoft
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
- functions [ODBC], time functions
- functions [ODBC], date functions
- interval functions [ODBC]
- functions [ODBC], interval functions
- time functions [ODBC]
- date functions [ODBC]
ms.assetid: bdf054a0-7aba-4e99-a34a-799917376fd5
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d2939125046525ec73f25499f75a4b981f301615
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="time-date-and-interval-functions"></a>Funciones de hora, fecha e intervalo
En la tabla siguiente se enumera las funciones de fecha y hora en que se incluyen en el conjunto de funciones escalares de ODBC. Una aplicación puede determinar qué funciones de fecha y hora son compatibles con un controlador mediante una llamada a **SQLGetInfo** con una *tipo de información* de SQL_TIMEDATE_FUNCTIONS.  
  
 Argumentos que se denotan *timestamp_exp* puede ser el nombre de una columna, el resultado de otra función escalar o una *escape de hora de ODBC*, *escape de fecha de ODBC*, o *Escape de marca de tiempo de ODBC*, donde el tipo de datos subyacente podría representar como SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME, SQL_TYPE_DATE o SQL_TYPE_TIMESTAMP.  
  
 Argumentos que se denotan *date_exp* puede ser el nombre de una columna, el resultado de otra función escalar o una *escape de fecha de ODBC* o *escape de marca de tiempo de ODBC*, donde el tipo de datos subyacente se puede representar como SQL_CHAR, SQL_VARCHAR, SQL_TYPE_DATE o SQL_TYPE_TIMESTAMP.  
  
 Argumentos que se denotan *time_exp* puede ser el nombre de una columna, el resultado de otra función escalar o una *escape de hora de ODBC* o *escape de marca de tiempo de ODBC*, donde el tipo de datos subyacente se puede representar como SQL_CHAR, SQL_VARCHAR, SQL_TYPE_TIME y SQL_TYPE_TIMESTAMP.  
  
 Los CURRENT_DATE, CURRENT_TIME y CURRENT_TIMESTAMP timedate funciones escalares se han agregado en ODBC 3.0 se alineen con SQL-92.  
  
|Función|Description|  
|--------------|-----------------|  
|**() CURRENT_DATE** (ODBC 3.0)|Devuelve la fecha actual.|  
|**CURRENT_TIME [(** *precisión de tiempo* **)]** (ODBC 3.0)|Devuelve la hora local actual. El *precisión de tiempo* argumento determina la precisión de segundos del valor devuelto.|  
|**CURRENT_TIMESTAMP**<br /> **[(** *precisión de la marca de tiempo* **)]** (ODBC 3.0)|Devuelve la fecha local actual y la hora local como un valor de marca de tiempo. El *precisión de la marca de tiempo* argumento determina la precisión de segundos de la marca de tiempo devuelto.|  
|**CURDATE ()** (ODBC 1.0)|Devuelve la fecha actual.|  
|**() CURTIME** (ODBC 1.0)|Devuelve la hora local actual.|  
|**DAYNAME (** *date_exp* **)** (ODBC 2.0)|Devuelve una cadena de caracteres que contiene el nombre específico del origen de datos del día (por ejemplo, Sunday a Saturday o Sun. a Sat. para un origen de datos que utiliza inglés, o bien Sonntag a Samstag para un origen de datos que utiliza alemán) para la parte de día de *date_exp*.|  
|**DAYOFMONTH (** *date_exp* **)** (ODBC 1.0)|Devuelve el día del mes basado en el campo de mes en *date_exp* como un valor entero en el intervalo de 1 a 31.|  
|**DAYOFWEEK (** *date_exp* **)** (ODBC 1.0)|Devuelve el día de la semana basado en el campo de semana en *date_exp* como un valor entero en el intervalo de 1 a 7, donde 1 representa el domingo.|  
|**DAYOFYEAR (** *date_exp* **)** (ODBC 1.0)|Devuelve el día del año basado en el campo año en *date_exp* como un valor entero en el intervalo de 1 – 366.|  
|**EXTRAER (** *extraer campos FROM* *extracción origen* **)** (ODBC 3.0)|Devuelve el *extraer campos* parte de la *extracción origen*. El *extracción origen* argumento es una expresión de fecha y hora o intervalo. El *extraer campos* argumento puede ser una de las siguientes palabras clave:<br /><br /> AÑO MES DÍA HORA MINUTO SEGUNDO<br /><br /> La precisión del valor devuelto es definido por la implementación. La escala es 0, a menos que se especifica en segundo lugar, en cuyo caso la escala no es menor que la precisión de fracciones de segundo de la *extracción origen* campo.|  
|**HORA (** *time_exp* **)** (ODBC 1.0)|Devuelve la hora basada en el campo de hora en *time_exp* como un valor entero en el intervalo de 0 a 23.|  
|**MINUTO (** *time_exp* **)** (ODBC 1.0)|Devuelve los minutos basados en el campo de miuntos en *time_exp* como un valor entero en el intervalo de 0 a 59.|  
|**MES (** *date_exp* **)** (ODBC 1.0)|Devuelve el mes basado en el campo de mes en *date_exp* como un valor entero en el intervalo de 1 a 12.|  
|**MONTHNAME (** *date_exp* **)** (ODBC 2.0)|Devuelve una cadena de caracteres que contiene el nombre específico del origen de datos del mes (por ejemplo, January a December o Jan. a DEC. para un origen de datos que utiliza a inglés, o bien Januar a Dezember para un origen de datos que utiliza alemán) para la parte del mes *date_exp*.|  
|**(AHORA)** (ODBC 1.0)|Devuelve la fecha y hora como un valor de marca de tiempo actual.|  
|**TRIMESTRE (** *date_exp* **)** (ODBC 1.0)|Devuelve el trimestre en *date_exp* como un valor entero en el intervalo de 1 a 4, donde 1 representa el 1 de enero hasta el 31 de marzo.|  
|**SEGUNDO (** *time_exp* **)** (ODBC 1.0)|Devuelve los segundos basados en el segundo campo de *time_exp* como un valor entero en el intervalo de 0 a 59.|
|**TIMESTAMPADD (** *intervalo*, *integer_exp*, *timestamp_exp* **)** (ODBC 2.0)|Devuelve la marca de tiempo que se calcula sumando *integer_exp* intervalos de tipo *intervalo* a *timestamp_exp*. Los valores válidos de *intervalo* son las palabras clave siguientes:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> donde las fracciones de segundo se expresan en milmillonésimas de segundo. Por ejemplo, la siguiente instrucción SQL devuelve el nombre de cada empleado y su fecha de aniversario de un año:<br /><br /> `SELECT NAME, {fn  TIMESTAMPADD(SQL_TSI_YEAR, 1, HIRE_DATE)} FROM  EMPLOYEES`<br /><br /> Si *timestamp_exp* es un valor de tiempo y *intervalo* especifica días, semanas, meses, trimestres o años, la parte de fecha *timestamp_exp* se establece en la fecha actual antes de calcular la marca de tiempo resultante.<br /><br /> Si *timestamp_exp* es un valor de fecha y *intervalo* especifica fracciones segundos, segundos, minutos u horas, la parte de hora de *timestamp_exp* se establece en 0 antes de calcular la marca de tiempo resultante.<br /><br /> Una aplicación determina qué intervalos es compatible con un origen de datos mediante una llamada a **SQLGetInfo** con la opción SQL_TIMEDATE_ADD_INTERVALS.|  
|**TIMESTAMPDIFF de ODBC (** *intervalo*, *timestamp_exp1*, *timestamp_exp2* **)** (ODBC 2.0)|Devuelve el número entero de intervalos de tipo *intervalo* mediante el cual *timestamp_exp2* es mayor que *timestamp_exp1*. Los valores válidos de *intervalo* son las palabras clave siguientes:<br /><br /> SQL_TSI_FRAC_SECOND<br /><br /> SQL_TSI_SECOND<br /><br /> SQL_TSI_MINUTE<br /><br /> SQL_TSI_HOUR<br /><br /> SQL_TSI_DAY<br /><br /> SQL_TSI_WEEK<br /><br /> SQL_TSI_MONTH<br /><br /> SQL_TSI_QUARTER<br /><br /> SQL_TSI_YEAR<br /><br /> donde las fracciones de segundo se expresan en milmillonésimas de segundo. Por ejemplo, la siguiente instrucción SQL devuelve el nombre de cada empleado y el número de años que se ha empleado:<br /><br /> `SELECT NAME, {fn  TIMESTAMPDIFF(SQL_TSI_YEAR, {fn CURDATE()}, HIRE_DATE)} FROM EMPLOYEES`<br /><br /> Si alguna expresión de marca de tiempo es un valor de tiempo y *intervalo* especifica días, semanas, meses, trimestres o años, la parte de la fecha de esa marca de hora se establece en la fecha actual antes de calcular la diferencia entre las marcas de tiempo.<br /><br /> Si alguna expresión de marca de tiempo es un valor de fecha y *intervalo* especifica fracciones segundos, segundos, minutos u horas, la parte de hora de esa marca de hora se establece en 0 antes de calcular la diferencia entre las marcas de tiempo.<br /><br /> Una aplicación determina qué intervalos es compatible con un origen de datos mediante una llamada a **SQLGetInfo** con la opción SQL_TIMEDATE_DIFF_INTERVALS.|  
|**SEMANA (** *date_exp* **)** (ODBC 1.0)|Devuelve la semana del año basado en el campo de semana en *date_exp* como un valor entero en el intervalo de 1 a 53.|  
|**AÑO (** *date_exp* **)** (ODBC 1.0)|Devuelve el año basándose en el campo año en *date_exp* como un valor entero. El intervalo es depende del origen de datos.|
