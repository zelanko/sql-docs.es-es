---
title: Compatibilidad con tipos de datos para mejoras de fecha y hora de OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], data type support
- OLE DB, date/time improvements
ms.assetid: d40e3fd6-9057-4371-8236-95cef300603e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 82d8de1aa71507b8d1397befc287041def1ab839
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "76929542"
---
# <a name="data-type-support-for-ole-db-date-and-time-improvements"></a>Compatibilidad con tipos de datos para mejoras de fecha y hora de OLE DB
  En este tema se proporciona información sobre los tipos OLE DB ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client) que admiten tipos de datos de fecha y hora [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="data-type-mapping-in-rowsets-and-parameters"></a>Asignar tipos de datos en conjuntos de filas y parámetros  
 OLE DB proporciona dos nuevos tipos de datos para admitir los nuevos tipos de servidor: DBTYPE_DBTIME2 y DBTYPE_DBTIMESTAMPOFFSET. La tabla siguiente muestra la asignación completa de tipo de servidor:  
  
|Tipo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Tipo de datos de OLE DB|Value|  
|-----------------------------------------|----------------------|-----------|  
|datetime|DBTYPE_DBTIMESTAMP|135 (oledb.h)|  
|smalldatetime|DBTYPE_DBTIMESTAMP|135 (oledb.h)|  
|date|DBTYPE_DBDATE|133 (oledb.h)|  
|time|DBTYPE_DBTIME2|145 (SQLNCLI. h)|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|146 (SQLNCLI. h)|  
|datetime2|DBTYPE_DBTIMESTAMP|135 (oledb.h)|  
  
## <a name="data-formats-strings-and-literals"></a>Formatos de datos: Cadenas y literales  
  
|Tipo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Tipo de datos de OLE DB|Formato de cadena para conversiones de cliente|  
|-----------------------------------------|----------------------|------------------------------------------|  
|datetime|DBTYPE_DBTIMESTAMP|'aaaa-mm-dd hh:mm:ss[.999]'<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite hasta tres dígitos de la fracción de segundo para Datetime.|  
|smalldatetime|DBTYPE_DBTIMESTAMP|'aaaa-mm-dd hh:mm:ss'<br /><br /> Este tipo de datos tiene una precisión de un minuto. El componente de segundos será cero en salida y será redondeado por el servidor al producir los resultados.|  
|date|DBTYPE_DBDATE|'aaaa-mm-dd'|  
|time|DBTYPE_DBTIME2|'hh:mm:ss[.9999999]'<br /><br /> Las fracciones de segundo se pueden especificar si se desea utilizando hasta siete dígitos.|  
|datetime2|DBTYPE_DBTIMESTAMP|'aaaa-mm-dd hh:mm:ss[.fffffff]'<br /><br /> Las fracciones de segundo se pueden especificar si se desea utilizando hasta siete dígitos.|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|'aaaa-mm-dd hh:mm:ss[.fffffff] +/-hh:mm'<br /><br /> Las fracciones de segundo se pueden especificar si se desea utilizando hasta siete dígitos.|  
  
 No hay ningún cambio en las secuencias de escape para los literales de fecha y hora.  
  
 Las fracciones de segundo de los resultados utilizan un punto (.), en lugar de dos puntos (:).  
  
 Los valores de cadena devueltos a las aplicaciones siempre tendrán la misma longitud para una columna determinada. Los componentes de año, mes, día, hora, minuto y segundo se rellenarán con ceros a la izquierda hasta su ancho máximo. Habrá exactamente un espacio entre la fecha y la hora, y exactamente un espacio entre la hora y el ajuste de zona horaria. Un ajuste de zona horaria siempre irá precedido de un signo. Este signo será un más (+) cuando el desplazamiento sea cero. No habrá ningún espacio en blanco entre el signo y el valor de desplazamiento. Las fracciones de segundo se rellenarán con ceros finales, si es necesario, hasta la precisión definida para la columna, pero no más. Para las columnas datetime, habrá tres dígitos de fracciones de segundo. Para las columnas de smalldatetime, no habrá dígitos de fracciones de segundo y los segundos siempre serán cero.  
  
 Las conversiones de los valores de cadena proporcionados por la aplicación serán más flexibles y permitirán valores de componente menores que el ancho máximo. Los años pueden ser de 1-4 dígitos. Los meses, días, horas, minutos y segundos pueden tener 1 o 2 dígitos. Puede haber espacio en blanco arbitrario entre los ajustes de fecha/hora y de hora/zona horaria. El signo de un ajuste con cero horas y cero minutos puede ser más o menos. Se permiten ceros finales para las fracciones de segundo hasta un máximo de 9 dígitos. Un componente de hora puede finalizar con un separador decimal y ningún dígito para las fracciones de segundo.  
  
 Una cadena vacía no es un literal válido de fecha y hora y no representa un valor NULL. Un intento para convertir una cadena vacía en un valor de fecha y hora producirá errores con SQLState 22018 y el mensaje "Valor de carácter no válido para especificación cast".  
  
## <a name="data-formats-data-structures"></a>Formatos de datos: Estructuras de datos  
 En las estructuras específicas de OLE DB descritas a continuación, OLE DB cumple las mismas restricciones que ODBC. Se toman del calendario Gregoriano:  
  
-   El intervalo de meses va de 1 a 12.  
  
-   El intervalo de campos de día va de 1 al número de días del mes y debe ser coherente con los campos de año y de mes, teniendo en cuenta los años bisiestos.  
  
-   El intervalo de fechas va de 0 a 23.  
  
-   El intervalo de minutos va de 0 a 59.  
  
-   El intervalo de segundos va de 0 a 59. Esto permite incluir hasta dos segundos intercalares para mantener la sincronización con el tiempo sidéreo.  
  
 Las implementaciones de las siguientes estructuras existentes de OLE DB se han modificado para admitir los nuevos tipos de datos de fecha y hora de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Las definiciones, sin embargo, no han cambiado.  
  
-   DBTYPE_DATE (Es un tipo DATE de automatización. Se representa internamente como `double`.. La parte entera es el número de días transcurridos desde el 30 de diciembre de 1899 y la parte decimal es una fracción de un día. Este tipo tiene una exactitud de 1 segundo, de modo que tiene una escala efectiva de 0.)  
  
-   DBTYPE_DBDATE  
  
-   DBTYPE_DBTIME  
  
-   DBTYPE_DBTIMESTAMP (OLE DB define el campo de fracción como el número de milmillonésimas de segundo (nanosegundos) y va de 0 a 999.999.999)  
  
-   DBTYPE_FILETIME  
  
### <a name="dbtype_dbtime2"></a>DBTYPE_DBTIME2  
 Esta estructura se rellena hasta los 12 bytes en sistemas operativos de 32 bits y 64 bits.  
  
```  
typedef struct tagDBTIME2 {  
    USHORT hour;  
    USHORT minute;  
    USHORT second;  
    ULONG fraction;  
    } DBTIME2;  
```  
  
### <a name="dbtype_-dbtimestampoffset"></a>DBTYPE_ DBTIMESTAMPOFFSET  
  
```  
typedef struct tagDBTIMESTAMPOFFSET {  
    SHORT year;  
    USHORT month;  
    USHORT day;  
    USHORT hour;  
    USHORT minute;  
    USHORT second;  
    ULONG fraction;  
    SHORT timezone_hour;  
    SHORT timezone_minute;  
    } DBTIMESTAMPOFFSET;  
```  
  
 Si `timezone_hour` es negativo, `timezone_minute` debe ser negativo o cero. Si `timezone_hour` es positivo, `timezone minute` debe ser positivo o cero. Si `timezone_hour` es cero, `timezone minute` puede contener un valor entre -59 y +59.  
  
### <a name="ssvariant"></a>SSVARIANT  
 Esta estructura incluye a partir de ahora las nuevas estructuras DBTYPE_DBTIME2 y DBTYPE_DBTIMESTAMPOFFSET, y agrega la escala de fracciones de segundo para los tipos adecuados.  
  
```  
struct SSVARIANT {  
   SSVARTYPE vt;  
   DWORD dwReserved1;  
   DWORD dwReserved2;  
   union {  
// ...  
      DBTIMESTAMP tsDateTimeVal;  
      DBDATE dDateVal;  
      struct _Time2Val {  
         DBTIME2 tTime2Val;  
         BYTE bScale;  
      } Time2Val;  
      struct _DateTimeVal {  
         DBTIMESTAMP tsDateTimeVal;  
         BYTE bScale;  
      } DateTimeVal;  
      struct _DateTimeOffsetVal {   
         DBTIMESTAMPOFFSET tsoDateTimeOffsetVal;  
         BYTE bScale;  
      } DateTimeOffsetVal;  
// ...  
   };  
};  
```  
  
 Además, la enumeración asociada con la codificación de tipo SSVARIANT, que determina el tipo de enumeración, se extenderá como sigue:  
  
```  
enum SQLVARENUM {  
// ...  
   // Datetime  
   VT_SS_DATETIME      = DBTYPE_DBTIMESTAMP,  
   VT_SS_SMALLDATETIME = 206,  
  
   VT_SS_DATE = DBTYPE_DBDATE,  
   VT_SS_TIME2 = DBTYPE_DBTIME2,  
   VT_SS_DATETIME2 = 212  
   VT_SS_DATETIMEOFFSET = DBTYPE_DBTIMESTAMPOFFSET  
};  
```  
  
 Las aplicaciones que migran a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client y utilizan `sql_variant`, y que se apoyan en la precisión limitada de `datetime` tendrán que actualizarse si el esquema subyacente está actualizado para utilizar `datetime2` en lugar de `datetime`.  
  
 Las macros de acceso para SSVARIANT también se han extendido con la adición de lo siguiente:  
  
```  
#define V_SS_DATETIME2(X)       V_SS_UNION(X, DateTimeVal)  
#define V_SS_TIME2(X)           V_SS_UNION(X, Time2Val)  
#define V_SS_DATE(X)            V_SS_UNION(X, dDateVal)  
#define V_SS_DATETIMEOFFSET(X)  V_SS_UNION(X, DateTimeOffsetVal)  
```  
  
## <a name="data-type-mapping-in-itabledefinitioncreatetable"></a>Asignar tipo de datos en ITableDefinition::CreateTable  
 La siguiente asignación de tipos se usa con las estructuras DBCOLUMNDESC que se emplean en ITableDefinition::CreateTable:  
  
|Tipo de datos de OLE DB (*wType*)|Tipo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Notas|  
|----------------------------------|-----------------------------------------|-----------|  
|DBTYPE_DBDATE|date||  
|DBTYPE_DBTIMESTAMP|`datetime2`(p)|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client inspecciona el miembro *bScale* de miembros para determinar la precisión de las fracciones de segundo.|  
|DBTYPE_DBTIME2|`time`(p)|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client inspecciona el miembro *bScale* de miembros para determinar la precisión de las fracciones de segundo.|  
|DBTYPE_DBTIMESTAMPOFFSET|`datetimeoffset`(p)|El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client inspecciona el miembro *bScale* de miembros para determinar la precisión de las fracciones de segundo.|  
  
 Cuando una aplicación especifica DBTYPE_DBTIMESTAMP en *wType*, puede invalidar la asignación a `datetime2` proporcionando un nombre de tipo en *pwszTypeName*. Si `datetime` se especifica, *bScale* debe ser 3. Si `smalldatetime` se especifica, *bScale* debe ser 0. Si *bScale* no es coherente con *wType* y *pwszTypeName*, se devuelve DB_E_BADSCALE.  
  
## <a name="see-also"></a>Consulte también  
 [Mejoras de fecha y hora &#40;OLE DB&#41;](date-and-time-improvements-ole-db.md)  
  
  
