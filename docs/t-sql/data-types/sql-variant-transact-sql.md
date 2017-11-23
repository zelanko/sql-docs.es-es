---
title: sql_variant (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 9/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sql_variant
- sql_variant_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sql_variant comparisons
- storing data [SQL Server], sql_variant
- sql_variant data type
- storage [SQL Server], sql_variant
ms.assetid: 01229779-8bc1-4c7d-890a-8246d4899250
caps.latest.revision: "43"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 01a11cca67bbf24afa7d74d5e776a969d62920dc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sqlvariant-transact-sql"></a>sql_variant (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Tipo de datos que almacena valores de varios tipos de datos admitidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
sql_variant  
```  
  
## <a name="remarks"></a>Comentarios  
**sql_variant** puede utilizarse en columnas, parámetros, variables y los valores devueltos de funciones definidas por el usuario. **sql_variant** permite que estos objetos de base de datos admitan valores de otros tipos de datos.
  
Una columna de tipo **sql_variant** puede contener filas de tipos de datos diferentes. Por ejemplo, una columna definida como **sql_variant** puede almacenar **int**, **binario**, y **char** valores.
  
**sql_variant** puede tener una longitud máxima de 8.016 bytes. Esto incluye la información y el valor de tipo base. La longitud máxima del tipo base real es 8.000 bytes.
  
A **sql_variant** tipo de datos en primer lugar debe convertirse a su valor de tipo de base de datos antes de participar en operaciones como la suma y resta.
  
**sql_variant** puede asignarse un valor predeterminado. Este tipo de datos también puede incluir NULL como valor subyacente, aunque estos valores NULL no dispondrán de un tipo base asociado. Además, **sql_variant** no puede tener otro **sql_variant** como su tipo base.
  
Una clave única, principal o externa puede incluir columnas de tipo **sql_variant**, pero la longitud total de los valores de datos que forman la clave de una fila determinada no debe ser mayor que la longitud máxima de un índice. Ésta es de 900 bytes.
  
Una tabla puede tener cualquier número de **sql_variant** columnas.
  
**sql_variant** no se puede usar en CONTAINSTABLE y FREETEXTTABLE.
  
ODBC no son totalmente compatibles con **sql_variant**. Por lo tanto, las consultas de **sql_variant** columnas se devuelven como datos binarios cuando se usa el proveedor Microsoft OLE DB para ODBC (MSDASQL). Por ejemplo, un **sql_variant** columna que contiene los datos de cadena de caracteres 'PS2091' se devuelve como 0 x 505332303931.
  
## <a name="comparing-sqlvariant-values"></a>Comparar los valores de sql_variant  
El **sql_variant** tipo de datos pertenece a la parte superior de la lista de jerarquías de tipo de datos para la conversión. Para **sql_variant** comparaciones, la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] orden de jerarquía de tipo de datos se agrupa en familias de tipos de datos.
  
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
  
Las siguientes reglas se aplican a **sql_variant** comparaciones:
-   Cuando **sql_variant** se comparan valores de tipos de datos base distintos y los tipos de datos base están en los datos distintas familias de tipos, el valor cuya familia de tipo de datos sea mayor en el diagrama de jerarquía se considera el mayor de los dos valores.  
-   Cuando **sql_variant** se comparan valores de tipos de datos base distintos y los tipos de datos base están en la misma familia de tipo de datos, el valor cuyo tipo de datos base tenga menor prioridad en el diagrama de jerarquía se convierte implícitamente al otro tipo de datos y a continuación, se realiza la comparación.  
-   Cuando **sql_variant** valores de la **char**, **varchar**, **nchar**, o **nvarchar** son tipos de datos en comparación, sus intercalaciones se comparan en primer lugar en función de los siguientes criterios: LCID, versión LCID, marcas de comparación y ordenación identificador. Cada uno de estos criterios se comparan valores enteros como en el orden indicado. Si todos estos criterios son iguales, se comparan los valores reales de las cadenas según la intercalación.  
  
## <a name="converting-sqlvariant-data"></a>Convertir datos sql_variant  
Al controlar la **sql_variant** tipo de datos, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite conversiones implícitas de objetos con otros tipos de datos a la **sql_variant** tipo. Sin embargo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite conversiones implícitas de **sql_variant** datos a un objeto con otro tipo de datos.
  
## <a name="restrictions"></a>Restricciones  
En la tabla siguiente se enumera los tipos de valores que no se pueden almacenar mediante **sql_variant**:
  
|||  
|-|-|  
|**varchar(max)**|**varbinary(max)**|  
|**nvarchar(max)**|**xml**|  
|**text**|**ntext**|  
|**image**|**rowversion** (**timestamp**)|  
|**sql_variant**|**geography**|  
|**hierarchyid**|**geometry**|  
|Tipos definidos por el usuario|**datetimeoffset**|  

## <a name="examples"></a>Ejemplos  

### <a name="a-using-a-sqlvariant-in-a-table"></a>A. Usar un sql_variant en una tabla  
 El ejemplo siguiente, se crea una tabla con un tipo de datos sql_variant. A continuación, en el ejemplo se recupera `SQL_VARIANT_PROPERTY` obtener información sobre la `colA` valor `46279.1` donde `colB`  = `1689`, dado que `tableA` tiene `colA` que es de tipo `sql_variant` y `colB`.  
  
```sql    
CREATE   TABLE tableA(colA sql_variant, colB int)  
INSERT INTO tableA values ( cast (46279.1 as decimal(8,2)), 1689)  
SELECT   SQL_VARIANT_PROPERTY(colA,'BaseType') AS 'Base Type',  
         SQL_VARIANT_PROPERTY(colA,'Precision') AS 'Precision',  
         SQL_VARIANT_PROPERTY(colA,'Scale') AS 'Scale'  
FROM      tableA  
WHERE      colB = 1689  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]Tenga en cuenta que cada uno de estos tres valores es un **sql_variant**.  
  
```  
Base Type    Precision    Scale  
---------    ---------    -----  
decimal      8           2  
  
(1 row(s) affected)  
```  
  
### <a name="b-using-a-sqlvariant-as-a-variable"></a>B. Usar un sql_variant como una variable   
 El ejemplo siguiente, se crea una variable utilizando el tipo de datos sql_variant y, a continuación, recupera `SQL_VARIANT_PROPERTY` información sobre una variable denominada @v1.  
  
```sql    
DECLARE @v1 sql_variant;  
SET @v1 = 'ABC';  
SELECT @v1;  
SELECT SQL_VARIANT_PROPERTY(@v1, 'BaseType');  
SELECT SQL_VARIANT_PROPERTY(@v1, 'MaxLength');  
```    


## <a name="see-also"></a>Vea también
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[SQL_VARIANT_PROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/sql-variant-property-transact-sql.md)
  
  
