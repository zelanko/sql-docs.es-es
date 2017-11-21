---
title: SQL_VARIANT_PROPERTY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SQL_VARIANT_PROPERTY_TSQL
- SQL_VARIANT_PROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- SQL_VARIANT_PROPERTY function
- sql_variant data type
ms.assetid: 50e5c1d9-4e95-4ed0-9c92-435c872a399e
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 71ca2fac0a6b9f087f9d434c5a701f5656889b9e
ms.openlocfilehash: bd9b181c04a96ee90b0bbb54546a1d925761224f
ms.contentlocale: es-es
ms.lasthandoff: 09/13/2017

---
# <a name="sqlvariantproperty-transact-sql"></a>SQL_VARIANT_PROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve el tipo de datos base y otra información sobre un **sql_variant** valor.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SQL_VARIANT_PROPERTY ( expression , property )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Es una expresión de tipo **sql_variant**.  
  
 *propiedad*  
 Contiene el nombre de la **sql_variant** para el que es proporcionar información de propiedad. *propiedad* es **varchar (**128**)**, y puede tener uno de los siguientes valores:  
  
|Valor|Description|Tipo base de sql_variant devuelto|  
|-----------|-----------------|----------------------------------------|  
|**BaseType**|Tipo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como:<br /><br /> **bigint**<br /><br /> **binario**<br /><br /> **char**<br /><br /> **date**<br /><br /> **datetime**<br /><br /> **datetime2**<br /><br /> **datetimeoffset**<br /><br /> **decimal**<br /><br /> **float**<br /><br /> **int**<br /><br /> **money**<br /><br /> **nchar**<br /><br /> **numeric**<br /><br /> **nvarchar**<br /><br /> **real**<br /><br /> **smalldatetime**<br /><br /> **smallint**<br /><br /> **smallmoney**<br /><br /> **time**<br /><br /> **tinyint**<br /><br /> **uniqueidentifier**<br /><br /> **varbinary**<br /><br /> **varchar**|**sysname**<br /><br /> NULL = La entrada no es válida.|  
|**Precisión**|Número de dígitos del tipo de datos base numérico:<br /><br /> **fecha y hora** = 23<br /><br /> **smalldatetime** = 16<br /><br /> **float** = 53<br /><br /> **real** = 24<br /><br /> **decimal** (p, s) y **numérico** (p, s) = p<br /><br /> **Money** = 19<br /><br /> **smallmoney** = 10<br /><br /> **bigint** = 19<br /><br /> **int** = 10<br /><br /> **smallint** = 5<br /><br /> **tinyint** = 3<br /><br /> **bit** = 1<br /><br /> Los demás tipos = 0|**int**<br /><br /> NULL = La entrada no es válida.|  
|**Escala**|Número de dígitos a la derecha del separador decimal del tipo de datos base numérico:<br /><br /> **decimal** (p, s) y **numérico** (p, s) = s<br /><br /> **Money** y **smallmoney** = 4<br /><br /> **fecha y hora** = 3<br /><br /> todos los demás tipos = 0|**int**<br /><br /> NULL = La entrada no es válida.|  
|**TotalBytes**|Número de bytes necesario para contener los metadatos y los datos del valor. Esta información sería útil para comprobar el tamaño máximo de los datos en un **sql_variant** columna. Si el valor es mayor que 900, se produce un error en la creación del índice.|**int**<br /><br /> NULL = La entrada no es válida.|  
|**Intercalación**|Representa la intercalación de ese **sql_variant** valor.|**sysname**<br /><br /> NULL = La entrada no es válida.|  
|**MaxLength**|Longitud máxima del tipo de datos, en bytes. Por ejemplo, **MaxLength** de **nvarchar (**50**)** es 100, **MaxLength** de **int** es 4.|**int**<br /><br /> NULL = La entrada no es válida.|  
  
## <a name="return-types"></a>Tipos devueltos  
 **sql_variant**  
  
## <a name="examples"></a>Ejemplos  
### <a name="a-using-a-sqlvariant-in-a-table"></a>A. Usar un sql_variant en una tabla  
 En el ejemplo siguiente se recuperan `SQL_VARIANT_PROPERTY` obtener información sobre la `colA` valor `46279.1` donde `colB`  = `1689`, dado que `tableA` tiene `colA` que es de tipo `sql_variant` y `colB`.  
  
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
 En el ejemplo siguiente se recuperan `SQL_VARIANT_PROPERTY` información sobre una variable denominada @v1.  
  
```sql    
DECLARE @v1 sql_variant;  
SET @v1 = 'ABC';  
SELECT @v1;  
SELECT SQL_VARIANT_PROPERTY(@v1, 'BaseType');  
SELECT SQL_VARIANT_PROPERTY(@v1, 'MaxLength');  
```  
  
## <a name="see-also"></a>Vea también  
 [sql_variant &#40;Transact-SQL&#41;](../../t-sql/data-types/sql-variant-transact-sql.md)  
  
  


