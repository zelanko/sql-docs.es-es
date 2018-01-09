---
title: "La asignación de datos de parámetro CLR | Documentos de Microsoft"
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
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
caps.latest.revision: "71"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 3592a4c547b3586df4be45b2e1734e330dd16664
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="mapping-clr-parameter-data"></a>Asignar datos de parámetros CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]La siguiente tabla se recogen [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos, sus equivalentes en common language runtime (CLR) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el **System.Data.SqlTypes** espacio de nombres y sus equivalentes CLR nativos en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET framework.  
  
||||  
|-|-|-|  
|**Tipo de datos de SQL Server**|Tipo (en System.Data.SqlTypes o Microsoft.SqlServer.Types)|**Tipo de datos CLR (.NET Framework)**|  
|**bigint**|**SqlInt64**|**Int64, que acepta valores NULL\<Int64 >**|  
|**binario**|**SqlBytes, SqlBinary**|**Byte]**|  
|**bit**|**SqlBoolean**|**Boolean, que acepta valores NULL\<booleano >**|  
|**char**|None|None|  
|**cursor**|None|None|  
|**date**|**SqlDateTime**|**Fecha y hora, que acepta valores NULL\<DateTime >**|  
|**datetime**|**SqlDateTime**|**Fecha y hora, que acepta valores NULL\<DateTime >**|  
|**datetime2**|None|**Fecha y hora, que acepta valores NULL\<DateTime >**|  
|**DATETIMEOFFSET**|**Ninguno**|**DateTimeOffset, que acepta valores NULL\<DateTimeOffset >**|  
|**decimal**|**SqlDecimal**|**Decimal, que acepta valores NULL\<Decimal >**|  
|**float**|**SqlDouble**|**Double, que acepta valores NULL\<dobles >**|  
|**geography**|**SqlGeography**<br /><br /> **SqlGeography** se define en Microsoft.SqlServer.Types.dll, que se instala con SQL Server y puede descargarse desde el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [feature pack de](https://www.microsoft.com/download/details.aspx?id=52676).|None|  
|**geometry**|**SqlGeometry**<br /><br /> **SqlGeometry** se define en Microsoft.SqlServer.Types.dll, que se instala con SQL Server y puede descargarse desde el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [feature pack de](https://www.microsoft.com/download/details.aspx?id=52676).|None|  
|**hierarchyid**|**Error de SqlHierarchyId**<br /><br /> **Error de SqlHierarchyId** se define en Microsoft.SqlServer.Types.dll, que se instala con SQL Server y puede descargarse desde el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [feature pack de](https://www.microsoft.com/download/details.aspx?id=52676).|None|  
|**imagen**|None|None|  
|**int**|**SqlInt32**|**Int32, que acepta valores NULL\<Int32 >**|  
|**money**|**SqlMoney**|**Decimal, que acepta valores NULL\<Decimal >**|  
|**nchar**|**SqlChars, SqlString**|**String, Char]**|  
|**ntext**|None|None|  
|**numeric**|**SqlDecimal**|**Decimal, que acepta valores NULL\<Decimal >**|  
|**nvarchar**|**SqlChars, SqlString**<br /><br /> **SQLChars** es una coincidencia mejor para la transferencia de datos y acceso, y **SQLString** es una coincidencia mejor para realizar operaciones de cadenas.|**String, Char]**|  
|**nvarchar(1), nchar (1)**|**SqlChars, SqlString**|**Char, String, Char [], Nullable\<char >**|  
|**real**|**SqlSingle** (el intervalo de **SqlSingle**, sin embargo, es mayor que **real**)|**Único, que acepta valores NULL\<único >**|  
|**rowversion**|None|**Byte]**|  
|**smallint**|**SqlInt16**|**Int16, que acepta valores NULL\<Int16 >**|  
|**smallmoney**|**SqlMoney**|**Decimal, que acepta valores NULL\<Decimal >**|  
|**sql_variant**|None|**Objeto**|  
|**table**|None|None|  
|**texto**|None|None|  
|**time**|None|**Intervalo de tiempo, que acepta valores NULL\<TimeSpan >**|  
|**timestamp**|None|None|  
|**tinyint**|**SqlByte**|**Bytes, que acepta valores NULL\<bytes >**|  
|**uniqueidentifier**|**SqlGuid**|**GUID, que acepta valores NULL\<Guid >**|  
|**Type(UDT) definido por el usuario**|None|La misma clase que está enlazada al tipo definido por el usuario en el mismo ensamblado o en un ensamblado dependiente.|  
|**varbinary**|**SqlBytes, SqlBinary**|**Byte]**|  
|**varbinary(1), binary(1)**|**SqlBytes, SqlBinary**|**Byte, Byte [], Nullable\<bytes >**|  
|**varchar**|None|None|  
|**xml**|**SqlXml**|None|  
  
## <a name="automatic-data-type-conversion-with-out-parameters"></a>Conversión automática de tipos de datos con parámetros OUT  
 Un método CLR puede devolver información en el código o el programa que realiza la llamada marcando un parámetro de entrada con el **out** modificador (Microsoft Visual C#) o  **\<Out() > ByRef** (Microsoft Visual Basic) Si el parámetro de entrada es un tipo de datos CLR en el **System.Data.SqlTypes** espacio de nombres y el programa que realiza la llamada especifica su equivalente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos como parámetro de entrada, una conversión de tipos se produce automáticamente Cuando el método CLR devuelve el tipo de datos.  
  
 Por ejemplo, el siguiente procedimiento almacenado CLR tiene un parámetro de entrada de **SqlInt32** tipo de datos CLR que se marca con **out** (C#) o  **\<Out() > ByRef** () Visual Basic):  
  
```csharp  
[Microsoft.SqlServer.Server.SqlProcedure]  
public static void PriceSum(out SqlInt32 value)  
{ … }  
```  
  
```vb  
\<Microsoft.SqlServer.Server.SqlProcedure> _  
Public Shared Sub PriceSum( \<Out()> ByRef value As SqlInt32)  
…  
End Sub  
```  
  
 Después de que el ensamblado generado y creado en la base de datos, el procedimiento almacenado se crea en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con Transact-SQL siguiente, que especifica un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos de **int** como un parámetro de salida:  
  
```  
CREATE PROCEDURE PriceSum (@sum int OUTPUT)  
AS EXTERNAL NAME TestStoredProc.StoredProcedures.PriceSum  
```  
  
 Cuando el CLR almacenado se llama a procedimiento la **SqlInt32** tipo de datos se convierte automáticamente en un **int** tipo de datos y se devuelve al programa de llamada.  
  
 Pero no todos los tipos de datos CLR se pueden convertir automáticamente en sus tipos de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] equivalentes mediante un parámetro OUT. En la tabla siguiente se enumeran estas excepciones.  
  
|||  
|-|-|  
|**Tipo de datos CLR (SQL Server)**|**Tipo de datos de SQL Server**|  
|**Decimal**|SMALLMONEY|  
|**SqlMoney**|SMALLMONEY|  
|**Decimal**|money|  
|**DateTime**|smalldatetime|  
|**SQLDateTime**|smalldatetime|  
  
## <a name="change-history"></a>Historial de cambios  
  
|Contenido actualizado|  
|---------------------|  
|Agregar **SqlGeography**, **SqlGeometry**, y **SqlHierarchyId** tipos a la tabla de asignación.|  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos de SQL Server en .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
