---
title: Estructura SSVARIANT | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
ms.assetid: d13c6aa6-bd49-467a-9093-495df8f1e2d9
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3877e7b8c6ccd0d5364b3aea291facb1799bff7d
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705104"
---
# <a name="ssvariant-structure"></a>Estructura SSVARIANT
  La estructura `SSVARIANT`, que se define en sqlncli.h, corresponde a un valor DBTYPE_SQLVARIANT en el proveedor OLEDB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 `SSVARIANT` es una unión de discriminación. Según el valor del miembro vt, el consumidor puede determinar qué miembro tiene que leerse. Los valores de vt se corresponden con tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por lo tanto, la estructura `SSVARIANT` puede contener cualquier tipo de SQL Server. Para más información sobre la estructura de datos de los tipos de OLE DB estándar, consulte [Indicadores de tipo](https://go.microsoft.com/fwlink/?LinkId=122171).  
  
## <a name="remarks"></a>Observaciones  
 Cuando DataTypeCompat==80, varios subtipos `SSVARIANT` se convierten en cadenas. Por ejemplo, los siguientes valores de vt se mostrarán en `SSVARIANT` como VT_SS_WVARSTRING:  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 Cuando DateTypeCompat == 0, estos tipos se mostrarán en su forma nativa.  
  
 Para obtener más información acerca de SSPROP_INIT_DATATYPECOMPATIBILITY, vea [usar palabras clave de cadena de conexión con SQL Server Native Client](../native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 El archivo sqlncli.h contiene macros de acceso a tipos de datos variant que simplifican la eliminación de referencias a los tipos de miembro de la estructura `SSVARIANT`. Un ejemplo sería V_SS_DATETIMEOFFSET, que puede utilizarse tal y como se indica a continuación:  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 Para obtener el conjunto completo de macros de acceso para cada miembro de la estructura `SSVARIANT`, consulte el archivo sqlncli.hi.  
  
 En la siguiente tabla se describen los miembros de la estructura `SSVARIANT`:  
  
|Miembro|Indicador de tipo OLE DB|Tipo de datos de OLE DB C|Valor de vt|Comentarios|  
|------------|---------------------------|------------------------|--------------|--------------|  
|vt|SSVARTYPE|||Especifica el tipo de valor incluido en la estructura `SSVARIANT`.|  
|bTinyIntVal|DBTYPE_UI1|`BYTE`|`VT_SS_UI1`|Admite el tipo de datos `tinyint`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|sShortIntVal|DBTYPE_I2|`SHORT`|`VT_SS_I2`|Admite el tipo de datos `smallint`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|lIntVal|DBTYPE_I4|`LONG`|`VT_SS_I4`|Admite el tipo de datos `int`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|llBigIntVal|DBTYPE_I8|`LARGE_INTEGER`|`VT_SS_I8`|Admite el tipo de datos `bigint`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|fltRealVal|DBTYPE_R4|`float`|`VT_SS_R4`|Admite el tipo de datos `real`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|dblFloatVal|DBTYPE_R8|`double`|`VT_SS_R8`|Admite el tipo de datos `float`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|cyMoneyVal|DBTYPE_CY|`LARGE_INTEGER`|**VT_SS_MONEY VT_SS_SMALLMONEY**|Admite los `money` tipos de datos y **smallmoney** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|fBitVal|DBTYPE_BOOL|`VARIANT_BOOL`|`VT_SS_BIT`|Admite el tipo de datos `bit`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|rgbGuidVal|DBTYPE_GUID|`GUID`|`VT_SS_GUID`|Admite el tipo de datos `uniqueidentifier`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|numNumericVal|DBTYPE_NUMERIC|`DB_NUMERIC`|`VT_SS_NUMERIC`|Admite el tipo de datos `numeric`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|dDateVal|DBTYPE_DATE|`DBDATE`|`VT_SS_DATE`|Admite el tipo de datos `date`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|`DBTIMESTAMP`|`VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2`|Admite los tipos de datos `smalldatetime`, `datetime` y `datetime2`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Time2Val|DBTYPE_DBTIME2|`DBTIME2`|`VT_SS_TIME2`|Admite el tipo de datos `time`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Incluye los miembros siguientes:<br /><br /> *tTime2Val* ( `DBTIME2` )<br /><br /> *bScale* ( `BYTE` ) especifica la escala para el valor de *tTime2Val* .|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|`DBTIMESTAMP`|`VT_SS_DATETIME2`|Admite el tipo de datos `datetime2`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Incluye los miembros siguientes:<br /><br /> *tsDataTimeVal* (DBTIMESTAMP)<br /><br /> *bScale* ( `BYTE` ) especifica la escala para el valor de *tsDataTimeVal* .|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|`DBTIMESTAMPOFFSET`|`VT_SS_DATETIMEOFFSET`|Admite el tipo de datos `datetimeoffset`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br /> Incluye los miembros siguientes:<br /><br /> *tsoDateTimeOffsetVal* ( `DBTIMESTAMPOFFSET` )<br /><br /> *bScale* ( `BYTE` ) especifica la escala para el valor de *tsoDateTimeOffsetVal* .|  
|NCharVal|No hay indicador de tipo OLE DB correspondiente.|`struct _NCharVal`|`VT_SS_WVARSTRING,`<br /><br /> `VT_SS_WSTRING`|Admite los `nchar` tipos de datos y **nvarchar** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Incluye los miembros siguientes:<br /><br /> *sActualLength* ( `SHORT` ) especifica la longitud real de la cadena a la que apunta *pwchNCharVal* . No incluye cero de terminación.<br /><br /> *sMaxLength* ( `SHORT` ) especifica la longitud máxima de la cadena a la que apunta *pwchNCharVal* .<br /><br /> puntero *pwchNCharVal* ( `WCHAR` \* ) a la cadena.<br /><br /> Miembros no usados: *rgbReserved*, *dwReserved*y *pwchReserved*.|  
|CharVal|No hay indicador de tipo OLE DB correspondiente.|`struct _CharVal`|`VT_SS_STRING,`<br /><br /> `VT_SS_VARSTRING`|Admite los `char` tipos de datos y **VARCHAR** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Incluye los miembros siguientes:<br /><br /> *sActualLength* ( `SHORT` ) especifica la longitud real de la cadena a la que apunta *pchCharVal* . No incluye cero de terminación.<br /><br /> *sMaxLength* ( `SHORT` ) especifica la longitud máxima de la cadena a la que apunta *pchCharVal* .<br /><br /> puntero *pchCharVal* ( `CHAR` \* ) a la cadena.<br /><br /> Miembros no usados:<br /><br /> *rgbReserved*, *dwReserved* y *pwchReserved*.|  
|BinaryVal|No hay indicador de tipo OLE DB correspondiente.|`struct _BinaryVal`|`VT_SS_VARBINARY,`<br /><br /> `VT_SS_BINARY`|Admite los `binary` tipos de datos y **varbinary** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Incluye los miembros siguientes:<br /><br /> *sActualLength* ( `SHORT` ) especifica la longitud real de los datos a los que apunta *prgbBinaryVal* .<br /><br /> *sMaxLength* ( `SHORT` ) especifica la longitud máxima de los datos a los que apunta *prgbBinaryVal* .<br /><br /> puntero *prgbBinaryVal* ( `BYTE` \* ) a los datos binarios.<br /><br /> Miembro no usado: *dwReserved*.|  
|TipoDesconocido|No se usa|No se usa|No se usa|No se usa|  
|BLOBType|No se usa|No se usa|No se usa|No se usa|  
  
## <a name="see-also"></a>Consulte también  
 [Tipos de datos &#40;OLE DB&#41;](data-types-ole-db.md)  
  
  
