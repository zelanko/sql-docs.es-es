---
title: Conversión de tipos de datos (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 7/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fee327575d3ce77197f0ed0a95d8f50eef19b5ac
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43069145"
---
# <a name="data-type-conversion-database-engine"></a>Conversión de tipos de datos (motor de base de datos)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Los tipos de datos se pueden convertir en los siguientes casos:
-   Cuando los datos de un objeto se comparan o se combinan con los datos de otro objeto, o bien se mueven a estos, puede que sea necesario convertir los datos desde el tipo de datos de un objeto al tipo de datos del otro.  
-   Cuando los datos de una columna de resultados, un código de retorno o un parámetro de salida de [!INCLUDE[tsql](../../includes/tsql-md.md)] se mueven a una variable de programa, se deben convertir del tipo de datos del sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al tipo de datos de la variable.  
  
Cuando se realiza una conversión entre una variable de aplicación y una columna de conjunto de resultados, código de retorno, parámetro o marcador de parámetro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la API de base de datos define cuáles son las conversiones de tipos de datos admitidas.
  
## <a name="implicit-and-explicit-conversion"></a>Conversiones implícitas y explícitas
Los tipos de datos se pueden convertir de forma implícita o explícita.
  
Las conversiones implícitas no son visibles para el usuario. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] convierte automáticamente los datos de un tipo de datos al otro. Por ejemplo, cuando se comparan **smallint** con **int**, antes de realizar la comparación, **smallint** se convierte implícitamente al tipo **int**.
  
**GETDATE()** se convierte implícitamente al estilo de fecha 0. **SYSDATETIME()** se convierte implícitamente al estilo de fecha 21.
  
Las conversiones explícitas utilizan las funciones CAST o CONVERT.
  
Las funciones [CAST y CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md) convierten un valor (una variable local, una columna u otra expresión) de un tipo de datos a otro. Por ejemplo, la siguiente función `CAST` convierte el valor numérico `$157.27` a una cadena de caracteres `'157.27'`:
  
```sql
CAST ( $157.27 AS VARCHAR(10) )  
```  
  
Utilice CAST en lugar de CONVERT si desea que el código de programa de [!INCLUDE[tsql](../../includes/tsql-md.md)] cumpla las normas ISO. Use CONVERT en lugar de CAST para aprovechar la funcionalidad de estilo de CONVERT.
  
En la ilustración siguiente se muestran todas las conversiones de tipos de datos explícitas e implícitas permitidas para los tipos de datos proporcionados por el sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Algunas de ellas son **xml**, **bigint** y **sql_variant**. No existe una conversión implícita en la asignación del tipo de datos **sql_variant**, pero sí hay una conversión implícita en **sql_variant**.
  
![Tabla de conversión de tipos de datos](../../t-sql/data-types/media/lrdatahd.png "Tabla de conversión de tipos de datos")
  
## <a name="data-type-conversion-behaviors"></a>Comportamientos de la conversión de tipos de datos
Algunas conversiones implícitas y explícitas de tipos de datos no se admiten cuando convierte el tipo de datos de un objeto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a otro. Por ejemplo, un valor **nchar** no se puede convertir a un valor **image**. Un valor **nchar** solo se puede convertir a **binary** con una conversión explícita; la conversión implícita a **binary** no se admite. Sin embargo, un valor **nchar** se puede convertir implícita o explícitamente a **nvarchar**.
  
En los temas siguientes se describen los comportamientos de conversión que presentan los tipos de datos correspondientes:
  
 - [binary y varbinary &#40;Transact-SQL&#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)  
 - [datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)  
 - [money y smallmoney &#40;Transact-SQL&#41;](../../t-sql/data-types/money-and-smallmoney-transact-sql.md)  
 - [bit &#40;Transact-SQL&#41;](../../t-sql/data-types/bit-transact-sql.md)  
 - [datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)  
 - [smalldatetime &#40;Transact-SQL&#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)  
 - [char y varchar &#40;Transact-SQL&#41;](../../t-sql/data-types/char-and-varchar-transact-sql.md)  
 - [decimal y numeric &#40;Transact-SQL&#41;](../../t-sql/data-types/decimal-and-numeric-transact-sql.md)  
 - [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)  
 - [date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)  
 - [float y real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md)  
 - [time &#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md)  
 - [datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md)  
 - [int, bigint, smallint y tinyint &#40;Transact-SQL&#41;](../../t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql.md)  
 - [uniqueidentifier &#40;Transact-SQL&#41;](../../t-sql/data-types/uniqueidentifier-transact-sql.md)  
  
###  <a name="converting-data-types-by-using-ole-automation-stored-procedures"></a>Convertir tipos de datos con procedimientos almacenados de OLE Automation  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza tipos de datos [!INCLUDE[tsql](../../includes/tsql-md.md)] y OLE Automation utiliza tipos de datos [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]; por tanto, los procedimientos almacenados de OLE Automation deben convertir los datos que se pasan entre ellos.
  
En la tabla siguiente se describen las conversiones de tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)].
  
|Tipo de datos de SQL Server|Tipo de datos de Visual Basic|  
|--------------------------|----------------------------|  
|**char**, **varchar**, **text**, **nvarchar**, **ntext**|**String**|  
|**decimal**, **numeric**|**String**|  
|**bit**|**Boolean**|  
|**binary**, **varbinary**, **image**|Matriz **Byte()** unidimensional|  
|**int**|**Long**|  
|**smallint**|**Integer**|  
|**tinyint**|**Byte**|  
|**float**|**Doble**|  
|**real**|**Único**|  
|**money**, **smallmoney**|**Moneda**|  
|**datetime**, **smalldatetime**|**Date**|  
|Cualquiera establecido en NULL|**Variant** establecido en NULL|  
  
Los valores únicos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se convierten a un valor único de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], con la excepción de los valores **binary**, **varbinary** e **image**. Estos valores se convierten a una matriz **Byte()** unidimensional en [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. Esta matriz tiene un intervalo de **Byte(** 0 to *length*1 **)** donde *length* es el número de bytes en los valores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **binary**, **varbinary** o **image**.
  
A continuación se indican las conversiones de tipos de datos de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] a tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
|Tipo de datos de Visual Basic|Tipo de datos de SQL Server|  
|----------------------------|--------------------------|  
|**Long**, **Integer**, **Byte**, **Boolean**, **Object**|**int**|  
|**Double**, **Single**|**float**|  
|**Moneda**|**money**|  
|**Date**|**datetime**|  
|**String** con 4000 caracteres o menos|**varchar**/**nvarchar**|  
|**String** con más de 4000 caracteres|**text**/**ntext**|  
|Matriz **Byte()** unidimensional con 8000 bytes o menos|**varbinary**|  
|Matriz **Byte()** unidimensional con más de 8000 bytes|**imagen**|  
  
## <a name="see-also"></a>Vea también
[Procedimientos almacenados de automatización OLE &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)  
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[COLLATE &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/4ba6b7d8-114a-4f4e-bb38-fe5697add4e9)
  
  
