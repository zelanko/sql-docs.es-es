---
title: Estructura SSVARIANT | Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3dffb546620f7a67f3dc8502d7a8e8b389d9ae7b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68128491"
---
# <a name="ssvariant-structure"></a>Estructura SSVARIANT
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El **SSVARIANT** estructura, que se define en sqlncli.h, corresponde a un valor DBTYPE_SQLVARIANT en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de cliente nativo.  
  
 **SSVARIANT** es una unión de discriminación. Según el valor del miembro vt, el consumidor puede determinar qué miembro tiene que leerse. Los valores de vt se corresponden con tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por tanto, la estructura **SSVARIANT** puede contener cualquier tipo de SQL Server. Para obtener más información sobre la estructura de datos para los tipos OLE DB estándar, consulte [indicadores de tipo](https://go.microsoft.com/fwlink/?LinkId=122171).  
  
## <a name="remarks"></a>Comentarios  
 Cuando DataTypeCompat==80, varios subtipos **SSVARIANT** se convierten en cadenas. Por ejemplo, los siguientes valores de vt se mostrarán en **SSVARIANT** como VT_SS_WVARSTRING:  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 Cuando DateTypeCompat == 0, estos tipos se mostrarán en su forma nativa.  
  
 Para obtener más información acerca de SSPROP_INIT_DATATYPECOMPATIBILITY, vea [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 El archivo sqlncli.h contiene macros de acceso variant que simplifican la desreferenciación de los tipos de miembro en el **SSVARIANT** estructura. Un ejemplo sería V_SS_DATETIMEOFFSET, que puede utilizarse tal y como se indica a continuación:  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 Para el conjunto completo de macros de acceso para cada miembro de la **SSVARIANT** estructura, consulte el archivo sqlncli.hi.  
  
 En la tabla siguiente, se describen los miembros de la estructura **SSVARIANT**:  
  
|Member|Indicador de tipo OLE DB|Tipo de datos de OLE DB C|Valor de vt|Comentarios|  
|------------|---------------------------|------------------------|--------------|--------------|  
|vt|SSVARTYPE|||Especifica el tipo de valor incluido en la estructura **SSVARIANT**.|  
|bTinyIntVal|DBTYPE_UI1|**BYTE**|**VT_SS_UI1**|Admite la **tinyint** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.|  
|sShortIntVal|DBTYPE_I2|**SHORT**|**VT_SS_I2**|Admite la **smallint** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.|  
|lIntVal|DBTYPE_I4|**LONG**|**VT_SS_I4**|Admite la **int** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.|  
|llBigIntVal|DBTYPE_I8|**LARGE_INTEGER**|**VT_SS_I8**|Admite la **bigint** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.|  
|fltRealVal|DBTYPE_R4|**float**|**VT_SS_R4**|Admite la **real** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.|  
|dblFloatVal|DBTYPE_R8|**double**|**VT_SS_R8**|Admite la **float** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.|  
|cyMoneyVal|DBTYPE_CY|**LARGE_INTEGER**|**VT_SS_MONEY VT_SS_SMALLMONEY**|Admite la **dinero** y **smallmoney** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos.|  
|fBitVal|DBTYPE_BOOL|**VARIANT_BOOL**|**VT_SS_BIT**|Admite la **bit** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.|  
|rgbGuidVal|DBTYPE_GUID|**GUID**|**VT_SS_GUID**|Admite la **uniqueidentifier** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.|  
|numNumericVal|DBTYPE_NUMERIC|**DB_NUMERIC**|**VT_SS_NUMERIC**|Admite la **numérico** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.|  
|dDateVal|DBTYPE_DATE|**DBDATE**|**VT_SS_DATE**|Admite el tipo de datos **date**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2**|Admite la **smalldatetime**, **datetime**, y **datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos.|  
|Time2Val|DBTYPE_DBTIME2|**DBTIME2**|**VT_SS_TIME2**|Admite la **tiempo** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.<br /><br /> Incluye los miembros siguientes:<br /><br /> *tTime2Val* (**DBTIME2**)<br /><br /> *bScale* (**bytes**) especifica la escala para *tTime2Val* valor.|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_DATETIME2**|Admite la **datetime2** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.<br /><br /> Incluye los miembros siguientes:<br /><br /> *tsDataTimeVal* (DBTIMESTAMP)<br /><br /> *bScale* (**bytes**) especifica la escala para *tsDataTimeVal* valor.|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|**DBTIMESTAMPOFFSET**|**VT_SS_DATETIMEOFFSET**|Admite la **datetimeoffset** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos.<br /><br /> Incluye los miembros siguientes:<br /><br /> *tsoDateTimeOffsetVal* (**DBTIMESTAMPOFFSET**)<br /><br /> *bScale* (**bytes**) especifica la escala para *tsoDateTimeOffsetVal* valor.|  
|NCharVal|No hay indicador de tipo OLE DB correspondiente.|**struct _NCharVal**|**VT_SS_WVARSTRING,**<br /><br /> **VT_SS_WSTRING**|Admite la **nchar** y **nvarchar** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos.<br /><br /> Incluye los miembros siguientes:<br /><br /> *sActualLength* (**corto**) especifica la longitud real de la cadena a la que *pwchNCharVal* puntos. No incluye cero de terminación.<br /><br /> *sMaxLength* (**corto**) especifica la longitud máxima de la cadena a la que *pwchNCharVal* puntos.<br /><br /> *pwchNCharVal* (**WCHAR** \*) puntero a la cadena.<br /><br /> Miembros no usados: *rgbReserved*, *dwReservado*, y *pwchReserved*.|  
|CharVal|No hay indicador de tipo OLE DB correspondiente.|**struct _CharVal**|**VT_SS_STRING,**<br /><br /> **VT_SS_VARSTRING**|Admite la **char** y **varchar** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos.<br /><br /> Incluye los miembros siguientes:<br /><br /> *sActualLength* (**corto**) especifica la longitud real de la cadena a la que *pchCharVal* puntos. No incluye cero de terminación.<br /><br /> *sMaxLength* (**corto**) especifica la longitud máxima de la cadena a la que *pchCharVal* puntos.<br /><br /> *pchCharVal* (**CHAR** \*) puntero a la cadena.<br /><br /> Miembros no usados:<br /><br /> *rgbReserved*, *dwReservado*, y *pwchReserved*.|  
|BinaryVal|No hay indicador de tipo OLE DB correspondiente.|**struct _BinaryVal**|**VT_SS_VARBINARY,**<br /><br /> **VT_SS_BINARY**|Admite la **binario** y **varbinary** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos.<br /><br /> Incluye los miembros siguientes:<br /><br /> *sActualLength* (**corto**) especifica la longitud real de los datos a la que *prgbBinaryVal* puntos.<br /><br /> *sMaxLength* (**corto**) especifica la longitud máxima de los datos a la que *prgbBinaryVal* puntos.<br /><br /> *prgbBinaryVal* (**bytes** \*) puntero a los datos binarios.<br /><br /> Miembro no usado: *dwReservado*.|  
|TipoDesconocido|No se usa|No se usa|No se usa|No se usa|  
|BLOBType|No se usa|No se usa|No se usa|No se usa|  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
  
