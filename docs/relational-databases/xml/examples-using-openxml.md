---
title: 'Ejemplos: usar OPENXML | Microsoft Docs'
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ColPattern [XML in SQL Server]
- XML [SQL Server], mapping data
- OPENXML statement, about OPENXML statement
- overflow in XML document [SQL Server]
- mapping XML data [SQL Server]
- combining attribute-centric and element centric mapping
- unconsumed data
- attribute-centric mapping
- column patterns [XML in SQL Server]
- XML [SQL Server], overflow handling
- row patterns [XML in SQL Server]
- rowpattern [XML in SQL Server]
- flags parameter
- element-centric mapping [SQL Server]
- edge tables
ms.assetid: 689297f3-adb0-4d8d-bf62-cfda26210164
caps.latest.revision: 36
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: edd4106a1e58631112337d0dcae8da78907a519d
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39087487"
---
# <a name="examples-using-openxml"></a>Ejemplos: usar OPENXML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Los ejemplos de este tema muestran cómo se utiliza OPENXML para crear una vista de conjunto de filas de un documento XML. Para obtener más información sobre la sintaxis de OPENXML, vea [OPENXML &#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md). Los ejemplos muestran todos los aspectos de OPENXML, pero no especifican metapropiedades en OPENXML. Para obtener más información sobre cómo especificar metapropiedades en OPENXML, vea [Especificar metapropiedades en OPENXML](../../relational-databases/xml/specify-metaproperties-in-openxml.md).  
  
## <a name="examples"></a>Ejemplos  
 Al recuperar los datos, se utiliza *rowpattern* para identificar los nodos del documento XML que determinan las filas. Además, *rowpattern* se expresa en el lenguaje del patrón XPath que se utiliza en la implementación XPath de MSXML. Por ejemplo, si el patrón termina en un elemento o atributo, se crea una fila para cada nodo de elemento o atributo que *rowpattern*seleccione.  
  
 El valor *flags* proporciona una asignación predeterminada. Si no se especifica *ColPattern* en *SchemaDeclaration*, se asume la asignación especificada en *flags* . El valor *flags* se omite si se especifica *ColPattern* en *SchemaDeclaration*. La especificación *ColPattern* determina la asignación (centrada en atributos o elementos) y también el comportamiento para manejar los datos de desbordamiento y los no usados.  
  
### <a name="a-executing-a-simple-select-statement-with-openxml"></a>A. Ejecutar una instrucción SELECT simple con OPENXML  
 El documento XML de este ejemplo se compone de los elementos <`Customer`>, <`Order`> y <`OrderDetail`>. La instrucción OPENXML recupera información del cliente del documento XML en un conjunto de filas de dos columnas (**CustomerID** y **ContactName**).  
  
 Primero, para obtener un identificador de documento se llama al procedimiento almacenado **sp_xml_preparedocument** . Este identificador de documento se pasa a OPENXML.  
  
 La instrucción OPENXML muestra lo siguiente:  
  
-   *rowpattern* (/ROOT/Customer) identifica los nodos <`Customer`> que se van a procesar.  
  
-   El valor del parámetro *flags* se establece en **1** e indica una asignación centrada en atributos. Como resultado, los atributos XML se asignan a las columnas del conjunto de filas definido en *SchemaDeclaration*.  
  
-   En *SchemaDeclaration*, en la cláusula WITH, los valores *ColName* especificados coinciden con los nombres de atributo XML correspondientes. Por lo tanto, el parámetro *ColPattern* no se especifica en *SchemaDeclaration*.  
  
 A continuación, la instrucción SELECT recupera todas las columnas del conjunto de filas que proporciona OPENXML.  
  
```  
DECLARE @DocHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
          OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
          OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @DocHandle OUTPUT, @XmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@DocHandle, '/ROOT/Customer',1)  
      WITH (CustomerID  varchar(10),  
            ContactName varchar(20))  
EXEC sp_xml_removedocument @DocHandle  
```  
  
 El resultado es el siguiente:  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 Si se ejecuta la misma instrucción SELECT con el parámetro *flags* establecido en **2** para indicar una asignación centrada en elementos, puesto que los elementos <`Customer`> no disponen de subelementos, los valores de **CustomerID** y **ContactName** de ambos clientes se devuelven como NULL.  
  
 \@xmlDocument también puede ser de tipo **xml** o de tipo **(n)varchar(max)**.  
  
 En el documento XML, si <`CustomerID`> y <`ContactName`> son subelementos, la asignación centrada en elementos recupera los valores.  
  
```  
DECLARE @XmlDocumentHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer>  
   <CustomerID>VINET</CustomerID>  
   <ContactName>Paul Henriot</ContactName>  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5" OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer>     
   <CustomerID>LILAS</CustomerID>  
   <ContactName>Carlos Gonzlez</ContactName>  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3" OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @XmlDocumentHandle OUTPUT, @XmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT    *  
FROM      OPENXML (@XmlDocumentHandle, '/ROOT/Customer',2)  
           WITH (CustomerID  varchar(10),  
                 ContactName varchar(20))  
EXEC sp_xml_removedocument @XmlDocumentHandle  
```  
  
 El resultado es el siguiente:  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 Observe que el identificador de documento devuelto por **sp_xml_preparedocument** es válido mientras dura el proceso por lotes y no la sesión.  
  
### <a name="b-specifying-colpattern-for-mapping-between-rowset-columns-and-the-xml-attributes-and-elements"></a>B. Especificar ColPattern para la asignación entre columnas del conjunto de filas y los atributos y elementos XML  
 Este ejemplo muestra cómo se especifica el patrón XPath en el parámetro opcional *ColPattern* para proporcionar una asignación entre columnas del conjunto de filas y los atributos y elementos XML.  
  
 El documento XML de este ejemplo se compone de los elementos <`Customer`>, <`Order`> y <`OrderDetail`>. La instrucción OPENXML recupera información del cliente y del pedido del documento XML en forma de conjunto de filas (**CustomerID**, **OrderDate**, **ProdID** y **Qty**).  
  
 Primero, para obtener un identificador de documento se llama al procedimiento almacenado **sp_xml_preparedocument** . Este identificador de documento se pasa a OPENXML.  
  
 La instrucción OPENXML muestra lo siguiente:  
  
-   *rowpattern* (/ROOT/Customer/Order/OrderDetail) identifica los nodos <`OrderDetail`> que se van a procesar.  
  
 A modo de ilustración, el valor del parámetro *flags* se establece en **2** e indica una asignación centrada en elementos. Sin embargo, la asignación especificada en *ColPattern* sobrescribe esta asignación. Es decir, el patrón XPath especificado en *ColPattern* asigna a atributos las columnas del conjunto de filas. El resultado es una asignación centrada en atributos.  
  
 En *SchemaDeclaration*, en la cláusula WITH, también se especifica *ColPattern* con los parámetros *ColName* y *ColType* . El parámetro opcional *ColPattern* es el patrón XPath especificado e indica lo siguiente:  
  
-   Las columnas **OrderID**, **CustomerID** y **OrderDate** del conjunto de filas se asignan a los atributos del elemento primario de los nodos identificados por *rowpattern*, y *rowpattern* identifica los nodos <`OrderDetail`>. Por lo tanto, las columnas **CustomerID** y **OrderDate** se asignan a los atributos **CustomerID** y **OrderDate** del elemento <`Order`>.  
  
-   Las columnas **ProdID** y **Qty** del conjunto de filas se asignan a los atributos **ProductID** y **Quantity** de los nodos identificados en *rowpattern*.  
  
 A continuación, la instrucción SELECT recupera todas las columnas del conjunto de filas que proporciona OPENXML.  
  
```  
DECLARE @XmlDocumentHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
           OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
           OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @XmlDocumentHandle OUTPUT, @XmlDocument  
-- Execute a SELECT stmt using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@XmlDocumentHandle, '/ROOT/Customer/Order/OrderDetail',2)  
WITH (OrderID     int         '../@OrderID',  
      CustomerID  varchar(10) '../@CustomerID',  
      OrderDate   datetime    '../@OrderDate',  
      ProdID      int         '@ProductID',  
      Qty         int         '@Quantity')  
EXEC sp_xml_removedocument @XmlDocumentHandle  
```  
  
 El resultado es el siguiente:  
  
```  
OrderID CustomerID        OrderDate          ProdID    Qty  
-------------------------------------------------------------  
10248    VINET     1996-07-04 00:00:00.000     11       12  
10248    VINET     1996-07-04 00:00:00.000     42       10  
10283    LILAS     1996-08-16 00:00:00.000     72        3  
```  
  
 El patrón XPath especificado como *ColPattern* también puede especificarse para asignar los elementos XML a las columnas del conjunto de filas. El resultado es una asignación centrada en elementos. En el siguiente ejemplo, en el documento XML, <`CustomerID`> y <`OrderDate`> son subelementos del elemento <`Orders`>. Dado que *ColPattern* sobrescribe la asignación especificada en el parámetro *flags*, este no se especifica en OPENXML.  
  
```  
DECLARE @docHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order EmployeeID="5" >  
      <OrderID>10248</OrderID>  
      <CustomerID>VINET</CustomerID>  
      <OrderDate>1996-07-04T00:00:00</OrderDate>  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order  EmployeeID="3" >  
      <OrderID>10283</OrderID>  
      <CustomerID>LILAS</CustomerID>  
      <OrderDate>1996-08-16T00:00:00</OrderDate>  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @XmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer/Order/OrderDetail')  
WITH (CustomerID  varchar(10)   '../CustomerID',  
      OrderDate   datetime      '../OrderDate',  
      ProdID      int           '@ProductID',  
      Qty         int           '@Quantity')  
EXEC sp_xml_removedocument @docHandle  
```  
  
### <a name="c-combining-attribute-centric-and-element-centric-mapping"></a>C. Combinar asignaciones centradas en elementos y en atributos  
 En este ejemplo, el parámetro *flags* se establece en **3** , lo que indica que se aplicarán tanto la asignación centrada en elementos como en atributos. En este caso, primero se aplica la asignación centrada en atributos y, a continuación, la centrada en elementos, en todas las columnas donde aún no se ha hecho.  
  
```  
DECLARE @docHandle int  
DECLARE @XmlDocument nvarchar(1000)  
SET @XmlDocument =N'<ROOT>  
<Customer CustomerID="VINET"  >  
     <ContactName>Paul Henriot</ContactName>  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
          OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" >   
     <ContactName>Carlos Gonzlez</ContactName>  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
          OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @XmlDocument  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer',3)  
      WITH (CustomerID  varchar(10),  
            ContactName varchar(20))  
EXEC sp_xml_removedocument @docHandle  
```  
  
 El resultado es el siguiente  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 La asignación centrada en atributos se aplica para **CustomerID**. No existe ningún atributo **ContactName** en el elemento <`Customer`>. Por lo tanto, se aplica la asignación centrada en elementos.  
  
### <a name="d-specifying-the-text-xpath-function-as-colpattern"></a>D. Especificar la función text() de XPath como ColPattern  
 El documento XML de este ejemplo se compone de los elementos <`Customer`> y <`Order`>. La instrucción OPENXML recupera un conjunto de filas que está compuesto por el atributo **oid** del elemento <`Order`>, el identificador del elemento primario del nodo identificado por *rowpattern* y la cadena del valor de hoja del contenido de elemento.  
  
 Primero, para obtener un identificador de documento se llama al procedimiento almacenado **sp_xml_preparedocument**. Este identificador de documento se pasa a OPENXML.  
  
 La instrucción OPENXML muestra lo siguiente:  
  
-   *rowpattern* (/root/Customer/Order) identifica los nodos <`Order`> que se van a procesar.  
  
-   El valor del parámetro *flags* se establece en **1** e indica una asignación centrada en atributos. Como resultado, los atributos XML se asignan a columnas del conjunto de filas definido en *SchemaDeclaration*.  
  
-   En *SchemaDeclaration* , en la cláusula WITH, los nombres de columna del conjunto de filas **oid** y **amount** coinciden con los nombres de atributo XML correspondientes. Por lo tanto, no se especifica el parámetro *ColPattern* . En la columna **comment** del conjunto de filas, la función **text()** de XPath se especifica como *ColPattern*. Esto sobrescribe la asignación centrada en atributos especificada en *flags*y la columna contiene la cadena del valor de hoja del contenido del elemento.  
  
 A continuación, la instrucción SELECT recupera todas las columnas del conjunto de filas que proporciona OPENXML.  
  
```  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
--sample XML document  
SET @xmlDocument =N'<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very satisfied  
      </Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue   
             white red">  
            <Urgency>Important</Urgency>  
            Happy Customer.  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/root/Customer/Order', 1)  
     WITH (oid     char(5),   
           amount  float,   
           comment ntext 'text()')  
EXEC sp_xml_removedocument @docHandle  
```  
  
 El resultado es el siguiente:  
  
```  
oid   amount        comment  
----- -----------   -----------------------------  
O1    3.5           NULL  
O2    13.4          Customer was very satisfied  
O3    100.0         Happy Customer.  
O4    10000.0       NULL  
```  
  
### <a name="e-specifying-tablename-in-the-with-clause"></a>E. Especificar TableName en la cláusula WITH  
 Este ejemplo especifica *TableName* en la cláusula WITH, en lugar de *SchemaDeclaration*. Resulta útil si dispone de una tabla con la estructura deseada y no se requieren patrones de columnas (parámetro *ColPattern* ).  
  
 El documento XML de este ejemplo se compone de los elementos <`Customer`> y <`Order`>. La instrucción OPENXML recupera información del pedido en un conjunto de filas de tres columnas (**oid**, **date** y **amount**) del documento XML.  
  
 Primero, para obtener un identificador de documento se llama al procedimiento almacenado **sp_xml_preparedocument** . Este identificador de documento se pasa a OPENXML.  
  
 La instrucción OPENXML muestra lo siguiente:  
  
-   *rowpattern* (/root/Customer/Order) identifica los nodos <`Order`> que se van a procesar.  
  
-   No existe ninguna *SchemaDeclaration* en la cláusula WITH. En vez de eso, se especifica un nombre de tabla. Por lo tanto, el esquema de tabla se utiliza como esquema del conjunto de filas.  
  
-   El valor del parámetro *flags* se establece en **1** e indica una asignación centrada en atributos. Por lo tanto, los atributos de los elementos, identificados por *rowpattern*, se asignan a las columnas del conjunto de filas con el mismo nombre.  
  
 A continuación, la instrucción SELECT recupera todas las columnas del conjunto de filas que proporciona OPENXML.  
  
```  
-- Create a test table. This table schema is used by OPENXML as the  
-- rowset schema.  
CREATE TABLE T1(oid char(5), date datetime, amount float)  
GO  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
-- Sample XML document  
SET @xmlDocument =N'<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very   
             satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue   
             white red">  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>'  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/root/Customer/Order', 1)  
     WITH T1  
EXEC sp_xml_removedocument @docHandle  
```  
  
 El resultado es el siguiente:  
  
```  
oid   date                        amount  
----- --------------------------- ----------  
O1    1996-01-20 00:00:00.000     3.5  
O2    1997-04-30 00:00:00.000     13.4  
O3    1999-07-14 00:00:00.000     100.0  
O4    1996-01-20 00:00:00.000     10000.0  
```  
  
### <a name="f-obtaining-the-result-in-an-edge-table-format"></a>F. Obtener el resultado en formato de tabla irregular  
 En este ejemplo, no se especifica la cláusula WITH en la instrucción OPENXML. Como resultado, el conjunto de filas que genera OPENXML tiene un formato de tabla irregular. La instrucción SELECT devuelve todas las columnas de la tabla irregular.  
  
 El documento XML del ejemplo se compone de los elementos <`Customer`>, <`Order`> y <`OrderDetail`>.  
  
 Primero, para obtener un identificador de documento se llama al procedimiento almacenado **sp_xml_preparedocument**. Este identificador de documento se pasa a OPENXML.  
  
 La instrucción OPENXML muestra lo siguiente:  
  
-   *rowpattern* (/ROOT/Customer) identifica los nodos <`Customer`> que se van a procesar.  
  
-   No se proporciona la cláusula WITH. Por esta razón, OPENXML devuelve el conjunto de filas en un formato de tabla irregular.  
  
 A continuación, la instrucción SELECT recupera todas las columnas de la tabla irregular.  
  
```  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
SET @xmlDocument = N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order CustomerID="VINET" EmployeeID="5" OrderDate=  
           "1996-07-04T00:00:00">  
      <OrderDetail OrderID="10248" ProductID="11" Quantity="12"/>  
      <OrderDetail OrderID="10248" ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order CustomerID="LILAS" EmployeeID="3" OrderDate=  
           "1996-08-16T00:00:00">  
      <OrderDetail OrderID="10283" ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer')  
  
EXEC sp_xml_removedocument @docHandle  
```  
  
 El resultado se devuelve como una tabla irregular. Puede escribir consultas con la tabla irregular para obtener información. Por ejemplo:  
  
-   La siguiente consulta devuelve el número de nodos **Customer** del documento. Dado que no se especifica la cláusula WITH, OPENXML devuelve una tabla irregular. La instrucción SELECT consulta la tabla irregular.  
  
    ```  
    SELECT count(*)  
    FROM OPENXML(@docHandle, '/')  
    WHERE localname = 'Customer'  
    ```  
  
-   La siguiente consulta devuelve los nombres locales de los nodos XML del tipo de elemento.  
  
    ```  
    SELECT distinct localname   
    FROM OPENXML(@docHandle, '/')   
    WHERE nodetype = 1   
    ORDER BY localname  
    ```  
  
### <a name="g-specifying-rowpattern-ending-with-an-attribute"></a>G. Especificar rowpattern con final en atributo  
 El documento XML de este ejemplo se compone de los elementos <`Customer`>, <`Order`> y <`OrderDetail`>. La instrucción OPENXML recupera información detallada del pedido en un conjunto de filas de tres columnas (**ProductID**, **Quantity** y **OrderID**) del documento XML.  
  
 Primero, para obtener un identificador de documento se llama a **sp_xml_preparedocument** . Este identificador de documento se pasa a OPENXML.  
  
 La instrucción OPENXML muestra lo siguiente:  
  
-   *rowpattern* (/ROOT/Customer/Order/OrderDetail/\@ProductID) termina en un atributo XML: **ProductID**. En el conjunto de filas resultante, se crea una fila por cada nodo de atributo seleccionado en el documento XML.  
  
-   En este ejemplo, no se especifica el parámetro *flags* . En su lugar, las asignaciones se especifican con el parámetro *ColPattern* .  
  
 En *SchemaDeclaration* , en la cláusula WITH, también se especifica *ColPattern* con los parámetros *ColName* y *ColType* . El parámetro opcional *ColPattern* es el patrón XPath especificado para indicar lo siguiente:  
  
-   El patrón XPath (**.**) especificado como *ColPattern* en la columna **ProdID** del conjunto de filas identifica el nodo de contexto (nodo actual). En cuanto al valor *rowpattern* especificado, es el atributo **ProductID** del elemento <`OrderDetail`>.  
  
-   *ColPattern*, **../\@Quantity**, especificado para la columna **Qty** del conjunto de filas, identifica el atributo **Quantity** del nodo principal (`OrderDetail`) del nodo de contexto \<ProductID>.  
  
-   Del mismo modo, *ColPattern*, **../../\@OrderID**, especificado para la columna **OID** del conjunto de filas, identifica el atributo **OrderID** del elemento primario (`Order`) del nodo principal del nodo de contexto. El nodo principal es <`OrderDetail`> y el nodo de contexto es <`ProductID`>.  
  
 A continuación, la instrucción SELECT recupera todas las columnas del conjunto de filas que proporciona OPENXML.  
  
```  
DECLARE @docHandle int  
DECLARE @xmlDocument nvarchar(1000)  
--Sample XML document  
SET @xmlDocument =N'<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5" OrderDate=  
           "1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3" OrderDate=  
           "1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @docHandle OUTPUT, @xmlDocument  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@docHandle, '/ROOT/Customer/Order/OrderDetail/@ProductID')  
       WITH ( ProdID  int '.',  
              Qty     int '../@Quantity',  
              OID     int '../../@OrderID')  
EXEC sp_xml_removedocument @docHandle  
```  
  
 El resultado es el siguiente:  
  
```  
ProdID      Qty         OID  
----------- ----------- -------   
11          12          10248  
42          10          10248  
72          3           10283  
```  
  
### <a name="h-specifying-an-xml-document-that-has-multiple-text-nodes"></a>H. Especificar un documento XML con varios nodos de texto  
 Si dispone de varios nodos de texto en un documento XML, una instrucción SELECT con *ColPattern*, **text()**, solamente devuelve el primer nodo de texto en lugar de todos. Por ejemplo:  
  
```  
DECLARE @h int  
EXEC sp_xml_preparedocument @h OUTPUT,  
         N'<root xmlns:a="urn:1">  
           <a:Elem abar="asdf">  
             T<a>a</a>U  
           </a:Elem>  
         </root>',  
         '<ns xmlns:b="urn:1" />'  
  
SELECT * FROM openxml(@h, '/root/b:Elem')  
      WITH (Col1 varchar(20) 'text()')  
EXEC sp_xml_removedocument @h  
```  
  
 La instrucción SELECT devuelve **T** como resultado (y no **TaU**).  
  
### <a name="i-specifying-the-xml-data-type-in-the-with-clause"></a>I. Especificar el tipo de datos xml en la cláusula WITH  
 En la cláusula WITH, un patrón de columna que se asigna a la columna de tipo de datos **xml** , tenga o no tenga tipo, debe devolver una secuencia vacía o una secuencia de elementos, instrucciones de procesamiento, nodos de texto y comentarios. Los datos se convierten a un tipo de datos **xml** .  
  
 En el siguiente ejemplo, la declaración de esquema de tabla en la cláusula WITH incluye columnas de tipo **xml** .  
  
```  
DECLARE @h int  
DECLARE @x xml  
set @x = '<Root>  
  <row id="1"><lname>Duffy</lname>  
   <Address>  
            <Street>111 Maple</Street>  
            <City>Seattle</City>  
   </Address>  
  </row>  
  <row id="2"><lname>Wang</lname>  
   <Address>  
            <Street>222 Pine</Street>  
            <City>Bothell</City>  
   </Address>  
  </row>  
</Root>'  
  
EXEC sp_xml_preparedocument @h output, @x  
SELECT *  
FROM   OPENXML (@h, '/Root/row', 10)  
      WITH (id int '@id',  
  
            lname    varchar(30),  
            xmlname  xml 'lname',  
            OverFlow xml '@mp:xmltext')  
EXEC sp_xml_removedocument @h  
```  
  
 Específicamente, se está pasando una variable de tipo **xml** (\@x) a la función **sp_xml_preparedocument()**.  
  
 El resultado es el siguiente:  
  
```  
id  lname   xmlname                   OverFlow  
--- ------- ------------------------------ -------------------------------  
1   Duffy   <lname>Duffy</lname>  <row><Address>  
                                   <Street>111 Maple</Street>  
                                   <City>Seattle</City>  
                                  </Address></row>  
2   Wang    <lname>Wang</lname>   <row><Address>  
                                    <Street>222 Pine</Street>  
                                    <City>Bothell</City>  
                                   </Address></row>  
```  
  
 Tenga en cuenta las siguientes observaciones en cuanto al resultado:  
  
-   En el caso de la columna **lname** de tipo **varchar(30)**, su valor se recupera del elemento <`lname`> correspondiente.  
  
-   En el caso de la columna **xmlname** de tipo **xml** , se devuelve el elemento del mismo nombre como su valor.  
  
-   La marca se establece en 10. El 10 significa 2 + 8, donde 2 indica asignación centrada en elementos y 8 indica que solo se pueden agregar datos XML no usados a la columna OverFlow definida en la cláusula WITH. Si la marca se establece en 2, el documento XML completo se copia en la columna OverFlow especificada en la cláusula WITH.  
  
-   Si la columna con la cláusula WITH es una columna XML con tipo y la instancia XML no se ajusta al esquema, se devuelve un error.  
  
### <a name="j-retrieving-individual-values-from-multivalued-attributes"></a>J. Recuperar valores individuales de atributos con varios valores  
 Un documento XML puede tener atributos que tienen varios valores. Por ejemplo, el atributo **IDREFS** puede tener varios valores. En un documento XML, los valores de atributo con varios valores se especifican como una cadena con los valores separados por un espacio. En el siguiente documento XML, el atributo **attends** del elemento \<Student> y el atributo **attendedBy** de \<Clase> tienen varios valores. Recuperar valores individuales de un atributo XML con varios valores y almacenar cada valor en una fila separada en la base de datos requiere un trabajo adicional. Este ejemplo muestra el proceso.  
  
 Este documento XML de ejemplo consta de los siguientes elementos:  
  
-   \<Student>  
  
     Los atributos **id** (identificador del estudiante), **name**y **attends** . El atributo **attends** es un atributo con varios valores.  
  
-   \<Class>  
  
     Los atributos **id** (identificador de la clase), **name**y **attendedBy** . El atributo **attendedBy** es un atributo con varios valores.  
  
 El atributo **attends** de \<Student> y el atributo **attendedBy** de \<Class> representan una relación **m:n** entre las tablas Student y Class. Un estudiante puede tener muchas clases y una clase puede tener varios estudiantes.  
  
 Suponga que desea dividir este documento y guardarlo en la base de datos de la forma siguiente:  
  
-   Guarde los datos de \<Student> en la tabla Students.  
  
-   Guarde los datos de \<Class> en la tabla Courses.  
  
-   Guarde los datos de la relación **m:n** (entre Student y Class) en la tabla CourseAttendence. Para extraer los valores se requiere trabajo adicional. Para recuperar esta información y almacenarla en la tabla, utilice estos procedimientos almacenados:  
  
    -   **Insert_Idrefs_Values**  
  
         Inserta los valores de Id. de curso e Id. de estudiante en la tabla CourseAttendence.  
  
    -   **Extract_idrefs_values**  
  
         Extrae los identificadores de estudiantes individuales de cada elemento \<Course>. Para recuperar estos valores se utiliza una tabla irregular.  
  
 He aquí los pasos:  
  
```  
-- Create these tables:  
DROP TABLE CourseAttendance  
DROP TABLE Students  
DROP TABLE Courses  
GO  
CREATE TABLE Students(  
                id   varchar(5) primary key,  
                name varchar(30)  
                )  
GO  
CREATE TABLE Courses(  
               id       varchar(5) primary key,  
               name     varchar(30),  
               taughtBy varchar(5)  
)  
GO  
CREATE TABLE CourseAttendance(  
             id         varchar(5) references Courses(id),  
             attendedBy varchar(5) references Students(id),  
             constraint CourseAttendance_PK primary key (id, attendedBy)  
)  
go  
-- Create these stored procedures:  
DROP PROCEDURE f_idrefs  
GO  
CREATE PROCEDURE f_idrefs  
    @t      varchar(500),  
    @idtab  varchar(50),  
    @id     varchar(5)  
AS  
DECLARE @sp int  
DECLARE @att varchar(5)  
SET @sp = 0  
WHILE (LEN(@t) > 0)  
BEGIN   
    SET @sp = CHARINDEX(' ', @t+ ' ')  
    SET @att = LEFT(@t, @sp-1)  
    EXEC('INSERT INTO '+@idtab+' VALUES ('''+@id+''', '''+@att+''')')  
    SET @t = SUBSTRING(@t+ ' ', @sp+1, LEN(@t)+1-@sp)  
END  
Go  
  
DROP PROCEDURE fill_idrefs  
GO  
CREATE PROCEDURE fill_idrefs   
    @xmldoc     int,  
    @xpath      varchar(100),  
    @from       varchar(50),  
    @to         varchar(50),  
    @idtable    varchar(100)  
AS  
DECLARE @t varchar(500)  
DECLARE @id varchar(5)  
  
/* Temporary Edge table */  
SELECT *   
INTO #TempEdge   
FROM OPENXML(@xmldoc, @xpath)  
  
DECLARE fillidrefs_cursor CURSOR FOR  
    SELECT CAST(iv.text AS nvarchar(200)) AS id,  
           CAST(av.text AS nvarchar(4000)) AS refs  
    FROM   #TempEdge c, #TempEdge i,  
           #TempEdge iv, #TempEdge a, #TempEdge av  
    WHERE  c.id = i.parentid  
    AND    UPPER(i.localname) = UPPER(@from)  
    AND    i.id = iv.parentid  
    AND    c.id = a.parentid  
    AND    UPPER(a.localname) = UPPER(@to)  
    AND    a.id = av.parentid  
  
OPEN fillidrefs_cursor  
FETCH NEXT FROM fillidrefs_cursor INTO @id, @t  
WHILE (@@FETCH_STATUS <> -1)  
BEGIN  
    IF (@@FETCH_STATUS <> -2)  
    BEGIN  
        execute f_idrefs @t, @idtable, @id  
    END  
    FETCH NEXT FROM fillidrefs_cursor INTO @id, @t  
END  
CLOSE fillidrefs_cursor  
DEALLOCATE fillidrefs_cursor  
Go  
-- This is the sample document that is shredded and the data is stored in the preceding tables.  
DECLARE @h int  
EXECUTE sp_xml_preparedocument @h OUTPUT, N'<Data>  
  <Student id = "s1" name = "Student1"  attends = "c1 c3 c6"  />  
  <Student id = "s2" name = "Student2"  attends = "c2 c4" />  
  <Student id = "s3" name = "Student3"  attends = "c2 c4 c6" />  
  <Student id = "s4" name = "Student4"  attends = "c1 c3 c5" />  
  <Student id = "s5" name = "Student5"  attends = "c1 c3 c5 c6" />  
  <Student id = "s6" name = "Student6" />  
  
  <Class id = "c1" name = "Intro to Programming"   
         attendedBy = "s1 s4 s5" />  
  <Class id = "c2" name = "Databases"   
         attendedBy = "s2 s3" />  
  <Class id = "c3" name = "Operating Systems"   
         attendedBy = "s1 s4 s5" />  
  <Class id = "c4" name = "Networks" attendedBy = "s2 s3" />  
  <Class id = "c5" name = "Algorithms and Graphs"   
         attendedBy =  "s4 s5"/>  
  <Class id = "c6" name = "Power and Pragmatism"   
         attendedBy = "s1 s3 s5" />  
</Data>'  
  
INSERT INTO Students SELECT * FROM OPENXML(@h, '//Student') WITH Students  
  
INSERT INTO Courses SELECT * FROM OPENXML(@h, '//Class') WITH Courses  
/* Using the edge table */  
EXECUTE fill_idrefs @h, '//Class', 'id', 'attendedby', 'CourseAttendance'  
  
SELECT * FROM Students  
SELECT * FROM Courses  
SELECT * FROM CourseAttendance  
  
EXECUTE sp_xml_removedocument @h  
```  
  
### <a name="k-retrieving-binary-from-base64-encoded-data-in-xml"></a>K. Recuperar datos binarios a partir de datos con codificación base64 en XML  
 Con frecuencia, se incluyen datos binarios en XML mediante codificación base64. Cuando este XML se divide mediante OPENXML, os datos se reciben con codificación base64. En este ejemplo se muestra cómo se puede convertir en binarios los datos con codificación base64.  
  
-   Cree una tabla con datos binarios de ejemplo.  
  
-   Use una consulta FOR XML y la opción BINARY BASE64 para generar XML que tenga los datos binarios codificados como base64.  
  
-   Divida el XML mediante OPENXML. Los datos devueltos por OPENXML tendrán codificación base64. A continuación, llame a la función .value para convertirlos de nuevo en binarios.  
  
```  
CREATE TABLE T (Col1 int primary key, Col2 varbinary(100))  
go  
-- Insert sample binary data  
INSERT T VALUES(1, 0x1234567890)   
go  
 -- Create test XML document that has base64 encoded binary data (use FOR XML query and specify BINARY BASE64 option)  
SELECT * FROM T  
FOR XML AUTO, BINARY BASE64  
go  
-- result  
-- <T Col1="1" Col2="EjRWeJA="/>  
  
-- Now shredd the sample XML using OPENXML.   
-- Call the .value function to convert   
-- the base64 encoded data returned by OPENXML to binary.  
DECLARE @h int ;  
EXEC sp_xml_preparedocument @h OUTPUT, '<T Col1="1" Col2="EjRWeJA="/>' ;  
SELECT Col1,   
CAST('<binary>' + Col2 + '</binary>' AS XML).value('.', 'varbinary(max)') AS BinaryCol   
FROM openxml(@h, '/T')   
WITH (Col1 integer, Col2 varchar(max)) ;  
EXEC sp_xml_removedocument @h ;  
GO  
```  
  
 Éste es el resultado. Los datos binarios devueltos son los datos binarios originales de la tabla T.  
  
```  
Col1        BinaryCol  
----------- ---------------------  
1           0x1234567890  
```  
  
## <a name="see-also"></a>Ver también  
 [sp_xml_preparedocument &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-preparedocument-transact-sql.md)   
 [sp_xml_removedocument &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-xml-removedocument-transact-sql.md)   
 [OPENXML &#40;Transact-SQL&#41;](../../t-sql/functions/openxml-transact-sql.md)   
 [OPENXML &#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
  
  
