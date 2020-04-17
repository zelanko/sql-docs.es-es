---
title: Asignación de datos de parámetros CLR (Mapping CLR Parameter Data) Microsoft Docs
description: En este artículo se enumeran los tipos de datos de Microsoft SQL Server, los equivalentes en CLR para SQL Server y los equivalentes nativos de CLR en .NET Framework.
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
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
ms.openlocfilehash: 360a94229b107e9f24bb2a769157c75cdeb3c143
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488478"
---
# <a name="mapping-clr-parameter-data"></a>Asignar datos de parámetros CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla siguiente se enumeran los tipos de datos, sus equivalentes en Common Language Runtime (CLR) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el espacio de **nombres System.Data.SqlTypes** y sus equivalentes CLR nativos en [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework.  
  
||||  
|-|-|-|  
|**Tipos de datos de SQL Server**|Tipo (en System.Data.SqlTypes o Microsoft.SqlServer.Types)|**Tipo de datos CLR (.NET Framework)**|  
|**bigint**|**SqlInt64**|**Int64, Int64 anulable\<>**|  
|**binary**|**SqlBytes, SqlBinary**|**Byte[]**|  
|**bit**|**SqlBoolean**|**Boolean, Nullable\<Boolean>**|  
|**char**|None|None|  
|**cursor**|None|None|  
|**date**|**SqlDateTime**|**DateTime, Nullable\<DateTime>**|  
|**datetime**|**SqlDateTime**|**DateTime, Nullable\<DateTime>**|  
|**datetime2**|None|**DateTime, Nullable\<DateTime>**|  
|**DATETIMEOFFSET**|**None**|**DateTimeOffset, Nullable\<DateTimeOffset>**|  
|**decimal**|**SqlDecimal**|**Decimal, nullable\<Decimal>**|  
|**float**|**SqlDouble**|**Doble>\<doble anulable**|  
|**geography**|**SqlGeography**<br /><br /> **SqlGeography** se define en Microsoft.SqlServer.Types.dll, que se instala con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SQL Server y se puede descargar desde el paquete de [características.](https://www.microsoft.com/download/details.aspx?id=52676)|None|  
|**geometry**|**SqlGeometry**<br /><br /> **SqlGeometry** se define en Microsoft.SqlServer.Types.dll, que se instala con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SQL Server y se puede descargar desde el paquete de [características.](https://www.microsoft.com/download/details.aspx?id=52676)|None|  
|**hierarchyid**|**SqlHierarchyId**<br /><br /> **SqlHierarchyId** se define en Microsoft.SqlServer.Types.dll, que se instala con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] SQL Server y se puede descargar desde el paquete de [características.](https://www.microsoft.com/download/details.aspx?id=52676)|None|  
|**image**|None|None|  
|**int**|**SqlInt32**|**Int32, Int32 anulable\<>**|  
|**money**|**SqlMoney**|**Decimal, nullable\<Decimal>**|  
|**nchar**|**SqlChars, SqlString**|**String, Char[]**|  
|**ntext**|None|None|  
|**numeric**|**SqlDecimal**|**Decimal, nullable\<Decimal>**|  
|**nvarchar**|**SqlChars, SqlString**<br /><br /> **SQLChars** es una mejor coincidencia para la transferencia de datos y el acceso, y **SQLString** es una mejor coincidencia para realizar operaciones String.|**String, Char[]**|  
|**nvarchar(1), nchar(1)**|**SqlChars, SqlString**|**Char, String, Char[],\<Carácter nullable>**|  
|**real**|**SqlSingle** (el rango de **SqlSingle,** sin embargo, es mayor que **real)**|**Single, Nullable\<Single>**|  
|**rowversion**|None|**Byte[]**|  
|**smallint**|**SqlInt16**|**Int16, Int16 anulable\<>**|  
|**smallmoney**|**SqlMoney**|**Decimal, nullable\<Decimal>**|  
|**sql_variant**|None|**Objeto**|  
|**table**|None|None|  
|**text**|None|None|  
|**time**|None|**TimeSpan, TimeSpan nullable\<>**|  
|**timestamp**|None|None|  
|**tinyint**|**SqlByte**|**Byte, Byte\<nullable>**|  
|**uniqueidentifier**|**SqlGuid**|**Guid, Guid\<nullable>**|  
|**Tipo definido por el usuario (UDT)**|None|La misma clase que está enlazada al tipo definido por el usuario en el mismo ensamblado o en un ensamblado dependiente.|  
|**varbinary**|**SqlBytes, SqlBinary**|**Byte[]**|  
|**varbinary(1), binario(1)**|**SqlBytes, SqlBinary**|**byte, Byte[],\<Byte Nullable>**|  
|**varchar**|None|None|  
|**xml**|**Sqlxml**|None|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>Conversión automática de tipos de datos con parámetros OUT  
 Un método CLR puede devolver información al código o programa de llamada marcando un parámetro de entrada con el modificador **out** (Microsoft Visual C)) o ** \<Out()> ByRef** (Microsoft Visual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Basic) Si el parámetro de entrada es un tipo de datos CLR en el espacio de nombres **System.Data.SqlTypes** y el programa de llamada especifica su tipo de datos equivalente como parámetro de entrada, se produce automáticamente una conversión de tipo cuando el método CLR devuelve el tipo de datos.  
  
 Por ejemplo, el siguiente procedimiento almacenado CLR tiene un parámetro de entrada de tipo de datos CLR **SqlInt32** que está marcado con **out** (C) o ** \<Out()> ByRef** (Visual Basic):  
  
```csharp  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void PriceSum(out SqlInt32 value)  
{ ... }  
```  
  
```vb  
\<Microsoft.SqlServer.Server.SqlProcedure> _  
Public Shared Sub PriceSum( \<Out()> ByRef value As SqlInt32)  
...  
End Sub  
```  
  
 Después de compilar y crear el ensamblado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la base de datos, el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] procedimiento almacenado se crea en el siguiente Transact-SQLTransact-SQL, que especifica un tipo de datos de **int** como parámetro OUTPUT:  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 Cuando se llama al procedimiento almacenado CLR, el **sqlInt32** tipo de datos se convierte automáticamente en un tipo de datos **int** y se devuelve al programa que realiza la llamada.  
  
 Pero no todos los tipos de datos CLR se pueden convertir automáticamente en sus tipos de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equivalentes mediante un parámetro OUT. En la tabla siguiente se enumeran estas excepciones.  
  
|||  
|-|-|  
|**Tipo de datos CLR (SQL Server)**|**Tipos de datos de SQL Server**|  
|**Decimal**|SMALLMONEY|  
|**SqlMoney**|SMALLMONEY|  
|**Decimal**|money|  
|**Datetime**|smalldatetime|  
|**SQLDateTime**|smalldatetime|  
  
## <a name="change-history"></a>Historial de cambios  
  
|Contenido actualizado|  
|---------------------|  
|Se han agregado los tipos **SqlGeography**, **SqlGeometry**y **SqlHierarchyId** a la tabla de asignación.|  
  
## <a name="see-also"></a>Consulte también  
 [Tipos de datos de SQL Server en .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
