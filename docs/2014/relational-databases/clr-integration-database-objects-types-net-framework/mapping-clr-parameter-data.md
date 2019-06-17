---
title: Asignar datos de parámetros CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- SqlBinary data type
- SqlInt16 data type
- SqlMoney data type
- SqlString data type
- SqlSingle data type
- data types [CLR integration]
- SqlInt64 data type
- SqlDateTime data type
- SqlXml data type
- SqlBoolean data type
- SqlDecimal data type
- SqlBytes data type
- mapping data types [CLR integration]
- SqlChars data type
- SqlInt32 data type
ms.assetid: 89b43ee9-b9ad-4281-a4bf-c7c8d116daa2
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b297d329f11e05ed1b1995004150644e4b76ec9b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62874836"
---
# <a name="mapping-clr-parameter-data"></a>Asignar datos de parámetros CLR
  La siguiente tabla enumera [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los tipos de datos, sus equivalentes en common language runtime (CLR) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el `System.Data.SqlTypes` espacio de nombres y sus equivalentes CLR nativos en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework.  
  
||||  
|-|-|-|  
|**Tipo de datos de SQL Server**|Tipo (en System.Data.SqlTypes o Microsoft.SqlServer.Types)|**Tipo de datos CLR (.NET Framework)**|  
|`bigint`|`SqlInt64`|**Int64, Nullable\<Int64>**|  
|`binary`|`SqlBytes, SqlBinary`|`Byte[]`|  
|`bit`|`SqlBoolean`|**Boolean, Nullable\<Boolean>**|  
|`char`|None|None|  
|`cursor`|None|None|  
|`date`|`SqlDateTime`|**DateTime, Nullable\<DateTime>**|  
|`datetime`|`SqlDateTime`|**DateTime, Nullable\<DateTime>**|  
|`datetime2`|None|**DateTime, Nullable\<DateTime>**|  
|`DATETIMEOFFSET`|`None`|**DateTimeOffset, Nullable\<DateTimeOffset>**|  
|`decimal`|`SqlDecimal`|**Decimal, Nullable\<Decimal>**|  
|`float`|`SqlDouble`|**Double, Nullable\<Double>**|  
|`geography`|`SqlGeography`<br /><br /> `SqlGeography` se define en Microsoft.SqlServer.Types.dll, que se instala con SQL Server y puede descargarse desde el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [feature pack de](https://www.microsoft.com/en-us/download/details.aspx?id=53164).|None|  
|`geometry`|`SqlGeometry`<br /><br /> `SqlGeometry` se define en Microsoft.SqlServer.Types.dll, que se instala con SQL Server y puede descargarse desde el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [feature pack de](https://www.microsoft.com/en-us/download/details.aspx?id=53164).|None|  
|`hierarchyid`|`SqlHierarchyId`<br /><br /> `SqlHierarchyId` se define en Microsoft.SqlServer.Types.dll, que se instala con SQL Server y puede descargarse desde el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [feature pack de](https://www.microsoft.com/en-us/download/details.aspx?id=53164).|None|  
|`image`|None|None|  
|`int`|`SqlInt32`|**Int32, Nullable\<Int32>**|  
|`money`|`SqlMoney`|**Decimal, Nullable\<Decimal>**|  
|`nchar`|`SqlChars, SqlString`|`String, Char[]`|  
|`ntext`|None|None|  
|`numeric`|`SqlDecimal`|**Decimal, Nullable\<Decimal>**|  
|`nvarchar`|`SqlChars, SqlString`<br /><br /> `SQLChars` es más adecuado para la transferencia de datos y el acceso a los mismos, mientras que `SQLString` es mejor para realizar operaciones de cadena.|`String, Char[]`|  
|`nvarchar(1), nchar(1)`|`SqlChars, SqlString`|**Char, String, Char[], Nullable\<char>**|  
|`real`|`SqlSingle` (el intervalo de `SqlSingle`, sin embargo, es mayor que `real`)|**Single, Nullable\<Single>**|  
|`rowversion`|None|`Byte[]`|  
|`smallint`|`SqlInt16`|**Int16, Nullable\<Int16>**|  
|`smallmoney`|`SqlMoney`|**Decimal, Nullable\<Decimal>**|  
|`sql_variant`|None|`Object`|  
|`table`|None|None|  
|`text`|None|None|  
|`time`|None|**TimeSpan, Nullable\<TimeSpan>**|  
|`timestamp`|None|None|  
|`tinyint`|`SqlByte`|**Byte, Nullable\<Byte>**|  
|`uniqueidentifier`|`SqlGuid`|**GUID, que acepta valores NULL\<Guid >**|  
|`User-defined type(UDT)`|None|La misma clase que está enlazada al tipo definido por el usuario en el mismo ensamblado o en un ensamblado dependiente.|  
|**varbinary**|`SqlBytes, SqlBinary`|`Byte[]`|  
|`varbinary(1), binary(1)`|`SqlBytes, SqlBinary`|**byte, Byte[], Nullable\<byte>**|  
|`varchar`|None|None|  
|`xml`|`SqlXml`|None|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>Conversión automática de tipos de datos con parámetros OUT  
 Un método CLR puede devolver información al código o programa de llamada marcando un parámetro de entrada con el modificador `out` (Microsoft Visual C#) o `<Out()> ByRef` (Microsoft Visual Basic). Si el parámetro de entrada es un tipo de datos CLR del espacio de nombres `System.Data.SqlTypes` y el programa de llamada especifica su tipo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equivalente como parámetro de entrada, se produce una conversión de tipos automáticamente cuando el método CLR devuelve el tipo de datos.  
  
 Por ejemplo, el siguiente procedimiento almacenado CLR tiene un parámetro de entrada de tipos de datos CLR `SqlInt32` que se marca con `out` (C#) o `<Out()> ByRef` (Visual Basic):  
  
```csharp  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void PriceSum(out SqlInt32 value)  
{ ... }  
```  
  
```vb  
<Microsoft.SqlServer.Server.SqlProcedure> _  
Public Shared Sub PriceSum( <Out()> ByRef value As SqlInt32)  
...  
End Sub  
```  
  
 Una vez generado y creado el ensamblado en la base de datos, el procedimiento almacenado se crea en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el siguiente Transact-SQL, que especifica un tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de `int` como parámetro OUTPUT:  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 Cuando se llama al procedimiento almacenado CLR, el tipo de datos `SqlInt32` se convierte automáticamente en un tipo de datos `int` y se devuelve al programa que hace la llamada.  
  
 Pero no todos los tipos de datos CLR se pueden convertir automáticamente en sus tipos de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equivalentes mediante un parámetro OUT. En la tabla siguiente se enumeran estas excepciones.  
  
|||  
|-|-|  
|**Tipo de datos CLR (SQL Server)**|**Tipo de datos de SQL Server**|  
|`Decimal`|SMALLMONEY|  
|`SqlMoney`|SMALLMONEY|  
|`Decimal`|money|  
|`DateTime`|smalldatetime|  
|`SQLDateTime`|smalldatetime|  
  
## <a name="change-history"></a>Historial de cambios  
  
|Contenido actualizado|  
|---------------------|  
|Se han agregado los tipos `SqlGeography`, `SqlGeometry` y `SqlHierarchyId` a la tabla de asignación.|  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos de SQL Server en .NET Framework](sql-server-data-types-in-the-net-framework.md)  
  
  
