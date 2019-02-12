---
title: nodes() (método del tipo de datos XML) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- nodes() method
- nodes method
ms.assetid: 7267fe1b-2e34-4213-8bbf-1c953822446c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 58a2a76cd79f7dded8fca3ded72dcaeaf4572482
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034156"
---
# <a name="nodes-method-xml-data-type"></a>nodes() (método del tipo de datos XML)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  El método **nodes()** es muy útil si desea dividir una instancia de tipo de datos **xml** en datos relacionales. Permite identificar nodos que se asignarán a una fila nueva.  
  
 Cada instancia de tipo de datos **xml** tiene un nodo de contexto proporcionado de manera implícita. En el caso de la instancia XML almacenada en una columna o variable, éste es el nodo de documento. El nodo de documento es el nodo implícito situado en la parte superior de cada instancia de tipo de datos **xml**.  
  
 El resultado del método **nodes()** es un conjunto de datos que contiene copias lógicas de las instancias XML originales. En estas copias lógicas, el nodo de contexto de cada instancia de fila se establece en uno de los nodos identificados con la expresión de consulta, de manera que las consultas posteriores pueden navegar de forma relativa hasta estos nodos de contexto.  
  
 Puede recuperar varios valores del conjunto de filas. Por ejemplo, puede aplicar el método **value()** al conjunto de filas devuelto por **nodes()** y recuperar varios valores de la instancia XML original. Tenga en cuenta que el método **value()**, cuando se aplica a la instancia XML, devuelve solo un valor.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
nodes (XQuery) as Table(Column)  
```  
  
## <a name="arguments"></a>Argumentos  
 *XQuery*  
 Es un literal de cadena, una expresión XQuery. Si la expresión de consulta construye nodos, éstos se exponen en el conjunto de filas resultante. Si la expresión de consulta da lugar a una secuencia vacía, el conjunto de filas estará vacío. Si la expresión de consulta da lugar estáticamente a una secuencia que contiene valores atómicos en lugar de nodos, se produce un error estático.  
  
 *Table*(*Column*)  
 Es el nombre de tabla y el nombre de columna del conjunto de filas resultante.  
  
## <a name="remarks"></a>Notas  
 Por ejemplo, imagine que tiene la tabla siguiente:  
  
```  
T (ProductModelID int, Instructions xml)  
```  
  
 En la tabla se almacena el siguiente documento de instrucciones de fabricación. Solo se muestra un fragmento. Tenga en cuenta que hay tres ubicaciones de fabricación en el documento.  
  
```  
<root>  
  <Location LocationID="10"...>  
     <step>...</step>  
     <step>...</step>  
      ...  
  </Location>  
  <Location LocationID="20" ...>  
       ...  
  </Location>  
  <Location LocationID="30" ...>  
       ...  
  </Location>  
</root>  
```  
  
 Una invocación del método `nodes()` con la expresión de consulta `/root/Location` devolvería un conjunto de filas con tres filas, cada una de ellas con una copia lógica del documento XML original y con el elemento de contexto establecido en uno de los nodos `<Location>`:  
  
```  
Product  
ModelID      Instructions  
----------------------------------  
1       <root>  
             <Location LocationID="20" ... />  
             <Location LocationID="30" .../></root>  
1      <root><Location LocationID="10" ... />  
  
             <Location LocationID="30" .../></root>  
1      <root><Location LocationID="10" ... />  
             <Location LocationID="20" ... />  
             </root>  
```  
  
 Tras ello, puede consultar este conjunto de filas usando métodos del tipo de datos **xml**. La siguiente consulta extrae el subárbol del elemento de contexto de cada fila generada:  
  
```  
SELECT T2.Loc.query('.')  
FROM   T  
CROSS APPLY Instructions.nodes('/root/Location') as T2(Loc)   
```  
  
 El resultado es el siguiente:  
  
```  
ProductModelID  Instructions  
----------------------------------  
1        <Location LocationID="10" ... />  
1        <Location LocationID="20" ... />  
1        <Location LocationID="30" .../>  
```  
  
 Observe que el conjunto de filas devuelto ha mantenido la información de tipo. Puede aplicar métodos del tipo de datos **xml** como **query()**, **value()**, **exist()** y **nodes()** al resultado de un método **nodes()**. En cambio, no puede aplicar el método **modify()** para modificar la instancia XML.  
  
 Asimismo, el nodo de contexto del conjunto de filas no se puede materializar. Es decir, no puede utilizarlo en una instrucción SELECT. Sin embargo, puede utilizarlo en IS NULL y COUNT(*).  
  
 Los escenarios para usar el método **nodes()** son los mismos que para usar [OPENXML &#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md). Esto proporciona una vista del conjunto de filas del documento XML. En cambio, no tiene que usar cursores cuando emplea el método **nodes()** en una tabla que contenga varias filas de documentos XML.  
  
 Observe que el conjunto de filas devuelto por el método **nodes()** no tiene nombre. Por tanto, se le debe dar un nombre de manera explícita utilizando alias.  
  
 La función **nodes()** no puede aplicarse directamente a los resultados de una función definida por el usuario. Para usar la función **nodes()** con el resultado de una función escalar definida por el usuario, puede asignar el resultado de la función definida por el usuario a una variable o usar una tabla derivada para asignar un alias de columna al valor devuelto de la función definida por el usuario y luego usar CROSS APPLY para seleccionar del alias.  
  
 En el ejemplo siguiente se muestra una forma de usar `CROSS APPLY` para seleccionar entre los resultados de una función definida por el usuario.  
  
```  
USE AdventureWorks;  
GO  
  
CREATE FUNCTION XTest()  
RETURNS xml  
AS  
BEGIN  
RETURN '<document/>';  
END;  
GO  
  
SELECT A2.B.query('.')  
FROM  
(SELECT dbo.XTest()) AS A1(X)   
CROSS APPLY X.nodes('.') A2(B);  
GO  
  
DROP FUNCTION XTest;  
GO  
```  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="using-nodes-method-against-a-variable-of-xml-type"></a>Usar el método nodes() con una variable de tipo xml  
 En el siguiente ejemplo, hay un documento XML que incluye un elemento <`Root`> de nivel superior y tres elementos secundarios <`row`>. La consulta utiliza el método `nodes()` para establecer nodos de contexto independientes, uno para cada elemento <`row`>. El método `nodes()` devuelve un conjunto de tres filas. Cada fila tiene una copia lógica del documento original, donde cada nodo de contexto identifica un elemento <`row`> distinto del documento original.  
  
 La consulta devuelve después el nodo de contexto de cada fila:  
  
```  
DECLARE @x xml   
SET @x='<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>'  
SELECT T.c.query('.') AS result  
FROM   @x.nodes('/Root/row') T(c)  
GO  
```  
  
 A continuación se muestra el resultado. En este ejemplo, el método de consulta devuelve el elemento de contexto y su contenido:  
  
```  
<row id="1"><name>Larry</name><oflw>some text</oflw></row>  
<row id="2"><name>moe</name></row>  
<row id="3"/>  
```  
  
 Si se aplica el descriptor de acceso primario en los nodos de contexto, devuelve el elemento <`Root`> para los tres:  
  
```  
SELECT T.c.query('..') AS result  
FROM   @x.nodes('/Root/row') T(c)  
go  
```  
  
 El resultado es el siguiente:  
  
```  
<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>  
<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>  
<Root>  
    <row id="1"><name>Larry</name><oflw>some text</oflw></row>  
    <row id="2"><name>moe</name></row>  
    <row id="3" />  
</Root>  
```  
  
### <a name="specifying-the-nodes-method-against-a-column-of-xml-type"></a>Especificar el método nodes() con una columna de tipo xml  
 En este ejemplo se usan las instrucciones de fabricación de bicicletas y se almacenan en la columna Instructions de tipo **xml** de la tabla **ProductModel**.  
  
 En el siguiente ejemplo, el método `nodes()` se especifica para la columna `Instructions` de tipo **xml** de la tabla `ProductModel`.  
  
 El método `nodes()` establece los elementos <`Location`> como nodos de contexto especificando la ruta de acceso `/MI:root/MI:Location`. El conjunto de filas resultante incluye copias lógicas del documento original, una para cada nodo <`Location`> del documento, con el nodo de contexto establecido en el elemento <`Location`>. Por tanto, la función `nodes()` ofrece un conjunto de nodos de contexto <`Location`>.  
  
 El método `query()` sobre este conjunto de resultados solicita `self::node` y, por lo tanto, devuelve el elemento `<Location>` de cada fila.  
  
 En este ejemplo, la consulta establece cada elemento <`Location`> como un nodo de contexto en el documento de instrucciones de fabricación del modelo de producto específico. Puede utilizar estos nodos de contexto para recuperar valores como los siguientes:  
  
-   Encontrar los identificadores de ubicación de cada <`Location`>  
  
-   Recuperar pasos de fabricación (elementos <`step`> secundarios) en cada <`Location`>  
  
 Esta consulta devuelve el elemento de contexto, en el que se especifica la sintaxis abreviada `'.'` para `self::node()`, en el método `query()`.  
  
 Observe lo siguiente:  
  
-   El método `nodes()` se aplica a la columna Instructions y devuelve un conjunto de filas, `T (C)`. Este conjunto de filas contiene copias lógicas del documento de instrucciones de fabricación original con `/root/Location` como elemento de contexto.  
  
-   CROSS APPLY aplica `nodes()` a cada fila de la tabla `Instructions` y devuelve solo las filas que producen un conjunto de resultados.  
  
    ```  
    SELECT C.query('.') as result  
    FROM Production.ProductModel  
    CROSS APPLY Instructions.nodes('  
    declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
    /MI:root/MI:Location') as T(C)  
    WHERE ProductModelID=7  
    ```  
  
     Éste es el resultado parcial:  
  
    ```  
    <MI:Location LocationID="10"  ...>  
       <MI:step ... />  
          ...  
    </MI:Location>  
    <MI:Location LocationID="20"  ... >  
        <MI:step ... />  
          ...  
    </MI:Location>  
    ...  
    ```  
  
### <a name="applying-nodes-to-the-rowset-returned-by-another-nodes-method"></a>Aplicar nodes() al conjunto de filas devuelto por otro método nodes()  
 El código siguiente realiza una consulta en los documentos XML sobre instrucciones de fabricación en la columna `Instructions` de la tabla `ProductModel`. La consulta devuelve un conjunto de filas que contiene el Id. del modelo de producto, las ubicaciones y los pasos de fabricación.  
  
 Observe lo siguiente:  
  
-   El método `nodes()` se aplica a la columna `Instructions` y devuelve el conjunto de filas `T1 (Locations)`. Este conjunto de filas contiene copias lógicas del documento de instrucciones de fabricación original con el elemento `/root/Location` como contexto del elemento.  
  
-   `nodes()` se aplica al conjunto de filas `T1 (Locations)` y devuelve el conjunto de filas `T2 (steps)`. Este conjunto de filas contiene copias lógicas del documento de instrucciones de fabricación original con el elemento `/root/Location/step` como contexto del elemento.  
  
```  
SELECT ProductModelID, Locations.value('./@LocationID','int') as LocID,  
steps.query('.') as Step         
FROM Production.ProductModel         
CROSS APPLY Instructions.nodes('         
declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
/MI:root/MI:Location') as T1(Locations)         
CROSS APPLY T1.Locations.nodes('         
declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
./MI:step ') as T2(steps)         
WHERE ProductModelID=7         
GO         
```  
  
 El resultado es el siguiente:  
  
```  
ProductModelID LocID Step         
----------------------------         
7      10   <step ... />         
7      10   <step ... />         
...         
7      20   <step ... />         
7      20   <step ... />         
7      20   <step ... />         
...         
```  
  
 La consulta declara el prefijo `MI` dos veces. En su lugar, puede utilizar `WITH XMLNAMESPACES` para declarar el prefijo una vez y utilizarlo en la consulta:  
  
```  
WITH XMLNAMESPACES (  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions'  AS MI)  
  
SELECT ProductModelID, Locations.value('./@LocationID','int') as LocID,  
steps.query('.') as Step         
FROM Production.ProductModel         
CROSS APPLY Instructions.nodes('         
/MI:root/MI:Location') as T1(Locations)         
CROSS APPLY T1.Locations.nodes('         
./MI:step ') as T2(steps)         
WHERE ProductModelID=7         
GO    
```  
  
## <a name="see-also"></a>Consulte también  
 [Agregar espacios de nombres a consultas con WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Crear instancias de datos XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [Métodos del tipo de datos xml](../../t-sql/xml/xml-data-type-methods.md)  
  
  
