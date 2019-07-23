---
title: Estructura SSVARIANT | Microsoft Docs
description: Estructura de SSVARIANT en el controlador de OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 09ff4af7026ce75a8668db22910e550dc0c72857
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67995168"
---
# <a name="ssvariant-structure"></a>Estructura SSVARIANT
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  La estructura **SSVARIANT** , que se define en msoledbsql. h, corresponde a un valor DBTYPE_SQLVARIANT en el controlador de OLE DB para SQL Server.  
  
 **SSVARIANT** es una Unión discriminadora. Según el valor del miembro vt, el consumidor puede determinar qué miembro tiene que leerse. Los valores de vt se corresponden con tipos de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por tanto, la estructura **SSVARIANT** puede contener cualquier tipo de SQL Server. Para obtener más información sobre la estructura de datos para los tipos de OLE DB estándar, vea [indicadores de tipo](https://go.microsoft.com/fwlink/?LinkId=122171).  
  
## <a name="remarks"></a>Notas  
 Cuando DataTypeCompat==80, varios subtipos **SSVARIANT** se convierten en cadenas. Por ejemplo, los siguientes valores de vt se mostrarán en **SSVARIANT** como VT_SS_WVARSTRING:  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 Cuando DateTypeCompat == 0, estos tipos se mostrarán en su forma nativa.  
  
 Para obtener más información sobre SSPROP_INIT_DATATYPECOMPATIBILITY, consulte [usar palabras clave de cadena de conexión con OLE DB controlador para SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md).  
  
 El archivo msoledbsql.h contiene macros de acceso a tipos de datos variant que simplifican la eliminación de referencias a los tipos de miembro de la estructura **SSVARIANT**. Un ejemplo sería V_SS_DATETIMEOFFSET, que puede utilizarse tal y como se indica a continuación:  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 Para obtener el conjunto completo de macros de acceso para cada miembro de la estructura **SSVARIANT** , consulte el archivo msoledbsql. h.  
  
 En la tabla siguiente, se describen los miembros de la estructura **SSVARIANT**:  
  
|Miembro|Indicador de tipo OLE DB|Tipo de datos de OLE DB C|Valor de vt|Comentarios|  
|------------|---------------------------|------------------------|--------------|--------------|  
|vt|SSVARTYPE|||Especifica el tipo de valor incluido en la estructura **SSVARIANT**.|  
|bTinyIntVal|DBTYPE_UI1|**BYTE**|**VT_SS_UI1**|Admite el tipo de datos **tinyint** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|sShortIntVal|DBTYPE_I2|**SHORT**|**VT_SS_I2**|Admite el tipo de datos **smallint** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|lIntVal|DBTYPE_I4|**LONG**|**VT_SS_I4**|Admite el tipo de datos **int** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|llBigIntVal|DBTYPE_I8|**LARGE_INTEGER**|**VT_SS_I8**|Admite el tipo de datos **BIGINT** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|fltRealVal|DBTYPE_R4|**float**|**VT_SS_R4**|Admite el tipo de datos **real** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|dblFloatVal|DBTYPE_R8|**double**|**VT_SS_R8**|Admite el tipo de datos **float** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|cyMoneyVal|DBTYPE_CY|**LARGE_INTEGER**|**VT_SS_MONEY VT_SS_SMALLMONEY**|Admite los tipos de datos **Money** y **smallmoney** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|fBitVal|DBTYPE_BOOL|**VARIANT_BOOL**|**VT_SS_BIT**|Admite el tipo de datos **bit** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|rgbGuidVal|DBTYPE_GUID|**GUID**|**VT_SS_GUID**|Admite el tipo de datos **uniqueidentifier** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|numNumericVal|DBTYPE_NUMERIC|**DB_NUMERIC**|**VT_SS_NUMERIC**|Admite el tipo de datos **Numeric** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|dDateVal|DBTYPE_DATE|**DBDATE**|**VT_SS_DATE**|Admite el tipo de datos **date**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2**|Admite los tipos de datos **smalldatetime**, **DateTime**y **datetime2** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|Time2Val|DBTYPE_DBTIME2|**DBTIME2**|**VT_SS_TIME2**|Admite el tipo de datos **Time** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .<br /><br /> Incluye los miembros siguientes:<br /><br /> *tTime2Val* (**DBTIME2**)<br /><br /> *bScale* (**Byte**) Especifica la escala para el valor de *tTime2Val* .|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_DATETIME2**|Admite el tipo de datos **datetime2** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .<br /><br /> Incluye los miembros siguientes:<br /><br /> *tsDataTimeVal* (DBTIMESTAMP)<br /><br /> *bScale* (**Byte**) Especifica la escala para el valor de *tsDataTimeVal* .|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|**DBTIMESTAMPOFFSET**|**VT_SS_DATETIMEOFFSET**|Admite el tipo de datos **DateTimeOffset** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .<br /><br /> Incluye los miembros siguientes:<br /><br /> *tsoDateTimeOffsetVal* (**DBTIMESTAMPOFFSET**)<br /><br /> *bScale* (**Byte**) Especifica la escala para el valor de *tsoDateTimeOffsetVal* .|  
|NCharVal|No hay indicador de tipo OLE DB correspondiente.|**struct _NCharVal**|**VT_SS_WVARSTRING,**<br /><br /> **VT_SS_WSTRING**|Admite los tipos de datos **nchar** y **nvarchar** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .<br /><br /> Incluye los miembros siguientes:<br /><br /> *sActualLength* (**Short**) Especifica la longitud real de la cadena a la que apunta *pwchNCharVal* . No incluye cero de terminación.<br /><br /> *sMaxLength* (**Short**) Especifica la longitud máxima de la cadena a la que apunta *pwchNCharVal* .<br /><br /> *pwchNCharVal* (**WCHAR** \*) puntero a la cadena.<br /><br /> Miembros no usados: *rgbReserved*, *dwReserved*y *pwchReserved*.|  
|CharVal|No hay indicador de tipo OLE DB correspondiente.|**struct _CharVal**|**VT_SS_STRING,**<br /><br /> **VT_SS_VARSTRING**|Admite los tipos de datos **Char** y **VARCHAR** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .<br /><br /> Incluye los miembros siguientes:<br /><br /> *sActualLength* (**Short**) Especifica la longitud real de la cadena a la que apunta *pchCharVal* . No incluye cero de terminación.<br /><br /> *sMaxLength* (**Short**) Especifica la longitud máxima de la cadena a la que apunta *pchCharVal* .<br /><br /> *pchCharVal* (**Char** \*) puntero en la cadena.<br /><br /> Miembros no usados:<br /><br /> *rgbReserved*, *dwReserved*y *pwchReserved*.|  
|BinaryVal|No hay indicador de tipo OLE DB correspondiente.|**struct _BinaryVal**|**VT_SS_VARBINARY,**<br /><br /> **VT_SS_BINARY**|Admite los tipos de datos **Binary** y **varbinary** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .<br /><br /> Incluye los miembros siguientes:<br /><br /> *sActualLength* (**Short**) Especifica la longitud real de los datos a los que apunta *prgbBinaryVal* .<br /><br /> *sMaxLength* (**Short**) Especifica la longitud máxima de los datos a los que apunta *prgbBinaryVal* .<br /><br /> *prgbBinaryVal* Puntero (**byte** \*) a los datos binarios.<br /><br /> Miembro no usado: *dwReserved*.|  
|TipoDesconocido|No se usa|No se usa|No se usa|No se usa|  
|BLOBType|No se usa|No se usa|No se usa|No se usa|  
  
## <a name="see-also"></a>Consulte también  
 [Tipos &#40;de datos OLE DB&#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  
