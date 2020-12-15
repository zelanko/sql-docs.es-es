---
description: Estructura SSVARIANT en SQL Server Native Client
title: Estructura SSVARIANT (proveedor de OLE DB de Native Client)
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
ms.assetid: d13c6aa6-bd49-467a-9093-495df8f1e2d9
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c081f415ad651ac48d033f298dd8f50064f3b982
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467676"
---
# <a name="ssvariant-structure-in-sql-server-native-client"></a>Estructura SSVARIANT en SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  La estructura **SSVARIANT** , que se define en SQLNCLI. h, corresponde a un valor DBTYPE_SQLVARIANT en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLEDB de Native Client.  
  
 **SSVARIANT** es una unión de discriminación. Según el valor del miembro vt, el consumidor puede determinar qué miembro tiene que leerse. Los valores de vt se corresponden con tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por tanto, la estructura **SSVARIANT** puede contener cualquier tipo de SQL Server. Para más información sobre la estructura de datos de los tipos de OLE DB estándar, consulte [Indicadores de tipo](/previous-versions/windows/desktop/ms711251(v=vs.85)).  
  
## <a name="remarks"></a>Observaciones  
 Cuando DataTypeCompat==80, varios subtipos **SSVARIANT** se convierten en cadenas. Por ejemplo, los siguientes valores de vt se mostrarán en **SSVARIANT** como VT_SS_WVARSTRING:  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 Cuando DateTypeCompat == 0, estos tipos se mostrarán en su forma nativa.  
  
 Para obtener más información acerca de SSPROP_INIT_DATATYPECOMPATIBILITY, vea [usar palabras clave de cadena de conexión con SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 El archivo SQLNCLI. h contiene macros de acceso variantes que simplifican la desreferenciación de los tipos de miembro de la estructura **SSVARIANT** . Un ejemplo sería V_SS_DATETIMEOFFSET, que puede utilizarse tal y como se indica a continuación:  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 Para obtener el conjunto completo de macros de acceso para cada miembro de la estructura **SSVARIANT** , consulte el archivo SQLNCLI. HI.  
  
 En la tabla siguiente, se describen los miembros de la estructura **SSVARIANT**:  
  
|Member|Indicador de tipo OLE DB|Tipo de datos de OLE DB C|Valor de vt|Comentarios|  
|------------|---------------------------|------------------------|--------------|--------------|  
|vt|SSVARTYPE|||Especifica el tipo de valor incluido en la estructura **SSVARIANT**.|  
|bTinyIntVal|DBTYPE_UI1|**BYTE**|**VT_SS_UI1**|Admite el tipo de datos **tinyint**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|sShortIntVal|DBTYPE_I2|**SHORT**|**VT_SS_I2**|Admite el tipo de datos **smallint**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|lIntVal|DBTYPE_I4|**LONG**|**VT_SS_I4**|Admite el tipo de datos **int**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|llBigIntVal|DBTYPE_I8|**LARGE_INTEGER**|**VT_SS_I8**|Admite el tipo de datos **bigint**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|fltRealVal|DBTYPE_R4|**float**|**VT_SS_R4**|Admite el tipo de datos **real**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|dblFloatVal|DBTYPE_R8|**double**|**VT_SS_R8**|Admite el tipo de datos **float**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|cyMoneyVal|DBTYPE_CY|**LARGE_INTEGER**|**VT_SS_MONEY VT_SS_SMALLMONEY**|Admite los tipos de datos **money** y **smallmoney**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|fBitVal|DBTYPE_BOOL|**VARIANT_BOOL**|**VT_SS_BIT**|Admite el tipo de datos **bit**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|rgbGuidVal|DBTYPE_GUID|**GUID**|**VT_SS_GUID**|Admite el tipo de datos **uniqueidentifier**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|numNumericVal|DBTYPE_NUMERIC|**DB_NUMERIC**|**VT_SS_NUMERIC**|Admite el tipo de datos **numeric**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|dDateVal|DBTYPE_DATE|**DBDATE**|**VT_SS_DATE**|Admite el tipo de datos **date**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2**|Admite los tipos de datos **smalldatetime**, **datetime** y **datetime2**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|Time2Val|DBTYPE_DBTIME2|**DBTIME2**|**VT_SS_TIME2**|Admite el tipo de datos **time**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Incluye los miembros siguientes:<br /><br /> *tTime2Val* (**DBTIME2**)<br /><br /> *bScale* (**BYTE**) Especifica la escala del valor *tTime2Val*.|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_DATETIME2**|Admite el tipo de datos **datetime2**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Incluye los miembros siguientes:<br /><br /> *tsDataTimeVal* (DBTIMESTAMP)<br /><br /> *bScale* (**BYTE**) Especifica la escala del valor *tsDataTimeVal*.|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|**DBTIMESTAMPOFFSET**|**VT_SS_DATETIMEOFFSET**|Admite el tipo de datos **datetimeoffset**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Incluye los miembros siguientes:<br /><br /> *tsoDateTimeOffsetVal* (**DBTIMESTAMPOFFSET**)<br /><br /> *bScale* (**BYTE**) Especifica la escala del valor *tsoDateTimeOffsetVal*.|  
|NCharVal|No hay indicador de tipo OLE DB correspondiente.|**struct _NCharVal**|**VT_SS_WVARSTRING,**<br /><br /> **VT_SS_WSTRING**|Admite los tipos de datos **nchar** y **nvarchar**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Incluye los miembros siguientes:<br /><br /> *sActualLength* (**SHORT**) especifica la longitud real de la cadena a la que apunta *pwchNCharVal*. No incluye cero de terminación.<br /><br /> *sMaxLength* (**SHORT**) especifica la longitud máxima de la cadena a la que apunta *pwchNCharVal*.<br /><br /> *pwchNCharVal* (**WCHAR** \*) Puntero a la cadena.<br /><br /> Miembros no usados: *rgbReserved*, *dwReserved* y *pwchReserved*.|  
|CharVal|No hay indicador de tipo OLE DB correspondiente.|**struct _CharVal**|**VT_SS_STRING,**<br /><br /> **VT_SS_VARSTRING**|Admite los tipos de datos **char** y **varchar**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Incluye los miembros siguientes:<br /><br /> *sActualLength* (**SHORT**) especifica la longitud real de la cadena a la que apunta *pchCharVal*. No incluye cero de terminación.<br /><br /> *sMaxLength* (**SHORT**) especifica la longitud máxima de la cadena a la que apunta *pchCharVal*.<br /><br /> *pchCharVal* (**CHAR** \*) Puntero a la cadena.<br /><br /> Miembros no usados:<br /><br /> *rgbReserved*, *dwReserved* y *pwchReserved*.|  
|BinaryVal|No hay indicador de tipo OLE DB correspondiente.|**struct _BinaryVal**|**VT_SS_VARBINARY,**<br /><br /> **VT_SS_BINARY**|Admite los tipos de datos **binary** y **varbinary**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Incluye los miembros siguientes:<br /><br /> *sActualLength* (**SHORT**) especifica la longitud real de los datos a los que apunta *prgbBinaryVal*.<br /><br /> *sMaxLength* (**SHORT**) especifica la longitud máxima de los datos a los que apunta *prgbBinaryVal*.<br /><br /> *prgbBinaryVal* (**BYTE** \*) Puntero a los datos binarios.<br /><br /> Miembro no usado: *dwReserved*.|  
|TipoDesconocido|No se usa|No se usa|No se usa|No se usa|  
|BLOBType|No se usa|No se usa|No se usa|No se usa|  
  
## <a name="see-also"></a>Consulte también  
 [Tipos de datos &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
