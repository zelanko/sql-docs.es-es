---
title: 'Especificar relaciones mediante SQL: Relationship (SQLXML 4,0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- IDREFS relationships [SQLXML]
- parent attribute [SQLXML]
- element relationships [SQLXML]
- multiple element relationships
- attribute relationships [SQLXML]
- sql:relationship
- relationship chains [SQLXML]
- IDREF relationships [SQLXML]
- parent-child relationships [SQLXML]
- relationship annotation
- XSD schemas [SQLXML], relationships
- annotated XSD schemas, relationships
- relationships [SQLXML], specifying
- unnamed relationships
- ID relationships [SQLXML]
- hierarchical relationships [SQLXML]
- named relationships [SQLXML]
ms.assetid: 98820afa-74e1-4e62-b336-6111a3dede4c
author: rothja
ms.author: jroth
ms.openlocfilehash: da461ea8715024c553a5deb29bf5a404237b979c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85002956"
---
# <a name="specifying-relationships-using-sqlrelationship-sqlxml-40"></a>Especificar relaciones mediante sql:relationship (SQLXML 4.0)
  Los elementos de un documento XML pueden estar relacionados. Los elementos pueden estar anidados jerárquicamente y pueden especificarse relaciones ID, IDREF o IDREFS entre los elementos.  
  
 Por ejemplo, en un esquema XSD, un **\<Customer>** elemento contiene **\<Order>** elementos secundarios. Cuando el esquema se asigna a la base de datos AdventureWorks, el **\<Customer>** elemento se asigna a la tabla sales. Customer y el **\<Order>** elemento se asigna a la tabla sales. SalesOrderHeader. Estas tablas subyacentes, Sales.Customer y Sales.SalesOrderHeader, están relacionadas puesto que los clientes realizan pedidos. La columna CustomerID de la tabla Sales.SalesOrderHeader es una clave externa que hace referencia a la clave principal CustomerID de la tabla Sales.Customer. Puede establecer estas relaciones entre los elementos de esquema de asignación mediante la `sql:relationship` anotación.  
  
 En el esquema XDR anotado, la anotación `sql:relationship` se usa para anidar jerárquicamente los elementos de esquema en función de las relaciones de clave principal y clave externa entre las tablas subyacentes a las que se asignan los elementos. Para especificar la anotación `sql:relationship`, debe identificar lo siguiente:  
  
-   La tabla primaria (Sales.Customer) y la tabla secundaria (Sales.SalesOrderHeader).  
  
-   La columna o las columnas que crean la relación entre las tablas primarias y secundarias. Por ejemplo, la columna CustomerID, que aparece tanto en las tablas primarias como en las secundarias.  
  
 Esta información se usa para generar la jerarquía apropiada.  
  
 Para proporcionar los nombres de tabla y la información de combinación necesaria, se especifican los siguientes atributos en la `sql:relationship` anotación. Estos atributos solo son válidos con el **\<sql:relationship>** elemento:  
  
 **Nombre**  
 Especifica el nombre único de la relación.  
  
 **Parent**  
 Especifica la relación primaria (tabla). Es un atributo opcional; si no se especifica, el nombre de la tabla primaria se obtiene a partir de la información de la jerarquía secundaria del documento. Si el esquema especifica dos jerarquías de elementos primarios y secundarios que utilizan los mismos **\<sql:relationship>** elementos primarios pero distintos, no se especifica el atributo primario en **\<sql:relationship>** . Esta información se obtiene de la jerarquía del esquema.  
  
 **parent-key**  
 Especifica la clave principal del elemento primario. Si la clave principal se compone de varias columnas, los valores se especifican con un espacio entre ellos. Hay una asignación de posición entre los valores que se especifican para la clave de varias columnas y la clave secundaria correspondiente.  
  
 **Elemento secundario**  
 Especifica la relación secundaria (tabla).  
  
 **child-key**  
 Especifica la clave secundaria del elemento secundario que hace referencia a la clave principal del elemento primario. Si la clave secundaria está compuesta de varios atributos (columnas), los valores de la clave del elemento secundario se especifican con un espacio entre ellos. Hay una asignación de posición entre los valores que se especifican para la clave de varias columnas y la clave principal correspondiente.  
  
 **Inverse**  
 Diagramas usa este atributo especificado en **\<sql:relationship>** . Para obtener más información, vea [especificar el atributo SQL: inverso en SQL: Relationship](specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md).  
  
 La `sql:key-fields` anotación debe especificarse en un elemento que contenga un elemento secundario, que tiene un **\<sql:relationship>** definido entre el elemento y el elemento secundario, y que no proporciona la clave principal de la tabla especificada en el elemento primario. Incluso si el esquema no especifica **\<sql:relationship>** , debe especificar `sql:key-fields` para generar la jerarquía adecuada. Para obtener más información, vea [identificar columnas de clave mediante SQL: Key-Fields](identifying-key-columns-using-sql-key-fields-sqlxml-4-0.md).  
  
 Para generar el anidamiento correcto en el resultado, se recomienda `sql:key-fields` especificar en todos los esquemas.  
  
## <a name="examples"></a>Ejemplos  
 Para crear muestras funcionales mediante los ejemplos siguientes, debe cumplir determinados requisitos. Para obtener más información, vea [Requirements for Running SQLXML examples](../sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-the-sqlrelationship-annotation-on-an-element"></a>A. Especificar la anotación sql:relationship en un elemento  
 El siguiente esquema XSD anotado incluye **\<Customer>** **\<Order>** los elementos y. El **\<Order>** elemento es un elemento secundario del **\<Customer>** elemento.  
  
 En el esquema, la `sql:relationship` anotación se especifica en el **\<Order>** elemento secundario. La propia relación se define en el **\<xsd:appinfo>** elemento.  
  
 El **\<relationship>** elemento identifica CustomerID en la tabla sales. SalesOrderHeader como una clave externa que hace referencia a la clave principal CustomerID de la tabla sales. Customer. Por lo tanto, los pedidos que pertenecen a un cliente aparecen como un elemento secundario de dicho **\<Customer>** elemento.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" type="CustomerType" />  
   <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"  
                    sql:relationship="CustOrders" >  
           <xsd:complexType>  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
           </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
    </xsd:complexType>  
  
</xsd:schema>  
```  
  
 El esquema anterior usa una relación con nombre. También puede especificar una relación sin nombre. Los resultados son los mismos.  
  
 Éste es el esquema revisado en el que se especifica una relación sin nombre:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer"  type="CustomerType" />  
   <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader">  
           <xsd:annotation>  
            <xsd:appinfo>  
              <sql:relationship   
                parent="Sales.Customer"  
                parent-key="CustomerID"  
                child="Sales.SalesOrderHeader"  
                child-key="CustomerID" />  
            </xsd:appinfo>  
           </xsd:annotation>  
           <xsd:complexType>  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
           </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
    </xsd:complexType>  
  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para probar una consulta XPath de ejemplo en el esquema  
  
1.  Copie el código de esquema anterior y péguelo en un archivo de texto. Guarde el archivo como sql-relationship.xml.  
  
2.  Copie la siguiente plantilla y péguela en un archivo de texto. Guarde el archivo como sql-relationshipT.xml en el mismo directorio donde guardó sql-relationship.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="sql-relationship.xml">  
            /Customer[@CustomerID=1]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (sql-relationship.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\MyDir\sql-relationship.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 El conjunto de resultados es:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Customer CustomerID="1">   
    <Order OrderID="43860" CustomerID="1" />   
    <Order OrderID="44501" CustomerID="1" />   
    <Order OrderID="45283" CustomerID="1" />   
    <Order OrderID="46042" CustomerID="1" />   
  </Customer>   
</ROOT>  
```  
  
### <a name="b-specifying-a-relationship-chain"></a>B. Especificar una cadena de relación  
 Para este ejemplo, supongamos que desea que el siguiente documento XML use los datos obtenidos de la base de datos AdventureWorks:  
  
```  
<Order SalesOrderID="43659">  
  <Product Name="Mountain Bike Socks, M"/>   
  <Product Name="Sport-100 Helmet, Blue"/>  
  ...  
</Order>  
...  
```  
  
 Para cada pedido de la tabla sales. SalesOrderHeader, el documento XML tiene un **\<Order>** elemento. Y cada **\<Order>** elemento tiene una lista de **\<Product>** elementos secundarios, uno para cada producto solicitado en el orden.  
  
 Para especificar un esquema XSD que generará esta jerarquía, debe especificar dos relaciones: OrderOD y ODProduct. La relación OrderOD especifica la relación de elementos primarios y secundarios entre las tablas Sales.SalesOrderHeader y Sales.SalesOrderDetail. La relación ODProduct especifica la relación entre las tablas Sales.SalesOrderDetail y Production.Product.  
  
 En el esquema siguiente, la `msdata:relationship` anotación en el **\<Product>** elemento especifica dos valores: OrderOD y ODProduct. Es importante el orden en que se especifican estos valores.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:msdata="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <msdata:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  
    <msdata:relationship name="ODProduct"  
          parent="Sales.SalesOrderDetail"  
          parent-key="ProductID"  
          child="Production.Product"  
          child-key="ProductID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Order" msdata:relation="Sales.SalesOrderHeader"   
               msdata:key-fields="SalesOrderID" type="OrderType" />  
   <xsd:complexType name="OrderType" >  
     <xsd:sequence>  
        <xsd:element name="Product" msdata:relation="Production.Product"   
                     msdata:key-fields="ProductID"  
                     msdata:relationship="OrderOD ODProduct">  
          <xsd:complexType>  
             <xsd:attribute name="Name" type="xsd:string" />  
          </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="SalesOrderID"   type="xsd:integer" />   
    </xsd:complexType>  
</xsd:schema>  
```  
  
 En lugar de especificar una relación con nombre, puede especificar una relación anónima. En este caso, todo el contenido de **\<annotation>** ... **\</annotation>** , que describe las dos relaciones, aparece como un elemento secundario de **\<Product>** .  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:msdata="urn:schemas-microsoft-com:mapping-schema">  
  
  <xsd:element name="Order" msdata:relation="Sales.SalesOrderHeader"   
               msdata:key-fields="SalesOrderID" type="OrderType" />  
  
   <xsd:complexType name="OrderType" >  
     <xsd:sequence>  
        <xsd:element name="Product" msdata:relation="Production.Product"   
                     msdata:key-fields="ProductID" >  
         <xsd:annotation>  
          <xsd:appinfo>  
           <msdata:relationship   
               parent="Sales.SalesOrderHeader"  
               parent-key="SalesOrderID"  
               child="Sales.SalesOrderDetail"  
               child-key="SalesOrderID" />  
  
           <msdata:relationship   
               parent="Sales.SalesOrderDetail"  
               parent-key="ProductID"  
               child="Production.Product"  
               child-key="ProductID" />  
         </xsd:appinfo>  
       </xsd:annotation>  
       <xsd:complexType>  
          <xsd:attribute name="Name" type="xsd:string" />  
       </xsd:complexType>  
     </xsd:element>  
   </xsd:sequence>  
   <xsd:attribute name="SalesOrderID"   type="xsd:integer" />   
  </xsd:complexType>  
 </xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para probar una consulta XPath de ejemplo en el esquema  
  
1.  Copie el código de esquema anterior y péguelo en un archivo de texto. Guarde el archivo como relationshipChain.xml.  
  
2.  Copie la siguiente plantilla y péguela en un archivo de texto. Guarde el archivo como relationshipChainT.xml en el mismo directorio donde guardó relationshipChain.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="relationshipChain.xml">  
            /Order  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (relationshipChain.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\MyDir\relationshipChain.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 El conjunto de resultados es:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Order SalesOrderID="43659">  
    <Product Name="Mountain Bike Socks, M" />   
    <Product Name="Sport-100 Helmet, Blue" />   
    <Product Name="AWC Logo Cap" />   
    <Product Name="Long-Sleeve Logo Jersey, M" />   
    <Product Name="Long-Sleeve Logo Jersey, XL" />   
    ...  
  </Order>  
  ...  
</ROOT>  
```  
  
### <a name="c-specifying-the-relationship-annotation-on-an-attribute"></a>C. Especificar la anotación relationship en un atributo  
 El esquema de este ejemplo incluye un \<Customer> elemento con un \<CustomerID> elemento secundario y un atributo atributo OrderIDList de tipo IDREFS. El \<Customer> elemento se asigna a la tabla sales. Customer de la base de datos AdventureWorks. De forma predeterminada, el ámbito de esta asignación se aplica a todos los elementos o atributos secundarios, a menos que `sql:relation` se especifique en el elemento o atributo secundario, en cuyo caso, la relación de clave principal y clave externa adecuada debe definirse mediante el \<relationship> elemento. Además, el elemento o atributo secundario, que especifica una tabla distinta mediante la anotación `relation`, también debe especificar la anotación `relationship`.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
          parent="Sales.Customer"  
          parent-key="CustomerID"  
          child="Sales.SalesOrderHeader"  
          child-key="CustomerID" />  
     </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" type="CustomerType" />  
   <xsd:complexType name="CustomerType" >  
     <xsd:sequence>  
        <xsd:element name="CustomerID"   type="xsd:string" />   
     </xsd:sequence>  
     <xsd:attribute name="OrderIDList"   
                     type="xsd:IDREFS"   
                     sql:relation="Sales.SalesOrderHeader"   
                     sql:field="SalesOrderID"  
                     sql:relationship="CustOrders" >  
        </xsd:attribute>  
    </xsd:complexType>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para probar una consulta XPath de ejemplo en el esquema  
  
1.  Copie el código de esquema anterior y péguelo en un archivo de texto. Guarde el archivo como relationship-on-attribute.xml.  
  
2.  Copie la plantilla siguiente y péguela en un archivo. Guarde el archivo como relationship-on-attributeT.xml en el mismo directorio donde guardó relationship-on-attribute.xml. La consulta de la plantilla selecciona un cliente cuyo CustomerID es 1.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="relationship-on-attribute.xml">  
        /Customer[CustomerID=1]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (relationship-on-attribute.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\MyDir\relationship-on-attribute.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 El conjunto de resultados es:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
  <Customer OrderIDList="43860 44501 45283 46042">  
    <CustomerID>1</CustomerID>   
  </Customer>  
</ROOT>  
```  
  
### <a name="d-specifying-sqlrelationship-on-multiple-elements"></a>D. Especificar sql:relationship en varios elementos  
 En este ejemplo, el esquema XSD anotado contiene los **\<Customer>** **\<Order>** elementos, y **\<OrderDetail>** .  
  
 El **\<Order>** elemento es un elemento secundario del **\<Customer>** elemento. **\<sql:relationship>** se especifica en el **\<Order>** elemento secundario; por lo tanto, los pedidos pertenecientes a un cliente aparecen como elementos secundarios de **\<Customer>** .  
  
 El **\<Order>** elemento incluye el **\<OrderDetail>** elemento secundario. **\<sql:relationship>** se especifica en **\<OrderDetail>** el elemento secundario, por lo que los detalles del pedido que pertenecen a un pedido aparecen como elementos secundarios de ese **\<Order>** elemento.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
        parent="Sales.Customer"  
        parent-key="CustomerID"  
        child="Sales.SalesOrderHeader"  
        child-key="CustomerID" />  
  
    <sql:relationship name="OrderOrderDetail"  
        parent="Sales.SalesOrderHeader"  
        parent-key="SalesOrderID"  
        child="Sales.SalesOrderDetail"  
        child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"    
              sql:relationship="CustOrders" maxOccurs="unbounded" >  
          <xsd:complexType>  
              <xsd:sequence>  
                <xsd:element name="OrderDetail"   
                             sql:relation="Sales.SalesOrderDetail"   
                             sql:relationship="OrderOrderDetail"   
                             maxOccurs="unbounded" >  
                  <xsd:complexType>  
                    <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
                    <xsd:attribute name="ProductID" type="xsd:string" />  
                    <xsd:attribute name="OrderQty" type="xsd:integer" />  
                  </xsd:complexType>  
                </xsd:element>  
              </xsd:sequence>  
              <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
              <xsd:attribute name="OrderDate" type="xsd:date" />  
              <xsd:attribute name="CustomerID" type="xsd:string" />  
          </xsd:complexType>  
        </xsd:element>  
      </xsd:sequence>  
      <xsd:attribute name="CustomerID" type="xsd:string" />  
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para probar una consulta XPath de ejemplo en el esquema  
  
1.  Copie el código de esquema anterior y péguelo en un archivo de texto. Guarde el archivo como relationship-multiple-elements.xml.  
  
2.  Copie la plantilla siguiente y péguela en un archivo de texto. Guarde el archivo como relationship-multiple-elementsT.xml en el mismo directorio donde guardó relationship-multiple-elements.xml. La consulta de la plantilla devuelve la información de pedidos de un cliente cuyo CustomerID es 1 y cuyo SalesOrderID es 43860.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="relationship-multiple-elements.xml">  
        /Customer[@CustomerID=1]/Order[@SalesOrderID=43860]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (relationship-multiple-elements.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\MyDir\relationship-multiple-elements.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 El conjunto de resultados es:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Order SalesOrderID="43860" OrderDate="2001-08-01" CustomerID="1">  
     <OrderDetail SalesOrderID="43860" ProductID="761" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="770" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="758" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="765" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="732" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="762" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="738" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="768" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="753" OrderQty="2" />   
     <OrderDetail SalesOrderID="43860" ProductID="729" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="763" OrderQty="1" />   
     <OrderDetail SalesOrderID="43860" ProductID="756" OrderQty="1" />   
  </Order>  
</ROOT>  
```  
  
### <a name="e-specifying-the-sqlrelationship-without-the-parent-attribute"></a>E. Especificar \<sql:relationship> sin el atributo primario  
 En este ejemplo se muestra cómo especificar **\<sql:relationship>** sin el atributo **primario** . Por ejemplo, imagine que tiene las siguientes tablas de empleados:  
  
```  
Emp1(SalesPersonID, FirstName, LastName, ReportsTo)  
Emp2(SalesPersonID, FirstName, LastName, ReportsTo)  
```  
  
 La siguiente vista XML tiene los **\<Emp1>** **\<Emp2>** elementos y asignados a las tablas sales. Emp1 y sales. Emp2:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="EmpOrders"  
          parent-key="SalesPersonID"  
          child="Sales.SalesOrderHeader"  
          child-key="SalesPersonID" />  
     </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Emp1" sql:relation="Sales.Emp1" type="EmpType" />  
  <xsd:element name="Emp2" sql:relation="Sales.Emp2" type="EmpType" />  
   <xsd:complexType name="EmpType" >  
     <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Sales.SalesOrderHeader"   
                     sql:relationship="EmpOrders" >  
          <xsd:complexType>  
             <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
             <xsd:attribute name="CustomerID" type="xsd:string" />  
          </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="SalesPersonID"   type="xsd:integer" />   
        <xsd:attribute name="LastName"   type="xsd:string" />   
    </xsd:complexType>  
  
</xsd:schema>  
```  
  
 En el esquema, el **\<Emp1>** elemento y el **\<Emp2>** elemento son de tipo `EmpType` . El tipo `EmpType` describe un **\<Order>** elemento secundario y el correspondiente **\<sql:relationship>** . En este caso, no hay ningún elemento primario único que se pueda identificar en **\<sql:relationship>** mediante el atributo **primario** . En esta situación, no se especifica el atributo **primario** en **\<sql:relationship>** ; la información de atributo **primario** se obtiene de la jerarquía del esquema.  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para probar una consulta XPath de ejemplo en el esquema  
  
1.  Cree estas tablas en la base de datos AdventureWorks:  
  
    ```  
    USE AdventureWorks  
    CREATE TABLE Sales.Emp1 (  
           SalesPersonID int primary key,   
           FirstName  varchar(20),   
           LastName   varchar(20),   
           ReportsTo int)  
    Go  
    CREATE TABLE Sales.Emp2 (  
           SalesPersonID int primary key,   
           FirstName  varchar(20),   
           LastName   varchar(20),   
           ReportsTo int)  
    Go  
    ```  
  
2.  Agregue estos datos de ejemplo en las tablas:  
  
    ```  
    INSERT INTO Sales.Emp1 values (279, 'Nancy', 'Devolio',NULL)  
    INSERT INTO Sales.Emp1 values (282, 'Andrew', 'Fuller',1)  
    INSERT INTO Sales.Emp1 values (276, 'Janet', 'Leverling',1)  
    INSERT INTO Sales.Emp2 values (277, 'Margaret', 'Peacock',3)  
    INSERT INTO Sales.Emp2 values (283, 'Steven', 'Devolio',4)  
    INSERT INTO Sales.Emp2 values (275, 'Nancy', 'Buchanan',5)  
    INSERT INTO Sales.Emp2 values (281, 'Michael', 'Suyama',6)  
    ```  
  
3.  Copie el código de esquema anterior y péguelo en un archivo de texto. Guarde el archivo como relationship-noparent.xml.  
  
4.  Copie la plantilla siguiente y péguela en un archivo de texto. Guarde el archivo como relationship-noparentT.xml en el mismo directorio donde guardó relationship-noparent.xml. La consulta de la plantilla selecciona todos los \<Emp1> elementos (por lo tanto, el elemento primario es Emp1).  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="relationship-noparent.xml">  
            /Emp1  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (relationship-noparent.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\MyDir\relationship-noparent.xml"  
    ```  
  
5.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML](../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 A continuación se muestra un conjunto de resultados parcial:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<Emp1 SalesPersonID="276" LastName="Leverling">  
  <Order SalesOrderID="43663" CustomerID="510" />   
  <Order SalesOrderID="43666" CustomerID="511" />   
  <Order SalesOrderID="43859" CustomerID="259" />  
  ...  
</Emp1>  
```  
  
  
