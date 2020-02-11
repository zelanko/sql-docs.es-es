---
title: Asignar datos de parámetros CLR | Microsoft Docs
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
ms.openlocfilehash: 530db4d31d3db4773713816f1b68404990997512
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081312"
---
# <a name="mapping-clr-parameter-data"></a>Asignar datos de parámetros CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En la tabla siguiente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se enumeran los tipos de datos, sus equivalentes en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Common Language Runtime (CLR) para en el espacio de nombres **System. Data. SqlTypes** y sus [!INCLUDE[msCoName](../../includes/msconame-md.md)] equivalentes de CLR nativos en el .NET Framework.  
  
||||  
|-|-|-|  
|**SQL Server tipo de datos**|Tipo (en System.Data.SqlTypes o Microsoft.SqlServer.Types)|**Tipo de datos CLR (.NET Framework)**|  
|**BIGINT**|**SqlInt64**|**Int64,\<Int64 que acepta valores NULL>**|  
|**binary**|**SqlBytes, SqlBinary**|**Byte []**|  
|**bit**|**SqlBoolean**|**Booleano,\<booleano que acepta valores NULL>**|  
|**char**|None|None|  
|**cursor**|None|None|  
|**date**|**SqlDateTime**|**DateTime,\<DateTime que acepta valores NULL>**|  
|**datetime**|**SqlDateTime**|**DateTime,\<DateTime que acepta valores NULL>**|  
|**datetime2**|None|**DateTime,\<DateTime que acepta valores NULL>**|  
|**DATETIMEOFFSET**|**None**|**DateTimeOffset,\<DateTimeOffset que admite valores NULL>**|  
|**Decimal**|**SqlDecimal**|**Decimal,>\<decimal que aceptan valores NULL**|  
|**float**|**SqlDouble**|**Double,\<doble>null**|  
|**geography**|**SqlGeography**<br /><br /> **SqlGeography** se define en Microsoft. SqlServer. types. dll, que se instala con SQL Server y se puede descargar desde [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] el [Feature Pack](https://www.microsoft.com/download/details.aspx?id=52676).|None|  
|**geometry**|**SqlGeometry**<br /><br /> **SqlGeometry** se define en Microsoft. SqlServer. types. dll, que se instala con SQL Server y se puede descargar desde [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] el [Feature Pack](https://www.microsoft.com/download/details.aspx?id=52676).|None|  
|**hierarchyid**|**SqlHierarchyId**<br /><br /> **SqlHierarchyId** se define en Microsoft. SqlServer. types. dll, que se instala con SQL Server y se puede descargar desde [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] el [Feature Pack](https://www.microsoft.com/download/details.aspx?id=52676).|None|  
|**impresión**|None|None|  
|**int**|**SqlInt32**|**Int32,\<Int32 que admite valores NULL>**|  
|**money**|**SqlMoney**|**Decimal,>\<decimal que aceptan valores NULL**|  
|**nchar**|**SqlChars, SqlString**|**String, Char[]**|  
|**ntext**|None|None|  
|**alfanumérico**|**SqlDecimal**|**Decimal,>\<decimal que aceptan valores NULL**|  
|**nvarchar**|**SqlChars, SqlString**<br /><br /> **SQLChars** es una mejor coincidencia para la transferencia de datos y el acceso, y **SQLString** es una coincidencia mejor para realizar operaciones de cadena.|**String, Char[]**|  
|**nvarchar (1), NCHAR (1)**|**SqlChars, SqlString**|**Char, String, Char [],\<carácter que admite valores NULL>**|  
|**impuestos**|**SqlSingle** (el intervalo de **SqlSingle**, sin embargo, es mayor que **real**)|**>único que admite\<valores NULL**|  
|**rowversion**|None|**Byte []**|  
|**smallint**|**SqlInt16**|**Int16,\<Int16 que admite valores NULL>**|  
|**SMALLMONEY**|**SqlMoney**|**Decimal,>\<decimal que aceptan valores NULL**|  
|**sql_variant**|None|**Object**|  
|**cuadro**|None|None|  
|**negrita**|None|None|  
|**time**|None|**TimeSpan,>\<TimeSpan que admite valores NULL**|  
|**timestamp**|None|None|  
|**tinyint**|**SqlByte**|**Byte,\<byte que acepta valores NULL>**|  
|**uniqueidentifier**|**SqlGuid**|**GUID,\<GUID que acepta valores NULL>**|  
|**Tipo definido por el usuario (UDT)**|None|La misma clase que está enlazada al tipo definido por el usuario en el mismo ensamblado o en un ensamblado dependiente.|  
|**varbinary**|**SqlBytes, SqlBinary**|**Byte []**|  
|**varbinary (1), binario (1)**|**SqlBytes, SqlBinary**|**byte, Byte [],\<byte que acepta valores NULL>**|  
|**varchar**|None|None|  
|**lenguaje**|**SqlXml**|None|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>Conversión automática de tipos de datos con parámetros OUT  
 Un método CLR puede devolver información al código o programa que realiza la llamada marcando un parámetro de entrada con el modificador **out** (Microsoft Visual C#) o ** \<out () > ByRef** (Microsoft Visual Basic) si el parámetro de entrada es un tipo de datos de CLR en el sistema. el espacio de nombres **Data. SqlTypes** y el programa que realiza la llamada especifican su tipo de datos equivalente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como parámetro de entrada, se produce una conversión de tipos automáticamente cuando el método CLR devuelve el tipo de datos.  
  
 Por ejemplo, el siguiente procedimiento almacenado CLR tiene un parámetro de entrada de tipo de datos de CLR **SqlInt32** que está marcado con **out** (C#) o ** \<out () > ByRef** (Visual Basic):  
  
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
  
 Una vez generado y creado el ensamblado en la base de datos, el procedimiento almacenado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se crea en con el siguiente TRANSACT-SQL, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que especifica un tipo de datos **int** como parámetro de salida:  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 Cuando se llama al procedimiento almacenado CLR, el tipo de datos **SqlInt32** se convierte automáticamente en un tipo de datos **int** y se devuelve al programa que realiza la llamada.  
  
 Pero no todos los tipos de datos CLR se pueden convertir automáticamente en sus tipos de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equivalentes mediante un parámetro OUT. En la tabla siguiente se enumeran estas excepciones.  
  
|||  
|-|-|  
|**Tipo de datos CLR (SQL Server)**|**SQL Server tipo de datos**|  
|**Decimal**|SMALLMONEY|  
|**SqlMoney**|SMALLMONEY|  
|**Decimal**|money|  
|**DateTime**|smalldatetime|  
|**SQLDateTime**|smalldatetime|  
  
## <a name="change-history"></a>Historial de cambios  
  
|Contenido actualizado|  
|---------------------|  
|Se han agregado los tipos **SqlGeography**, **SqlGeometry**y **SqlHierarchyId** a la tabla de asignación.|  
  
## <a name="see-also"></a>Consulte también  
 [Tipos de datos de SQL Server en .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
