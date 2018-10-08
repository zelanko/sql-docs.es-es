---
title: Estructura SSVARIANT | Microsoft Docs
description: Estructura SSVARIANT en el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: d17aae38a8cc95ce4a602fed1a241327eec0a9d8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47632823"
---
# <a name="ssvariant-structure"></a>Estructura SSVARIANT
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  El **SSVARIANT** estructura, que se define en msoledbsql.h, corresponde a un valor DBTYPE_SQLVARIANT en el controlador OLE DB para SQL Server.  
  
 **SSVARIANT** es una unión de discriminación. Según el valor del miembro vt, el consumidor puede determinar qué miembro tiene que leerse. Los valores de vt se corresponden con tipos de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por tanto, la estructura **SSVARIANT** puede contener cualquier tipo de SQL Server. Para obtener más información sobre la estructura de datos para los tipos OLE DB estándar, consulte [indicadores de tipo](http://go.microsoft.com/fwlink/?LinkId=122171).  
  
## <a name="remarks"></a>Notas  
 Cuando DataTypeCompat==80, varios subtipos **SSVARIANT** se convierten en cadenas. Por ejemplo, los siguientes valores de vt se mostrarán en **SSVARIANT** como VT_SS_WVARSTRING:  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 Cuando DateTypeCompat == 0, estos tipos se mostrarán en su forma nativa.  
  
 Para obtener más información acerca de SSPROP_INIT_DATATYPECOMPATIBILITY, vea [Using Connection String Keywords con el controlador OLE DB para SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md).  
  
 El archivo msoledbsql.h contiene macros de acceso a tipos de datos variant que simplifican la eliminación de referencias a los tipos de miembro de la estructura **SSVARIANT**. Un ejemplo sería V_SS_DATETIMEOFFSET, que puede utilizarse tal y como se indica a continuación:  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 Para el conjunto completo de macros de acceso para cada miembro de la **SSVARIANT** estructura, consulte el archivo msoledbsql.h.  
  
 En la tabla siguiente, se describen los miembros de la estructura **SSVARIANT**:  
  
|Miembro|Indicador de tipo OLE DB|Tipo de datos de OLE DB C|Valor de vt|Comentarios|  
|------------|---------------------------|------------------------|--------------|--------------|  
|VT|SSVARTYPE|||Especifica el tipo de valor incluido en la estructura **SSVARIANT**.|  
|bTinyIntVal|DBTYPE_UI1|**BYTE**|**VT_SS_UI1**|Admite la **tinyint** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de datos.|  
|sShortIntVal|DBTYPE_I2|**SHORT**|**VT_SS_I2**|Admite la **smallint** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de datos.|  
|lIntVal|DBTYPE_I4|**LONG**|**VT_SS_I4**|Admite la **int** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de datos.|  
|llBigIntVal|DBTYPE_I8|**LARGE_INTEGER**|**VT_SS_I8**|Admite la **bigint** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de datos.|  
|fltRealVal|DBTYPE_R4|**float**|**VT_SS_R4**|Admite la **real** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de datos.|  
|dblFloatVal|DBTYPE_R8|**double**|**VT_SS_R8**|Admite la **float** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de datos.|  
|cyMoneyVal|DBTYPE_CY|**LARGE_INTEGER**|**VT_SS_MONEY VT_SS_SMALLMONEY**|Admite la **dinero** y **smallmoney** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de datos.|  
|fBitVal|DBTYPE_BOOL|**VARIANT_BOOL**|**VT_SS_BIT**|Admite la **bit** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de datos.|  
|rgbGuidVal|DBTYPE_GUID|**GUID**|**VT_SS_GUID**|Admite la **uniqueidentifier** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de datos.|  
|numNumericVal|DBTYPE_NUMERIC|**DB_NUMERIC**|**VT_SS_NUMERIC**|Admite la **numérico** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de datos.|  
|dDateVal|DBTYPE_DATE|**DBDATE**|**VT_SS_DATE**|Admite el tipo de datos **date**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2**|Admite la **smalldatetime**, **datetime**, y **datetime2** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de datos.|  
|Time2Val|DBTYPE_DBTIME2|**DBTIME2**|**VT_SS_TIME2**|Admite la **tiempo** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de datos.<br /><br /> Incluye los miembros siguientes:<br /><br /> *tTime2Val* (**DBTIME2**)<br /><br /> *bScale* (**bytes**) especifica la escala para *tTime2Val* valor.|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_DATETIME2**|Admite la **datetime2** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de datos.<br /><br /> Incluye los miembros siguientes:<br /><br /> *tsDataTimeVal* (DBTIMESTAMP)<br /><br /> *bScale* (**bytes**) especifica la escala para *tsDataTimeVal* valor.|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|**DBTIMESTAMPOFFSET**|**VT_SS_DATETIMEOFFSET**|Admite la **datetimeoffset** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de datos.<br /><br /> Incluye los miembros siguientes:<br /><br /> *tsoDateTimeOffsetVal* (**DBTIMESTAMPOFFSET**)<br /><br /> *bScale* (**bytes**) especifica la escala para *tsoDateTimeOffsetVal* valor.|  
|NCharVal|No hay indicador de tipo OLE DB correspondiente.|**struct _NCharVal**|**VT_SS_WVARSTRING,**<br /><br /> **VT_SS_WSTRING**|Admite la **nchar** y **nvarchar** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de datos.<br /><br /> Incluye los miembros siguientes:<br /><br /> *sActualLength* (**corto**) especifica la longitud real de la cadena a la que *pwchNCharVal* puntos. No incluye cero de terminación.<br /><br /> *sMaxLength* (**corto**) especifica la longitud máxima de la cadena que *pwchNCharVal* puntos.<br /><br /> *pwchNCharVal* (**WCHAR** \*) puntero a la cadena.<br /><br /> Miembros no usados: *rgbReserved*, *dwReservado*, y *pwchReserved*.|  
|CharVal|No hay indicador de tipo OLE DB correspondiente.|**struct _CharVal**|**VT_SS_STRING,**<br /><br /> **VT_SS_VARSTRING**|Admite la **char** y **varchar** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de datos.<br /><br /> Incluye los miembros siguientes:<br /><br /> *sActualLength* (**corto**) especifica la longitud real de la cadena a la que *pchCharVal* puntos. No incluye cero de terminación.<br /><br /> *sMaxLength* (**corto**) especifica la longitud máxima de la cadena a la que *pchCharVal* puntos.<br /><br /> *pchCharVal* (**CHAR** \*) puntero a la cadena.<br /><br /> Miembros no usados:<br /><br /> *rgbReserved*, *dwReservado*, y *pwchReserved*.|  
|BinaryVal|No hay indicador de tipo OLE DB correspondiente.|**struct _BinaryVal**|**VT_SS_VARBINARY,**<br /><br /> **VT_SS_BINARY**|Admite la **binario** y **varbinary** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de datos.<br /><br /> Incluye los miembros siguientes:<br /><br /> *sActualLength* (**corto**) especifica la longitud real de los datos a la que *prgbBinaryVal* puntos.<br /><br /> *sMaxLength* (**corto**) especifica la longitud máxima de los datos a la que *prgbBinaryVal* puntos.<br /><br /> *prgbBinaryVal* (**bytes** \*) puntero a los datos binarios.<br /><br /> Miembro no usado: *dwReservado*.|  
|TipoDesconocido|No se usa|No se usa|No se usa|No se usa|  
|BLOBType|No se usa|No se usa|No se usa|No se usa|  
  
## <a name="see-also"></a>Ver también  
 [Tipos de datos &#40;OLE DB&#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  
