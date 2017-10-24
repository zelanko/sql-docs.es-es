---
title: JSON_MODIFY (Transact-SQL) | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 96bc8255-a037-4907-aec4-1a9c30814651
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 70f2c1456da6469c39389fada6a74ccf46383582
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="jsonmodify-transact-sql"></a>JSON_MODIFY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Actualiza el valor de una propiedad en una cadena JSON y devuelve la cadena JSON actualizada.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```sql  
JSON_MODIFY ( expression , path , newValue )  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Expresión. Normalmente es el nombre de una variable o una columna que contiene texto JSON.  
  
 **JSON_MODIFY** devuelve un error si *expresión* no contiene un valor JSON válido.  
  
 *ruta de acceso*  
 Una expresión de ruta de acceso JSON que especifica la propiedad que se va a actualizar.

 *ruta de acceso* tiene la siguiente sintaxis:  
  
 `[append] [ lax | strict ] $.<json path>`  
  
-   *anexar*  
    Modificador opcional que especifica que el nuevo valor se debe anexar a la matriz al que hace referencia  *\<ruta de acceso json >*.  
  
-   *lax*  
    Especifica que la propiedad hace referencia a  *\<ruta de acceso json >* no tiene que existir. Si la propiedad no está presente, JSON_MODIFY intenta insertar el nuevo valor en la ruta de acceso especificada. Inserción puede producir un error si la propiedad no se pueden insertar en la ruta de acceso. Si no se especifica *lax* o *estricta*, *lax* es el modo predeterminado.  
  
-   *Strict*  
    Especifica que la propiedad hace referencia a  *\<ruta de acceso json >* debe estar en la expresión de JSON. Si la propiedad no está presente, JSON_MODIFY devuelve un error.  
  
-   *\<ruta de acceso JSON >*  
    Especifica la ruta de acceso para la propiedad que se va a actualizar. Para obtener más información, consulte [expresiones de ruta de acceso JSON &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
En [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y en [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)], puede proporcionar una variable como el valor de *ruta de acceso*.

**JSON_MODIFY** devuelve un error si el formato de *ruta de acceso* no es válido.  
  
 *newValue*  
 El nuevo valor de la propiedad especificada por *ruta de acceso*.  
  
 En el modo lax, JSON_MODIFY elimina la clave especificada, si el nuevo valor es NULL.  
  
JSON_MODIFY convierte todos los caracteres especiales en el nuevo valor si el tipo del valor es NVARCHAR o VARCHAR. Un valor de texto no sea de escape si está correctamente con el formato JSON generado por FOR JSON, JSON_QUERY o JSON_MODIFY.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve el valor actualizado del *expresión* como correctamente con el formato de texto JSON.  
  
## <a name="remarks"></a>Comentarios  
 La función JSON_MODIFY le permite actualizar el valor de una propiedad existente, inserte un nuevo par clave-valor o eliminar una clave según una combinación de modos y proporcione los valores.  
  
 En la tabla siguiente se compara el comportamiento de **JSON_MODIFY** en modo lax y en modo strict. Para obtener más información acerca de la especificación del modo de ruta de acceso opcional (lax o strict), consulte [expresiones de ruta de acceso JSON &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|Valor existente|Ruta de acceso existe|Modo lax|Modo Strict|  
|--------------------|-----------------|--------------|-----------------|  
|No es NULL|Sí|Actualice el valor existente.|Actualice el valor existente.|  
|No es NULL|No|Intente crear un nuevo par clave-valor en la ruta de acceso especificada.<br /><br /> Esto puede producir un error. Por ejemplo, si especifica la ruta de acceso `$.user.setting.theme`, JSON_MODIFY no inserta la clave `theme` si la `$.user` o `$.user.settings` objetos no existen, o si la configuración es una matriz o un valor escalar.|Error: INVALID_PROPERTY|  
|NULL|Sí|Elimine la propiedad existente.|Establezca el valor existente en null.|  
|NULL|No|Ninguna acción. El primer argumento se devuelve como resultado.|Error: INVALID_PROPERTY|  
  
 En el modo lax, JSON_MODIFY intenta crear un nuevo par de clave-valor, pero en algunos casos se podría producir un error.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="example---basic-operations"></a>Por ejemplo, operaciones básicas  
 El ejemplo siguiente muestra las operaciones básicas que se pueden realizar con texto JSON.  
  
 **Query**  
  
```sql  

DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Update name  

SET @info=JSON_MODIFY(@info,'$.name','Mike')

PRINT @info

-- Insert surname  

SET @info=JSON_MODIFY(@info,'$.surname','Smith')

PRINT @info

-- Delete name  

SET @info=JSON_MODIFY(@info,'$.name',NULL)

PRINT @info

-- Add skill  

SET @info=JSON_MODIFY(@info,'append $.skills','Azure')

PRINT @info
```  
  
 **Resultado**  
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "Mike",
    "skills": ["C#", "SQL"]
} {
    "name": "Mike",
    "skills": ["C#", "SQL"],
    "surname": "Smith"
} {
    "skills": ["C#", "SQL"],
    "surname": "Smith"
} {
    "skills": ["C#", "SQL", "Azure"],
    "surname": "Smith"
}
```  
  
### <a name="example---multiple-updates"></a>Por ejemplo, varias actualizaciones  
 Con JSON_MODIFY puede actualizar solo una propiedad. Si tiene que realizar varias actualizaciones, puede utilizar varias llamadas JSON_MODIFY.  
  
 **Query**  
  
```sql  
DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Multiple updates  

SET @info=JSON_MODIFY(JSON_MODIFY(JSON_MODIFY(@info,'$.name','Mike'),'$.surname','Smith'),'append $.skills','Azure')

PRINT @info
```  
  
 **Resultado**  
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "Mike",
    "skills": ["C#", "SQL", "Azure"],
    "surname": "Smith"
}
```  
  
### <a name="example---rename-a-key"></a>Por ejemplo, cambiar el nombre de una clave  
 En el ejemplo siguiente se muestra cómo cambiar el nombre de una propiedad en texto JSON con la función JSON_MODIFY. En primer lugar puede tomar el valor de una propiedad existente e insértelo como un nuevo par de clave-valor. A continuación, puede eliminar la antigua clave estableciendo el valor de la propiedad anterior en NULL.  
  
 **Query**  
  
```sql  
DECLARE @product NVARCHAR(100)='{"price":49.99}'

PRINT @product

-- Rename property  

SET @product=
 JSON_MODIFY(
  JSON_MODIFY(@product,'$.Price',CAST(JSON_VALUE(@product,'$.price') AS NUMERIC(4,2))),
  '$.price',
  NULL
 )

PRINT @product
```  
  
 **Resultado**  
  
```json  
{
    "price": 49.99
} {
    "Price": 49.99
}
```  
  
 Si no convierte el nuevo valor a un tipo numérico, JSON_MODIFY lo trata como texto y la coloca entre comillas dobles.  
  
### <a name="example---increment-a-value"></a>Por ejemplo, un valor de incremento  
 En el ejemplo siguiente se muestra cómo incrementar el valor de una propiedad en texto JSON con la función JSON_MODIFY. En primer lugar puede tomar el valor de la propiedad existente e insértelo como un nuevo par de clave-valor. A continuación, puede eliminar la antigua clave estableciendo el valor de la propiedad anterior en NULL.  
  
 **Query**  
  
```sql  
DECLARE @stats NVARCHAR(100)='{"click_count": 173}'

PRINT @stats

-- Increment value  

SET @stats=JSON_MODIFY(@stats,'$.click_count',
 CAST(JSON_VALUE(@stats,'$.click_count') AS INT)+1)

PRINT @stats
```  
  
 **Resultado**  
  
```json  
{
    "click_count": 173
} {
    "click_count": 174
}
```  
  
### <a name="example---modify-a-json-object"></a>Ejemplo: modificar un objeto JSON  
 JSON_MODIFY trata el *newValue* argumento como texto sin formato incluso si contiene correctamente con el formato de texto JSON. Como resultado, la salida JSON de la función está acotada por comillas dobles y todos los caracteres especiales son caracteres de escape, tal como se muestra en el ejemplo siguiente.  
  
 **Query**  
  
```sql  
DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Update skills array

SET @info=JSON_MODIFY(@info,'$.skills','["C#","T-SQL","Azure"]')

PRINT @info
```  
  
 **Resultado**  
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "John",
    "skills": "["C#","T-SQL","Azure"]"
}
```  
  
 Para evitar la secuencia de escape automática, proporcionar *newValue* mediante la función JSON_QUERY. JSON_MODIFY sabe que el valor devuelto por JSON_MODIFY correctamente con el formato JSON, por lo que no el valor de escape.  
  
 **Query**  
  
```sql  
DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Update skills array  

SET @info=JSON_MODIFY(@info,'$.skills',JSON_QUERY('["C#","T-SQL","Azure"]'))

PRINT @info
```  
  
 **Resultado**  
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "John",
    "skills": ["C#", "T-SQL", "Azure"]
}
```  
  
### <a name="example---update-a-json-column"></a>Ejemplo: actualizar una columna JSON  
 En el ejemplo siguiente se actualiza el valor de una propiedad en una columna de tabla que contiene un valor JSON.  
  
```sql  
UPDATE Employee
SET jsonCol=JSON_MODIFY(jsonCol,"$.info.address.town",'London')
WHERE EmployeeID=17
 
```  
  
## <a name="see-also"></a>Vea también  
 [Expresiones de ruta de acceso JSON &#40; SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [Datos JSON &#40; SQL Server &#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  

