---
title: "(tipo de datos xml) del método Value() | Documentos de Microsoft"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- value method
- value() method
ms.assetid: 298a7361-dc9a-4902-9b1e-49a093cd831d
caps.latest.revision: 38
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3b2cd81e4b96ce5c38a816c50728d794390bb383
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="value-method-xml-data-type"></a>value() (método del tipo de datos xml)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Realiza una consulta XQuery en datos XML y devuelve un valor de tipo SQL. Este método devuelve un valor escalar.  
  
 Este método se utiliza normalmente para extraer un valor de una instancia XML almacenada en un **xml** columna de tipo, parámetro o variable. De esta manera, se pueden especificar consultas SELECT que combinen o comparen datos XML con datos de columnas que no son XML.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
value (XQuery, SQLType)  
```  
  
## <a name="arguments"></a>Argumentos  
 *XQuery*  
 Es el *XQuery* expresión, un literal de cadena, que recupera los datos de la instancia XML. La expresión XQuery debe devolver un valor como máximo. En caso contrario, se devolverá un error.  
  
 *SQLType*  
 Es el tipo SQL preferido, un literal de cadena, que se devuelve. El tipo de valor devuelto de este método coincide con el *SQLType* parámetro. *SQLType* no puede ser un **xml** tipo de datos, un tipo common language runtime (CLR) definido por el usuario, **imagen**, **texto**, **ntext**, o **sql_variant** tipo de datos. *SQLType* puede ser un SQL, tipo de datos definido por el usuario.  
  
 El **value()** método usa la [!INCLUDE[tsql](../../includes/tsql-md.md)] convertir implícitamente operador e intenta convertir el resultado de la expresión XQuery, la representación de cadena serializada, del tipo XSD al tipo SQL correspondiente especificado por [!INCLUDE[tsql](../../includes/tsql-md.md)] conversión. Para obtener más información acerca de las reglas de conversión de tipo para que la conversión, consulte [CAST y CONVERT &#40; Transact-SQL &#41; ](../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
> [!NOTE]  
>  Por motivos de rendimiento, en lugar de utilizar el **value()** método en un predicado para compararlo con un valor relacional, utilice **exist()** con **SQL:Column()**. Esto se muestra en el ejemplo D a continuación.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-the-value-method-against-an-xml-type-variable"></a>A. Utilizar el método value() con una variable de tipo xml  
 En el ejemplo siguiente, una instancia XML está almacenada en una variable de tipo `xml`. El método `value()` recupera el valor del atributo `ProductID` en el XML. Después, el valor se asigna a una variable `int`.  
  
```  
DECLARE @myDoc xml  
DECLARE @ProdID int  
SET @myDoc = '<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>  
</ProductDescription>  
</Root>'  
  
SET @ProdID =  @myDoc.value('(/Root/ProductDescription/@ProductID)[1]', 'int' )  
SELECT @ProdID  
```  
  
 Como resultado se devuelve el valor 1.  
  
 Aunque hay un solo atributo `ProductID` en la instancia XML, las reglas de los tipos estáticos requieren que se especifique explícitamente que la expresión de ruta de acceso devuelva un singleton. Por tanto, se especifica `[1]` al final de la expresión de ruta de acceso. Para obtener más información acerca de tipos estáticos, vea [XQuery y tipos estáticos](../../xquery/xquery-and-static-typing.md).  
  
### <a name="b-using-the-value-method-to-retrieve-a-value-from-an-xml-type-column"></a>B. Utilizar el método value() para recuperar un valor de una columna de tipo xml  
 La siguiente consulta se especifica en un **xml** columna de tipo (`CatalogDescription`) en el `AdventureWorks` base de datos. La consulta recupera los valores del atributo `ProductModelID` de cada instancia XML almacenada en la columna.  
  
```  
SELECT CatalogDescription.value('             
    declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";             
       (/PD:ProductDescription/@ProductModelID)[1]', 'int') AS Result             
FROM Production.ProductModel             
WHERE CatalogDescription IS NOT NULL             
ORDER BY Result desc             
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   Se utiliza la palabra clave `namespace` para definir un prefijo de espacio de nombres.  
  
-   Según los requisitos de los tipos estáticos, se agrega `[1]` al final de la expresión de ruta de acceso del método `value()` para indicar explícitamente que la expresión de ruta de acceso devuelva un singleton.  
  
 Éste es el resultado parcial:  
  
```  
-----------  
35           
34           
...  
```  
  
### <a name="c-using-the-value-and-exist-methods-to-retrieve-values-from-an-xml-type-column"></a>C. Utilizar los métodos value() y exist() para recuperar valores de una columna de tipo xml  
 En el ejemplo siguiente se muestra el uso tanto la `value()` método y la [método exist()](../../t-sql/xml/exist-method-xml-data-type.md) de la **xml** tipo de datos. El método `value()` se utiliza para recuperar los valores del atributo `ProductModelID` del XML. El método `exist()` de la cláusula `WHERE` se utiliza para filtrar las filas de la tabla.  
  
 La consulta recupera los identificadores de modelo de producto de las instancias XML que incluyen información de garantía (el elemento <`Warranty`>) entre sus características. La condición de la cláusula `WHERE` utiliza el método `exist()` para recuperar únicamente las filas que cumplan esta condición.  
  
```  
SELECT CatalogDescription.value('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
           (/PD:ProductDescription/@ProductModelID)[1] ', 'int') as Result  
FROM  Production.ProductModel  
WHERE CatalogDescription.exist('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
  
     /PD:ProductDescription/PD:Features/wm:Warranty ') = 1  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   La columna `CatalogDescription` es una columna XML con tipo. Esto significa que tiene asociada una colección de esquemas. En el [prólogo de XQuery](../../xquery/modules-and-prologs-xquery-prolog.md), la declaración de espacio de nombres se utiliza para definir el prefijo que se utiliza más adelante en el cuerpo de la consulta.  
  
-   Si el método `exist()` devuelve `1` (True), significa que la instancia XML incluye el elemento secundario <`Warranty`> entre sus características.  
  
-   Después, el método `value()` de la cláusula `SELECT` recupera los valores del atributo `ProductModelID` como enteros.  
  
 Éste es el resultado parcial:  
  
```  
Result       
-----------  
19           
23           
...  
```  
  
### <a name="d-using-the-exist-method-instead-of-the-value-method"></a>D. Utilizar el método exist() en lugar del método value()  
 Por motivos de rendimiento, en lugar de utilizar el método `value()` de un predicado para compararlo con un valor relacional, utilice `exist()` con `sql:column()`. Por ejemplo:  
  
```  
CREATE TABLE T (c1 int, c2 varchar(10), c3 xml)  
GO  
  
SELECT c1, c2, c3   
FROM T  
WHERE c3.value( '/root[1]/@a', 'integer') = c1  
GO  
```  
  
 Esto se puede escribir de la forma siguiente:  
  
```  
SELECT c1, c2, c3   
FROM T  
WHERE c3.exist( '/root[@a=sql:column("c1")]') = 1  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Agregar espacios de nombres a consultas con WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Comparar XML con tipo y XML sin tipo](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Crear instancias de datos XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [métodos del tipo de datos xml](../../t-sql/xml/xml-data-type-methods.md)   
 [Lenguaje de manipulación de datos XML &#40; XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  

