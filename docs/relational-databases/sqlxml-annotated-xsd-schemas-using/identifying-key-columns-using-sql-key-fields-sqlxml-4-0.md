---
title: 'Identificar columnas de clave mediante SQL: key-fields (SQLXML 4.0) | Documentos de Microsoft'
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ac42ee657dd46f070eccf5d63ae9a454c3306e95
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2018
---
# <a name="identifying-key-columns-using-sqlkey-fields-sqlxml-40"></a>Identificar columnas de clave mediante sql:key-fields (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
Cuando se especifica una consulta XPath en un esquema XSD, la información de claves resulta necesaria en la mayoría de los casos para obtener un anidamiento correcto en el resultado. Especificar el **SQL: Key-campos** anotación es una manera de asegurarse de que se genera la jerarquía correcta.  
  
> [!NOTE]  
>  Para garantizar un anidamiento correcto, se recomienda especificar **SQL: Key-campos** para los elementos que se asignan a las tablas. El código XML generado distingue la ordenación del conjunto de resultados subyacente. Si **SQL: Key-campos** no se especifica, el XML generado no se puede formar correctamente.  
  
 El valor de **SQL: Key-campos** identifica las columnas que identifican de forma única las filas de la relación. Si es necesaria más de una columna para identificar de forma única una fila, los valores de columna se delimitan mediante espacios.  
  
 Debe utilizar el **SQL: Key-campos** anotación cuando un elemento contiene una  **\<SQL: Relationship >** que se define entre el elemento y un elemento secundario, pero no proporciona la clave principal de la tabla especificada en el elemento primario.  
  
## <a name="examples"></a>Ejemplos  
 Para crear muestras funcionales mediante los ejemplos siguientes, debe cumplir determinados requisitos. Para obtener más información, consulte [requisitos para ejecutar los ejemplos de SQLXML](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-producing-the-appropriate-nesting-when-sqlrelationship-does-not-provide-sufficient-information"></a>A. Crear un anidamiento correcto cuando \<SQL: Relationship > no proporciona suficiente información  
 Este ejemplo muestra dónde **SQL: Key-campos** debe especificarse.  
  
 Fíjese en el siguiente esquema. El esquema especifica una jerarquía entre el  **\<orden >** y  **\<cliente >** elementos en los que la  **\<orden >**es el elemento primario y el  **\<cliente >** es un elemento secundario.  
  
 El  **\<SQL: Relationship >** etiqueta se utiliza para especificar la relación de elementos primarios y secundarios. Identifica CustomerID en la tabla Sales.SalesOrderHeader como la clave primaria que hace referencia a la clave secundaria CustomerID en la tabla Sales.Customer. La información proporcionada en  **\<SQL: Relationship >** no es suficiente para identificar filas de la tabla primaria (Sales.SalesOrderHeader). Por lo tanto, sin la **SQL: Key-campos** anotación, la jerarquía que se genera es inexacta.  
  
 Con **SQL: Key-campos** especificado en  **\<orden >**, la anotación identifica de forma única las filas en el elemento primario (tabla Sales.SalesOrderHeader) y sus elementos secundarios aparecen debajo de su elemento primario.  
  
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
  
2.  Copie la plantilla siguiente y péguela en un archivo de texto. Guarde el archivo como KeyFields1T.xml en el mismo directorio donde guardó KeyFields1.xml. La consulta XPath en la plantilla devuelve todos los  **\<orden >** elementos cuyo valor CustomerID es menor que 3.  
  
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
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas SQLXML](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
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
 En el siguiente esquema, no hay ninguna jerarquía especificada mediante  **\<SQL: Relationship >**. El esquema todavía requiere especificar la **SQL: Key-campos** anotación para identificar los empleados en la tabla HumanResources.Employee.  
  
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
  
2.  Copie la plantilla siguiente y péguela en un archivo de texto. Guarde el archivo como KeyFields2T.xml en el mismo directorio donde guardó KeyFields2.xml. La consulta XPath en la plantilla devuelve todos los  **\<HumanResources.Employee >** elementos:  
  
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
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas SQLXML](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
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
  
  
