---
title: "Tipo de datos de conversión (motor de base de datos) | Documentos de Microsoft"
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- CAST function
- converting data types [SQL Server]
- CONVERT function
- data types [SQL Server], converting
- implicit data type conversions
- explicit data type conversions [SQL Server]
- converting data types [SQL Server], about converting data types
ms.assetid: ffacf45e-a488-48d0-9bb0-dcc7fd365299
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c0ed7f8e0e681de9f962e3eb963c0af315a0c25c
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="data-type-conversion-database-engine"></a>Conversión de tipos de datos (motor de base de datos)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Los tipos de datos se pueden convertir en los siguientes casos:
-   Cuando los datos de un objeto se comparan o se combinan con los datos de otro objeto, o bien se mueven a estos, puede que sea necesario convertir los datos desde el tipo de datos de un objeto al tipo de datos del otro.  
-   Cuando los datos de un [!INCLUDE[tsql](../../includes/tsql-md.md)] columna de resultados, código de retorno o parámetro de salida se mueve a una variable de programa, deben convertir los datos desde el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al tipo de datos de la variable de tipo de datos de sistema.  
  
Cuando se realiza una conversión entre una variable de aplicación y una columna de conjunto de resultados, código de retorno, parámetro o marcador de parámetro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la API de base de datos define cuáles son las conversiones de tipos de datos admitidas.
  
## <a name="implicit-and-explicit-conversion"></a>Conversiones implícitas y explícitas
Los tipos de datos se pueden convertir de forma implícita o explícita.
  
Las conversiones implícitas no son visibles para el usuario. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] convierte automáticamente los datos de un tipo de datos al otro. Por ejemplo, cuando un **smallint** se compara con un **int**, **smallint** se convierte implícitamente en **int** antes de la comparación lleva a cabo.
  
**GETDATE()** convierte implícitamente al estilo de fecha 0. **SYSDATETIME()** convierte implícitamente al estilo de fecha 21.
  
Las conversiones explícitas utilizan las funciones CAST o CONVERT.
  
El [CAST y CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) funciones convierten un valor (una variable local, una columna o expresión otro) de un tipo de datos a otro. Por ejemplo, la siguiente función `CAST` convierte el valor numérico `$157.27` a una cadena de caracteres `'157.27'`:
  
```sql
CAST ( $157.27 AS VARCHAR(10) )  
```  
  
Utilice CAST en lugar de CONVERT si desea que el código de programa de [!INCLUDE[tsql](../../includes/tsql-md.md)] cumpla las normas ISO. Use CONVERT en lugar de CAST para aprovechar la funcionalidad de estilo de CONVERT.
  
En la ilustración siguiente se muestran todas las conversiones de tipos de datos explícitas e implícitas permitidas para los tipos de datos proporcionados por el sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede tratarse de **xml**, **bigint**, y **sql_variant**. No hay ninguna conversión implícita en la asignación de la **sql_variant** tipo de datos, pero no hay conversión implícita a **sql_variant**.
  
![Tabla de conversión de tipos de datos](../../t-sql/data-types/media/lrdatahd.png "tabla de conversión de tipos de datos")
  
## <a name="data-type-conversion-behaviors"></a>Comportamientos de la conversión de tipos de datos
Algunas conversiones implícitas y explícitas de tipos de datos no se admiten cuando convierte el tipo de datos de un objeto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a otro. Por ejemplo, un **nchar** valor no puede convertirse a un **imagen** valor. Un **nchar** sólo se puede convertir en **binario** mediante el uso de conversión explícita, una conversión implícita a **binario** no se admite. Sin embargo, un **nchar** puede convertir implícita o explícitamente a **nvarchar**.
  
En los temas siguientes se describen los comportamientos de conversión que presentan los tipos de datos correspondientes:
  
 - [binary y varbinary &#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)  
 - [datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)  
 - [Money y smallmoney &#40; Transact-SQL &#41;](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)  
 - [bit &#40; Transact-SQL &#41;](../../t-sql/data-types/bit-transact-sql.md)  
 - [datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)  
 - [smalldatetime &#40; Transact-SQL &#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)  
 - [char y varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)  
 - [decimal y numeric &#40; Transact-SQL &#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)  
 - [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)  
 - [date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)  
 - [float y real &#40; Transact-SQL &#41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
 - [tiempo &#40; Transact-SQL &#41;](../../t-sql/data-types/time-transact-sql.md)  
 - [fecha y hora &#40; Transact-SQL &#41;](../../t-sql/data-types/datetime-transact-sql.md)  
 - [int, bigint, smallint y tinyint &#40; Transact-SQL &#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
 - [uniqueidentifier &#40; Transact-SQL &#41;](../../t-sql/data-types/uniqueidentifier-transact-sql.md)  
  
###  <a name="converting-data-types-by-using-ole-automation-stored-procedures"></a>Convertir tipos de datos con procedimientos almacenados de OLE Automation  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza tipos de datos [!INCLUDE[tsql](../../includes/tsql-md.md)] y OLE Automation utiliza tipos de datos [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]; por tanto, los procedimientos almacenados de OLE Automation deben convertir los datos que se pasan entre ellos.
  
En la tabla siguiente se describen las conversiones de tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)].
  
|Tipo de datos de SQL Server|Tipo de datos de Visual Basic|  
|--------------------------|----------------------------|  
|**char**, **varchar**, **texto**, **nvarchar**, **ntext**|**String**|  
|**decimal**, **numérico**|**String**|  
|**bit**|**Boolean**|  
|**binario**, **varbinary**, **imagen**|Unidimensional **Byte()** matriz|  
|**int**|**Long**|  
|**smallint**|**Integer**|  
|**tinyint**|**Bytes**|  
|**float**|**Doble**|  
|**real**|**Único**|  
|**money**, **smallmoney**|**Moneda**|  
|**fecha y hora**, **smalldatetime**|**Fecha**|  
|Cualquiera establecido en NULL|**Variant** establecido en Null|  
  
Todos los único [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valores se convierten en una sola [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] valor con la excepción de **binario**, **varbinary**, y **imagen** valores. Estos valores se convierten en un unidimensional **Byte()** la matriz en [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. Esta matriz tiene un intervalo de **bytes (**0 a *longitud*1**)** donde *longitud* es el número de bytes en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  **binario**, **varbinary**, o **imagen** valores.
  
A continuación se indican las conversiones de tipos de datos de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] a tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
|Tipo de datos de Visual Basic|Tipo de datos de SQL Server|  
|----------------------------|--------------------------|  
|**Long**, **entero**, **bytes**, **booleano**, **objeto**|**int**|  
|**Doble**, **único**|**float**|  
|**Moneda**|**money**|  
|**Fecha**|**datetime**|  
|**Cadena** con 4.000 caracteres o menos|**varchar**/**nvarchar**|  
|**Cadena** con más de 4.000 caracteres|**texto**/**ntext**|  
|Unidimensional **Byte()** matriz con 8.000 bytes o menos|**varbinary**|  
|Unidimensional **Byte()** matriz con más de 8.000 bytes.|**image**|  
  
## <a name="see-also"></a>Vea también
[Procedimientos almacenados de automatización OLE &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[COLLATE &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)
  
  

