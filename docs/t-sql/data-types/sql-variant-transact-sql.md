---
title: sql_variant (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 9/12/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|data-types
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sql_variant
- sql_variant_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sql_variant comparisons
- storing data [SQL Server], sql_variant
- sql_variant data type
- storage [SQL Server], sql_variant
ms.assetid: 01229779-8bc1-4c7d-890a-8246d4899250
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: fc20b30cf079bb597108483e3b71d5c151535f2a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33055732"
---
# <a name="sqlvariant-transact-sql"></a>sql_variant (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Tipo de datos que almacena valores de varios tipos de datos admitidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
sql_variant  
```  
  
## <a name="remarks"></a>Notas  
**sql_variant** puede usarse en columnas, parámetros, variables y los valores devueltos de las funciones definidas por el usuario. **sql_variant** permite que estos objetos de base de datos admitan valores de otros tipos de datos.
  
Una columna de tipo **sql_variant** puede contener filas de tipos de datos diferentes. Por ejemplo, una columna definida como **sql_variant** puede almacenar valores **int**, **binario** y **char**.
  
**sql_variant** puede tener una longitud máxima de 8016 bytes. Esto incluye la información y el valor de tipo base. La longitud máxima del tipo base real es 8.000 bytes.
  
Un tipo de datos **sql_variant** debe convertirse en su valor de tipo de datos base antes de poder tomar parte en operaciones como la adición y la sustracción.
  
Se puede asignar un valor predeterminado a **sql_variant**. Este tipo de datos también puede incluir NULL como valor subyacente, aunque estos valores NULL no dispondrán de un tipo base asociado. Además, **sql_variant** no puede tener otro **sql_variant** como su tipo base.
  
Una clave única, primaria o externa puede incluir columnas de tipo **sql_variant**, aunque la longitud total de los valores de datos que integran la clave de una fila determinada no debe superar la longitud máxima de un índice. Ésta es de 900 bytes.
  
Una tabla puede constar de cualquier número de columnas **sql_variant**.
  
No se puede usar **sql_variant** en CONTAINSTABLE y FREETEXTTABLE.
  
ODBC no es totalmente compatible con **sql_variant**. Por tanto, las columnas de consultas de **sql_variant** se devuelven como datos binarios con el proveedor OLE DB de Microsoft para ODBC (MSDASQL). Por ejemplo, una columna **sql_variant** que contiene los datos de la cadena de caracteres 'PS2091' se devuelve como 0x505332303931.
  
## <a name="comparing-sqlvariant-values"></a>Comparar los valores de sql_variant  
El tipo de datos **sql_variant** pertenece a la parte superior de la lista de jerarquías de tipos de datos para conversión. En las comparaciones de **sql_variant**, el orden de la jerarquía del tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se agrupa en familias de tipos de datos.
  
|Jerarquía de tipo de datos|Familia de tipo de datos|  
|---|---|
|**sql_variant**|sql_variant |  
|**datetime2**|Fecha y hora|  
|**datetimeoffset**|Fecha y hora|  
|**datetime**|Fecha y hora|  
|**smalldatetime**|Fecha y hora|  
|**date**|Fecha y hora|  
|**time**|Fecha y hora|  
|**float**|Valor numérico aproximado|  
|**real**|Valor numérico aproximado|  
|**decimal**|Valor numérico exacto|  
|**money**|Valor numérico exacto|  
|**smallmoney**|Valor numérico exacto|  
|**bigint**|Valor numérico exacto|  
|**int**|Valor numérico exacto|  
|**smallint**|Valor numérico exacto|  
|**tinyint**|Valor numérico exacto|  
|**bit**|Valor numérico exacto|  
|**nvarchar**|Unicode|  
|**nchar**|Unicode|  
|**varchar**|Unicode|  
|**char**|Unicode|  
|**varbinary**|Binario|  
|**binario**|Binario|  
|**uniqueidentifier**|Uniqueidentifier |  
  
Las comparaciones de **sql_variant** siguen estas reglas:
-   Cuando se comparan valores **sql_variant** de distintos tipos de datos base y los tipos de datos base están en familias de tipos de datos diferentes, el valor cuya familia de tipo de datos ocupa una posición superior en el gráfico de jerarquía se considera el mayor de los dos valores.  
-   Cuando se comparan valores **sql_variant** de distintos tipos de datos base y los tipos de datos base están en la misma familia de tipos de datos, el valor cuyo tipo de datos base ocupa una posición inferior en el gráfico de jerarquía se convierte implícitamente al otro tipo de datos y, después, se realiza la comparación.  
-   Cuando se comparan valores **sql_variant** de los tipos de datos **char**, **varchar**, **nchar** o **nvarchar**, en primer lugar se comparan sus intercalaciones por los siguientes criterios: LCID, versión de LCID, marcas de comparación e identificador de orden. Cada uno de estos criterios se compara como valores enteros y en el orden enumerado. Si todos estos criterios son iguales, se comparan los valores reales de las cadenas según la intercalación.  
  
## <a name="converting-sqlvariant-data"></a>Convertir datos sql_variant  
Cuando se usa el tipo de datos **sql_variant**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite conversiones implícitas de objetos con otros tipos de datos al tipo **sql_variant**, pero [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite conversiones implícitas de datos **sql_variant** a un objeto con otro tipo de datos.
  
## <a name="restrictions"></a>Restrictions  
En esta tabla se muestran los tipos de valores que no se pueden almacenar mediante **sql_variant**:
  
|||  
|-|-|  
|**ntext**|**varbinary(max)**|  
|**nvarchar(max)**|**xml**|  
|**texto**|**ntext**|  
|**imagen**|**rowversion** (**timestamp**)|  
|**sql_variant**|**geography**|  
|**hierarchyid**|**geometry**|  
|Tipos definidos por el usuario|**datetimeoffset**|  

## <a name="examples"></a>Ejemplos  

### <a name="a-using-a-sqlvariant-in-a-table"></a>A. Usar un tipo de datos sql_variant en una tabla  
 En este ejemplo se crea una tabla con varios tipos de datos sql_variant. Luego se recupera la información de `SQL_VARIANT_PROPERTY` sobre el valor `colA` de `46279.1`, donde `colB` =`1689`, teniendo en cuenta que `tableA` tiene `colA` que es del tipo `sql_variant` y `colB`.  
  
```sql    
CREATE   TABLE tableA(colA sql_variant, colB int)  
INSERT INTO tableA values ( cast (46279.1 as decimal(8,2)), 1689)  
SELECT   SQL_VARIANT_PROPERTY(colA,'BaseType') AS 'Base Type',  
         SQL_VARIANT_PROPERTY(colA,'Precision') AS 'Precision',  
         SQL_VARIANT_PROPERTY(colA,'Scale') AS 'Scale'  
FROM      tableA  
WHERE      colB = 1689  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)] Tenga en cuenta que cada uno de estos tres valores es **sql_variant**.  
  
```  
Base Type    Precision    Scale  
---------    ---------    -----  
decimal      8           2  
  
(1 row(s) affected)  
```  
  
### <a name="b-using-a-sqlvariant-as-a-variable"></a>B. Usar un tipo de datos sql_variant como una variable   
 En este ejemplo se crea una variable mediante el tipo de datos sql_variant y después se recupera información de `SQL_VARIANT_PROPERTY` sobre una variable denominada @v1.  
  
```sql    
DECLARE @v1 sql_variant;  
SET @v1 = 'ABC';  
SELECT @v1;  
SELECT SQL_VARIANT_PROPERTY(@v1, 'BaseType');  
SELECT SQL_VARIANT_PROPERTY(@v1, 'MaxLength');  
```    


## <a name="see-also"></a>Vea también
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[SQL_VARIANT_PROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/sql-variant-property-transact-sql.md)
  
  
