---
title: JSON_VALUE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- JSON_VALUE
- JSON_VALUE_TSQL
helpviewer_keywords:
- JSON_VALUE function
- JSON, extracting
- JSON, querying
ms.assetid: cd016e14-11eb-4eaf-bf05-c7cfcc820a10
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: ab4c14769dc51c6d5b97a6ad2fe6f0cb06fad4e0
ms.sourcegitcommit: 19e1c4067142d33e8485cb903a7a9beb7d894015
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2017
---
# <a name="jsonvalue-transact-sql"></a>JSON_VALUE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Extrae un valor escalar de una cadena JSON.  
  
 Para extraer un objeto o una matriz de una cadena JSON en lugar de un valor escalar, consulte [JSON_QUERY &#40; Transact-SQL &#41; ](../../t-sql/functions/json-query-transact-sql.md). Para obtener información sobre las diferencias entre **JSON_VALUE** y **JSON_QUERY**, consulte [comparar JSON_VALUE y JSON_QUERY](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md#JSONCompare).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
JSON_VALUE ( expression , path )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Expresión. Normalmente es el nombre de una variable o una columna que contiene texto JSON.  
 
 Si **JSON_VALUE** busca JSON que no es válido en *expresión* antes de encuentra el valor identificado por *ruta de acceso*, la función devuelve un error. Si **JSON_VALUE* no encuentra el valor identificado por *ruta de acceso*, examina todo el texto y devuelve un error si encuentra JSON que no es válida en cualquier lugar en *expresión*.
  
 *ruta de acceso*  
 Una ruta de acceso JSON que especifica la propiedad que se va a extraer. Para obtener más información, consulte [expresiones de ruta de acceso JSON &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
 
En [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y en [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)], puede proporcionar una variable como el valor de *ruta de acceso*.
  
 Si el formato de *ruta de acceso* no es válida, **JSON_VALUE** devuelve un error.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve un valor de texto de tipo nvarchar (4000). La intercalación del valor devuelto es la misma que la intercalación de la expresión de entrada.  
  
 Si el valor es mayor que 4000 caracteres:  
  
-   En el modo lax, **JSON_VALUE** devuelve null.  
  
-   En modo strict, **JSON_VALUE** devuelve un error.  
  
 Si tiene que devolver valores escalares de más de 4.000 caracteres, utilice **OPENJSON** en lugar de **JSON_VALUE**. Para obtener más información, vea [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
## <a name="remarks"></a>Comentarios

### <a name="lax-mode-and-strict-mode"></a>Modo lax y modo strict

 Tenga en cuenta el siguiente texto JSON:  
  
```json  
DECLARE @jsonInfo NVARCHAR(MAX)

SET @jsonInfo=N'{  
     "info":{    
       "type":1,  
       "address":{    
         "town":"Bristol",  
         "county":"Avon",  
         "country":"England"  
       },  
       "tags":["Sport", "Water polo"]  
    },  
    "type":"Basic"  
 }'  
```  
  
 En la tabla siguiente se compara el comportamiento de **JSON_VALUE** en modo lax y en modo strict. Para obtener más información acerca de la especificación del modo de ruta de acceso opcional (lax o strict), consulte [expresiones de ruta de acceso JSON &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|Ruta de acceso|Valor devuelto en el modo lax|Valor devuelto en modo strict|Más información|  
|----------|------------------------------|---------------------------------|---------------|  
|$|NULL|Error|No es un valor escalar.<br /><br /> Use **JSON_QUERY** en su lugar.|  
|$. info.type|N '1'|N '1'|N/A|  
|$. info.address.town|N'Bristol'|N'Bristol'|N/A|  
|$.info." dirección"|NULL|Error|No es un valor escalar.<br /><br /> Use **JSON_QUERY** en su lugar.|  
|$. info.tags|NULL|Error|No es un valor escalar.<br /><br /> Use **JSON_QUERY** en su lugar.|  
|$. info.type[0]|NULL|Error|No es una matriz.|  
|$. info.none|NULL|Error|Propiedad no existe.|  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="example-1"></a>Ejemplo 1  
 El ejemplo siguiente utiliza los valores de las propiedades JSON `town` y `state` en los resultados de la consulta. Puesto que **JSON_VALUE** conserva la intercalación de la fuente, el criterio de ordenación de los resultados depende de la intercalación de la `jsonInfo` columna. 

> [!NOTE]
> (En este ejemplo se da por supuesto que una tabla denominada `Person.Person` contiene un `jsonInfo` columna de texto JSON y que esta columna tiene la estructura se ha mostrado anteriormente en el análisis de modo lax y modo strict. En la base de datos de ejemplo de AdventureWorks, el `Person` tabla no contiene realmente una `jsonInfo` columna.)
  
```sql  
SELECT FirstName, LastName,
 JSON_VALUE(jsonInfo,'$.info.address[0].town') AS Town
FROM Person.Person
WHERE JSON_VALUE(jsonInfo,'$.info.address[0].state') LIKE 'US%'
ORDER BY JSON_VALUE(jsonInfo,'$.info.address[0].town')
```  
  
### <a name="example-2"></a>Ejemplo 2  
 En el ejemplo siguiente se extrae el valor de la propiedad JSON `town` en una variable local.  
  
```sql  
DECLARE @jsonInfo NVARCHAR(MAX)
DECLARE @town NVARCHAR(32)

SET @jsonInfo=N'<array of address info>'

SET @town=JSON_VALUE(@jsonInfo,'$.info.address.town')
```  
  
### <a name="example-3"></a>Ejemplo 3  
 En el ejemplo siguiente se crea columnas calculadas en función de los valores de propiedades JSON.  
  
```sql  
CREATE TABLE dbo.Store
 (
  StoreID INT IDENTITY(1,1) NOT NULL,
  Address VARCHAR(500),
  jsonContent NVARCHAR(8000),
  Longitude AS JSON_VALUE(jsonContent, '$.address[0].longitude'),
  Latitude AS JSON_VALUE(jsonContent, '$.address[0].latitude')
 )
```  
  
## <a name="see-also"></a>Vea también  
 [Expresiones de ruta de acceso JSON &#40; SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [Datos JSON &#40; SQL Server &#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  
