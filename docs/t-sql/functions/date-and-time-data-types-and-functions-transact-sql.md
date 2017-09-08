---
title: Datos de fecha y hora tipos y funciones (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 09/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- dates [SQL Server], functions
- dates [SQL Server]
- date and time [SQL Server], all data types and functions
- date and time [SQL Server]
- functions [SQL Server], time
- functions [SQL Server], date and time
- time [SQL Server], functions
ms.assetid: 83e378a2-6e89-4c80-bc4f-644958d9e0a9
caps.latest.revision: 79
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 60272ce672c0a32738b0084ea86f8907ec7fc0a5
ms.openlocfilehash: 7ce3baac7ec87ff3cad771234ab1196fb0a3855e
ms.contentlocale: es-es
ms.lasthandoff: 09/06/2017

---
# <a name="date-and-time-data-types-and-functions-transact-sql"></a>Tipos de datos y funciones de fecha y hora (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

Las secciones siguientes de este tema proporcionan información de todos los tipos de datos y funciones de fecha y la hora de [!INCLUDE[tsql](../../includes/tsql-md.md)].
-   [Tipos de fecha y hora](#DateandTimeDataTypes)  
-   [Funciones de fecha y hora](#DateandTimeFunctions)  
    -   [Función que valores Get sistema fecha y hora](#GetSystemDateandTimeValues)  
    -   [Funciones que obtienen la fecha y hora partes](#GetDateandTimeParts)  
    -   [Funciones que obtienen valores de fecha y hora de sus partes](#fromParts)  
    -   [Funciones que obtienen la fecha y hora de diferencia](#GetDateandTimeDifference)  
    -   [Funciones que modifican la fecha y hora de valores](#ModifyDateandTimeValues)  
    -   [Funciones que establecen u obtienen funciones de formato de sesión](#SetorGetSessionFormatFunctions)  
    -   [Funciones que validan la fecha y hora de valores](#ValidateDateandTimeValues)  
-   [Fecha y temas relacionados con el tiempo](#DateandTimeRelatedTopics)  
  
##  <a name="DateandTimeDataTypes"></a>Tipos de datos de fecha y hora
El [!INCLUDE[tsql](../../includes/tsql-md.md)] tipos de datos de fecha y hora se muestran en la tabla siguiente:
  
|Tipo de datos|Formato|Intervalo|Precisión|Tamaño de almacenamiento (bytes)|Precisión de fracciones de segundo definida por el usuario|Ajuste de zona horaria|  
|---|---|---|---|---|---|---|
|[time](../../t-sql/data-types/time-transact-sql.md)|hh:mm:ss[.nnnnnnn]|De 00:00:00.0000000 a 23:59:59.9999999|100 nanosegundos|3 to 5|Sí|No|  
|[date](../../t-sql/data-types/date-transact-sql.md)|YYYY-MM-DD|De 0001-01-01 a 31.12.99|1 día|3|No|No|  
|[smalldatetime](../../t-sql/data-types/smalldatetime-transact-sql.md)|AAAA-MM-DD hh:mm:ss|De 1900-01-01 a 2079-06-06|1 minuto.|4|No|No|  
|[datetime](../../t-sql/data-types/datetime-transact-sql.md)|AAAA-MM-DD hh:mm:ss[.nnn]|De 1753-01-01 a 9999-12-31|0,00333 segundos|8|No|No|  
|[datetime2](../../t-sql/data-types/datetime2-transact-sql.md)|AAAA-MM-DD hh:mm:ss[.nnnnnnn]|De 0001-01-01 00:00:00.0000000 a 9999-12-31 23:59:59.9999999|100 nanosegundos|De 6 a 8|Sí|No|  
|[datetimeoffset](../../t-sql/data-types/datetimeoffset-transact-sql.md)|AAAA-MM-DD hh [.nnnnnnn] [+ &#124;-] hh: mm|De 0001-01-01 00:00:00.0000000 a 9999-12-31 23:59:59.9999999 (en UTC)|100 nanosegundos|De 8 a 10|Sí|Sí|  
  
> [!NOTE]  
>  El [!INCLUDE[tsql](../../includes/tsql-md.md)] [rowversion](../../t-sql/data-types/rowversion-transact-sql.md) tipo de datos no es un tipo de datos de fecha u hora. **marca de tiempo** es un sinónimo desusado de **rowversion**.  
  
##  <a name="DateandTimeFunctions"></a>Funciones de fecha y hora  
En las tablas siguientes se enumeran las funciones de fecha y hora de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para obtener más información acerca del determinismo, vea [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).
  
###  <a name="GetSystemDateandTimeValues"></a>Funciones que obtienen valores de fecha y hora de sistema 
Todos los valores de fecha y hora del sistema se derivan del sistema operativo del equipo en el que se ejecuta la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
#### <a name="higher-precision-system-date-and-time-functions"></a>Funciones de fecha y hora del sistema de precisión elevada  
[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]Obtiene los valores de fecha y hora mediante la API de Windows GetSystemTimeAsFileTime(). La exactitud depende del hardware del equipo y de la versión de Windows en las que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se esté ejecutando. La precisión de esta API se fija en 100 nanosegundos. La precisión se puede determinar mediante la API de Windows GetSystemTimeAdjustment().
  
|Función|Sintaxis|Valor devuelto|Tipo de datos devuelto|Determinismo|  
|---|---|---|---|---|
|[SYSDATETIME](../../t-sql/functions/sysdatetime-transact-sql.md)|SYSDATETIME ()|Devuelve un **datetime2(7)** valor que contiene la fecha y hora del equipo en el que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está ejecutando. El ajuste de zona horaria no está incluido.|**datetime2(7)**|No determinista|  
|[SYSDATETIMEOFFSET](../../t-sql/functions/sysdatetimeoffset-transact-sql.md)|SYSDATETIMEOFFSET ( )|Devuelve un **datetimeoffset(7)** valor que contiene la fecha y hora del equipo en el que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está ejecutando. El ajuste de zona horaria está incluido.|**DateTimeOffset(7)**|No determinista|  
|[SYSUTCDATETIME](../../t-sql/functions/sysutcdatetime-transact-sql.md)|SYSUTCDATETIME ( )|Devuelve un **datetime2(7)** valor que contiene la fecha y hora del equipo en el que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está ejecutando. La fecha y hora se devuelven como hora UTC (hora Universal).|**datetime2(7)**|No determinista|  
  
#### <a name="lower-precision--system-date-and-time-functions"></a>Funciones de fecha y hora del sistema de precisión baja
  
|Función|Sintaxis|Valor devuelto|Tipo de datos devuelto|Determinismo|  
|---|---|---|---|---|
|[CURRENT_TIMESTAMP](../../t-sql/functions/current-timestamp-transact-sql.md)|CURRENT_TIMESTAMP|Devuelve un **datetime** valor que contiene la fecha y hora del equipo en el que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está ejecutando. El ajuste de zona horaria no está incluido.|**datetime**|No determinista|  
|[GETDATE](../../t-sql/functions/getdate-transact-sql.md)|GETDATE ( )|Devuelve un **datetime** valor que contiene la fecha y hora del equipo en el que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está ejecutando. El ajuste de zona horaria no está incluido.|**datetime**|No determinista|  
|[GETUTCDATE](../../t-sql/functions/getutcdate-transact-sql.md)|GETUTCDATE ( )|Devuelve un **datetime** valor que contiene la fecha y hora del equipo en el que la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está ejecutando. La fecha y hora se devuelven como hora UTC (hora Universal).|**datetime**|No determinista|  
  
###  <a name="GetDateandTimeParts"></a>Funciones que obtienen partes de fecha y hora
  
|Función|Sintaxis|Valor devuelto|Tipo de datos devuelto|Determinismo|  
|--------------|------------|------------------|----------------------|-----------------|  
|[DATENAME](../../t-sql/functions/datename-transact-sql.md)|DATENAME ( *datepart* , *fecha* )|Devuelve una cadena de caracteres que representa el parámetro *datepart* de la fecha especificada.|**nvarchar**|No determinista|  
|[DATEPART](../../t-sql/functions/datepart-transact-sql.md)|DATEPART ( *datepart* , *fecha* )|Devuelve un entero que representa el parámetro *datepart* del elemento especificado *fecha*.|**int**|No determinista|  
|[DÍA](../../t-sql/functions/day-transact-sql.md)|DÍA ( *fecha* )|Devuelve un entero que representa la parte del día del elemento especificado *fecha*.|**int**|Determinista|  
|[MES](../../t-sql/functions/month-transact-sql.md)|MES ( *fecha* )|Devuelve un entero que representa la parte del mes de un determinado *fecha*.|**int**|Determinista|  
|[AÑO](../../t-sql/functions/year-transact-sql.md)|AÑO ( *fecha* )|Devuelve un entero que representa la parte del año de un *fecha*.|**int**|Determinista|  
  
###  <a name="fromParts"></a>Funciones que obtienen valores de fecha y hora de sus partes
  
|Función|Sintaxis|Valor devuelto|Tipo de datos devuelto|Determinismo|  
|---|---|---|---|---|
|[DATEFROMPARTS](../../t-sql/functions/datefromparts-transact-sql.md)|DATEFROMPARTS ( *año*, *mes*, *día* )|Devuelve un **fecha** valor para el año, mes y día.|**date**|Determinista|  
|[DATETIME2FROMPARTS](../../t-sql/functions/datetime2fromparts-transact-sql.md)|DATETIME2FROMPARTS ( *año*, *mes*, *día*, *hora*, *minuto*, *segundos* , *fracciones*, *precisión*)|Devuelve un **datetime2** valor para la fecha y hora especificadas y con la precisión especificada.|**datetime2 (** *precisión* **)**|Determinista|  
|[DATETIMEFROMPARTS](../../t-sql/functions/datetimefromparts-transact-sql.md)|DATETIMEFROMPARTS ( *año*, *mes*, *día*, *hora*, *minuto*, *segundos* , *milisegundos*)|Devuelve un **datetime** valor para la fecha y hora especificadas.|**datetime**|Determinista|  
|[DATETIMEOFFSETFROMPARTS](../../t-sql/functions/datetimeoffsetfromparts-transact-sql.md)|DATETIMEOFFSETFROMPARTS ( *año*, *mes*, *día*, *hora*, *minuto*,  *segundos*, *fracciones*, *hour_offset*, *minute_offset*, *precisión*)|Devuelve un **datetimeoffset** valor para la fecha y hora especificadas y con los desplazamientos especificados y la precisión.|**fecha y hora (** *precisión* **)**|Determinista|  
|[SMALLDATETIMEFROMPARTS](../../t-sql/functions/smalldatetimefromparts-transact-sql.md)|SMALLDATETIMEFROMPARTS ( *año*, *mes*, *día*, *hora*, *minuto* )|Devuelve un **smalldatetime** valor para la fecha y hora especificadas.|**smalldatetime**|Determinista|  
|[TIMEFROMPARTS](../../t-sql/functions/timefromparts-transact-sql.md)|TIMEFROMPARTS ( *hora*, *minuto*, *segundos*, *fracciones*, *precisión* )|Devuelve un **tiempo** valor durante el tiempo especificado y con la precisión especificada.|**tiempo (** *precisión* **)**|Determinista|  
  
###  <a name="GetDateandTimeDifference"></a>Funciones que obtienen la diferencia de fecha y hora
  
|Función|Sintaxis|Valor devuelto|Tipo de datos devuelto|Determinismo|  
|---|---|---|---|---|
|[DATEDIFF](../../t-sql/functions/datediff-transact-sql.md)|DATEDIFF ( *datepart* , *startdate* , *enddate* )|Devuelve el número de fecha u hora *datepart* los límites que se cruzan entre dos fechas especificadas.|**int**|Determinista|  
|[DATEDIFF_BIG](../../t-sql/functions/datediff-big-transact-sql.md)|DATEDIFF_BIG ( *datepart* , *startdate* , *enddate* )|Devuelve el número de fecha u hora *datepart* los límites que se cruzan entre dos fechas especificadas.|**bigint**|Determinista|  
  
###  <a name="ModifyDateandTimeValues"></a>Funciones que modifican los valores de fecha y hora
  
|Función|Sintaxis|Valor devuelto|Tipo de datos devuelto|Determinismo|  
|---|---|---|---|---|
|[DATEADD](../../t-sql/functions/dateadd-transact-sql.md)|DATEADD (*datepart* , *número* , *fecha* )|Devuelve un nuevo **datetime** valor agregando un intervalo a especificado *datepart* del elemento especificado *fecha*.|Tipo de datos de la *fecha* argumento|Determinista|  
|[EOMONTH](../../t-sql/functions/eomonth-transact-sql.md)|EOMONTH ( *start_date* [, *month_to_add* ])|Devuelve el último día del mes que contiene la fecha especificada, con un desplazamiento opcional.|Tipo de valor devuelto es el tipo de *start_date* o **fecha**.|Determinista|  
|[SWITCHOFFSET](../../t-sql/functions/switchoffset-transact-sql.md)|CONMUTADOR*desplazamiento* (*DATETIMEOFFSET* , *valor time_zone*)|CONMUTADOR*desplazamiento* cambia el ajuste de zona horaria de un valor DATETIMEOFFSET y conserva el valor de hora UTC.|**DateTimeOffset** con la precisión fraccionaria de los *DATETIMEOFFSET*|Determinista|  
|[TODATETIMEOFFSET](../../t-sql/functions/todatetimeoffset-transact-sql.md)|TODATETIMEOFFSET (*expresión* , *valor time_zone*)|TODATETIMEOFFSET transforma un valor datetime2 en un valor datetimeoffset. El valor datetime2 se interpreta en la hora local para el valor time_zone especificado.|**DateTimeOffset** con la precisión fraccionaria de los *datetime* argumento|Determinista|  
  
###  <a name="SetorGetSessionFormatFunctions"></a>Funciones que obtienen o establecen sesiones de formato
  
|Función|Sintaxis|Valor devuelto|Tipo de datos devuelto|Determinismo|  
|---|---|---|---|---|
|[@@DATEFIRST](../../t-sql/functions/datefirst-transact-sql.md)|@@DATEFIRST|Devuelve el valor actual, para la sesión, de SET DATEFIRST.|**tinyint**|No determinista|  
|[SET DATEFIRST](../../t-sql/statements/set-datefirst-transact-sql.md)|SET DATEFIRST { *número* &#124;  **@**  *number_var* }|Establece el primer día de la semana en un número del 1 al 7.|No aplicable|No aplicable|  
|[SET DATEFORMAT](../../t-sql/statements/set-dateformat-transact-sql.md)|SET DATEFORMAT { *formato* &#124;  **@**  *format_var* }|Establece el orden de la fecha (mes/día/año) para escribir **datetime** o **smalldatetime** datos.|No aplicable|No aplicable|  
|[@@LANGUAGE](../../t-sql/functions/language-transact-sql.md)|@@LANGUAGE|Devuelve el nombre del idioma que se está utilizando actualmente. @@LANGUAGE no es una función de fecha u hora. Sin embargo, la configuración de idioma puede afectar a la salida de las funciones de fecha.|No aplicable|No aplicable|  
|[DEFINIR IDIOMA](../../t-sql/statements/set-language-transact-sql.md)|SET LANGUAGE {[N] **'***lenguaje***'** &#124;  **@**  *language_var* }|Establece el entorno del idioma de la sesión y los mensajes del sistema. SET LANGUAGE no es ninguna función de fecha u hora. Sin embargo, la configuración de idioma afecta a la salida de las funciones de fecha.|No aplicable|No aplicable|  
|[sp_helplanguage](../../relational-databases/system-stored-procedures/sp-helplanguage-transact-sql.md)|**sp_helplanguage** [[  **@language =** ] **'***lenguaje***'** ]|Devuelve información sobre los formatos de fecha de todos los idiomas compatibles. **sp_helplanguage** no es una fecha u hora procedimiento almacenado. Sin embargo, la configuración de idioma afecta a la salida de las funciones de fecha.|No aplicable|No aplicable|  
  
###  <a name="ValidateDateandTimeValues"></a>Funciones que validan valores de fecha y hora
  
|Función|Sintaxis|Valor devuelto|Tipo de datos devuelto|Determinismo|  
|---|---|---|---|---|
|[ISDATE](../../t-sql/functions/isdate-transact-sql.md)|ISDATE ( *expresión* )|Determina si un **datetime** o **smalldatetime** expresión de entrada es un valor de hora o fecha válida.|**int**|ISDATE solo es determinista si se utiliza con la función CONVERT, cuando se especifica el parámetro de estilo CONVERT y cuando el estilo no es igual a 0, 100, 9 ni 109.|  
  
##  <a name="DateandTimeRelatedTopics"></a>Fecha y temas relacionados con el tiempo 
  
|Tema|Description|  
|-----------|-----------------|  
|[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)|Proporciona información sobre la conversión de los valores de fecha y hora de literales de cadena y otros formatos de fecha y hora.|  
|[Escribir instrucciones Transact-SQL internacionales](../../relational-databases/collations/write-international-transact-sql-statements.md)|Proporciona directrices para la portabilidad de bases de datos y las aplicaciones de base de datos que utilizan [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones de un idioma a otro, o que admiten varios idiomas.|  
|[Funciones escalares de ODBC &#40; Transact-SQL &#41;](../../t-sql/functions/odbc-scalar-functions-transact-sql.md)|Proporciona información acerca de funciones escalares de ODBC que pueden utilizarse en [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucciones. Esto incluye las funciones de fecha y hora ODBC.|  
|[EN la zona HORARIA &#40; Transact-SQL &#41;](../../t-sql/queries/at-time-zone-transact-sql.md)|Proporciona la conversión de zona horaria.|  
  
## <a name="see-also"></a>Vea también
[Funciones](../../t-sql/functions/functions.md)  
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  

