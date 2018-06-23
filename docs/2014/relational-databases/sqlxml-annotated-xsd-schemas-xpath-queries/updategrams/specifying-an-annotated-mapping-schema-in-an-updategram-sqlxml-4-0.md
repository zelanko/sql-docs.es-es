---
title: Especificar un esquema de asignación anotados en un diagrama de actualización (SQLXML 4.0) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- annotated XSD schemas, updategrams
- data types [SQLXML], mapping schema in updategrams
- updategrams [SQLXML], annotated mapping schemas
- annotated XDR schemas, updategrams
- inverse attribute
- parent-child relationships [SQLXML]
- mapping-schema attribute
- mapping schema [SQLXML], updategrams
- sql:inverse
ms.assetid: 2e266ed9-4cfb-434a-af55-d0839f64bb9a
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5bba718cbb6fd94fc6e50fda3fa423736aeb7a03
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36110898"
---
# <a name="specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-40"></a>Cómo especificar un esquema de asignación anotado en un diagrama de actualización (SQLXML 4.0)
  En este tema se explica el modo de usar el esquema de asignación (XSD o XDR) especificado en un diagrama de actualización para procesar las actualizaciones. En un diagrama de actualización, puede proporcionar el nombre de un esquema de asignación anotados para usarlo para asignar los elementos y atributos en el diagrama de actualización a las tablas y columnas en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Al especificar un esquema de asignación en un diagrama de actualización, los nombres de elementos y atributos especificados en el diagrama de actualización deben asignarse a los elementos y atributos del esquema de asignación.  
  
 Para especificar un esquema de asignación, utilice la `mapping-schema` atributo de la  **\<sincronización >** elemento. En los ejemplos siguientes se muestran dos diagramas de actualización: uno que usa un esquema de asignación simple y otro que usa un esquema más complejo.  
  
> [!NOTE]  
>  En esta documentación se asume que está familiarizado con la compatibilidad de las plantillas y el esquema de asignación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [Introducción a los esquemas XSD anotados &#40;SQLXML 4.0&#41;](../../sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md). Para obtener información sobre las aplicaciones heredadas que usan XDR, vea [esquemas XDR anotados &#40;desusado en SQLXML 4.0&#41;](../../sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
## <a name="dealing-with-data-types"></a>Trabajar con tipos de datos  
 Si el esquema especifica la `image`, `binary`, o `varbinary` [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de datos (mediante el uso de `sql:datatype`) y no especifica un tipo de datos XML, el diagrama de actualización, se da por supuesto que el tipo de datos XML es `binary base 64`. Si los datos son de tipo `bin.base`, debe especificar de forma explícita el tipo (`dt:type=bin.base` o `type="xsd:hexBinary"`).  
  
 Si el sistema especifica el tipo de datos XSD `dateTime`, `date` o `time`, también debe especificar el tipo de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] correspondiente mediante `sql:datatype="dateTime"`.  
  
 Al administrar los parámetros de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `money` tipo, debe especificar explícitamente `sql:datatype="money"` en el nodo correspondiente en el esquema de asignación.  
  
## <a name="examples"></a>Ejemplos  
 Para crear ejemplos funcionales mediante los siguientes ejemplos, debe cumplir los requisitos especificados en [requisitos para ejecutar los ejemplos de SQLXML](../../sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-creating-an-updategram-with-a-simple-mapping-schema"></a>A. Crear un diagrama de actualización con un esquema de asignación simple  
 El siguiente esquema XSD (SampleSchema.xml) es un esquema de asignación que se asigna el  **\<cliente >** elemento a la tabla Sales.Customer:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
        <xsd:attribute name="CustID"    
                       sql:field="CustomerID"   
                       type="xsd:string" />  
        <xsd:attribute name="RegionID"    
                       sql:field="TerritoryID"    
                       type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 El diagrama de actualización siguiente inserta un registro en la tabla Sales.Customer y se basa en el esquema de asignación anterior para asignar correctamente estos datos a la tabla. Observe que el diagrama de actualización usa el mismo nombre de elemento,  **\<cliente >**, tal como se define en el esquema. Esto resulta obligatorio porque el diagrama de actualización especifica un esquema determinado.  
  
##### <a name="to-test-the-updategram"></a>Para probar el diagrama de actualización  
  
1.  Copie el código de esquema anterior y péguelo en un archivo de texto. Guarde el archivo como SampleUpdateSchema.xml.  
  
2.  Copie la plantilla de diagrama de actualización siguiente y péguela en un archivo de texto. Guarde el archivo como SampleUpdategram.xml en el mismo directorio donde guardó SampleUpdateSchema.xml.  
  
    ```  
    <ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
      <updg:sync mapping-schema="SampleUpdateSchema.xml">  
        <updg:before>  
          <Customer CustID="1" RegionID="1"  />  
        </updg:before>  
        <updg:after>  
          <Customer CustID="1" RegionID="2" />  
        </updg:after>  
      </updg:sync>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (SampleUpdateSchema.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Éste es el esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
   <Schema xmlns="urn:schemas-microsoft-com:xml-data"   
         xmlns:dt="urn:schemas-microsoft-com:datatypes"   
         xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
     <ElementType name="Customer" sql:relation="Sales.Customer" >  
       <AttributeType name="CustID" />  
       <AttributeType name="RegionID" />  
  
       <attribute type="CustID" sql:field="CustomerID" />  
       <attribute type="RegionID" sql:field="TerritoryID" />  
     </ElementType>  
   </Schema>   
```  
  
### <a name="b-inserting-a-record-by-using-the-parent-child-relationship-specified-in-the-mapping-schema"></a>B. Insertar un registro mediante la relación de elementos primarios y secundarios especificada en el esquema de asignación  
 Los elementos de esquema pueden estar relacionados. El  **\<SQL: Relationship >** elemento especifica la relación de elementos primarios y secundarios entre los elementos de esquema. Esta información se usa para actualizar las tablas correspondientes que tienen una relación de clave principal y clave externa.  
  
 El siguiente esquema de asignación (SampleSchema.xml) consta de dos elementos,  **\<orden >** y  **\<OD >**:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="OrderOD"  
          parent="Sales.SalesOrderHeader"  
          parent-key="SalesOrderID"  
          child="Sales.SalesOrderDetail"  
          child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="OD"   
                     sql:relation="Sales.SalesOrderDetail"  
                     sql:relationship="OrderOD" >  
           <xsd:complexType>  
              <xsd:attribute name="SalesOrderID"   type="xsd:integer" />  
              <xsd:attribute name="ProductID" type="xsd:integer" />  
             <xsd:attribute name="UnitPrice"  type="xsd:decimal" />  
             <xsd:attribute name="OrderQty"   type="xsd:integer" />  
             <xsd:attribute name="UnitPriceDiscount"   type="xsd:decimal" />  
  
           </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
        <xsd:attribute name="CustomerID"   type="xsd:string" />   
        <xsd:attribute name="SalesOrderID"  type="xsd:integer" />  
        <xsd:attribute name="OrderDate"  type="xsd:date" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 El siguiente diagrama de actualización usa este esquema XSD para agregar un nuevo registro de detalle de pedido (un  **\<OD >** elemento en el  **\<después >** bloque) para el pedido 43860. El atributo `mapping-schema` se usa para especificar el esquema de asignación en el diagrama de actualización.  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="SampleUpdateSchema.xml" >  
    <updg:before>  
       <Order SalesOrderID="43860" />  
    </updg:before>  
    <updg:after>  
      <Order SalesOrderID="43860" >  
           <OD ProductID="753" UnitPrice="$10.00"  
               Quantity="5" Discount="0.0" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Para probar el diagrama de actualización  
  
1.  Copie el código de esquema anterior y péguelo en un archivo de texto. Guarde el archivo como SampleUpdateSchema.xml.  
  
2.  Copie la plantilla de diagrama de actualización anterior y péguela en un archivo de texto. Guarde el archivo como SampleUpdategram.xml en el mismo directorio donde guardó SampleUpdateSchema.xml.  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (SampleUpdateSchema.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Éste es el esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"  
        xmlns:dt="urn:schemas-microsoft-com:datatypes"  
        xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  
<ElementType name="OD" sql:relation="Sales.SalesOrderDetail" >  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="ProductID" />  
    <AttributeType name="UnitPrice"  dt:type="fixed.14.4" />  
    <AttributeType name="OrderQty" />  
    <AttributeType name="UnitPriceDiscount" />  
  
    <attribute type="SalesOrderID" />  
    <attribute type="ProductID" />  
    <attribute type="UnitPrice" />  
    <attribute type="OrderQty" />  
    <attribute type="UnitPriceDiscount" />  
</ElementType>  
  
<ElementType name="Order" sql:relation="Sales.SalesOrderHeader" >  
    <AttributeType name="CustomerID" />  
    <AttributeType name="SalesOrderID" />  
    <AttributeType name="OrderDate" />  
  
    <attribute type="CustomerID" />  
    <attribute type="SalesOrderID" />  
    <attribute type="OrderDate" />  
    <element type="OD" >  
             <sql:relationship   
                   key-relation="Sales.SalesOrderHeader"  
                   key="SalesOrderID"  
                   foreign-key="SalesOrderID"  
                   foreign-relation="Sales.SalesOrderDetail" />  
    </element>  
</ElementType>  
</Schema>  
```  
  
### <a name="c-inserting-a-record-by-using-the-parent-child-relationship-and-inverse-annotation-specified-in-the-xsd-schema"></a>C. Insertar un registro mediante la relación de elementos primarios y secundarios y la anotación inversa especificada en el esquema XSD  
 En este ejemplo se muestra el modo en que la lógica del diagrama de actualización usa la relación de elementos primarios y secundarios especificada en el esquema XSD para procesar actualizaciones, y el modo en que se usa la anotación `inverse`. Para obtener más información sobre la `inverse` anotación, consulte [especificando el atributo SQL: Inverse en SQL: Relationship &#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-using/specifying-the-sql-inverse-attribute-on-sql-relationship-sqlxml-4-0.md).  
  
 En este ejemplo se da por supuesto que las tablas siguientes se encuentran en el **tempdb** base de datos:  
  
-   `Cust (CustomerID, CompanyName)`, donde `CustomerID` es la clave principal  
  
-   `Ord (OrderID, CustomerID)`, donde `CustomerID` es una clave externa que hace referencia a la clave principal `CustomerID` de la tabla `Cust`.  
  
 El diagrama de actualización usa el esquema XSD siguiente para insertar registros en las tablas Cust y Ord:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
       <sql:relationship name="OrdCust" inverse="true"  
                  parent="Ord"  
                  parent-key="CustomerID"  
                  child-key="CustomerID"  
                  child="Cust"/>  
  </xsd:appinfo>  
</xsd:annotation>  
  
<xsd:element name="Order" sql:relation="Ord">  
  <xsd:complexType>  
    <xsd:sequence>  
      <xsd:element ref="Customer" sql:relationship="OrdCust"/>  
    </xsd:sequence>  
    <xsd:attribute name="OrderID"   type="xsd:int"/>  
    <xsd:attribute name="CustomerID" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:element>  
  
<xsd:element name="Customer" sql:relation="Cust">  
  <xsd:complexType>  
     <xsd:attribute name="CustomerID"  type="xsd:string"/>  
    <xsd:attribute name="CompanyName" type="xsd:string"/>  
  </xsd:complexType>  
</xsd:element>  
  
</xsd:schema>  
```  
  
 El esquema XSD en este ejemplo tiene  **\<cliente >** y  **\<orden >** elementos y especifica una relación de elementos primarios y secundarios entre los dos elementos. Identifica  **\<orden >** como el elemento primario y  **\<cliente >** como el elemento secundario.  
  
 La lógica de procesamiento del diagrama de actualización usa la información de la relación de elementos primarios y secundarios para determinar el orden en que los registros se insertan en las tablas. En este ejemplo, la lógica del diagrama de actualización en primer lugar intenta insertar un registro en la tabla Ord (porque  **\<orden >** es el elemento primario) y, a continuación, intenta insertar un registro en la tabla Cust (porque  **\<Cliente >** es el elemento secundario). Sin embargo, debido a la información de clave principal y clave externa incluida en el esquema de tabla de base de datos, esta operación de inserción provoca una infracción de clave externa en la base de datos y se produce un error en la operación de inserción.  
  
 Para indicar a la lógica del diagrama de actualización para invertir la relación de elementos primarios y secundarios durante la operación de actualización, el `inverse` anotación se especifica en el  **\<relación >** elemento. Como resultado, los registros se agregan primero en la tabla Cust y después en la tabla Ord, y la operación se realiza correctamente.  
  
 El diagrama de actualización siguiente inserta un pedido (OrderID=2) en la tabla Ord y un cliente (CustomerID='AAAAA) en la tabla Cust mediante el esquema XSD especificado:  
  
```  
<ROOT xmlns:updg="urn:schemas-microsoft-com:xml-updategram">  
  <updg:sync mapping-schema="SampleUpdateSchema.xml" >  
    <updg:before/>  
    <updg:after>  
      <Order OrderID="2" CustomerID="AAAAA" >  
        <Customer CustomerID="AAAAA" CompanyName="AAAAA Company" />  
      </Order>  
    </updg:after>  
  </updg:sync>  
</ROOT>  
```  
  
##### <a name="to-test-the-updategram"></a>Para probar el diagrama de actualización  
  
1.  Cree estas tablas en el **tempdb** base de datos:  
  
    ```  
    USE tempdb  
    CREATE TABLE Cust(CustomerID varchar(5) primary key,   
                      CompanyName varchar(20))  
    GO  
    CREATE TABLE Ord (OrderID int primary key,   
                      CustomerID varchar(5) references Cust(CustomerID))  
    GO  
    ```  
  
2.  Copie el código de esquema anterior y péguelo en un archivo de texto. Guarde el archivo como SampleUpdateSchema.xml.  
  
3.  Copie la plantilla de diagrama de actualización anterior y péguela en un archivo de texto. Guarde el archivo como SampleUpdategram.xml en el mismo directorio donde guardó SampleUpdateSchema.xml.  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (SampleUpdateSchema.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\SampleUpdateSchema.xml"  
    ```  
  
4.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="see-also"></a>Vea también  
 [Consideraciones de seguridad de updategram &#40;SQLXML 4.0&#41;](../security/updategram-security-considerations-sqlxml-4-0.md)  
  
  