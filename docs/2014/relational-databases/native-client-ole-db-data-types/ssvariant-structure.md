---
title: Estructura SSVARIANT | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
ms.assetid: d13c6aa6-bd49-467a-9093-495df8f1e2d9
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8c8d98a54155179fe481fc0a7202a07e6cbf2aff
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198231"
---
# <a name="ssvariant-structure"></a>Estructura SSVARIANT
  La estructura `SSVARIANT`, que se define en sqlncli.h, corresponde a un valor DBTYPE_SQLVARIANT en el proveedor OLEDB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 `SSVARIANT` es una unión de discriminación. Dependiendo del valor del miembro vt, el consumidor puede determinar qué miembro para leer. valores de VT se corresponden con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos. Por lo tanto, la estructura `SSVARIANT` puede contener cualquier tipo de SQL Server. Para obtener más información acerca de la estructura de datos para los tipos de OLE DB estándares, consulte [indicadores de tipo](http://go.microsoft.com/fwlink/?LinkId=122171).  
  
## <a name="remarks"></a>Notas  
 Cuando DataTypeCompat==80, varios subtipos `SSVARIANT` se convierten en cadenas. Por ejemplo, los siguientes valores de vt se mostrarán en `SSVARIANT` como VT_SS_WVARSTRING:  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 Cuando DateTypeCompat == 0, estos tipos se mostrarán en su forma nativa.  
  
 Para obtener más información acerca de SSPROP_INIT_DATATYPECOMPATIBILITY, vea [Using Connection String Keywords with SQL Server Native Client](../native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 El archivo sqlncli.h contiene macros de acceso a tipos de datos variant que simplifican la eliminación de referencias a los tipos de miembro de la estructura `SSVARIANT`. Un ejemplo sería V_SS_DATETIMEOFFSET, que puede utilizarse tal y como se indica a continuación:  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 Para obtener el conjunto completo de macros de acceso para cada miembro de la estructura `SSVARIANT`, consulte el archivo sqlncli.hi.  
  
 En la siguiente tabla se describen los miembros de la estructura `SSVARIANT`:  
  
|Miembro|Indicador de tipo OLE DB|Tipo de datos de OLE DB C|Valor de vt|Comentarios|  
|------------|---------------------------|------------------------|--------------|--------------|  
|VT|SSVARTYPE|||Especifica el tipo de valor incluido en la estructura `SSVARIANT`.|  
|bTinyIntVal|DBTYPE_UI1|`BYTE`|`VT_SS_UI1`|Admite la `tinyint` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.|  
|sShortIntVal|DBTYPE_I2|`SHORT`|`VT_SS_I2`|Admite la `smallint` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.|  
|lIntVal|DBTYPE_I4|`LONG`|`VT_SS_I4`|Admite la `int` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.|  
|llBigIntVal|DBTYPE_I8|`LARGE_INTEGER`|`VT_SS_I8`|Admite la `bigint` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.|  
|fltRealVal|DBTYPE_R4|`float`|`VT_SS_R4`|Admite la `real` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.|  
|dblFloatVal|DBTYPE_R8|`double`|`VT_SS_R8`|Admite la `float` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.|  
|cyMoneyVal|DBTYPE_CY|`LARGE_INTEGER`|**VT_SS_MONEY VT_SS_SMALLMONEY**|Admite la `money` y **smallmoney** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos.|  
|fBitVal|DBTYPE_BOOL|`VARIANT_BOOL`|`VT_SS_BIT`|Admite la `bit` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.|  
|rgbGuidVal|DBTYPE_GUID|`GUID`|`VT_SS_GUID`|Admite la `uniqueidentifier` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.|  
|numNumericVal|DBTYPE_NUMERIC|`DB_NUMERIC`|`VT_SS_NUMERIC`|Admite la `numeric` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.|  
|dDateVal|DBTYPE_DATE|`DBDATE`|`VT_SS_DATE`|Admite la `date` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|`DBTIMESTAMP`|`VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2`|Admite la `smalldatetime`, `datetime`, y `datetime2` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos.|  
|Time2Val|DBTYPE_DBTIME2|`DBTIME2`|`VT_SS_TIME2`|Admite la `time` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.<br /><br /> Incluye los miembros siguientes:<br /><br /> *tTime2Val* (`DBTIME2`)<br /><br /> *bScale* (`BYTE`) especifica la escala para *tTime2Val* valor.|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|`DBTIMESTAMP`|`VT_SS_DATETIME2`|Admite la `datetime2` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.<br /><br /> Incluye los miembros siguientes:<br /><br /> *tsDataTimeVal* (DBTIMESTAMP)<br /><br /> *bScale* (`BYTE`) especifica la escala para *tsDataTimeVal* valor.|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|`DBTIMESTAMPOFFSET`|`VT_SS_DATETIMEOFFSET`|Admite la `datetimeoffset` [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.<br /><br /> Incluye los miembros siguientes:<br /><br /> *tsoDateTimeOffsetVal* (`DBTIMESTAMPOFFSET`)<br /><br /> *bScale* (`BYTE`) especifica la escala para *tsoDateTimeOffsetVal* valor.|  
|NCharVal|No hay indicador de tipo OLE DB correspondiente.|`struct _NCharVal`|`VT_SS_WVARSTRING,`<br /><br /> `VT_SS_WSTRING`|Admite la `nchar` y **nvarchar** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos.<br /><br /> Incluye los miembros siguientes:<br /><br /> *sActualLength* (`SHORT`) especifica la longitud real de la cadena a la que *pwchNCharVal* puntos. No incluye cero de terminación.<br /><br /> *sMaxLength* (`SHORT`) especifica la longitud máxima de la cadena a la que *pwchNCharVal* puntos.<br /><br /> *pwchNCharVal* (`WCHAR` \*) puntero a la cadena.<br /><br /> Miembros no usados: *rgbReserved*, *dwReservado*, y *pwchReserved*.|  
|CharVal|No hay indicador de tipo OLE DB correspondiente.|`struct _CharVal`|`VT_SS_STRING,`<br /><br /> `VT_SS_VARSTRING`|Admite la `char` y **varchar** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos.<br /><br /> Incluye los miembros siguientes:<br /><br /> *sActualLength* (`SHORT`) especifica la longitud real de la cadena a la que *pchCharVal* puntos. No incluye cero de terminación.<br /><br /> *sMaxLength* (`SHORT`) especifica la longitud máxima de la cadena a la que *pchCharVal* puntos.<br /><br /> *pchCharVal* (`CHAR` \*) puntero a la cadena.<br /><br /> Miembros no usados:<br /><br /> *rgbReserved*, *dwReservado*, y *pwchReserved*.|  
|BinaryVal|No hay indicador de tipo OLE DB correspondiente.|`struct _BinaryVal`|`VT_SS_VARBINARY,`<br /><br /> `VT_SS_BINARY`|Admite la `binary` y **varbinary** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos.<br /><br /> Incluye los miembros siguientes:<br /><br /> *sActualLength* (`SHORT`) especifica la longitud real de los datos a la que *prgbBinaryVal* puntos.<br /><br /> *sMaxLength* (`SHORT`) especifica la longitud máxima de los datos a la que *prgbBinaryVal* puntos.<br /><br /> *prgbBinaryVal* (`BYTE` \*) puntero a los datos binarios.<br /><br /> Miembro no usado: *dwReservado*.|  
|UnknownType|No se usa|No se usa|No se usa|No se usa|  
|BLOBType|No se usa|No se usa|No se usa|No se usa|  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos &#40;OLE DB&#41;](data-types-ole-db.md)  
  
  