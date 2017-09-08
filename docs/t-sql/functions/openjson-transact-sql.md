---
title: OPENJSON (Transact-SQL) | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENJSON
- OPENJSON_TSQL
helpviewer_keywords:
- OPENJSON rowset function
- JSON, importing
- JSON, converting from
ms.assetid: 233d0877-046b-4dcc-b5da-adeb22f78531
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: def6c774a66262f2baa7cdfc726a0ddf6c299075
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="openjson-transact-sql"></a>OPENJSON (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

**OPENJSON** es una función con valores de tabla que analiza el texto JSON y devuelve objetos y propiedades de la entrada JSON como filas y columnas. En otras palabras, **OPENJSON** proporciona una vista de conjunto de filas en un documento JSON. Puede especificar explícitamente las columnas en el conjunto de filas y las rutas de acceso de propiedad JSON usados para rellenar las columnas. Puesto que **OPENJSON** devuelve un conjunto de filas, puede usar **OPENJSON** en el `FROM` cláusula de una [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción al igual que puede usar cualquier otra tabla, vista o función con valores de tabla.  
  
Use **OPENJSON** para importar datos JSON en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o convertir datos JSON en un formato relacional para una aplicación o servicio que no se puede usar directamente JSON.  
  
> [!NOTE]  
>  El **OPENJSON** función está disponible sólo en el nivel de compatibilidad 130 o superior. Si el nivel de compatibilidad de la base de datos es inferior a 130, SQL Server no podrá encontrar ni ejecutar la función **OPENJSON**. Hay otras funciones JSON que sí están disponibles en todos los niveles de compatibilidad.
> 
> Puede comprobar el nivel de compatibilidad en la vista `sys.databases` o en las propiedades de la base de datos. Puede cambiar el nivel de compatibilidad de una base de datos con el siguiente comando:  
> 
> `ALTER DATABASE DatabaseName SET COMPATIBILITY_LEVEL = 130`
>   
> Nivel de compatibilidad 120 puede ser el valor predeterminado incluso en una nueva base de datos de SQL Azure.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema")[convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
OPENJSON( jsonExpression [ , path ] )  [ <with_clause> ]

<with_clause> ::= WITH ( { colName type [ column_path ] [ AS JSON ] } [ ,...n ] )
```  

El **OPENJSON** función con valores de tabla analiza el *jsonExpression* proporcionada como primer argumento y devuelve una o varias filas que contienen datos de los objetos JSON en la expresión. *jsonExpression* puede contener objetos secundarios anidados. Si desea analizar un subobjeto desde *jsonExpression*, puede especificar un **ruta de acceso** parámetro para el subobjeto JSON.

### <a name="openjson"></a>openjson

![Sintaxis de OPENJSON TVF](../../relational-databases/json/media/openjson-syntax.png "sintaxis OPENJSON")  

De forma predeterminada, el **OPENJSON** función con valores de tabla devuelve tres columnas, que contienen el nombre de clave, el valor y el tipo de cada par de {clave: value} se encuentra en *jsonExpression*. Como alternativa, puede especificar explícitamente el esquema del resultado juego que **OPENJSON** devuelve proporcionando *with_clause*.
  
### <a name="withclause"></a>with_clause
  
![Sintaxis de con la cláusula en OPENJSON TVF](../../relational-databases/json/media/openjson-shema-syntax.png "OPENJSON con sintaxis")

*with_clause* contiene una lista de columnas con sus tipos de **OPENJSON** para devolver. De forma predeterminada, **OPENJSON** coincide con las claves en *jsonExpression* con los nombres de columna en *with_clause*. Si un nombre de columna no coincide con un nombre de clave, puede proporcionar una función opcional *column_path*, que es un [expresión de ruta de acceso JSON](../../relational-databases/json/json-path-expressions-sql-server.md) que hace referencia a una clave en el *jsonExpression*. 

## <a name="arguments"></a>Argumentos  
### <a name="jsonexpression"></a>*jsonExpression*  
Es una expresión de caracteres Unicode que contiene texto JSON.  
  
OPENJSON recorre en iteración los elementos de la matriz o las propiedades del objeto en la expresión de JSON y devuelve una fila por cada elemento o propiedad. El ejemplo siguiente devuelve cada propiedad del objeto proporcionado como *jsonExpression*:  
  
```sql  
DECLARE @json NVARCHAR(4000) = N'{  
   "StringValue":"John",  
   "IntValue":45,  
   "TrueValue":true,  
   "FalseValue":false,  
   "NullValue":null,  
   "ArrayValue":["a","r","r","a","y"],  
   "ObjectValue":{"obj":"ect"}  
}'

SELECT *
FROM OPENJSON(@json)
```  
  
**Resultado**  
  
|Key|value|Tipo|  
|---------|-----------|----------|  
|StringValue|John|1|  
|IntValue|Doe|2|  
|trueValue|true|3|  
|falseValue|false|3|  
|nullValue|NULL|0|  
|ArrayValue|["a", "r", "r", "un","y"]|4|  
|ObjectValue|{"obj": "ect"}|5|  

### <a name="path"></a>*ruta de acceso*  
Es una expresión de ruta de acceso JSON opcional que hace referencia a un objeto o una matriz de *jsonExpression*. **OPENJSON** búsquedas en el texto de JSON en la posición especificada y analiza solo el fragmento que se hace referencia. Para obtener más información, consulte [expresiones de ruta de acceso JSON &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).

En [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] y en [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)], puede proporcionar una variable como el valor de *ruta de acceso*.
  
En el ejemplo siguiente se devuelve un objeto anidado especificando el *ruta de acceso*:  

```sql  
DECLARE @json NVARCHAR(4000) = N'{  
      "path": {  
            "to":{  
                 "sub-object":["en-GB", "en-UK","de-AT","es-AR","sr-Cyrl"]  
                 }  
              }  
 }';

SELECT [key], value
FROM OPENJSON(@json,'$.path.to."sub-object"')
```  
  
 **Resultado**  
  
|Key|Valor|  
|---------|-----------|  
|0|en-GB|  
|1|en-UK|  
|2|de-AT|  
|3|es-AR|  
|4|sr-Cyrl|  
 
Cuando **OPENJSON** analiza una matriz JSON, la función devuelve los índices de los elementos en el texto JSON como claves.

La comparación que se usa para hacer coincidir los pasos de ruta de acceso con las propiedades de la expresión de JSON es entre mayúsculas y minúsculas y sin tener en cuenta la intercalación (es decir, una comparación de BIN2). 

### <a name="withclause"></a>*with_clause*
Se define explícitamente el esquema de salida para el **OPENJSON** función para devolver. Opcional *with_clause* puede contener los siguientes elementos:

*colName* es el nombre de la columna de salida.  
  
De forma predeterminada, **OPENJSON** utiliza el nombre de la columna para que coincida con una propiedad en el texto JSON. Por ejemplo, si especifica la columna *nombre* en el esquema, OPENJSON intenta rellenar esta columna con la propiedad "name" en el texto JSON. Puede invalidar esta asignación predeterminada mediante el uso de la *column_path* argumento.  
  
*Tipo*  
Es el tipo de datos para la columna de salida.  

> [!NOTE]
> Si también utiliza el **AS JSON** opción, la columna *tipo* debe ser `NVARCHAR(MAX)`.
  
*column_path*  
Es la ruta de acceso JSON que especifica la propiedad que se va a devolver en la columna especificada. Para obtener más información, vea la descripción de la *ruta de acceso* parámetro anteriormente en este tema.  
  
Use *column_path* para invalidar las reglas de asignación de manera predeterminada, cuando el nombre de una columna de salida no coincide con el nombre de la propiedad.  
  
La comparación que se usa para hacer coincidir los pasos de ruta de acceso con las propiedades de la expresión de JSON es entre mayúsculas y minúsculas y sin tener en cuenta la intercalación (es decir, una comparación de BIN2).  
  
Para obtener más información sobre las rutas de acceso, consulte [expresiones de ruta de acceso JSON &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
*COMO JSON*  
Use la **AS JSON** opción en una definición de columna para especificar que la propiedad que se hace referencia contiene un objeto JSON interno o una matriz. Si especifica la **AS JSON** opción, el tipo de la columna debe ser nvarchar (max).

-   Si no se especifica **AS JSON** para una columna, la función devuelve un valor escalar (por ejemplo, int, string, true, false) de la propiedad JSON especificada en la ruta de acceso especificada. Si la ruta de acceso representa un objeto o una matriz y la propiedad no se encuentra en la ruta de acceso especificada, la función devuelve null en modo lax o devuelve un error en modo strict. Este comportamiento es similar al comportamiento de la **JSON_VALUE** (función).  
  
-   Si especifica **AS JSON** para una columna, la función devuelve un fragmento de JSON de la propiedad JSON especificada en la ruta de acceso especificada. Si la ruta de acceso representa un valor escalar, y la propiedad no se encuentra en la ruta de acceso especificada, la función devuelve null en modo lax o devuelve un error en modo strict. Este comportamiento es similar al comportamiento de la **JSON_QUERY** (función).  
  
> [!NOTE]  
> Si desea devolver un fragmento de JSON anidado de una propiedad JSON, tendrá que proporcionar el **AS JSON** marca. Sin esta opción, si no se encuentra la propiedad, OPENJSON devuelve un valor NULL en lugar de la matriz o un objeto JSON que se hace referencia, o bien devuelve un error en tiempo de ejecución en modo strict.  
  
Por ejemplo, la siguiente consulta devuelve y da formato a los elementos de una matriz:  
  
```sql  
DECLARE @json NVARCHAR(MAX) = N'[  
  {  
    "Order": {  
      "Number":"SO43659",  
      "Date":"2011-05-31T00:00:00"  
    },  
    "AccountNumber":"AW29825",  
    "Item": {  
      "Price":2024.9940,  
      "Quantity":1  
    }  
  },  
  {  
    "Order": {  
      "Number":"SO43661",  
      "Date":"2011-06-01T00:00:00"  
    },  
    "AccountNumber":"AW73565",  
    "Item": {  
      "Price":2024.9940,  
      "Quantity":3  
    }  
  }
]'  
   
SELECT *
FROM OPENJSON ( @json )  
WITH (   
              Number   varchar(200)   '$.Order.Number',  
              Date     datetime       '$.Order.Date',  
              Customer varchar(200)   '$.AccountNumber',  
              Quantity int            '$.Item.Quantity',  
              [Order]  nvarchar(MAX)  AS JSON  
 )
```  
  
**Resultado**  
  
|Number|Date|Customer|Cantidad|Pedido de|  
|------------|----------|--------------|--------------|-----------|  
|SO43659|2011-05-31T00:00:00|AW29825|1|{"Número": "SO43659", "Fecha": "2011-05-31T00:00:00"}|  
|SO43661|2011-06-01T00:00:00|AW73565|3|{"Número": "SO43661", "Fecha": "2011-06-01T00:00:00"}|  
  

## <a name="return-value"></a>Valor devuelto  
Las columnas que devuelve la función OPENJSON dependen de la opción WITH.  
  
1. Cuando se llama a OPENJSON con el esquema predeterminado: es decir, cuando no se especifica un esquema explícito en la cláusula WITH - la función devuelve una tabla con las siguientes columnas:  
    1.  **Clave**. Un valor nvarchar (4000) que contiene el nombre de la propiedad especificada o el índice del elemento de la matriz especificada. La columna de clave tiene una intercalación BIN2.  
    2.  **Valor**. Un valor nvarchar (max) que contiene el valor de la propiedad. La columna de valor hereda la intercalación de *jsonExpression*.
    3.  **Tipo de**. Un valor entero que contiene el tipo del valor. El **tipo** columna se devuelve solo cuando el uso de OPENJSON con el esquema predeterminado. La columna de tipo tiene uno de los siguientes valores:  
  
        |Valor de la columna de tipo|Tipo de datos JSON|  
        |------------------------------|--------------------|  
        |0|null|  
        |1|string|  
        |2|int|  
        |3|Verdadero/Falso|  
        |4|array|  
        |5|objeto|  
  
     Solo se devuelven las propiedades de primer nivel. La instrucción produce un error si el texto JSON no se formateó correctamente.  

2. Cuando se llama a OPENJSON y especificar un esquema explícito en la cláusula WITH, la función devuelve una tabla con el esquema que ha definido en la cláusula WITH.  

## <a name="remarks"></a>Comentarios  

*json_path* usada en el segundo argumento de **OPENJSON** o en *with_clause* puede comenzar con la **lax** o **estricta** palabra clave.

-   En **lax** modo, **OPENJSON** no se genera un error si no se encuentra el objeto o el valor en la ruta de acceso especificada. Si no se encuentra la ruta de acceso, **OPENJSON** devuelve un conjunto de resultados vacío o un valor NULL.
-   En **estricta**, modo **OPENJSON** devuelve un error si no se encuentra la ruta de acceso.

Algunos de los ejemplos en esta página especifican explícitamente el modo de ruta de acceso, lax o strict. El modo de ruta de acceso es opcional. Si no especifica explícitamente un modo de ruta de acceso, el modo lax es el valor predeterminado. Para obtener más información acerca del modo de ruta de acceso y expresiones de ruta de acceso, consulte [expresiones de ruta de acceso JSON &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).    

Nombres de columna en *with_clause* se hacen coincidir con las claves en el texto JSON. Si especifica el nombre de columna `[Address.Country]`, se compara con la clave `Address.Country`. Si desea hacer referencia a una clave anidada `Country` dentro del objeto `Address`, tendrá que especificar la ruta de acceso `$.Address.Country` en la ruta de acceso de columna.

*json_path* puede contener claves con caracteres alfanuméricos. El nombre de clave en *json_path* entre comillas dobles si hay caracteres especiales en las claves. Por ejemplo, `$."my key $1".regularKey."key with . dot"` coincide con el valor 1 en el siguiente texto JSON:

```json
{
  "my key $1": {
    "regularKey":{
      "key with . dot": 1
    }
  }
}
```  

## <a name="examples"></a>Ejemplos  
  
### <a name="example-1---convert-a-json-array-to-a-temporary-table"></a>Ejemplo 1: convertir una matriz JSON en una tabla temporal  
En el ejemplo siguiente se proporciona una lista de identificadores como una matriz JSON de números. La consulta convierte la matriz JSON en una tabla de identificadores y filtra todos los productos con los identificadores especificados.  
  
```sql  
DECLARE @pSearchOptions NVARCHAR(4000) = N'[1,2,3,4]'

SELECT *
FROM products
INNER JOIN OPENJSON(@pSearchOptions) AS productTypes
 ON product.productTypeID = productTypes.value
```  
  
Esta consulta es equivalente al ejemplo siguiente. Sin embargo, en el ejemplo siguiente, se deben incrustar números en la consulta en lugar de pasarlos como parámetros.  
  
```sql  
SELECT *
FROM products
WHERE product.productTypeID IN (1,2,3,4)
```  
  
### <a name="example-2---merge-properties-from-two-json-objects"></a>Ejemplo 2: propiedades de la combinación de dos objetos JSON  
En el ejemplo siguiente se seleccionan una unión de todas las propiedades de dos objetos JSON. Los dos objetos tienen un duplicado *nombre* propiedad. En el ejemplo se utiliza el valor de clave que se excluirán los resultados en la fila duplicada.  
  
```sql  
DECLARE @json1 NVARCHAR(MAX),@json2 NVARCHAR(MAX)

SET @json1=N'{"name": "John", "surname":"Doe"}'

SET @json2=N'{"name": "John", "age":45}'

SELECT *
FROM OPENJSON(@json1)
UNION ALL
SELECT *
FROM OPENJSON(@json2)
WHERE [key] NOT IN (SELECT [key] FROM OPENJSON(@json1))
```  
  
### <a name="example-3---join-rows-with-json-data-stored-in-table-cells-using-cross-apply"></a>Ejemplo 3: filas de combinación con datos JSON almacenados en las celdas de tabla con CROSS APPLY  
En el ejemplo siguiente, la `SalesOrderHeader` tabla tiene un `SalesReason` columna de texto que contiene una matriz de `SalesOrderReasons` en formato JSON. El `SalesOrderReasons` objetos contienen propiedades como *calidad* y *fabricante*. En el ejemplo se crea un informe que combina cada fila de pedido de ventas y las razones de ventas relacionadas. El operador OPENJSON expande la matriz JSON de razones de venta como si las razones se almacenaran en una tabla secundaria independiente. A continuación, el operador CROSS APPLY combina cada fila de pedido de ventas con las filas devueltas por la función con valores de tabla OPENJSON.  
  
```sql  
SELECT SalesOrderID,OrderDate,value AS Reason
FROM Sales.SalesOrderHeader
CROSS APPLY OPENJSON(SalesReasons)
```  
  
> [!TIP] 
> Cuando tenga que expandir matrices JSON almacenan en campos individuales y combinación con sus filas primarias, que se usa normalmente el [!INCLUDE[tsql](../../includes/tsql-md.md)] operador CROSS APPLY. Para obtener más información acerca de CROSS APPLY, consulte [FROM &#40; Transact-SQL &#41; ](../../t-sql/queries/from-transact-sql.md).  
  
La misma consulta puede modificarse mediante el uso de `OPENJSON` con un esquema definido explícitamente de filas que se va a devolver:  
  
```sql  
SELECT SalesOrderID, OrderDate, value AS Reason  
FROM Sales.SalesOrderHeader  
     CROSS APPLY OPENJSON (SalesReasons) WITH (value nvarchar(100) '$')
```  
  
En este ejemplo, el `$` ruta de acceso hace referencia a cada elemento de la matriz. Si desea convertir explícitamente el valor devuelto, puede usar este tipo de consulta.  
  
### <a name="example-4---combine-relational-rows-and-json-elements-with-cross-apply"></a>Ejemplo 4: combinar filas relacional y elementos JSON con CROSS APPLY  
La consulta siguiente combina filas relacional y los elementos JSON en los resultados mostrados en la tabla siguiente.  
  
```sql  
SELECT store.title, location.street, location.lat, location.long  
FROM store  
CROSS APPLY OPENJSON(store.jsonCol, 'lax $.location')   
     WITH (street varchar(500) ,  postcode  varchar(500) '$.postcode' ,  
     lon int '$.geo.longitude', lat int '$.geo.latitude')  
     AS location
```  
  
**Resultado**  
  
|title|street|código postal|LON|LAT|  
|-----------|------------|--------------|---------|---------|  
|Tiendas de comestibles todo|Forma de Redmond 17991|WA 98052|47.666124|-122.10155|  
|Sears|148th Ave NE|WA 98052|47.63024|-122.141246,17|  
  
### <a name="example-5---import-json-data-into-sql-server"></a>Ejemplo 5: importar datos JSON en SQL Server  
En el ejemplo siguiente se carga un objeto JSON completo en una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
```sql  
DECLARE @json NVARCHAR(max)  = N'{  
  "id" : 2,  
  "firstName": "John",  
  "lastName": "Smith",  
  "isAlive": true,  
  "age": 25,  
  "dateOfBirth": "2015-03-25T12:00:00",  
  "spouse": null  
  }';  
   
  INSERT INTO Person  
  SELECT *   
  FROM OPENJSON(@json)  
  WITH (id int,  
        firstName nvarchar(50), lastName nvarchar(50),   
        isAlive bit, age int,  
        dateOfBirth datetime2, spouse nvarchar(50)
```  
  
## <a name="see-also"></a>Vea también  
 [Expresiones de ruta de acceso JSON &#40; SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [Convertir datos JSON en filas y columnas con OPENJSON &#40; SQL Server &#41;](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)   
 [Uso de OPENJSON con el esquema predeterminado &#40; SQL Server &#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md)   
 [Uso de OPENJSON con un esquema explícito &#40; SQL Server &#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md)  
  
  

