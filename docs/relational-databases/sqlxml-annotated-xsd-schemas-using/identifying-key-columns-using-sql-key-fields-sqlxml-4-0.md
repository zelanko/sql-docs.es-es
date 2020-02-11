---
title: 'Identificar columnas de clave mediante SQL: Key-Fields (SQLXML)'
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- nesting XML results
- proper nesting in results [SQLXML]
- sql:key-fields
- XSD schemas [SQLXML], key columns
- identifying key columns [SQLXML]
- annotated XSD schemas, key columns
- key columns [SQLXML]
- relationships [SQLXML], key columns
- hierarchical relationships [SQLXML]
- key-fields annotation
ms.assetid: 1a5ad868-8602-45c4-913d-6fbb837eebb0
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 71d42f9f3f819dc12964ea0f13de92dfc8db5663
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "75257393"
---
# <a name="identifying-key-columns-using-sqlkey-fields-sqlxml-40"></a>Identificar columnas de clave mediante sql:key-fields (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Cuando se especifica una consulta XPath en un esquema XSD, la información de claves resulta necesaria en la mayoría de los casos para obtener un anidamiento correcto en el resultado. Especificar la anotación **SQL: Key-Fields** es una manera de asegurarse de que se genera la jerarquía adecuada.  
  
> [!NOTE]  
>  Para garantizar el anidamiento correcto, se recomienda especificar **SQL: Key-Fields** para los elementos que se asignan a las tablas. El código XML generado distingue la ordenación del conjunto de resultados subyacente. Si no se especifica **SQL: Key-Fields** , es posible que no se haya formado correctamente el XML generado.  
  
 El valor de **SQL: Key-Fields** identifica las columnas que identifican de forma única las filas de la relación. Si es necesaria más de una columna para identificar de forma única una fila, los valores de columna se delimitan mediante espacios.  
  
 Debe utilizar la anotación **SQL: Key-Fields** cuando un elemento contiene un ** \<>SQL: Relationship** definido entre el elemento y un elemento secundario, pero no proporciona la clave principal de la tabla que se especifica en el elemento primario.  
  
## <a name="examples"></a>Ejemplos  
 Para crear muestras funcionales mediante los ejemplos siguientes, debe cumplir determinados requisitos. Para obtener más información, vea [Requirements for Running SQLXML examples](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-producing-the-appropriate-nesting-when-sqlrelationship-does-not-provide-sufficient-information"></a>A. Generar el anidamiento adecuado cuando \<SQL: Relationship> no proporciona información suficiente  
 Este ejemplo muestra dónde se debe especificar **SQL: Key-Fields** .  
  
 Fíjese en el siguiente esquema. El esquema especifica una jerarquía entre el ** \<orden>** y ** \<** los elementos de>de cliente en los que el ** \<elemento Order>** es el elemento primario y el ** \<elemento Customer>** es un elemento secundario.  
  
 La ** \<etiqueta SQL: Relationship>** se usa para especificar la relación de elementos primarios y secundarios. Identifica CustomerID en la tabla Sales.SalesOrderHeader como la clave primaria que hace referencia a la clave secundaria CustomerID en la tabla Sales.Customer. La información proporcionada en ** \<SQL: Relationship>** no es suficiente para identificar de forma única las filas de la tabla primaria (sales. SalesOrderHeader). Por lo tanto, sin la anotación **SQL: Key-Fields** , la jerarquía que se genera es inexacta.  
  
 Con **SQL: Key-Fields** especificado en ** \<el orden>**, la anotación identifica de forma única las filas de la tabla primaria (sales. SalesOrderHeader) y sus elementos secundarios aparecen debajo de su elemento primario.  
  
 Éste es el esquema:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="OrdCust"  
        parent="Sales.SalesOrderHeader"  
        parent-key="CustomerID"  
        child="Sales.Customer"  
        child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"   
               sql:key-fields="SalesOrderID">  
   <xsd:complexType>  
     <xsd:sequence>  
     <xsd:element name="Customer" sql:relation="Sales.Customer"   
                       sql:relationship="OrdCust"  >  
       <xsd:complexType>  
         <xsd:attribute name="CustID" sql:field="CustomerID" />  
         <xsd:attribute name="SoldBy" sql:field="SalesPersonID" />  
       </xsd:complexType>  
     </xsd:element>  
     </xsd:sequence>  
     <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
     <xsd:attribute name= "CustomerID" type="xsd:string" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-create-a-working-sample-of-this-schema"></a>Para crear un ejemplo funcional de este esquema  
  
1.  Copie el código de esquema anterior y péguelo en un archivo de texto. Guarde el archivo como KeyFields1.xml.  
  
2.  Copie la plantilla siguiente y péguela en un archivo de texto. Guarde el archivo como KeyFields1T.xml en el mismo directorio donde guardó KeyFields1.xml. La consulta XPath de la plantilla devuelve todos los ** \<elementos de order>** con un CustomerID de menos de 3.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
        <sql:xpath-query mapping-schema="KeyFields1.xml">  
            /Order[@CustomerID < 3]  
        </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (KeyFields1.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\MyDir\KeyFields1.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  

     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Éste es el conjunto de resultados parciales:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
    <Order SalesOrderID="43860" CustomerID="1">  
       <Customer CustID="1" SoldBy="280"/>  
    </Order>  
    <Order SalesOrderID="44501" CustomerID="1">  
       <Customer CustID="1" SoldBy="280"/>  
    </Order>  
    <Order SalesOrderID="45283" CustomerID="1">  
       <Customer CustID="1" SoldBy="280"/>  
    </Order>  
    .....  
</ROOT>  
```  
  
### <a name="b-specifying-sqlkey-fields-to-produce-proper-nesting-in-the-result"></a>B. Especificar sql:key-fields para generar un anidamiento correcto del resultado  
 En el esquema siguiente, no se ha especificado ninguna jerarquía mediante ** \<SQL: Relationship>**. El esquema todavía requiere la especificación de la anotación **SQL: Key-Fields** para identificar de forma exclusiva a los empleados en la tabla humanresources. Employee.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="HumanResources.Employee" sql:key-fields="EmployeeID" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Title">  
          <xsd:complexType>  
            <xsd:simpleContent>  
              <xsd:extension base="xsd:string">  
                 <xsd:attribute name="EmployeeID" type="xsd:integer" />  
              </xsd:extension>  
            </xsd:simpleContent>  
          </xsd:complexType>  
        </xsd:element>  
     </xsd:sequence>  
   </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-create-a-working-sample-of-this-schema"></a>Para crear un ejemplo funcional de este esquema  
  
1.  Copie el código de esquema anterior y péguelo en un archivo de texto. Guarde el archivo como KeyFields2.xml.  
  
2.  Copie la plantilla siguiente y péguela en un archivo de texto. Guarde el archivo como KeyFields2T.xml en el mismo directorio donde guardó KeyFields2.xml. La consulta XPath de la plantilla devuelve todos los elementos ** \<humanresources. Employee>** :  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="KeyFields2.xml">  
        /HumanResources.Employee  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     La ruta de acceso al directorio especificada para el esquema de asignación (KeyFields2.xml) es relativa al directorio donde se guarda la plantilla. También puede especificarse una ruta de acceso absoluta como, por ejemplo:  
  
    ```  
    mapping-schema="C:\MyDir\KeyFields2.xml"  
    ```  
  
3.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar la plantilla.  
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 El resultado es el siguiente:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <HumanResources.Employee>  
    <Title EmployeeID="1">Production Technician - WC60</Title>   
  </HumanResources.Employee>  
  <HumanResources.Employee>  
    <Title EmployeeID="2">Marketing Assistant</Title>   
  </HumanResources.Employee>  
  <HumanResources.Employee>  
    <Title EmployeeID="3">Engineering Manager</Title>   
  </HumanResources.Employee>  
  ...  
</ROOT>  
```  
  
  
