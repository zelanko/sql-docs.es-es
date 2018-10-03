---
title: Insertar datos con diagramas de actualización XML (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- xsi:nil attribute
- unique values
- <after> block
- id attribute
- data insertions [SQLXML]
- nil attribute
- <before> block
- updg:guid attribute
- multiple record insertions
- returnid attribute
- updategrams [SQLXML], inserting data
- updg:at-identity attribute
- invalid characters [SQLXML]
- updg:returnid attribute
- updg:id attribute
- namespaces [SQLXML], updategrams
- IDENTITY-type column
- guid attribute
- record insertion [SQLXML]
- null values [SQLXML]
- at-identity attribute
- xml data type [SQL Server], SQLXML
ms.assetid: 4dc48762-bc12-43fb-b356-ea1b9c1e287e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 95989f956f01039cec5bbbc3ab61417981a094f6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48053305"
---
# <a name="inserting-data-using-xml-updategrams-sqlxml-40"></a>Insertar datos con diagramas de actualización XML (SQLXML 4.0)
  Un diagrama de actualización indica una operación de inserción cuando una instancia de registro aparece en el  **\<después >** bloque pero no en las correspondientes  **\<antes >** bloque. En este caso, el diagrama de actualización inserta el registro en el  **\<después >** bloque en la base de datos.  
  
 Éste es el formato del diagrama de actualización para una operación de inserción:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync [mapping-schema="SampleSchema.xml"]  >  
   [<updg:before>  
   </updg:before>]  
    <updg:after [updg:returnid="x y ...] >  
       <ElementName [updg:id="value"]   
                   [updg:at-identity="x"]   
                   [updg:guid="y"]  
                   attribute="value"   
                   attribute="value"  
                   ...  
       />  
      [<ElementName .../>... ]  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
## <a name="before-block"></a>\<antes de > bloque  
 El  **\<antes >** bloque puede omitirse en una operación de inserción. Si el elemento opcional `mapping-schema` atributo no se especifica, el  **\<ElementName >** que se especifica en el diagrama de actualización se asigna a una tabla de base de datos y los elementos secundarios o atributos se asignan a columnas de la tabla.  
  
## <a name="after-block"></a>\<una vez > bloque  
 Puede especificar uno o más registros en el  **\<después >** bloque.  
  
 Si el  **\<después >** bloque no proporciona un valor para una columna en particular, el diagrama de actualización usa el valor predeterminado que se especifica en el esquema anotado (si se ha especificado un esquema). Si el esquema no especifica un valor predeterminado para la columna, el diagrama de actualización no especifica ningún valor explícito para esta columna y, en su lugar, se asigna el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] valor de predeterminado (si se especifica) a esta columna. Si no hay ningún valor predeterminado de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y la columna acepta un valor NULL, el diagrama de actualización establece el valor de columna en NULL. Si la columna no tiene un valor predeterminado ni acepta un valor NULL, se produce un error en el comando y el diagrama de actualización devuelve un error. El atributo `updg:returnid` opcional se utiliza para devolver el valor de identidad que genera el sistema cuando se agrega un registro a una tabla con una columna de tipo IDENTITY.  
  
## <a name="updgid-attribute"></a>Atributo updg:id  
 Si el diagrama de actualización inserta solamente registros, no requiere el atributo `updg:id`. Para obtener más información acerca de `updg:id`, consulte [Updategrams de actualización de datos utilizando XML &#40;SQLXML 4.0&#41;](updating-data-using-xml-updategrams-sqlxml-4-0.md).  
  
## <a name="updgat-identity-attribute"></a>Atributo updg:at-identity  
 Cuando un diagrama de actualización inserta un registro en una tabla que tiene una columna de tipo IDENTITY, el diagrama de actualización puede capturar el valor asignado por el sistema mediante el atributo `updg:at-identity` opcional. El diagrama de actualización puede utilizar este valor en operaciones posteriores. Al ejecutar el diagrama de actualización, puede devolver el valor de identidad que se genera especificando el atributo `updg:returnid`.  
  
## <a name="updgguid-attribute"></a>Atributo updg:guid  
 El atributo `updg:guid` es un atributo opcional que genera un identificador único global. Este valor permanece en el ámbito de todo el  **\<sincronización >** bloque en el que se especifica. Puede usar este valor en cualquier lugar en el  **\<sincronización >** bloque. El atributo llama a la `NEWGUID()` [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] función para generar el identificador único.  
  
## <a name="examples"></a>Ejemplos  
 Para crear ejemplos funcionales mediante los siguientes ejemplos, debe cumplir los requisitos especificados en [requisitos para ejecutar los ejemplos de SQLXML](../../sqlxml/requirements-for-running-sqlxml-examples.md).  
  
 Antes de usar los ejemplos del diagrama de actualización, tenga en cuenta lo siguiente:  
  
-   En la mayoría de los ejemplos se usa una asignación predeterminada (es decir, no se especifica ningún esquema de asignación en el diagrama de actualización). Para obtener más ejemplos de diagramas de actualización que utilizan los esquemas de asignación, consulte [especificar un esquema de asignación anotados en un diagrama de actualización &#40;SQLXML 4.0&#41;](specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
-   La mayoría de los ejemplos usan la base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)]. Todas las actualizaciones se aplican a las tablas de esta base de datos.  
  
### <a name="a-inserting-a-record-by-using-an-updategram"></a>A. Insertar un registro usando un diagrama de actualización  
 Este diagrama de actualización centrado en atributos inserta un registro en la tabla HumanResources.Employee de la base de datos [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)].  
  
 En este ejemplo, el diagrama de actualización no especifica ningún esquema de asignación. Por lo tanto, el diagrama de actualización usa la asignación predeterminada, en la que el nombre de elemento se asigna a un nombre de tabla y los atributos o elementos secundarios se asignan a columnas de dicha tabla.  
  
 El esquema [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] para la tabla HumanResources.Department impone una restricción 'not null' en todas las columnas. Por lo tanto, el diagrama de actualización debe tener valores especificados para todas las columnas. DepartmentID es una columna de tipo IDENTITY. Por ello, no se especifica ningún valor para ella.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
       <HumanResources.Department   
            Name="New Product Research"   
            GroupName="Research and Development"   
            ModifiedDate="2010-08-31"/>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para probar una consulta de XPath de ejemplo con respecto al esquema  
  
1.  Copie el diagrama de actualización anterior y péguelo en un archivo de texto. Guarde el archivo como MyUpdategram.xml.  
  
2.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 En una asignación centrada en elementos, el diagrama de actualización presenta un aspecto como el siguiente:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
       <HumanResources.Department>  
            <Name> New Product Research </Name>  
            <GroupName> Research and Development </GroupName>  
            <ModifiedDate>2010-08-31</ModifiedDate>  
       </HumanResources.Department>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 En un diagrama de actualización de modo mixto (centrado en elementos y en atributos), un elemento puede incluir atributos y subelementos, tal y como se muestra en este diagrama de actualización:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
       <HumanResources.Department   
            Name=" New Product Research "   
            <GroupName>Research and Development</GroupName>  
            <ModifiedDate>2010-08-31</ModifiedDate>  
       </HumanResources.Department>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
### <a name="b-inserting-multiple-records-by-using-an-updategram"></a>B. Insertar varios registros utilizando un diagrama de actualización  
 Este diagrama de actualización agrega dos nuevos registros de turno a la tabla HumanResources.Shift. El diagrama de actualización no especifica opcional  **\<antes >** bloque.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync>  
    <updg:after >  
       <HumanResources.Shift Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
       <HumanResources.Shift Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para probar una consulta de XPath de ejemplo con respecto al esquema  
  
1.  Copie el diagrama de actualización anterior y péguelo en un archivo de texto. Guarde el archivo como Updategram-AddShifts.xml.  
  
2.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Otra versión de este ejemplo es un diagrama de actualización que utiliza dos  **\<después >** bloques en lugar de un bloque para insertar los dos empleados. Esta versión es válida y puede codificarse del siguiente modo:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync>  
    <updg:after >  
       <HumanResources.Shift Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
    </updg:after>  
    <updg:before>  
    </updg:before>  
    <updg:after >  
       <HumanResources.Shift Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
### <a name="c-working-with-valid-sql-server-characters-that-are-not-valid-in-xml"></a>C. Trabajar con caracteres de SQL Server válidos que no son válidos en XML  
 En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], los nombres de tabla pueden incluir un espacio, como la tabla Order Details de la base de datos Northwind. Sin embargo, esto no es válido en los caracteres XML válidos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] identificadores, pero no identificadores XML válidos pueden codificarse utilizando ' __xHHHH\_\_' como valor de codificación, donde HHHH representa el código UCS-2 hexadecimal de cuatro dígitos de el carácter en el orden de primero bit más significativo.  
  
> [!NOTE]  
>  Este ejemplo usa la base de datos de ejemplo Northwind. Puede instalar la base de datos Northwind mediante el uso de un script SQL disponible para su descarga desde esta [sitio Web de Microsoft](http://go.microsoft.com/fwlink/?LinkId=30196).  
  
 Además, el nombre del elemento debe incluirse entre corchetes ([]). Dado que los caracteres [y] no son válidos en XML, debe codificarlos como _x005B\_ y _x005D\_, respectivamente. (Si utiliza un esquema de asignación, puede especificar nombres de elemento que no contengan caracteres no válidos, como espacios en blanco. El esquema de asignación realiza la asignación necesaria; por lo tanto, no necesita codificar estos caracteres.)  
  
 Este diagrama de actualización agrega un registro a la tabla Order Details de la base de datos Northwind:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after>  
      <_x005B_Order_x0020_Details_x005D_ OrderID="1"  
            ProductID="11"  
            UnitPrice="$1.0"  
            Quantity="1"  
            Discount="0.0" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 La columna UnitPrice de la tabla Order Details es de tipo `money`. Para aplicar la conversión de tipos adecuada (de un tipo `string` a un tipo `money`), debe agregarse el carácter del signo de dólar ($) como parte del valor. Si el diagrama de actualización no especifica ningún esquema de asignación, se evalúa el primer carácter del valor `string`. Si el primer carácter es un signo de dólar ($), se aplica la conversión adecuada.  
  
 Si el diagrama de actualización se especifica en un esquema de asignación donde la columna está correctamente marcada como `dt:type="fixed.14.4"` o `sql:datatype="money"`, no se requiere el signo de dólar ($) y la asignación controla la conversión. Ésta es la forma recomendada de asegurarse de que se realice la conversión de tipos adecuada.  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para probar una consulta de XPath de ejemplo con respecto al esquema  
  
1.  Copie el diagrama de actualización anterior y péguelo en un archivo de texto. Guarde el archivo como UpdategramSpacesInTableName.xml.  
  
2.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="d-using-the-at-identity-attribute-to-retrieve-the-value-that-has-been-inserted-in-the-identity-type-column"></a>D. Utilizar el atributo at-identity para recuperar el valor insertado en la columna de tipo IDENTITY  
 El siguiente diagrama de actualización inserta dos registros: uno en la tabla Sales.SalesOrderHeader y otra en la tabla Sales.SalesOrderDetail.  
  
 En primer lugar, el diagrama de actualización agrega un registro a la tabla Sales.SalesOrderHeader. En esta tabla, la columna SalesOrderID es una columna de tipo IDENTITY. Por lo tanto, al agregar este registro a la tabla, el diagrama de actualización usa el atributo `at-identity` para capturar el valor de SalesOrderID asignado como "x" (un valor de marcador de posición). A continuación, el diagrama de actualización especifica esto `at-identity` variable como el valor del atributo SalesOrderID en el \<Sales.SalesOrderDetail > elemento.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
 <updg:sync >  
  <updg:before>  
  </updg:before>  
  <updg:after>  
   <Sales.SalesOrderHeader updg:at-identity="x"   
             RevisionNumber="1"  
             OrderDate="2001-07-01 00:00:00.000"  
             DueDate="2001-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             CustomerID="676"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="24643.9362"  
             TaxAmt="1971.5149"  
             Freight="616.0984"  
             rowguid="00001111-2222-3333-4444-556677889900"  
             ModifiedDate="2001-07-08 00:00:00.000" />  
      <Sales.SalesOrderDetail SalesOrderID="x"  
                LineNumber="1"  
                OrderQty="1"  
                ProductID="776"  
                SpecialOfferID="1"  
                UnitPrice="2429.9928"  
                UnitPriceDiscount="0.00"  
                rowguid="aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee"  
                ModifiedDate="2001-07-01 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 Si desea devolver el valor de identidad generado por el atributo `updg:at-identity`, puede usar el atributo `updg:returnid`. A continuación se muestra un diagrama de actualización revisado que devuelve este valor de identidad. (Este diagrama de actualización agrega dos registros de pedido y dos registros de detalles del pedido, simplemente para complicar un poco el ejemplo.)  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
 <updg:sync>  
  <updg:before>  
  </updg:before>  
  <updg:after updg:returnid="x y" >  
       <HumanResources.Shift updg:at-identity="x" Name="Day-Evening"  
                        StartTime="1900-01-01 11:00:00.000"  
                        EndTime="1900-01-01 19:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
       <HumanResources.Shift updg:at-identity="y" Name="Evening-Night"  
                        StartTime="1900-01-01 19:00:00.000"  
                        EndTime="1900-01-01 03:00:00.000"  
                        ModifiedDate="2004-01-01 00:00:00.000" />  
  </updg:after>  
 </updg:sync>  
</ROOT>  
```  
  
 Cuando se ejecuta el diagrama de actualización, devuelve resultados similares a los siguientes, que incluyen el valor de identidad generado (el valor generado de la columna ShiftID utilizada para la identidad de la tabla):  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">   
  <returnid>   
    <x>4</x>   
    <y>5</y>   
  </returnid>   
</ROOT>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para probar una consulta de XPath de ejemplo con respecto al esquema  
  
1.  Copie el diagrama de actualización anterior y péguelo en un archivo de texto. Guarde el archivo como Updategram-returnId.xml.  
  
2.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="e-using-the-updgguid-attribute-to-generate-a-unique-value"></a>E. Utilizar el atributo updg:guid para generar un valor único  
 En este ejemplo, el diagrama de actualización inserta un registro en las tablas Cust y CustOrder. Asimismo, genera un valor único para el atributo CustomerID utilizando el atributo `updg:guid`.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync >  
    <updg:before>  
    </updg:before>  
    <updg:after updg:returnid="x" >  
      <Cust updg:guid="x" >  
         <CustID>x</CustID>  
         <LastName>Fuller</LastName>  
      </Cust>  
      <CustOrder>  
         <CustID>x</CustID>  
         <OrderID>1</OrderID>  
      </CustOrder>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 El diagrama de actualización especifica el atributo `returnid`. Como resultado, se devuelve el GUID generado:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <returnid>  
    <x>7111BD1A-7F0B-4CEE-B411-260DADFEFA2A</x>   
  </returnid>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Para probar el diagrama de actualización  
  
1.  Copie el diagrama de actualización anterior y péguelo en un archivo de texto. Guarde el archivo como Updategram-GenerateGuid.xml.  
  
2.  Cree estas tablas:  
  
    ```  
    USE tempdb  
    CREATE TABLE Cust (CustID uniqueidentifier, LastName varchar(20))  
    CREATE TABLE CustOrder (CustID uniqueidentifier, OrderID int)  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="f-specifying-a-schema-in-an-updategram"></a>F. Especificar un esquema en un diagrama de actualización  
 El diagrama de actualización de este ejemplo inserta un registro en la tabla siguiente:  
  
```  
CustOrder(OrderID, EmployeeID, OrderType)  
```  
  
 En este diagrama de actualización se especifica un esquema XSD (es decir, no existe ninguna asignación predeterminada de elementos y atributos del diagrama de actualización). El esquema proporciona la asignación necesaria de elementos y atributos a las tablas y columnas de la base de datos.  
  
 El esquema siguiente (CustOrderSchema.xml) describe un  **\<CustOrder >** elemento que consta de los **OrderID** y **EmployeeID** atributos. Para hacer que el esquema más interesante, el valor predeterminado se asigna a la **EmployeeID** atributo. Un diagrama de actualización utiliza el valor predeterminado de un atributo solamente para las operaciones de inserción y solamente si el diagrama de actualización no especifica dicho atributo.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="CustOrder" >  
   <xsd:complexType>  
        <xsd:attribute name="OrderID"     type="xsd:integer" />   
        <xsd:attribute name="EmployeeID"  type="xsd:integer" />  
        <xsd:attribute name="OrderType  " type="xsd:integer" default="1"/>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Este diagrama de actualización inserta un registro en la tabla CustOrder. El diagrama de actualización solamente especifica los valores de atributo de OrderID y EmployeeID. No especifica el valor de atributo de OrderType. Por lo tanto, el diagrama de actualización utiliza el valor predeterminado del atributo OrderType especificado en el esquema anterior.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql"  
             xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
<updg:sync mapping-schema='CustOrderSchema.xml'>  
<updg:after>  
       <CustOrder OrderID="98000" EmployeeID="1" />  
</updg:after>  
</updg:sync>  
</ROOT>  
```  
  
 Para obtener más ejemplos de diagramas de actualización que especifican un esquema de asignación, consulte [especificar un esquema de asignación anotados en un diagrama de actualización &#40;SQLXML 4.0&#41;](specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md).  
  
##### <a name="to-test-the-updategram"></a>Para probar el diagrama de actualización  
  
1.  Cree esta tabla en la **tempdb** base de datos:  
  
    ```  
    USE tempdb  
    CREATE TABLE CustOrder(  
                     OrderID int,   
                     EmployeeID int,   
                     OrderType int)  
    ```  
  
2.  Copie el esquema anterior y péguelo en un archivo de texto. Guarde el archivo como CustOrderSchema.xml.  
  
3.  Copie el diagrama de actualización anterior y péguelo en un archivo de texto. Guarde el archivo como CustOrderUpdategram.xml en la misma carpeta utilizada en el paso anterior.  
  
4.  Cree y use el script de prueba de SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar el diagrama de actualización.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Éste es el esquema XDR equivalente:  
  
```  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
 <ElementType name="CustOrder" >  
    <AttributeType name="OrderID" />  
    <AttributeType name="EmployeeID" />  
    <AttributeType name="OrderType" default="1" />  
    <attribute type="OrderID"  />  
    <attribute type="EmployeeID" />  
    <attribute type="OrderType" />  
  </ElementType>  
</Schema>  
```  
  
### <a name="g-using-the-xsinil-attribute-to-insert-null-values-in-a-column"></a>G. Usar el atributo xsi:nil para insertar valores NULL en una columna  
 Si desea insertar un valor NULL en la columna correspondiente de la tabla, puede especificar el atributo `xsi:nil` en un elemento de un diagrama de actualización. En el esquema XSD correspondiente, también debe especificarse el atributo XSD `nillable`.  
  
 Por ejemplo, fíjese en este esquema XSD:  
  
```  
<?xml version="1.0"?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:element name="Student" sql:relation="Students">  
  <xsd:complexType>  
    <xsd:all>  
      <xsd:element name="fname" sql:field="first_name"   
                                type="xsd:string"   
                                 nillable="true"/>  
    </xsd:all>  
    <xsd:attribute name="SID"   
                        sql:field="StudentID"  
                        type="xsd:ID"/>      
    <xsd:attribute name="lname"       
                        sql:field="last_name"  
                        type="xsd:string"/>  
    <xsd:attribute name="minitial"    
                        sql:field="middle_initial"   
                        type="xsd:string"/>  
    <xsd:attribute name="years"       
                         sql:field="no_of_years"  
                         type="xsd:integer"/>  
  </xsd:complexType>  
 </xsd:element>  
</xsd:schema>  
```  
  
 Especifica el esquema XSD **nillable = "true"** para el  **\<fname >** elemento. El siguiente diagrama de actualización usa este esquema:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql"  
      xmlns:updg="urn:schemas-microsoft-com:xml-updategram"  
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  
<updg:sync mapping-schema='StudentSchema.xml'>  
  <updg:before/>  
  <updg:after>  
    <Student SID="S00004" lname="Elmaci" minitial="" years="2">  
      <fname xsi:nil="true">  
    </fname>  
    </Student>  
  </updg:after>  
</updg:sync>  
  
</ROOT>  
```  
  
 El diagrama de actualización especifica `xsi:nil` para el  **\<fname >** elemento en el  **\<después >** bloque. Por lo tanto, cuando se ejecuta este diagrama de actualización, se inserta un valor NULL en la columna first_name de la tabla.  
  
##### <a name="to-test-the-updategram"></a>Para probar el diagrama de actualización  
  
1.  Cree la siguiente tabla en la **tempdb** base de datos:  
  
    ```  
    USE tempdb  
    CREATE TABLE Students (  
       StudentID char(6)NOT NULL ,  
       first_name varchar(50),  
       last_name varchar(50),  
       middle_initial char(1),  
       no_of_years int NULL)  
    GO  
    ```  
  
2.  Copie el esquema anterior y péguelo en un archivo de texto. Guarde el archivo como StudentSchema.xml.  
  
3.  Copie el diagrama de actualización anterior y péguelo en un archivo de texto. Guarde el archivo como StudentUpdategram.xml en la misma carpeta que se utilizó en el paso anterior para guardar StudentSchema.xml.  
  
4.  Cree y use el script de prueba de SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar el diagrama de actualización.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="h-specifying-namespaces-in-an-updategram"></a>H. Especificar espacios de nombres en un diagrama de actualización  
 En un diagrama de actualización puede tener elementos que pertenezcan a un espacio de nombres declarado en el mismo elemento del diagrama de actualización. En este caso, el esquema correspondiente también debe declarar el mismo espacio de nombres y el elemento debe pertenecer a este espacio de nombres de destino.  
  
 Por ejemplo, en el siguiente diagrama de actualización (UpdateGram-ElementHavingNamespace.xml), el  **\<orden >** elemento pertenece a un espacio de nombres declarado en el elemento.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema='XSD-ElementHavingNameSpace.xml'>  
    <updg:after>  
       <x:Order  xmlns:x="http://server/xyz/schemas/"  
             updg:at-identity="SalesOrderID"   
             RevisionNumber="1"  
             OrderDate="2001-07-01 00:00:00.000"  
             DueDate="2001-07-13 00:00:00.000"  
             OnlineOrderFlag="0"  
             CustomerID="676"  
             ContactID="378"  
             BillToAddressID="985"  
             ShipToAddressID="985"  
             ShipMethodID="5"  
             SubTotal="24643.9362"  
             TaxAmt="1971.5149"  
             Freight="616.0984"  
             rowguid="00009999-8888-7777-6666-554433221100"  
             ModifiedDate="2001-07-08 00:00:00.000" />  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 En este caso, el esquema también debe declarar el espacio de nombres tal y como se muestra en este esquema:  
  
 En el esquema siguiente (XSD-ElementHavingNamespace.xml) se indica cómo debe declararse el elemento y los atributos correspondientes.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
     xmlns:dt="urn:schemas-microsoft-com:datatypes"   
     xmlns:sql="urn:schemas-microsoft-com:mapping-schema"    
     xmlns:x="http://server/xyz/schemas/"   
     targetNamespace="http://server/xyz/schemas/" >  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader" type="x:Order_type"/>  
  <xsd:complexType name="Order_type">  
    <xsd:attribute name="SalesOrderID"  type="xsd:ID"/>  
    <xsd:attribute name="RevisionNumber" type="xsd:unsignedByte"/>  
    <xsd:attribute name="OrderDate" type="xsd:dateTime"/>  
    <xsd:attribute name="DueDate" type="xsd:dateTime"/>  
    <xsd:attribute name="ShipDate" type="xsd:dateTime"/>  
    <xsd:attribute name="Status" type="xsd:unsignedByte"/>  
    <xsd:attribute name="OnlineOrderFlag" type="xsd:boolean"/>  
    <xsd:attribute name="SalesOrderNumber" type="xsd:string"/>  
    <xsd:attribute name="PurchaseOrderNumber" type="xsd:string"/>  
    <xsd:attribute name="AccountNumber" type="xsd:string"/>  
    <xsd:attribute name="CustomerID" type="xsd:int"/>  
    <xsd:attribute name="ContactID" type="xsd:int"/>  
    <xsd:attribute name="SalesPersonID" type="xsd:int"/>  
    <xsd:attribute name="TerritoryID" type="xsd:int"/>  
    <xsd:attribute name="BillToAddressID" type="xsd:int"/>  
    <xsd:attribute name="ShipToAddressID" type="xsd:int"/>  
    <xsd:attribute name="ShipMethodID" type="xsd:int"/>  
    <xsd:attribute name="CreditCardID" type="xsd:int"/>  
    <xsd:attribute name="CreditCardApprovalCode" type="xsd:string"/>  
    <xsd:attribute name="CurrencyRateID" type="xsd:int"/>  
    <xsd:attribute name="SubTotal" type="xsd:decimal"/>  
    <xsd:attribute name="TaxAmt" type="xsd:decimal"/>  
    <xsd:attribute name="Freight" type="xsd:decimal"/>  
    <xsd:attribute name="TotalDue" type="xsd:decimal"/>  
    <xsd:attribute name="Comment" type="xsd:string"/>  
    <xsd:attribute name="rowguid" type="xsd:string"/>  
    <xsd:attribute name="ModifiedDate" type="xsd:dateTime"/>  
  </xsd:complexType>  
</xsd:schema>  
```  
  
##### <a name="to-test-the-updategram"></a>Para probar el diagrama de actualización  
  
1.  Copie el esquema anterior y péguelo en un archivo de texto. Guarde el archivo como XSD-ElementHavingNamespace.xml.  
  
2.  Copie el diagrama de actualización anterior y péguelo en un archivo de texto. Guarde el archivo como Updategram-ElementHavingNamespace.xml en la misma carpeta donde haya guardado XSD-ElementHavingnamespace.xml.  
  
3.  Cree y use el script de prueba de SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar el diagrama de actualización.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
### <a name="i-inserting-data-into-an-xml-data-type-column"></a>I. Insertar datos en una columna de tipo de datos XML  
 El tipo de datos `xml` se introdujo en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Puede usar diagramas de actualización para insertar y actualizar datos almacenados en columnas de tipo de datos `xml` teniendo en cuenta estas indicaciones:  
  
-   La columna `xml` no puede utilizarse para identificar una fila existente. Por lo tanto, no puede incluirse en la sección `updg:before` de un diagrama de actualización.  
  
-   Se conservarán los espacios de nombres que se encuentren en el ámbito del fragmento XML insertado en la columna `xml` y sus declaraciones de espacio de nombres se agregarán al elemento superior del fragmento insertado.  
  
 Por ejemplo, en el siguiente diagrama de actualización (SampleUpdateGram.xml), el  **\<Desc >** elemento actualiza la columna ProductDescription de la producción > tabla productModel en la [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] base de datos de ejemplo. El resultado de este diagrama de actualización es que el contenido XML de la columna ProductDescription se update con el contenido XML de la  **\<Desc >** elemento.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
    <updg:sync mapping-schema="SampleSchema.xml" >  
       <updg:before>  
<ProductModel ProductModelID="19">  
   <Name>Mountain-100</Name>  
</ProductModel>  
    </updg:before>  
    <updg:after>  
 <ProductModel>  
    <Name>Mountain-100</Name>  
    <Desc><?xml-stylesheet href="ProductDescription.xsl" type="text/xsl"?>  
        <p1:ProductDescription xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
              xmlns:wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"   
              xmlns:wf="http://www.adventure-works.com/schemas/OtherFeatures"   
              xmlns:html="http://www.w3.org/1999/xhtml"   
              xmlns="">  
  <p1:Summary>  
     <html:p>Insert Example</html:p>  
  </p1:Summary>  
  <p1:Manufacturer>  
    <p1:Name>AdventureWorks</p1:Name>  
    <p1:Copyright>2002</p1:Copyright>  
    <p1:ProductURL>HTTP://www.Adventure-works.com</p1:ProductURL>  
  </p1:Manufacturer>  
  <p1:Features>These are the product highlights.   
    <wm:Warranty>  
       <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
       <wm:Description>parts and labor</wm:Description>  
    </wm:Warranty>  
    <wm:Maintenance>  
       <wm:NoOfYears>10 years</wm:NoOfYears>  
       <wm:Description>maintenance contract available through your dealer or any AdventureWorks retail store.</wm:Description>  
    </wm:Maintenance>  
    <wf:wheel>High performance wheels.</wf:wheel>  
    <wf:saddle>  
      <html:i>Anatomic design</html:i> and made from durable leather for a full-day of riding in comfort.</wf:saddle>  
    <wf:pedal>  
       <html:b>Top-of-the-line</html:b> clipless pedals with adjustable tension.</wf:pedal>  
    <wf:BikeFrame>Each frame is hand-crafted in our Bothell facility to the optimum diameter and wall-thickness required of a premium mountain frame. The heat-treated welded aluminum frame has a larger diameter tube that absorbs the bumps.</wf:BikeFrame>  
    <wf:crankset> Triple crankset; alumunim crank arm; flawless shifting. </wf:crankset>  
   </p1:Features>  
   <p1:Picture>  
      <p1:Angle>front</p1:Angle>  
      <p1:Size>small</p1:Size>  
      <p1:ProductPhotoID>118</p1:ProductPhotoID>  
   </p1:Picture>  
   <p1:Specifications> These are the product specifications.  
     <Material>Almuminum Alloy</Material>  
     <Color>Available in most colors</Color>  
     <ProductLine>Mountain bike</ProductLine>  
     <Style>Unisex</Style>  
     <RiderExperience>Advanced to Professional riders</RiderExperience>  
   </p1:Specifications>  
  </p1:ProductDescription>  
 </Desc>  
      </ProductModel>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
 El diagrama de actualización hace referencia al siguiente esquema XSD anotado (SampleSchema.xml).  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
           xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
           xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">   
  <xsd:element name="ProductModel"  sql:relation="Production.ProductModel" >  
     <xsd:complexType>  
       <xsd:sequence>  
          <xsd:element name="Name" type="xsd:string"></xsd:element>  
          <xsd:element name="Desc" sql:field="CatalogDescription" sql:datatype="xml">  
           <xsd:complexType>  
            <xsd:sequence>  
              <xsd:element name="ProductDescription">  
                 <xsd:complexType>  
                   <xsd:sequence>  
                     <xsd:element name="Summary" type="xsd:anyType">  
                     </xsd:element>  
                   </xsd:sequence>  
                 </xsd:complexType>  
              </xsd:element>  
            </xsd:sequence>  
           </xsd:complexType>  
          </xsd:element>   
       </xsd:sequence>  
       <xsd:attribute name="ProductModelID" sql:field="ProductModelID"/>  
     </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-the-updategram"></a>Para probar el diagrama de actualización  
  
1.  Copie el esquema anterior y péguelo en un archivo de texto. Guarde el archivo como XSD-SampleSchema.xml.  
  
    > [!NOTE]  
    >  Dado que los diagramas de actualización admiten la asignación predeterminada, no existe ningún modo de identificar el principio y el final del tipo de datos `xml`. Lo que esto significa realmente es que se requiere un esquema de asignación cuando se insertan o actualizan tablas con columnas de tipo de datos `xml`. Si no se proporciona ningún esquema, SQLXML devuelve un error que indica que falta una de las columnas de la tabla.  
  
2.  Copie el diagrama de actualización anterior y péguelo en un archivo de texto. Guarde el archivo como SampleUpdategram.xml en la misma carpeta donde ha guardado SampleSchema.xml.  
  
3.  Cree y use el script de prueba de SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar el diagrama de actualización.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="see-also"></a>Vea también  
 [Consideraciones de seguridad de updategram &#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  
