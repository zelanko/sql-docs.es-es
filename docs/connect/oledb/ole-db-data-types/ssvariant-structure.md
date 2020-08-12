---
title: Estructura SSVARIANT | Microsoft Docs
description: Estructura SSVARIANT en OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
f1_keywords:
- SSVARIANT
helpviewer_keywords:
- SSVARIANT struct
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 0d11a6f839fba1905055aefafa65353008530f8d
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86004527"
---
# <a name="ssvariant-structure"></a>Estructura SSVARIANT
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  La estructura **SSVARIANT**, que se define en msoledbsql.h, corresponde a un valor DBTYPE_SQLVARIANT en OLE DB Driver for SQL Server.  
  
 **SSVARIANT** es una unión de discriminación. Según el valor del miembro vt, el consumidor puede determinar qué miembro tiene que leerse. Los valores de vt se corresponden con tipos de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por tanto, la estructura **SSVARIANT** puede contener cualquier tipo de SQL Server. Para más información sobre la estructura de datos de los tipos de OLE DB estándar, consulte [Indicadores de tipo](https://go.microsoft.com/fwlink/?LinkId=122171).  
  
## <a name="remarks"></a>Observaciones  
 Cuando DataTypeCompat==80, varios subtipos **SSVARIANT** se convierten en cadenas. Por ejemplo, los siguientes valores de vt se mostrarán en **SSVARIANT** como VT_SS_WVARSTRING:  
  
-   VT_SS_DATETIMEOFFSET  
  
-   VT_SS_DATETIME2  
  
-   VT_SS_TIME2  
  
-   VT_SS_DATE  
  
 Cuando DateTypeCompat == 0, estos tipos se mostrarán en su forma nativa.  
  
 Para más información sobre SSPROP_INIT_DATATYPECOMPATIBILITY, consulte [Uso de palabras clave de cadena de conexión con OLE DB Driver for SQL Server](../../oledb/applications/using-connection-string-keywords-with-oledb-driver-for-sql-server.md).  
  
 El archivo msoledbsql.h contiene macros de acceso a tipos de datos variant que simplifican la eliminación de referencias a los tipos de miembro de la estructura **SSVARIANT**. Un ejemplo sería V_SS_DATETIMEOFFSET, que puede utilizarse tal y como se indica a continuación:  
  
```  
memcpy(&V_SS_DATETIMEOFFSET(pssVar).tsoDateTimeOffsetVal, pDTO, cbNative);  
V_SS_DATETIMEOFFSET(pssVar).bScale = bScale;  
```  
  
 Para obtener el conjunto completo de macros de acceso para cada miembro de la estructura **SSVARIANT**, consulte el archivo msoledbsql.h.  
  
 En la tabla siguiente, se describen los miembros de la estructura **SSVARIANT**:  
  
|Member|Indicador de tipo OLE DB|Tipo de datos de OLE DB C|Valor de vt|Comentarios|  
|------------|---------------------------|------------------------|--------------|--------------|  
|vt|SSVARTYPE|||Especifica el tipo de valor incluido en la estructura **SSVARIANT**.|  
|bTinyIntVal|DBTYPE_UI1|**BYTE**|**VT_SS_UI1**|Admite el tipo de datos **tinyint**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|sShortIntVal|DBTYPE_I2|**SHORT**|**VT_SS_I2**|Admite el tipo de datos **smallint**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|lIntVal|DBTYPE_I4|**LONG**|**VT_SS_I4**|Admite el tipo de datos **int**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|llBigIntVal|DBTYPE_I8|**LARGE_INTEGER**|**VT_SS_I8**|Admite el tipo de datos **bigint**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|fltRealVal|DBTYPE_R4|**float**|**VT_SS_R4**|Admite el tipo de datos **real**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|dblFloatVal|DBTYPE_R8|**double**|**VT_SS_R8**|Admite el tipo de datos **float**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|cyMoneyVal|DBTYPE_CY|**LARGE_INTEGER**|**VT_SS_MONEY VT_SS_SMALLMONEY**|Admite los tipos de datos **money** y **smallmoney**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|fBitVal|DBTYPE_BOOL|**VARIANT_BOOL**|**VT_SS_BIT**|Admite el tipo de datos **bit**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|rgbGuidVal|DBTYPE_GUID|**GUID**|**VT_SS_GUID**|Admite el tipo de datos **uniqueidentifier**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|numNumericVal|DBTYPE_NUMERIC|**DB_NUMERIC**|**VT_SS_NUMERIC**|Admite el tipo de datos **numeric**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|dDateVal|DBTYPE_DATE|**DBDATE**|**VT_SS_DATE**|Admite el tipo de datos **date**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|tsDateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_SMALLDATETIME VT_SS_DATETIME VT_SS_DATETIME2**|Admite los tipos de datos **smalldatetime**, **datetime** y **datetime2**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|Time2Val|DBTYPE_DBTIME2|**DBTIME2**|**VT_SS_TIME2**|Admite el tipo de datos **time**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> Incluye los miembros siguientes:<br /><br /> *tTime2Val* (**DBTIME2**)<br /><br /> *bScale* (**BYTE**) Especifica la escala del valor *tTime2Val*.|  
|DateTimeVal|DBTYPE_DBTIMESTAMP|**DBTIMESTAMP**|**VT_SS_DATETIME2**|Admite el tipo de datos **datetime2**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> Incluye los miembros siguientes:<br /><br /> *tsDataTimeVal* (DBTIMESTAMP)<br /><br /> *bScale* (**BYTE**) Especifica la escala del valor *tsDataTimeVal*.|  
|DateTimeOffsetVal|DBTYPE_DBTIMESTAMPOFSET|**DBTIMESTAMPOFFSET**|**VT_SS_DATETIMEOFFSET**|Admite el tipo de datos **datetimeoffset**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> Incluye los miembros siguientes:<br /><br /> *tsoDateTimeOffsetVal* (**DBTIMESTAMPOFFSET**)<br /><br /> *bScale* (**BYTE**) Especifica la escala del valor *tsoDateTimeOffsetVal*.|  
|NCharVal|No hay indicador de tipo OLE DB correspondiente.|**struct _NCharVal**|**VT_SS_WVARSTRING,**<br /><br /> **VT_SS_WSTRING**|Admite los tipos de datos **nchar** y **nvarchar**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> Incluye los miembros siguientes:<br /><br /> *sActualLength* (**SHORT**) especifica la longitud real de la cadena a la que apunta *pwchNCharVal*. No incluye cero de terminación.<br /><br /> *sMaxLength* (**SHORT**) especifica la longitud máxima de la cadena a la que apunta *pwchNCharVal*.<br /><br /> *pwchNCharVal* (**WCHAR** \*) Puntero a la cadena.<br /><br /> *rgbReserved* (**BYTE[5]** ) Especifica la información de intercalación.<br /><br /> Miembros sin usar: *dwReserved* y *pwchReserved*.|  
|CharVal|No hay indicador de tipo OLE DB correspondiente.|**struct _CharVal**|**VT_SS_STRING,**<br /><br /> **VT_SS_VARSTRING**|Admite los tipos de datos **char** y **varchar**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> Incluye los miembros siguientes:<br /><br /> *sActualLength* (**SHORT**) especifica la longitud real de la cadena a la que apunta *pchCharVal*. No incluye cero de terminación.<br /><br /> *sMaxLength* (**SHORT**) especifica la longitud máxima de la cadena a la que apunta *pchCharVal*.<br /><br /> *pchCharVal* (**CHAR** \*) Puntero a la cadena.<br /><br /> *rgbReserved* (**BYTE[5]** ) Especifica la información de intercalación.<br /><br /> Miembros no usados:<br /><br /> *dwReserved* y *pwchReserved*.|  
|BinaryVal|No hay indicador de tipo OLE DB correspondiente.|**struct _BinaryVal**|**VT_SS_VARBINARY,**<br /><br /> **VT_SS_BINARY**|Admite los tipos de datos **binary** y **varbinary**[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> Incluye los miembros siguientes:<br /><br /> *sActualLength* (**SHORT**) especifica la longitud real de los datos a los que apunta *prgbBinaryVal*.<br /><br /> *sMaxLength* (**SHORT**) especifica la longitud máxima de los datos a los que apunta *prgbBinaryVal*.<br /><br /> *prgbBinaryVal* (**BYTE** \*) Puntero a los datos binarios.<br /><br /> Miembro no usado: *dwReserved*.|  
|TipoDesconocido|No se usa|No se usa|No se usa|No se usa|  
|BLOBType|No se usa|No se usa|No se usa|No se usa|  
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |
  
## <a name="known-issues"></a>Problemas conocidos
### <a name="possible-narrow-string-data-corruption"></a>Posibles daños en los datos de cadena de caracteres estrechos
Antes de la versión 18.4 del controlador OLE DB, la inserción en una columna `sql_variant` podía provocar daños en los datos en el servidor si se cumplían todas las condiciones siguientes:
- La página de códigos del equipo cliente no coincidía con la página de códigos de intercalación de la base de datos.
- El búfer cliente que se va a insertar contenía caracteres de cadena estrechos no ASCII codificados en la página de códigos del cliente.
- Se cumplía alguna de las condiciones siguientes:
  - El campo `pwszDataSourceType` de la estructura `DBPARAMBINDINFO` que describe el parámetro correspondiente a la columna `sql_variant` se ha establecido en `L"DBTYPE_SQLVARIANT"`, `L"DBTYPE_VARIANT"` o `L"sql_variant"`. Para obtener detalles, consulte: [ICommandWithParameters::SetParameterInfo](https://docs.microsoft.com/previous-versions/windows/desktop/ms725393(v=vs.85)).

    *or*
  - Se ha preparado la consulta SQL con parámetros utilizada para la inserción.

En concreto, el controlador OLE DB no ha traducido los datos en la página de códigos de intercalación de la base de datos antes de insertarlos. Pero el controlador indicaba erróneamente al servidor que los datos estaban codificados en la página de códigos de intercalación de la base de datos. Este comportamiento ha producido una desigualdad entre los datos y su página de códigos correspondiente almacenada en la columna `sql_variant`.

De forma similar, al recuperar el mismo valor, el controlador OLE DB no ha traducido las cadenas a la página de códigos del cliente. Pero como los datos insertados ya estaban en la página de códigos del cliente (vea el párrafo anterior), la aplicación cliente podría interpretar los datos correctamente. Aun así, las aplicaciones que usan otros controladores recuperarían estos valores en un formato dañado. Los daños se producen porque otros controladores han interpretado la cadena en la página de códigos de intercalación de la base de datos y han intentado traducirla a la página de códigos del cliente.

A partir de la versión 18.4, el controlador OLE DB traduce las cadenas de caracteres estrechos a la página de códigos de intercalación de la base de datos antes de la inserción. Del mismo modo, el controlador vuelve a convertir los datos en la página de códigos del cliente tras la recuperación. Como resultado, es posible que las aplicaciones cliente que se basan en el error mencionado antes experimenten problemas al recuperar los datos que se insertan con una versión anterior del controlador OLE DB. El [procedimiento de recuperación](#recovery-procedure) siguiente pretende proporcionar instrucciones para resolver estos problemas.

### <a name="recovery-procedure"></a>Procedimiento de recuperación
> [!IMPORTANT]  
> Antes de realizar los pasos de recuperación siguientes, asegúrese de hacer una copia de seguridad de los datos existentes.

Si la aplicación experimenta problemas al recuperar datos de una columna `sql_variant` después de cambiar a la versión 18.4 del controlador OLE DB, es necesario modificar los datos dañados para que tengan la misma intercalación que la base de datos en la que se almacenan. Se puede usar el script siguiente para recuperar un valor único de una columna `sql_variant`. El script es una plantilla y la debe ajustar para adecuarla al escenario.

> [!IMPORTANT]  
> Como la página de códigos original de los datos no se almacena, debe indicar al servidor cómo se han codificado inicialmente los datos. Para ello, ejecute el script en el contexto de una base de datos que tenga la misma página de códigos que la del cliente que ha insertado inicialmente los datos. Por ejemplo, si los datos dañados se han insertado desde un cliente configurado con la página de códigos `932`, es necesario ejecutar el script siguiente en el contexto de una base de datos con una intercalación japonesa (por ejemplo, `Japanese_XJIS_100_CS_AI`).

```sql
/*
    Description:
        Template that can be used to recover the corrupted value inserted into the sql_variant column.

    Scenario:
        The database is named [YourDatabase] and it contains a table named [YourTable], which contains the corrupted value.
        Schema is named [dbo].
        The corrupted value is stored in a column of type sql_variant named [YourColumn].
        The corrupted value is sql_variant of BaseType char. For details on sql_variant properties, see:
            https://docs.microsoft.com/sql/t-sql/functions/sql-variant-property-transact-sql
*/

-- Base type in sql_variant can hold a maximum of 8000 bytes
-- For details see: 
--  https://docs.microsoft.com/sql/t-sql/data-types/sql-variant-transact-sql#remarks
DECLARE @bin VARBINARY(8000)

-- In the following lines we convert the sql_variant base type to binary.
-- <FilterExpression>
--      Is a placeholder and must be replaced with an expression that filters a single corrupted value to be recovered.
--      Therefore, the expression must result in a single value being returned only.
SET @bin = (SELECT CAST([YourColumn] AS VARBINARY(8000)) FROM [YourDatabase].[dbo].[YourTable] WHERE <FilterExpression>)

-- In the following lines we store the binary value in char(59) (a fixed-size character data type).
-- IMPORTANT NOTE: 
--      This example assumes the corrupted sql_variant's base type is char(59).
--      You MUST adjust the type (that is, char/varchar) and size to match your scenario exactly.
DECLARE @char CHAR(59)
SET @char = CAST((@bin) AS CHAR(59))
DECLARE @sqlvariant sql_variant

-- The following lines recover the corrupted value by translating the value to the collation of the database.
-- <DBCollation>
--      Must be replaced with the collation (for example, Latin1_General_100_CI_AS_SC_UTF8) of the database holding the data.
SET @sqlvariant = @char collate <DBCollation>

-- Finally, we update the corrupted value with the recovered value.
-- "<FilterExpression>"
--      Is a placeholder and must be replaced with an expression that filters a single corrupted value to be recovered.
--      Therefore, the expression must result in a single value being returned only.
UPDATE [YourDatabase].[dbo].[YourTable] SET [YourColumn] = @sqlvariant WHERE <FilterExpression>
```

## <a name="see-also"></a>Consulte también  
 [Tipos de datos &#40;OLE DB&#41;](../../oledb/ole-db-data-types/data-types-ole-db.md)  
  
  
