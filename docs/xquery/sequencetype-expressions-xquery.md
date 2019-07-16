---
title: Expresiones SequenceType (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- SequenceType expressions
- instance of operator [XQuery]
- expressions [XQuery], SequenceType
- cast as operator
ms.assetid: ad3573da-d820-4d1c-81c4-a83c4640ce22
author: rothja
ms.author: jroth
ms.openlocfilehash: e7c3cdf33b0765ba50e5553f3bc31fd5c69312e0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946284"
---
# <a name="sequencetype-expressions-xquery"></a>Expresiones SequenceType (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  En XQuery, un valor siempre es una secuencia. Se hace referencia a los tipos de valor como tipos de secuencia. El tipo de secuencia se puede usar en un **instanci** expresión XQuery. La sintaxis SequenceType descrita en la especificación de XQuery se utiliza cuando se debe hacer referencia a un tipo de una expresión XQuery.  
  
 El nombre de tipo atómico también se puede utilizar en el **convertido** expresión XQuery. En [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], el **instanci** y **convertido** se admiten parcialmente las expresiones XQuery en SequenceTypes.  
  
## <a name="instance-of-operator"></a>Operador instance of  
 El **instanci** operador puede usarse para determinar el tipo dinámico o tiempo de ejecución, del valor de la expresión especificada. Por ejemplo:  
  
```  
  
Expression instance of SequenceType[Occurrence indicator]  
```  
  
 Tenga en cuenta que el `instance of` operador, el `Occurrence indicator`, especifica la cardinalidad, número de elementos de la secuencia resultante. Si no se especifica esto, se supone que la cardinalidad es 1. En [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], solo el signo de interrogación ( **?)**  es compatible con el indicador de repetición. ¿El **?** indicador de repetición indica que `Expression` puede devolver cero o un elemento. ¿Si el **?** se especifica el indicador de repetición, `instance of` devuelve True si el `Expression` tipo coincide con el especificado `SequenceType`, independientemente de si `Expression` devuelve un singleton o una secuencia vacía.  
  
 ¿Si el **?** no se especifica el indicador de repetición, `sequence of` solo devolverá True cuando la `Expression` escriba coincide con el `Type` especificado y `Expression` devuelve un singleton.  
  
 **Tenga en cuenta** el signo más ( **+** ) y el asterisco ( **&#42;** ) indicadores de repetición no se admiten en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Los ejemplos siguientes ilustran el uso de la**instanci** operador XQuery.  
  
### <a name="example-a"></a>Ejemplo A  
 En el ejemplo siguiente se crea un **xml** variable de tipo y especifica una consulta en ella. La expresión de consulta especifica un operador `instance of` para determinar si el tipo dinámico del valor devuelto por el primer operando coincide con el tipo especificado en el segundo operando.  
  
 La consulta siguiente devuelve True, porque el valor 125 es una instancia del tipo especificado, **xs: Integer**:  
  
```  
declare @x xml  
set @x=''  
select @x.query('125 instance of xs:integer')  
go  
```  
  
 La consulta siguiente devuelve True, pues el valor devuelto por la expresión, /a[1], del primer operando es un elemento:  
  
```  
declare @x xml  
set @x='<a>1</a>'  
select @x.query('/a[1] instance of element()')  
go  
```  
  
 De forma similar, `instance of` devuelve True en la consulta siguiente, porque el tipo de valor de la primera expresión es un atributo:  
  
```  
declare @x xml  
set @x='<a attr1="x">1</a>'  
select @x.query('/a[1]/@attr1 instance of attribute()')  
go  
```  
  
 En el ejemplo siguiente, la expresión, `data(/a[1]`, devuelve un valor atómico con el tipo xdt:untypedAtomic. Por lo tanto, el `instance of` devuelve True.  
  
```  
declare @x xml  
set @x='<a>1</a>'  
select @x.query('data(/a[1]) instance of xdt:untypedAtomic')  
go  
```  
  
 En la consulta siguiente, la expresión, `data(/a[1]/@attrA`, devuelve un valor atómico sin tipo. Por lo tanto, el `instance of` devuelve True.  
  
```  
declare @x xml  
set @x='<a attrA="X">1</a>'  
select @x.query('data(/a[1]/@attrA) instance of xdt:untypedAtomic')  
go  
```  
  
### <a name="example-b"></a>Ejemplo B  
 En este ejemplo, se consulta una columna con el tipo XML de la base de datos de ejemplo AdventureWorks. La colección de esquemas XML asociada con la columna que se consulta proporciona la información de escritura.  
  
 En la expresión, **data()** devuelve el valor del atributo ProductModelID cuyo tipo es xs: String según el esquema asociado a la columna con tipo. Por lo tanto, el `instance of` devuelve True.  
  
```  
SELECT CatalogDescription.query('  
   declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
   data(/PD:ProductDescription[1]/@ProductModelID) instance of xs:string  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 Para obtener más información, vea [Comparar XML con tipo y XML sin tipo](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
 La siguiente consulta usetheBoolean `instance of` expresión para determinar si el atributo LocationID es de tipo xs: Integer:  
  
```  
SELECT Instructions.query('  
   declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   /AWMI:root[1]/AWMI:Location[1]/@LocationID instance of attribute(LocationID,xs:integer)  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 La consulta siguiente se especifica con la columna XML de tipo CatalogDescription. La colección de esquemas XML asociada con esta columna proporciona la información de escritura.  
  
 La consulta usa la prueba `element(ElementName, ElementType?)` en la expresión `instance of` para comprobar que `/PD:ProductDescription[1]` devuelve un nodo de elemento con un nombre y un tipo específicos.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /PD:ProductDescription[1] instance of element(PD:ProductDescription, PD:ProductDescription?)  
    ') as Result  
FROM  Production.ProductModel  
where ProductModelID=19  
```  
  
 La consulta devuelve True.  
  
### <a name="example-c"></a>Ejemplo C  
 Al usar tipos de unión, el `instance of` expresión en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tiene una limitación: En concreto, cuando el tipo de un elemento o atributo es un tipo de unión, `instance of` no se puede determinar el tipo exacto. Por tanto, una consulta devolverá False, a menos que los tipos atómicos utilizados en SequenceType sean los elementos principales máximos del tipo real de la expresión de la jerarquía simpleType. Es decir, los tipos atómicos especificados en SequenceType deben ser secundarios directos de anySimpleType. Para obtener información acerca de la jerarquía de tipos, vea [reglas de conversión de tipos en XQuery](../xquery/type-casting-rules-in-xquery.md).  
  
 En la siguiente consulta de ejemplo se realiza lo siguiente:  
  
-   Se crea una colección de esquemas XML con un tipo de unión, como un tipo entero o de cadena, definido en la misma.  
  
-   Declarar un tipo **xml** variable mediante el uso de la colección de esquemas XML.  
  
-   Se asigna una instancia XML de ejemplo a la variable.  
  
-   Se consulta la variable para ilustrar el comportamiento de `instance of` cuando se trata con un tipo de unión.  
  
 Esta es la consulta:  
  
```  
CREATE XML SCHEMA COLLECTION MyTestSchema AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="http://ns" xmlns:ns="http://ns">  
<simpleType name="MyUnionType">  
<union memberTypes="integer string"/>  
</simpleType>  
<element name="TestElement" type="ns:MyUnionType"/>  
</schema>'  
Go  
```  
  
 La consulta siguiente devuelve False, pues el valor de SequenceType especificado en la expresión `instance of` no es el principal máximo del tipo real de la expresión especificada. Es decir, el valor de la <`TestElement`> es un tipo entero. El principal máximo es xs:decimal. No obstante, no se especifica como el segundo operando del operador `instance of`.  
  
```  
SET QUOTED_IDENTIFIER ON  
DECLARE @var XML(MyTestSchema)  
  
SET @var = '<TestElement xmlns="http://ns">123</TestElement>'  
  
SELECT @var.query('declare namespace ns="http://ns"   
   data(/ns:TestElement[1]) instance of xs:integer')  
go  
```  
  
 Puesto que el principal máximo de xs:integer es xs:decimal, la consulta devolverá True si se modifica la consulta y se especifica xs:decimal como SequenceType en la misma.  
  
```  
SET QUOTED_IDENTIFIER ON  
DECLARE @var XML(MyTestSchema)  
SET @var = '<TestElement xmlns="http://ns">123</TestElement>'  
SELECT @var.query('declare namespace ns="http://ns"     
   data(/ns:TestElement[1]) instance of xs:decimal')  
go  
```  
  
### <a name="example-d"></a>Ejemplo D  
 En este ejemplo, que primero cree una colección de esquemas XML y utilizarla para escribir un **xml** variable. El tipado **xml** , a continuación, se consulta la variable para ilustrar la `instance of` funcionalidad.  
  
 La colección de esquemas XML siguiente define un tipo simple, myType y un elemento, <`root`>, de tipo myType:  
  
```  
drop xml schema collection SC  
go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="myNS" xmlns:ns="myNS"  
xmlns:s="https://schemas.microsoft.com/sqlserver/2004/sqltypes">  
      <import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes"/>  
      <simpleType name="myType">  
           <restriction base="s:varchar">  
                  <maxLength value="20"/>  
            </restriction>  
      </simpleType>  
      <element name="root" type="ns:myType"/>  
</schema>'  
Go  
```  
  
 Ahora, cree un tipo **xml** variable y realiza consultas:  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "https://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
   data(/ns:root[1]) instance of ns:myType')  
go  
```  
  
 Puesto que el tipo myType procede por restricción de un tipo varchar definido en el esquema sqltypes, `instance of` también devolverá True.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<root xmlns="myNS">My data</root>'  
SELECT @var.query('declare namespace sqltypes = "https://schemas.microsoft.com/sqlserver/2004/sqltypes";  
declare namespace ns="myNS";   
data(/ns:root[1]) instance of sqltypes:varchar?')  
go  
```  
  
### <a name="example-e"></a>Ejemplo E  
 En el ejemplo siguiente, la expresión recupera uno de los valores del atributo IDREFS y utiliza `instance of` para determinar si el valor es del tipo IDREF. En el ejemplo, se realizan las tareas siguientes:  
  
-   Crea una colección de esquemas XML en la que el <`Customer`> elemento tiene un **OrderList** tipo IDREFS y la <`Order`> elemento tiene un **OrderID** atributo de tipo ID.  
  
-   Crea un tipo **xml** variable y asigna un ejemplo de XML de instancia a él.  
  
-   Se especifica una consulta con la variable. La expresión de consulta recupera el primer valor de Id. de pedido desde el atributo de tipo IDRERS OrderList del primer <`Customer`>. El valor recuperado es de tipo IDREF. Por lo tanto, `instance of` devuelve True.  
  
```  
create xml schema collection SC as  
'<schema xmlns="http://www.w3.org/2001/XMLSchema" xmlns:Customers="Customers" targetNamespace="Customers">  
            <element name="Customers" type="Customers:CustomersType"/>  
            <complexType name="CustomersType">  
                        <sequence>  
                            <element name="Customer" type="Customers:CustomerType" minOccurs="0" maxOccurs="unbounded" />  
                        </sequence>  
            </complexType>  
             <complexType name="OrderType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="OrderValue" type="integer" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="OrderID" type="ID" />  
            </complexType>  
  
            <complexType name="CustomerType">  
                <sequence minOccurs="0" maxOccurs="unbounded">  
                            <choice>  
                                <element name="spouse" type="string" minOccurs="0" maxOccurs="unbounded"/>  
                                <element name="Order" type="Customers:OrderType" minOccurs="0" maxOccurs="unbounded"/>  
                            </choice>  
                </sequence>                                             
                <attribute name="CustomerID" type="string" />  
                <attribute name="OrderList" type="IDREFS" />  
            </complexType>  
 </schema>'  
go  
declare @x xml(SC)  
set @x='<CustOrders:Customers xmlns:CustOrders="Customers">  
                <Customer CustomerID="C1" OrderList="OrderA OrderB"  >  
                              <spouse>Jenny</spouse>  
                                <Order OrderID="OrderA"><OrderValue>11</OrderValue></Order>  
                                <Order OrderID="OrderB"><OrderValue>22</OrderValue></Order>  
  
                </Customer>  
                <Customer CustomerID="C2" OrderList="OrderC OrderD" >  
                                <spouse>John</spouse>  
                                <Order OrderID="OrderC"><OrderValue>33</OrderValue></Order>  
                                <Order OrderID="OrderD"><OrderValue>44</OrderValue></Order>  
  
                        </Customer>  
                <Customer CustomerID="C3"  OrderList="OrderE OrderF" >  
                                <spouse>Jane</spouse>  
                                <Order OrderID="OrderE"><OrderValue>55</OrderValue></Order>  
                                <Order OrderID="OrderF"><OrderValue>55</OrderValue></Order>  
                </Customer>  
                <Customer CustomerID="C4"  OrderList="OrderG"  >  
                                <spouse>Tim</spouse>  
                                <Order OrderID="OrderG"><OrderValue>66</OrderValue></Order>  
                        </Customer>  
                <Customer CustomerID="C5"  >  
                </Customer>  
                <Customer CustomerID="C6" >  
                </Customer>  
                <Customer CustomerID="C7"  >  
                </Customer>  
</CustOrders:Customers>'  
  
select @x.query(' declare namespace CustOrders="Customers";   
 data(CustOrders:Customers/Customer[1]/@OrderList)[1] instance of xs:IDREF ? ') as XML_result  
```  
  
### <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones:  
  
-   El **schema-element()** y **schema-attribute()** no se admiten los tipos de secuencia para la comparación para la `instance of` operador.  
  
-   No se admiten las secuencias completas, como `(1,2) instance of xs:integer*`.  
  
-   Cuando se utiliza un formulario de la **element()** de secuencia de tipo que especifica un nombre de tipo, como `element(ElementName, TypeName)`, el tipo debe calificarse con un signo de interrogación (?). Por ejemplo, `element(Title, xs:string?)` indica que el elemento puede ser NULL. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no admite la detección de tiempo de ejecución de la **xsi: nil** propiedad mediante el uso de `instance of`.  
  
-   Si el valor de `Expression` procede de un elemento o atributo del tipo unión, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] solo podrá identificar el tipo primitivo, no derivado, del que procede el tipo del valor. Por ejemplo, si <`e1`> se define para tener un tipo estático de (xs: Integer | xs: String), el siguiente devolverá False.  
  
    ```  
    data(<e1>123</e1>) instance of xs:integer  
    ```  
  
     Sin embargo, `data(<e1>123</e1>) instance of xs:decimal` devolverá True.  
  
-   Para el **//processing-instruction ()** y **document-node()** se permiten tipos de secuencia, sólo formas sin argumentos. Por ejemplo, se admite `processing-instruction()` pero no `processing-instruction('abc')`.  
  
## <a name="cast-as-operator"></a>Operador cast as  
 El **convertido** expresión puede utilizarse para convertir un valor a un tipo de datos específico. Por ejemplo:  
  
```  
  
Expression cast as  AtomicType?  
```  
  
 En [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], se requiere el signo de interrogación (?) después de `AtomicType`. Por ejemplo, como se muestra en la siguiente consulta, `"2" cast as xs:integer?` convierte el valor de cadena en un entero:  
  
```  
declare @x xml  
set @x=''  
select @x.query('"2" cast as xs:integer?')  
```  
  
 En la siguiente consulta, **data()** devuelve el valor con tipo del atributo ProductModelID, un tipo de cadena. El `cast as`operador convierte el valor en xs: Integer.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD)  
SELECT CatalogDescription.query('  
   data(/PD:ProductDescription[1]/@ProductModelID) cast as xs:integer?  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 El uso explícito de **data()** no es necesario en esta consulta. La expresión `cast as` realiza una atomización implícita en la expresión de entrada.  
  
### <a name="constructor-functions"></a>Funciones de constructor  
 Se pueden utilizar las funciones de constructor de tipo atómico. Por ejemplo, en lugar de usar el `cast as` operador, `"2" cast as xs:integer?`, puede usar el **xs:integer()** función constructora, como en el ejemplo siguiente:  
  
```  
declare @x xml  
set @x=''  
select @x.query('xs:integer("2")')  
```  
  
 En el ejemplo siguiente se devuelve un valor xs:date equivalente a 2000-01-01Z.  
  
```  
declare @x xml  
set @x=''  
select @x.query('xs:date("2000-01-01Z")')  
```  
  
 También se pueden utilizar constructores para los tipos atómicos definidos por el usuario. Por ejemplo, si la colección de esquemas XML asociada con el tipo de datos XML define un tipo simple, un **myType()** constructor puede utilizarse para devolver un valor de ese tipo.  
  
#### <a name="implementation-limitations"></a>Limitaciones de la implementación  
  
-   Las expresiones XQuery **typeswitch**, **convertibles**, y **tratar** no se admiten.  
  
-   **convertido** requiere un signo de interrogación (?) después del tipo atómico.  
  
-   **xs: QName** no se admite como un tipo para la conversión. Use **expanded-QName** en su lugar.  
  
-   **xs: Date**, **xs: Time**, y **xs: DateTime** requieren una zona horaria, que se indica mediante una Z.  
  
     La consulta siguiente provocará un error, pues no se ha especificado ninguna zona horaria.  
  
    ```  
    DECLARE @var XML  
    SET @var = ''  
    SELECT @var.query(' <a>{xs:date("2002-05-25")}</a>')  
    go  
    ```  
  
     Si se agrega el indicador de zona horaria Z al valor, la consulta funcionará.  
  
    ```  
    DECLARE @var XML  
    SET @var = ''  
    SELECT @var.query(' <a>{xs:date("2002-05-25Z")}</a>')  
    go  
    ```  
  
     Éste es el resultado:  
  
    ```  
    <a>2002-05-25Z</a>  
    ```  
  
## <a name="see-also"></a>Vea también  
 [Expresiones XQuery](../xquery/xquery-expressions.md)   
 [Sistema de tipos &#40;XQuery&#41;](../xquery/type-system-xquery.md)  
  
  
