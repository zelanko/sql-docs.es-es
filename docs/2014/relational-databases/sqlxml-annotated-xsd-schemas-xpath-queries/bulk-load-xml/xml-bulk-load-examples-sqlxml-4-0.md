---
title: Ejemplos de carga masiva XML (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- overflow-field annotation
- ConnectionCommand property
- XMLFragment property
- relationship chains [SQLXML]
- multiple table bulk loading
- examples [SQLXML], XML Bulk Load
- overflow data [SQLXML]
- sql:datatype
- transaction mode [SQLXML]
- CheckConstraints property
- sql:overflow-field
- XML Bulk Load [SQLXML], examples
- TempFilePath property
- datatype annotation
- Transaction property
- KeepIdentity property
- Execute method
- streaming XML data
- xml data type [SQL Server], SQLXML
- bulk load [SQLXML], examples
ms.assetid: 970e4553-b41d-4a12-ad50-0ee65d1f305d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fc1618a40585ad1b20d4f59019f1dd3674468da7
ms.sourcegitcommit: 45a9d7ffc99502c73f08cb937cbe9e89d9412397
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/22/2019
ms.locfileid: "66013266"
---
# <a name="xml-bulk-load-examples-sqlxml-40"></a>Ejemplos de carga masiva XML (SQLXML 4.0)
  En los ejemplos siguientes se muestra la funcionalidad de la carga masiva XML en Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. En cada ejemplo se proporcionan un esquema XSD y su esquema XDR equivalente.  
  
## <a name="bulk-loader-script-validateandbulkloadvbs"></a>Script de carga masiva (ValidateAndBulkload.vbs)  
 El script siguiente, escrito en el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic Scripting Edition (VBScript), carga un documento XML en DOM XML; de lo valida con respecto a un esquema; y, si el documento es válido, se ejecuta un masiva XML carga a carga el XML en un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabla. Este script puede usarse en cada uno de los ejemplos individuales que hacen referencia a él más adelante en este tema.  
  
> [!NOTE]  
>  La carga masiva XML no genera ninguna advertencia o error si no se carga contenido del archivo de datos. Por lo tanto, es recomendable validar el archivo de datos XML antes de ejecutar cualquier operación de carga masiva.  
  
```  
Dim FileValid  
  
set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
objBL.ConnectionString = "provider=SQLOLEDB;data source=MyServer;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
  
'Validate the data file prior to bulkload  
Dim sOutput   
sOutput = ValidateFile("SampleXMLData.xml", "", "SampleSchema.xml")  
WScript.Echo sOutput  
  
If FileValid Then  
   ' Check constraints and initiate transaction (if needed)  
   ' objBL.CheckConstraints = True  
   ' objBL.Transaction=True  
  'Execute XML bulkload using file.  
  objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
  set objBL=Nothing  
End If  
  
Function ValidateFile(strXmlFile,strUrn,strXsdFile)  
  
   ' Create a schema cache and add SampleSchema.xml to it.  
   Dim xs, fso, sAppPath  
   Set fso = CreateObject("Scripting.FileSystemObject")   
   Set xs = CreateObject("MSXML2.XMLSchemaCache.6.0")  
   sAppPath = fso.GetFolder(".")   
   xs.Add strUrn, sAppPath & "\" & strXsdFile  
  
   ' Create an XML DOMDocument object.  
   Dim xd   
   Set xd = CreateObject("MSXML2.DOMDocument.6.0")  
  
   ' Assign the schema cache to the DOM document.  
   ' schemas collection.  
   Set xd.schemas = xs  
  
   ' Load XML document as DOM document.  
   xd.async = False  
   xd.Load sAppPath & "\" & strXmlFile  
  
   ' Return validation results in message to the user.  
   If xd.parseError.errorCode <> 0 Then  
        ValidateFile = "Validation failed on " & _  
             strXmlFile & vbCrLf & _  
             "=======" & vbCrLf & _  
             "Reason: " & xd.parseError.reason & _  
             vbCrLf & "Source: " & _  
             xd.parseError.srcText & _  
             vbCrLf & "Line: " & _  
             xd.parseError.Line & vbCrLf  
             FileValid = False  
    Else  
        ValidateFile = "Validation succeeded for " & _  
             strXmlFile & vbCrLf & _  
             "========" & _  
             vbCrLf & "Contents to be bulkloaded" & vbCrLf  
             FileValid = True  
    End If  
End Function  
```  
  
## <a name="a-bulk-loading-xml-in-a-table"></a>A. Cargar XML de forma masiva en una tabla  
 En este ejemplo se establece una conexión a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que se especifica en la propiedad ConnectionString (MyServer). El ejemplo también especifica el errorlogfile, propiedad. Por lo tanto, la salida de error se guarda en el archivo especificado ("C:\error.log"), aunque es posible cambiar esta ubicación por otra distinta. Observe también que el método Execute tiene como parámetros el archivo de esquema de asignación (SampleSchema.xml) y el archivo de datos XML (SampleXMLData.xml). Cuando se ejecuta la carga masiva, la tabla Cust que ha creado en **tempdb** base de datos incluirá nuevos registros basados en el contenido del archivo de datos XML.  
  
#### <a name="to-test-a-sample-bulk-load"></a>Para probar una carga masiva del ejemplo  
  
1.  Cree esta tabla:  
  
    ```  
    CREATE TABLE Cust(CustomerID  int PRIMARY KEY,  
                      CompanyName varchar(20),  
                      City        varchar(20));  
    GO  
    ```  
  
2.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como SampleSchema.xml. En este archivo, agregue el siguiente esquema XSD:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
       <xsd:element name="ROOT" sql:is-constant="1" >  
         <xsd:complexType>  
           <xsd:sequence>  
             <xsd:element name="Customers" sql:relation="Cust" maxOccurs="unbounded">  
               <xsd:complexType>  
                 <xsd:sequence>  
                   <xsd:element name="CustomerID"  type="xsd:integer" />  
                   <xsd:element name="CompanyName" type="xsd:string" />  
                   <xsd:element name="City"        type="xsd:string" />  
                 </xsd:sequence>  
               </xsd:complexType>  
             </xsd:element>  
           </xsd:sequence>  
          </xsd:complexType>  
         </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como SampleXMLData.xml. En este archivo, agregue el siguiente documento XML:  
  
    ```  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Sean Chai</CompanyName>  
        <City>New York</City>  
      </Customers>  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Tom Johnston</CompanyName>  
         <City>Los Angeles</City>  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Institute of Art</CompanyName>  
        <City>Chicago</City>  
      </Customers>  
    </ROOT>  
    ```  
  
4.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como ValidateAndBulkload.vbs. En este archivo, agregue el código VBScript proporcionado anteriormente al principio de este tema. Modifique la cadena de conexión para especificar el nombre de servidor adecuado. Especifique la ruta de acceso adecuada para los archivos que se especifican como parámetros al método Execute.  
  
5.  Ejecute el código VBScript. La carga masiva XML carga el XML en la tabla Cust.  
  
 Éste es el esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >   
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="ROOT" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers"  sql:relation="Cust" >  
      <element type="CustomerID"  sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City"        sql:field="City" />  
  
   </ElementType>  
</Schema>  
```  
  
## <a name="b-bulk-loading-xml-data-in-multiple-tables"></a>b. Cargar datos XML de forma masiva en varias tablas  
 En este ejemplo, el documento XML consta de los  **\<cliente >** y  **\<orden >** elementos.  
  
```  
<ROOT>  
  <Customers>  
    <CustomerID>1111</CustomerID>  
    <CompanyName>Sean Chai</CompanyName>  
    <City>NY</City>  
    <Order OrderID="1" />  
    <Order OrderID="2" />  
  </Customers>  
  <Customers>  
    <CustomerID>1112</CustomerID>  
    <CompanyName>Tom Johnston</CompanyName>  
     <City>LA</City>    
    <Order OrderID="3" />  
  </Customers>  
  <Customers>  
    <CustomerID>1113</CustomerID>  
    <CompanyName>Institute of Art</CompanyName>  
    <Order OrderID="4" />  
  </Customers>  
</ROOT>  
```  
  
 Este masiva de ejemplo carga los datos XML en dos tablas, **Cust** y **CustOrder**:  
  
```  
Cust(CustomerID, CompanyName, City)  
CustOrder(OrderID, CustomerID)  
```  
  
 El esquema XSD siguiente define la vista XML de estas tablas. El esquema especifica la relación de elementos primarios y secundarios entre los  **\<cliente >** y  **\<orden >** elementos.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:annotation>  
    <xsd:appinfo>  
      <sql:relationship name="CustCustOrder"  
          parent="Cust"  
          parent-key="CustomerID"  
          child="CustOrder"  
          child-key="CustomerID" />  
    </xsd:appinfo>  
  </xsd:annotation>  
  <xsd:element name="ROOT" sql:is-constant="1" >  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Customers" sql:relation="Cust" >  
          <xsd:complexType>  
            <xsd:sequence>  
              <xsd:element name="CustomerID"  type="xsd:integer" />  
              <xsd:element name="CompanyName" type="xsd:string" />  
              <xsd:element name="City"        type="xsd:string" />  
              <xsd:element name="Order"   
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder" >  
                <xsd:complexType>  
                  <xsd:attribute name="OrderID" type="xsd:integer" />  
                </xsd:complexType>  
              </xsd:element>  
             </xsd:sequence>  
          </xsd:complexType>  
        </xsd:element>  
      </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Carga masiva XML utiliza la relación de clave externa y clave principal especificada anteriormente entre el  **\<Cust >** y  **\<CustOrder >** elementos masiva cargar los datos en ambas tablas .  
  
#### <a name="to-test-a-sample-bulk-load"></a>Para probar una carga masiva del ejemplo  
  
1.  Cree dos tablas en **tempdb** base de datos:  
  
    ```  
    USE tempdb;  
    CREATE TABLE Cust(  
           CustomerID  int PRIMARY KEY,  
           CompanyName varchar(20),  
           City        varchar(20));  
    CREATE TABLE CustOrder(        OrderID     int PRIMARY KEY,   
            CustomerID int FOREIGN KEY REFERENCES Cust(CustomerID));  
    ```  
  
2.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como SampleSchema.xml. Agregue al archivo el esquema XSD que se proporciona en este ejemplo.  
  
3.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como SampleData.xml. Agregue al archivo el documento XML proporcionado anteriormente en este ejemplo.  
  
4.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como ValidateAndBulkload.vbs. En este archivo, agregue el código VBScript proporcionado anteriormente al principio de este tema. Modifique la cadena de conexión para especificar el nombre de servidor y de base de datos adecuado. Especifique la ruta de acceso adecuada para los archivos que se especifican como parámetros al método Execute.  
  
5.  Ejecute el código VBScript anterior. La carga masiva XML carga el documento XML en las tablas Cust y CustOrder.  
  
 Éste es el esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >   
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="ROOT" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust" >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
<sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
</Schema>  
```  
  
## <a name="c-using-chain-relationships-in-the-schema-to-bulk-load-xml"></a>C. Usar las relaciones de cadena del esquema para cargar XML de forma masiva  
 En este ejemplo se muestra la forma en que la carga masiva XML usa la relación M:N especificada en el esquema de asignación para cargar datos en una tabla que representa una relación M:N.  
  
 Por ejemplo, fíjese en este esquema XSD:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="OrderOD"  
          parent="Ord"  
          parent-key="OrderID"  
          child="OrderDetail"  
          child-key="OrderID" />  
  
    <sql:relationship name="ODProduct"  
          parent="OrderDetail"  
          parent-key="ProductID"  
          child="Product"  
          child-key="ProductID"   
          inverse="true"/>  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="ROOT" sql:is-constant="1" >  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Order"   
                     sql:relation="Ord"   
                     sql:key-fields="OrderID" >  
          <xsd:complexType>  
            <xsd:sequence>  
             <xsd:element name="Product"  
                          sql:relation="Product"   
                          sql:key-fields="ProductID"  
                          sql:relationship="OrderOD ODProduct">  
               <xsd:complexType>  
                 <xsd:attribute name="ProductID" type="xsd:int" />  
                 <xsd:attribute name="ProductName" type="xsd:string" />  
               </xsd:complexType>  
             </xsd:element>  
           </xsd:sequence>  
           <xsd:attribute name="OrderID"   type="xsd:integer" />   
           <xsd:attribute name="CustomerID"   type="xsd:string" />  
         </xsd:complexType>  
       </xsd:element>  
      </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 El esquema especifica un  **\<orden >** elemento con un  **\<producto >** elemento secundario. El  **\<orden >** elemento se asigna a la tabla Ord y  **\<producto >** elemento se asigna a la tabla Product de la base de datos. La relación de cadena especificada en el  **\<producto >** elemento identifica una relación m: n representada por la tabla OrderDetail. (Un pedido puede incluir muchos productos y un producto puede estar incluido en muchos pedidos.)  
  
 Al cargar un documento XML de forma masiva con este esquema, los registros se agregan a las tablas Ord, Product y OrderDetail.  
  
#### <a name="to-test-a-working-sample"></a>Para probar un ejemplo funcional  
  
1.  Cree tres tablas:  
  
    ```  
    CREATE TABLE Ord (  
             OrderID     int  PRIMARY KEY,  
             CustomerID  varchar(5));  
    GO  
    CREATE TABLE Product (  
             ProductID   int PRIMARY KEY,  
             ProductName varchar(20));  
    GO  
    CREATE TABLE OrderDetail (  
           OrderID     int FOREIGN KEY REFERENCES Ord(OrderID),  
           ProductID   int FOREIGN KEY REFERENCES Product(ProductID),  
                       CONSTRAINT OD_key PRIMARY KEY (OrderID, ProductID));  
    GO  
    ```  
  
2.  Guarde el esquema proporcionado anteriormente en este ejemplo como SampleSchema.xml.  
  
3.  Guarde los siguientes datos XML de ejemplo como SampleXMLData.xml:  
  
    ```  
    <ROOT>    
      <Order OrderID="1" CustomerID="ALFKI">  
        <Product ProductID="1" ProductName="Chai" />  
        <Product ProductID="2" ProductName="Chang" />  
      </Order>  
      <Order OrderID="2" CustomerID="ANATR">  
        <Product ProductID="3" ProductName="Aniseed Syrup" />  
        <Product ProductID="4" ProductName="Gumbo Mix" />  
      </Order>  
    </ROOT>  
    ```  
  
4.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como ValidateAndBulkload.vbs. En este archivo, agregue el código VBScript proporcionado anteriormente al principio de este tema. Modifique la cadena de conexión para especificar el nombre de servidor y de base de datos adecuado. Para este ejemplo, quite los comentarios de las siguientes líneas del código fuente.  
  
    ```  
    objBL.CheckConstraints = True  
    objBL.Transaction=True  
    ```  
  
5.  Ejecute el código VBScript. La carga masiva XML carga el documento XML en las tablas Ord y Product.  
  
## <a name="d-bulk-loading-in-identity-type-columns"></a>D. Cargar datos de forma masiva en columnas de tipo Identity  
 En este ejemplo se muestra la forma en que la carga masiva administra las columnas de tipo Identity. En el ejemplo, los datos se cargan de forma masiva en tres tablas (Ord, Product y OrderDetail).  
  
 En estas tablas:  
  
-   La columna OrderID de la tabla Ord es una columna de tipo Identity  
  
-   La columna ProductID de la tabla Product es una columna de tipo Identity.  
  
-   Las columnas OrderID y ProductID de OrderDetail son columnas de clave externa que hacen referencia a las columnas de clave principal correspondientes de las tablas Ord y Product.  
  
 Los esquemas de tabla de este ejemplo son los siguientes:  
  
```  
Ord (OrderID, CustomerID)  
Product (ProductID, ProductName)  
OrderDetail (OrderID, ProductID)  
```  
  
 En este ejemplo de carga masiva XML, la propiedad KeepIdentity del modelo de objetos carga masiva se establece en false. Por lo tanto, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] genera valores de identidad para las columnas ProductID y OrderID de las tablas Product y Ord, respectivamente (se omiten los valores proporcionados en los documentos que van a cargarse de forma masiva).  
  
 En este caso, la carga masiva XML identifica la relación de clave principal y clave externa entre las tablas. En primer lugar, la carga masiva inserta los registros en las tablas con la clave principal y, a continuación, propaga el valor de identidad generado por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a las tablas con columnas de clave externa. En el siguiente ejemplo, la carga masiva XML inserta datos en las tablas en el orden que se indica a continuación:  
  
1.  Producto  
  
2.  Ord  
  
3.  OrderDetail  
  
    > [!NOTE]  
    >  Para propagar los valores de identidad generados en las tablas Products y Orders, la lógica de procesamiento exige que la carga masiva XML realice un seguimiento de estos valores para insertarlos posteriormente en la tabla OrderDetails. Para ello, la carga masiva XML crea tablas intermedias, rellena de datos estas tablas y, a continuación, quita estos datos.  
  
#### <a name="to-test-a-working-sample"></a>Para probar un ejemplo funcional  
  
1.  Cree estas tablas:  
  
    ```  
    CREATE TABLE Ord (  
             OrderID     int identity(1,1)  PRIMARY KEY,  
             CustomerID  varchar(5));  
    GO  
    CREATE TABLE Product (  
             ProductID   int identity(1,1) PRIMARY KEY,  
             ProductName varchar(20));  
    GO  
    CREATE TABLE OrderDetail (  
           OrderID     int FOREIGN KEY REFERENCES Ord(OrderID),  
           ProductID   int FOREIGN KEY REFERENCES Product(ProductID),  
                       CONSTRAINT OD_key PRIMARY KEY (OrderID, ProductID));  
    GO  
    ```  
  
2.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como SampleSchema.xml. Agregue este esquema XSD al archivo.  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
     <xsd:annotation>  
       <xsd:appinfo>  
        <sql:relationship name="OrderOD"  
              parent="Ord"  
              parent-key="OrderID"  
              child="OrderDetail"  
              child-key="OrderID" />  
        <sql:relationship name="ODProduct"  
              parent="OrderDetail"  
              parent-key="ProductID"  
              child="Product"  
              child-key="ProductID"   
              inverse="true"/>  
       </xsd:appinfo>  
     </xsd:annotation>  
  
      <xsd:element name="Order" sql:relation="Ord"   
                                sql:key-fields="OrderID" >  
       <xsd:complexType>  
         <xsd:sequence>  
            <xsd:element name="Product" sql:relation="Product"   
                         sql:key-fields="ProductID"  
                         sql:relationship="OrderOD ODProduct">  
              <xsd:complexType>  
                 <xsd:attribute name="ProductID" type="xsd:int" />  
                 <xsd:attribute name="ProductName" type="xsd:string" />  
              </xsd:complexType>  
            </xsd:element>  
         </xsd:sequence>  
            <xsd:attribute name="OrderID"   type="xsd:integer" />   
            <xsd:attribute name="CustomerID"   type="xsd:string" />  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como SampleXMLData.xml. Agregue el siguiente documento XML.  
  
    ```  
    <ROOT>    
      <Order OrderID="11" CustomerID="ALFKI">  
        <Product ProductID="11" ProductName="Chai" />  
        <Product ProductID="22" ProductName="Chang" />  
      </Order>  
      <Order OrderID="22" CustomerID="ANATR">  
         <Product ProductID="33" ProductName="Aniseed Syrup" />  
        <Product ProductID="44" ProductName="Gumbo Mix" />  
      </Order>  
    </ROOT>  
    ```  
  
4.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como ValidateAndBulkload.vbs. En este archivo, agregue el siguiente código VBScript. Modifique la cadena de conexión para especificar el nombre de servidor y de base de datos adecuado. Especifique la ruta de acceso adecuada para los archivos que actúan como parámetros en el `Execute` método.  
  
    ```  
    Set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "C:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Transaction = False  
    objBL.KeepIdentity = False  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    Set objBL = Nothing  
    MsgBox "Done."  
    ```  
  
5.  Ejecute el código VBScript. La carga masiva XML cargará los datos en las tablas pertinentes.  
  
## <a name="e-generating-table-schemas-before-bulk-loading"></a>E. Generar esquemas de tabla antes de la carga masiva  
 La carga masiva XML puede generar las tablas si no existen antes de la carga masiva. Si se establece la propiedad SchemaGen de la sqlxmlbulkload, objeto en TRUE. Opcionalmente, también puede solicitar la carga masiva XML para quitar las tablas existentes y volver a crearlos estableciendo el sgdroptables, propiedad en TRUE. En el siguiente ejemplo de VBScript se muestra el uso de estas propiedades.  
  
 Asimismo, este ejemplo establece dos propiedades adicionales en TRUE:  
  
-   CheckConstraints. Estableciendo esta propiedad en TRUE se asegurará de que los datos que se inserten en las tablas no infrinjan ninguna restricción especificada en las tablas (en este caso, las restricciones PRIMARY KEY y FOREIGN KEY especificadas entre las tablas Cust y CustOrder). Si se infringe alguna restricción, se produce un error en la carga masiva.  
  
-   XMLFragment. Esta propiedad debe establecerse en TRUE porque el documento XML de ejemplo (origen de datos) no contiene ningún elemento único de nivel superior (y, por lo tanto, es un fragmento).  
  
 Éste es el código VBScript:  
  
```  
Dim objBL   
Set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
  
objBL.CheckConstraints=true  
objBL.XMLFragment = True  
objBL.SchemaGen = True  
objBL.SGDropTables = True  
  
objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
Set objBL = Nothing  
```  
  
#### <a name="to-test-a-working-sample"></a>Para probar un ejemplo funcional  
  
1.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como SampleSchema.xml. Agregue al archivo el esquema XSD proporcionado en el ejemplo anterior, "Usar las relaciones de cadena del esquema para cargar XML de forma masiva".  
  
2.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como SampleXMLData.xml. Agregue al archivo el documento XML proporcionado en el ejemplo anterior, "Usar las relaciones de cadena del esquema para cargar XML de forma masiva". Quitar el \<raíz > elemento de documento (para convertirlo en un fragmento).  
  
3.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como ValidateAndBulkload.vbs. En este archivo, agregue el código VBScript de este ejemplo. Modifique la cadena de conexión para especificar el nombre de servidor y de base de datos adecuado. Especifique la ruta de acceso adecuada para los archivos que se especifican como parámetros al método Execute.  
  
4.  Ejecute el código VBScript. La carga masiva XML crea las tablas necesarias en función del esquema de asignación proporcionado y carga los datos de forma masiva en el mismo.  
  
## <a name="f-bulk-loading-from-a-stream"></a>F. Cargar datos de forma masiva desde un flujo  
 El método Execute del modelo de objetos carga masiva XML toma dos parámetros. El primer parámetro es el archivo de esquema de asignación. El segundo, proporciona los datos XML que se cargarán en la base de datos. Hay dos maneras de pasar los datos XML para el método Execute de la carga masiva XML:  
  
-   Especificar el nombre de archivo como parámetro.  
  
-   Pasar un flujo que contenga los datos XML.  
  
 Este ejemplo muestra cómo realizar la carga masiva desde un flujo.  
  
 VBScript ejecuta primero una instrucción SELECT para recuperar la información del cliente de la tabla Customers de la base de datos Northwind. Puesto que se ha especificado la cláusula FOR XML (con la opción ELEMENTS) en la instrucción SELECT, la consulta devuelve un documento XML centrado en elementos de este formulario:  
  
```  
<Customer>  
  <CustomerID>..</CustomerID>  
  <CompanyName>..</CompanyName>  
  <City>..</City>  
</Customer>  
...  
```  
  
 La secuencia de comandos, a continuación, pasa el XML como un flujo al método Execute como su segundo parámetro. El grueso del método Execute carga los datos en la tabla Cust.  
  
 Dado que esta secuencia de comandos establece la propiedad SchemaGen en TRUE y sgdroptables, propiedad en TRUE, carga masiva XML crea la tabla Cust en la base de datos especificado. (Si la tabla ya existe, quita primero la tabla y, a continuación, vuelve a crearla.)  
  
 Éste es el ejemplo de VBScript:  
  
```  
Set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
Set objCmd = CreateObject("ADODB.Command")  
Set objConn = CreateObject("ADODB.Connection")  
Set objStrmOut = CreateObject ("ADODB.Stream")  
  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile     = "c:\error.log"  
objBL.CheckConstraints = True  
objBL.SchemaGen        = True  
objBL.SGDropTables     = True  
objBL.XMLFragment      = True  
' Open a connection to the instance of SQL Server to get the source data.  
  
objConn.Open "provider=SQLOLEDB;server=(local);database=tempdb;integrated security=SSPI"  
Set objCmd.ActiveConnection = objConn  
objCmd.CommandText = "SELECT CustomerID, CompanyName, City FROM Customers FOR XML AUTO, ELEMENTS"  
  
' Open the return stream and execute the command.  
Const adCRLF = -1  
Const adExecuteStream = 1024  
objStrmOut.Open  
objStrmOut.LineSeparator = adCRLF  
objCmd.Properties("Output Stream").Value = objStrmOut  
objCmd.Execute , , adExecuteStream  
objStrmOut.Position = 0  
  
' Execute bulk load. Read source XML data from the stream.  
objBL.Execute "SampleSchema.xml", objStrmOut  
  
Set objBL = Nothing  
```  
  
 El siguiente esquema de asignación XSD proporciona la información necesaria para crear la tabla:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:element name="ROOT" sql:is-constant="true" >  
  <xsd:complexType>  
    <xsd:sequence>  
      <xsd:element ref="Customers"/>  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
<xsd:element name="Customers" sql:relation="Cust" >  
  <xsd:complexType>  
    <xsd:sequence>  
      <xsd:element name="CustomerID"  
                   type="xsd:string"  
                   sql:datatype="nvarchar(5)"/>  
      <xsd:element name="CompanyName"  
                   type="xsd:string"  
                   sql:datatype="nvarchar(40)"/>  
      <xsd:element name="City"  
                   type="xsd:string"  
                   sql:datatype="nvarchar(40)"/>  
    </xsd:sequence>  
  </xsd:complexType>  
</xsd:element>  
</xsd:schema>  
```  
  
 Éste es el esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
    </ElementType>  
</Schema>  
```  
  
### <a name="opening-a-stream-on-an-existing-file"></a>Abrir un flujo en un archivo existente  
 También puede abrir una secuencia en un archivo de datos XML existente y pasar la secuencia como un parámetro al método Execute (en lugar de pasar el nombre de archivo como parámetro).  
  
 Éste es un ejemplo de Visual Basic que muestra cómo pasar un flujo como parámetro:  
  
```  
Private Sub Form_Load()  
Dim objBL As New SQLXMLBulkLoad  
Dim objStrm As New ADODB.Stream  
Dim objFileSystem As New Scripting.FileSystemObject  
Dim objFile As Scripting.TextStream  
  
MsgBox "Begin BulkLoad..."  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
objBL.CheckConstraints = True  
objBL.SchemaGen = True  
objBL.SGDropTables = True  
' Here again a stream is specified that contains the source data   
' (instead of the file name). But this is just an illustration.  
' Usually this is useful if you have an XML data   
' stream that is created by some other means that you want to bulk   
' load. This example starts with an XML text file, so it may not be the   
' best to use a stream (you can specify the file name directly).  
' Here you could have specified the file name itself.   
Set objFile = objFileSystem.OpenTextFile("c:\SampleData.xml")  
objStrm.Open  
objStrm.WriteText objFile.ReadAll  
objStrm.Position = 0  
objBL.Execute "c:\SampleSchema.xml", objStrm  
  
Set objBL = Nothing  
MsgBox "Done."  
End Sub  
```  
  
 Para probar la aplicación, use el siguiente documento XML en un archivo (SampleData.xml) y el esquema XSD proporcionado en este ejemplo:  
  
 Éstos son los datos de origen XML (SampleData.xml):  
  
```  
<ROOT>  
  <Customers>  
    <CustomerID>1111</CustomerID>  
    <CompanyName>Hanari Carnes</CompanyName>  
    <City>NY</City>  
    <Order OrderID="1" />  
    <Order OrderID="2" />  
  </Customers>  
  
  <Customers>  
    <CustomerID>1112</CustomerID>  
    <CompanyName>Toms Spezialitten</CompanyName>  
     <City>LA</City>  
    <Order OrderID="3" />  
  </Customers>  
  <Customers>  
    <CustomerID>1113</CustomerID>  
    <CompanyName>Victuailles en stock</CompanyName>  
    <Order CustomerID= "4444" OrderID="4" />  
</Customers>  
</ROOT>  
```  
  
 Éste es el esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
             <sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
</Schema>  
```  
  
## <a name="g-bulk-loading-in-overflow-columns"></a>G. Cargar datos de forma masiva en columnas de desbordamiento  
 Si el esquema de asignación especifica una columna de desbordamiento mediante la anotación `sql:overflow-field`, la carga masiva XML copia todos los datos sin consumir del documento de origen a esta columna.  
  
 Fíjese en este esquema XSD:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustCustOrder"  
          parent="Cust"  
          parent-key="CustomerID"  
          child="CustOrder"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  <xsd:element name="Customers" sql:relation="Cust"  
                                sql:overflow-field="OverflowColumn" >  
   <xsd:complexType>  
     <xsd:sequence>  
       <xsd:element name="CustomerID"  type="xsd:integer" />  
       <xsd:element name="CompanyName" type="xsd:string" />  
       <xsd:element name="City"        type="xsd:string" />  
       <xsd:element name="Order"   
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder" >  
         <xsd:complexType>  
          <xsd:attribute name="OrderID" type="xsd:integer" />  
          <xsd:attribute name="CustomerID" type="xsd:integer" />  
         </xsd:complexType>  
       </xsd:element>  
     </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 El esquema identifica una columna de desbordamiento (OverflowColumn) para la tabla Cust. Como resultado, todos no consumidos datos XML para cada  **\<cliente >** elemento se agrega a esta columna.  
  
> [!NOTE]  
>  Todos los elementos abstractos (elementos para los que **abstract = "true"** se especifica) y todos los atributos prohibidos (atributos para los que **prohibido = "true"** se especifica) se consideran de desbordamiento mediante masiva de XML Carga y se agregan a la columna de desbordamiento, si se especifica. (De lo contrario, se omiten.)  
  
#### <a name="to-test-a-working-sample"></a>Para probar un ejemplo funcional  
  
1.  Cree dos tablas en **tempdb** base de datos:  
  
    ```  
    USE tempdb;  
    CREATE TABLE Cust (  
                  CustomerID     int         PRIMARY KEY,  
                  CompanyName    varchar(20) NOT NULL,  
                  City           varchar(20) DEFAULT 'Seattle',  
                  OverflowColumn nvarchar(200));  
    GO  
    CREATE TABLE CustOrder (  
                  OrderID    int PRIMARY KEY,  
                  CustomerID int FOREIGN KEY   
                                 REFERENCES Cust(CustomerID));  
    GO  
    ```  
  
2.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como SampleSchema.xml. Agregue al archivo el esquema XSD que se proporciona en este ejemplo.  
  
3.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como SampleXMLData.xml. Agregue al archivo el siguiente documento XML:  
  
    ```  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City><![CDATA[NY]]> </City>  
        <Junk>garbage in overflow</Junk>  
        <Order OrderID="1" />  
        <Order OrderID="2" />  
      </Customers>  
  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Toms Spezialitten</CompanyName>  
         <![CDATA[LA]]>   
        <!-- <xyz><address>111 Maple, Seattle</address></xyz>   -->  
        <Order OrderID="3" />  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
    </Customers>  
    </ROOT>  
    ```  
  
4.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como ValidateAndBulkload.vbs. Agregue a este archivo el siguiente código Microsoft Visual Basic Scripting Edition (VBScript). Modifique la cadena de conexión para especificar el nombre de servidor y de base de datos adecuado. Especifique la ruta de acceso adecuada para los archivos que se especifican como parámetros al método Execute.  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
5.  Ejecute el código VBScript.  
  
 Éste es el esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"   
                       sql:overflow-field="OverflowColumn"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
             <sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
</Schema>  
```  
  
## <a name="h-specifying-the-file-path-for-temp-files-in-transaction-mode"></a>H. Especificar la ruta de acceso de los archivos temporales en modo de transacción  
 Cuando se carga masiva en modo de transacción (es decir, cuando la propiedad de transacción se establece en TRUE), también debe establecer la propiedad TempFilePath cuando se cumple alguna de las condiciones siguientes:  
  
-   La carga masiva se realiza en un servidor remoto.  
  
-   Se desea usar una unidad local o carpeta alternativa (distinta de la ruta de acceso especificada por la variable de entorno TEMP) para almacenar los archivos temporales creados en el modo de transacción.  
  
 Por ejemplo, el siguiente código VBScript carga datos de forma masiva del archivo SampleXMLData.xml a las tablas de base de datos en modo de transacción. La propiedad TempFilePath es especificada para establecer la ruta de acceso de los archivos temporales que se generan en el modo de transacción.  
  
```  
set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
objBL.ErrorLogFile = "c:\error.log"  
objBL.CheckConstraints = True  
objBL.Transaction=True  
objBL.TempFilePath="\\Server\MyDir"  
objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
set objBL=Nothing  
```  
  
> [!NOTE]  
>  La ruta de acceso de los archivos temporales debe ser una ubicación compartida accesible para la cuenta de servicio de la instancia de destino de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y para la cuenta que está ejecutando la aplicación de carga masiva. A menos que esté la carga masiva en un servidor local, la ruta de acceso de archivo temporal debe ser una ruta de acceso UNC (como \\\servername\sharename).  
  
#### <a name="to-test-a-working-sample"></a>Para probar un ejemplo funcional  
  
1.  Cree esta tabla en **tempdb** base de datos:  
  
    ```  
    USE tempdb;  
    CREATE TABLE Cust (     CustomerID uniqueidentifier,   
          LastName  varchar(20));  
    GO  
    ```  
  
2.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como SampleSchema.xml. Agregue al archivo el siguiente esquema XSD:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="ROOT" sql:is-constant="true" >  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element ref="Customers" />  
          </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
  
      <xsd:element name="Customers" sql:relation="Cust" >  
       <xsd:complexType>  
         <xsd:attribute name="CustomerID"  type="xsd:string" />  
         <xsd:attribute name="LastName" type="xsd:string" />  
       </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como SampleXMLData.xml. Agregue al archivo el siguiente documento XML:  
  
    ```  
    <ROOT>  
    <Customers CustomerID="6F9619FF-8B86-D011-B42D-00C04FC964FF"   
               LastName="Smith" />  
    </ROOT>  
    ```  
  
4.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como ValidateAndBulkload.vbs. En este archivo, agregue el siguiente código VBScript. Modifique la cadena de conexión para especificar el nombre de servidor y de base de datos adecuado. Especifique la ruta de acceso adecuada para los archivos que se especifican como parámetros al método Execute. Especifique también la ruta de acceso adecuada para la propiedad TempFilePath.  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Transaction=True  
    objBL.TempFilePath="\\server\folder"  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
5.  Ejecute el código VBScript.  
  
     Debe especificar el esquema correspondiente `sql:datatype` para el **CustomerID** atributo cuando el valor de **CustomerID** se especifica como un GUID que incluye llaves ({y}), tales como:  
  
    ```  
    <ROOT>  
    <Customers CustomerID="{6F9619FF-8B86-D011-B42D-00C04FC964FF}"   
               LastName="Smith" />  
    </ROOT>  
    ```  
  
     Éste es el esquema actualizado:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
      <xsd:element name="ROOT" sql:is-constant="true" >  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element ref="Customers" />  
          </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
  
      <xsd:element name="Customers" sql:relation="Cust" >  
       <xsd:complexType>  
         <xsd:attribute name="CustomerID"  type="xsd:string"   
                        sql:datatype="uniqueidentifier" />  
         <xsd:attribute name="LastName" type="xsd:string" />  
       </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
     Cuando `sql:datatype` se especifica que identifica el tipo de columna como `uniqueidentifier`, la operación de carga masiva quita las llaves ({y}) desde el **CustomerID** valor antes de insertarlo en la columna.  
  
 Éste es el esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
<ElementType name="ROOT" sql:is-constant="1">  
      <element type="Customers" />  
</ElementType>  
<ElementType name="Customers" sql:relation="Cust" >  
  <AttributeType name="CustomerID"  sql:datatype="uniqueidentifier" />  
  <AttributeType name="LastName"   />  
  
  <attribute type="CustomerID" />  
  <attribute type="LastName"   />  
</ElementType>  
</Schema>  
```  
  
## <a name="i-using-an-existing-database-connection-with-the-connectioncommand-property"></a>I. Usar una conexión de base de datos existente con la propiedad ConnectionCommand  
 Puede usar una conexión ADO existente para la carga masiva XML. Esto resulta de gran utilidad si la carga masiva XML es simplemente una de entre las muchas operaciones que se realizarán en un origen de datos.  
  
 La propiedad ConnectionCommand le permite usar una conexión ADO existente mediante el uso de un objeto de comando ADO. Esto se muestra en el siguiente ejemplo de Visual Basic:  
  
```  
Private Sub Form_Load()  
Dim objBL As New SQLXMLBulkLoad4  
Dim objCmd As New ADODB.Command  
Dim objConn As New ADODB.Connection  
  
'Open a connection to an instance of SQL Server.  
objConn.Open "provider=SQLOLEDB;data source=(local);database=tempdb;integrated security=SSPI"  
'Ask the Command object to use the connection just established.  
Set objCmd.ActiveConnection = objConn  
  
'Tell Bulk Load to use the active command object that is using the Connection obj.  
objBL.ConnectionCommand = objCmd  
objBL.ErrorLogFile = "c:\error.log"  
objBL.CheckConstraints = True  
'The Transaction property must be set to True if you use ConnectionCommand.  
objBL.Transaction = True  
objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
Set objBL = Nothing  
End Sub  
```  
  
#### <a name="to-test-a-working-sample"></a>Para probar un ejemplo funcional  
  
1.  Cree dos tablas en **tempdb** base de datos:  
  
    ```  
    USE tempdb;  
    CREATE TABLE Cust(  
                   CustomerID   varchar(5) PRIMARY KEY,  
                   CompanyName  varchar(30),  
                   City         varchar(20));  
    GO  
    CREATE TABLE CustOrder(  
                   CustomerID  varchar(5) references Cust (CustomerID),  
                   OrderID     varchar(5) PRIMARY KEY);  
    GO  
    ```  
  
2.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como SampleSchema.xml. Agregue al archivo el siguiente esquema XSD:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
    <xsd:annotation>  
      <xsd:appinfo>  
        <sql:relationship name="CustCustOrder"  
              parent="Cust"  
              parent-key="CustomerID"  
              child="CustOrder"  
              child-key="CustomerID" />  
      </xsd:appinfo>  
    </xsd:annotation>  
      <xsd:element name="ROOT" sql:is-constant="true" >  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element ref="Customers" />  
          </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
      <xsd:element name="Customers" sql:relation="Cust" >  
       <xsd:complexType>  
         <xsd:sequence>  
           <xsd:element name="CustomerID"  type="xsd:integer" />  
           <xsd:element name="CompanyName" type="xsd:string" />  
           <xsd:element name="City"        type="xsd:string" />  
           <xsd:element name="Order"   
                              sql:relation="CustOrder"  
                              sql:relationship="CustCustOrder" >  
             <xsd:complexType>  
              <xsd:attribute name="OrderID" type="xsd:integer" />  
              <xsd:attribute name="CustomerID" type="xsd:integer" />  
             </xsd:complexType>  
           </xsd:element>  
         </xsd:sequence>  
        </xsd:complexType>  
      </xsd:element>  
    </xsd:schema>  
    ```  
  
3.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como SampleXMLData.xml. Agregue al archivo el siguiente documento XML:  
  
    ```  
    <ROOT>  
      <Customers>  
        <CustomerID>1111</CustomerID>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City>NY</City>  
        <Order OrderID="1" />  
        <Order OrderID="2" />  
      </Customers>  
  
      <Customers>  
        <CustomerID>1112</CustomerID>  
        <CompanyName>Toms Spezialitten</CompanyName>  
         <City>LA</City>  
        <Order OrderID="3" />  
      </Customers>  
      <Customers>  
        <CustomerID>1113</CustomerID>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
    </Customers>  
    </ROOT>  
    ```  
  
4.  Cree una aplicación de Visual Basic (EXE estándar) y el código anterior. Agregue estas referencias al proyecto:  
  
    ```  
    Microsoft XML BulkLoad for SQL Server 4.0 Type Library  
    Microsoft ActiveX Data objects 2.6 Library  
    ```  
  
5.  Ejecute la aplicación.  
  
 Éste es el esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >  
  
   <ElementType name="CustomerID" dt:type="int" />  
   <ElementType name="CompanyName" dt:type="string" />  
   <ElementType name="City" dt:type="string" />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust"  >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
         <sql:relationship  
                key-relation="Cust"  
                key="CustomerID"  
                foreign-key="CustomerID"  
                foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
</Schema>  
```  
  
## <a name="j-bulk-loading-in-xml-data-type-columns"></a>J. Cargar datos de forma masiva en columnas de tipo de datos xml  
 Si el esquema de asignación especifica una [tipo de datos xml](/sql/t-sql/xml/xml-transact-sql) columna utilizando el `sql:datatype="xml"` anotación, carga masiva XML puede copiar los elementos secundarios XML para el campo asignado del documento de origen en esta columna.  
  
 Fíjese en el esquema XSD siguiente, que asigna una vista de la tabla Production.ProductModel de la base de datos de ejemplo AdventureWorks. En esta tabla, el campo CatalogDescription de `xml` tipo de datos se asigna a un  **\<Desc >** elemento mediante el `sql:field` y `sql:datatype="xml"` anotaciones.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
           xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
           xmlns="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">   
  <xsd:element name="ProductModel"  sql:relation="Production.ProductModel" >  
    <xsd:complexType>  
      <xsd:sequence>  
        <xsd:element name="Name" type="xs:string"></xsd:element>  
        <xsd:element name="Desc" sql:field="CatalogDescription" sql:datatype="xml">  
        <xsd:complexType>  
          <xsd:sequence>  
            <xsd:element name="ProductDescription">  
              <xsd:complexType>  
                <xsd:sequence>  
                  <xsd:element name="Summary" type="xs:anyType"/>  
                </xsd:sequence>  
              </xsd:complexType>  
            </xsd:element>  
          </xsd:sequence>  
        </xsd:complexType>  
        </xsd:element>   
     </xsd:sequence>  
     <xsd:attribute name="ProductModelID" sql:field="ProductModelID" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
#### <a name="to-test-a-working-sample"></a>Para probar un ejemplo funcional  
  
1.  Compruebe que esté instalada la base de datos de ejemplo AdventureWorks.  
  
2.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como SampleSchema.xml. Copie el esquema XSD anterior, péguelo en el archivo y guárdelo.  
  
3.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como SampleXMLData.xml. Copie el siguiente documento XML, péguelo en el archivo y guárdelo en la misma carpeta utilizada en el paso anterior.  
  
    ```  
    <ProductModel ProductModelID="2005">  
        <Name>Mountain-100 (2005 model)</Name>  
        <Desc><?xml-stylesheet href="ProductDescription.xsl" type="text/xsl"?>  
            <p1:ProductDescription xmlns:p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription"   
                  xmlns:wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain"   
                  xmlns:wf="http://www.adventure-works.com/schemas/OtherFeatures"   
                  xmlns:html="http://www.w3.org/1999/xhtml"   
                  xmlns="">  
                <p1:Summary>  
                    <html:p>Our top-of-the-line competition mountain bike.   
          Performance-enhancing options include the innovative HL Frame,   
          super-smooth front suspension, and traction for all terrain.  
                            </html:p>  
                </p1:Summary>  
                <p1:Manufacturer>  
                    <p1:Name>AdventureWorks</p1:Name>  
                    <p1:Copyright>2002-2005</p1:Copyright>  
                    <p1:ProductURL>HTTP://www.Adventure-works.com</p1:ProductURL>  
                </p1:Manufacturer>  
                <p1:Features>These are the product highlights.   
                     <wm:Warranty>  
                        <wm:WarrantyPeriod>3 years</wm:WarrantyPeriod>  
                        <wm:Description>parts and labor</wm:Description>  
                    </wm:Warranty><wm:Maintenance>  
                        <wm:NoOfYears>10 years</wm:NoOfYears>  
                        <wm:Description>maintenance contract available through your dealer or any AdventureWorks retail store.</wm:Description>  
                    </wm:Maintenance><wf:wheel>High performance wheels.</wf:wheel><wf:saddle>  
                        <html:i>Anatomic design</html:i> and made from durable leather for a full-day of riding in comfort.</wf:saddle><wf:pedal>  
                        <html:b>Top-of-the-line</html:b> clipless pedals with adjustable tension.</wf:pedal><wf:BikeFrame>Each frame is hand-crafted in our Bothell facility to the optimum diameter   
          and wall-thickness required of a premium mountain frame.   
          The heat-treated welded aluminum frame has a larger diameter tube that absorbs the bumps.</wf:BikeFrame><wf:crankset> Triple crankset; alumunim crank arm; flawless shifting. </wf:crankset></p1:Features>  
                <!-- add one or more of these elements... one for each specific product in this product model -->  
                <p1:Picture>  
                    <p1:Angle>front</p1:Angle>  
                    <p1:Size>small</p1:Size>  
                    <p1:ProductPhotoID>118</p1:ProductPhotoID>  
                </p1:Picture>  
                <!-- add any tags in <specifications> -->  
                <p1:Specifications> These are the product specifications.  
                       <Material>Almuminum Alloy</Material><Color>Available in most colors</Color><ProductLine>Mountain bike</ProductLine><Style>Unisex</Style><RiderExperience>Advanced to Professional riders</RiderExperience></p1:Specifications>  
            </p1:ProductDescription>  
        </Desc>  
    </ProductModel>  
    ```  
  
4.  Cree un archivo en su editor de texto o editor XML preferido y guárdelo como BulkloadXml.vbs. Copie el siguiente código VBScript y péguelo en el archivo. Guárdelo en la misma carpeta utilizada para los archivos de esquema y datos XML anteriores.  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=MyServer;database=AdventureWorks;integrated security=SSPI"  
  
    Dim fso, sAppPath  
    Set fso = CreateObject("Scripting.FileSystemObject")   
    sAppPath = fso.GetFolder(".")   
  
    objBL.ErrorLogFile = sAppPath & "\error.log"  
  
    'Execute XML bulkload using file.  
    objBL.Execute "SampleSchema.xml", "SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
5.  Ejecute el script BulkloadXml.vbs.  
  
  
