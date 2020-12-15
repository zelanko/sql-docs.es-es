---
title: Compatibilidad de tipos, fecha y hora de ODBC
description: Obtenga información sobre los tipos ODBC que admiten SQL Server tipos de datos de fecha y hora, incluidos los formatos y la asignación de tipos de datos para cadenas, literales y estructuras de datos.
ms.custom: ''
ms.date: 12/18/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- date/time [ODBC], data type support
- ODBC, date/time improvements
ms.assetid: 8e0d9ba2-3ec1-4680-86e3-b2590ba8e2e9
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9b886ac6a15930146fedda1d6ee336234fc6cf57
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97438591"
---
# <a name="data-type-support-for-odbc-date-and-time-improvements"></a>Compatibilidad con tipos de datos para mejoras de fecha y hora de ODBC
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  En este tema se proporciona información sobre los tipos ODBC compatibles con los tipos de datos de fecha y hora de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="data-type-mapping-in-parameters-and-resultsets"></a>Asignación de tipos de datos en parámetros y conjuntos de resultados  
 Además de los tipos de datos de ODBC (SQL_TYPE_TIMESTAMP y SQL_TIMESTAMP), se han agregado dos nuevos tipos de datos en ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para exponer los nuevos tipos de servidor:  
  
-   SQL_SS_TIME2  
  
-   SQL_SS_TIMESTAMPOFFSET  
  
 La tabla siguiente muestra la asignación completa servidor-tipo. Observe que algunas celdas de la tabla contienen dos entradas; en esos casos, el primero es el valor de ODBC 3.0 y el segundo es el valor de ODBC 2.0.  
  
|Tipos de datos de SQL Server|Tipo de datos de SQL|Value|  
|--------------------------|-------------------|-----------|  
|Datetime|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|93 (sql.h)<br /><br /> 11 (sqlext.h)|  
|Smalldatetime|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|93 (sql.h)<br /><br /> 11 (sqlext.h)|  
|Fecha|SQL_TYPE_DATE<br /><br /> SQL_DATE|91 (SQL. h)<br /><br /> 9 (sqlext. h)|  
|Time|SQL_SS_TIME2|-154 (SQLNCLI. h)|  
|DatetimeOFFSET|SQL_SS_TIMESTAMPOFFSET|-155 (SQLNCLI.h)|  
|Datetime2|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|93 (sql.h)<br /><br /> 11 (sqlext.h)|  
||||

 En la tabla siguiente se enumeran las estructuras y los tipos C de ODBC correspondientes. Puesto que ODBC no permite tipos C definidos por el controlador, se utiliza SQL_C_BINARY para time y datetimeoffset como estructuras binarias.  
  
|Tipo de datos de SQL|Diseño de memoria|Tipo de datos C predeterminado|Valor (sqlext.h)|  
|-------------------|-------------------|-------------------------|------------------------|  
|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|SQL_TIMESTAMP_STRUCT<br /><br /> TIMESTAMP_STRUCT|SQL_C_TYPE_TIMESTAMP<br /><br /> SQL_C_TIMESTAMP|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|  
|SQL_TYPE_DATE<br /><br /> SQL_DATE|SQL_DATE_STRUCT<br /><br /> DATE_STRUCT|SQL_C_TYPE_DATE<br /><br /> SQL_C_DATE|SQL_TYPE_DATE<br /><br /> SQL_DATE|  
|SQL_SS_TIME2|SQL_SS_TIME2_STRUCT|SQL_C_SS_TIME2<br /><br /> SQL_C_BINARY (ODBC 3.5 y anteriores)|0x4000 (sqlncli.h)<br /><br /> SQL_BINARY (-2)|  
|SQL_SS_TIMESTAMPOFFSET|SQL_SS_TIMESTAMPOFFSET_STRUCT|SQL_C_SS_TIMESTAMPOFFSET<br /><br /> SQL_C_BINARY (ODBC 3.5 y anteriores)|0x4001 (sqlncli.h)<br /><br /> SQL_BINARY (-2)|  
|||||

 Cuando se especifica el enlace SQL_C_BINARY, se comprueba la alineación y se genera un error para notificar que la alineación es incorrecta. El SQLSTATE para este error será IM016, con un mensaje del tipo "Alineación de estructura incorrecta".  
  
## <a name="data-formats-strings-and-literals"></a>Formatos de datos: Cadenas y literales  
 En la tabla siguiente se muestran las asignaciones entre tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tipos de datos de ODBC y literales de cadena de ODBC.  
  
|Tipos de datos de SQL Server|Tipo de datos de ODBC|Formato de cadena para conversiones de cliente|  
|--------------------------|--------------------|------------------------------------------|  
|Datetime|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|'aaaa-mm-dd hh:mm:ss[.999]'<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite hasta tres dígitos de la fracción de segundo para Datetime.|  
|Smalldatetime|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|'yyyy-mm-dd hh:hh:ss'<br /><br /> Este tipo de datos tiene una precisión de un minuto. El componente de segundos será cero en salida y será redondeado por el servidor al producir los resultados.|  
|Fecha|SQL_TYPE_DATE<br /><br /> SQL_DATE|'aaaa-mm-dd'|  
|Time|SQL_SS_TIME2|'hh:mm:ss[.9999999]'<br /><br /> Las fracciones de segundo se pueden especificar si se desea utilizando hasta siete dígitos.|  
|Datetime2|SQL_TYPE_TIMESTAMP<br /><br /> SQL_TIMESTAMP|' AAAA-MM-DD HH: mm: SS [. 9999999] '<br /><br /> Las fracciones de segundo se pueden especificar si se desea utilizando hasta siete dígitos.|  
|DatetimeOFFSET|SQL_SS_TIMESTAMPOFFSET|'yyyy-mm-dd hh:mm:ss[.9999999] +/- hh:mm'<br /><br /> Las fracciones de segundo se pueden especificar si se desea utilizando hasta siete dígitos.|  
||||

 No hay ningún cambio en las secuencias de escape de ODBC para los literales de fecha y hora.  
  
 Las fracciones de segundo de los resultados siempre utilizan un punto (.), en lugar de dos puntos (:).  
  
 Los valores de cadena devueltos a las aplicaciones siempre tienen la misma longitud para una columna determinada. Los componentes de año, mes, día, hora, minuto y segundo se rellenan con ceros a la izquierda hasta su ancho máximo, y en los valores datetime hay un espacio entre la fecha y la hora. En los valores datetimeoffset también hay un espacio entre la hora y el ajuste de zona horaria. Un ajuste de zona horaria va siempre precedido de un signo; si el ajuste es cero, el signo es más (+). Las fracciones de segundo se rellenan con ceros a la derecha si es necesario, hasta la precisión definida para la columna. Para las columnas datetime, hay tres dígitos de fracciones de segundo. Para las columnas smalldatetime, no hay dígitos de fracciones de segundo y los segundos siempre serán cero.  
  
 Una cadena vacía no es un literal válido de fecha y hora y no representa un valor NULL. Un intento de convertir una cadena vacía en un valor de fecha y hora producirá el error SQLState 22018 y el mensaje "Valor de carácter no válido para especificación cast".  
  
 Las conversiones a partir de parámetros de cadena esperarán cadenas en el mismo formato, con la excepción de que el signo de una zona horaria con cero horas y cero minutos puede ser más o menos, y se permiten ceros a la derecha para las fracciones de segundo hasta un máximo de 9 dígitos. Un componente de hora puede finalizar con un separador decimal y ningún dígito para las fracciones de segundo.  
  
 Actualmente, el controlador permite un espacio en blanco adicional en torno a los caracteres de puntuación y el espacio entre la hora y el ajuste de zona horaria es opcional. Sin embargo, esto puede cambiar en una versión futura; las aplicaciones no deben basarse en el comportamiento actual.  
  
## <a name="data-formats-data-structures"></a>Formatos de datos: Estructuras de datos  
 En las estructuras descritas a continuación, ODBC especifica las restricciones siguientes, que se toman del calendario gregoriano:  
  
-   El intervalo de meses va de 1 a 12.  
  
-   El intervalo de campos de día va de 1 al número de días del mes y debe ser coherente con los campos de año y de mes, teniendo en cuenta los años bisiestos.  
  
-   El intervalo de fechas va de 0 a 23.  
  
-   El intervalo de minutos va de 0 a 59.  
  
-   El intervalo de segundos es de 0 a 61.9(n). Esto permite incluir hasta dos segundos intercalares para mantener la sincronización con el tiempo sidéreo.  
  
     Tenga en cuenta que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite segundos intercalares, de modo que los valores de segundos superiores a 59 producirán un error de servidor.  
  
 Las implementaciones de las siguientes estructuras existentes de ODBC se han modificado para admitir los nuevos tipos de datos de fecha y hora de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Las definiciones, sin embargo, no han cambiado.  
  
-   DATE_STRUCT  
  
-   TIME_STRUCT  
  
-   TIMESTAMP_STRUCT  
  
 Hay también dos nuevas estructuras:  
  
-   SQL_SS_TIME2_STRUCT  
  
-   SQL_SS_TIMESTAMPOFFSET_STRUCT  
  
### <a name="sql_ss_time2_struct"></a>SQL_SS_TIME2_STRUCT  
 Esta estructura se rellena hasta los 12 bytes en sistemas operativos de 32 bits y 64 bits.  
  
```cpp
typedef struct tagSS_TIME2_STRUCT {  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
   SQLUINTEGER fraction;  
} SQL_SS_TIME2_STRUCT;  
```  
  
### <a name="sql_ss_timestampoffset_struct"></a>SQL_SS_TIMESTAMPOFFSET_STRUCT  
  
```cpp
typedef struct tagSS_TIMESTAMPOFFSET_STRUCT {  
   SQLSMALLINT year;  
   SQLUSMALLINT month;  
   SQLUSMALLINT day;  
   SQLUSMALLINT hour;  
   SQLUSMALLINT minute;  
   SQLUSMALLINT second;  
   SQLUINTEGER fraction;  
   SQLSMALLINT timezone_hour;  
   SQLSMALLINT timezone_minute;  
} SQL_SS_TIMESTAMPOFFSET_STRUCT;  
```  
  
 Si el **timezone_hour** es negativo, el **timezone_minute** debe ser negativo o cero. Si el **timezone_hour** es positivo, el **timezone_minute** debe ser positivo o cero. Si el **timezone_hour** es cero, el **timezone_minute** puede tener cualquier valor comprendido entre-59 y + 59.  
  
## <a name="see-also"></a>Consulte también  
 [Mejoras de fecha y hora &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
