---
title: 'SQL: Relationship y la regla de ordenación de claves (SQLXML)'
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sql:relationship
- key ordering rules [SQLXML]
- relationship annotation
ms.assetid: 914cb152-09f5-4b08-b35d-71940e4e9986
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6c04b14f474e2afc0e6feb18eaa0bd321fdbb5e0
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2019
ms.locfileid: "75246772"
---
# <a name="annotation-interpretation---sqlrelationship-and-key-ordering-rule"></a>Interpretación de anotaciones: sql:relationship y regla de ordenación de claves
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Dado que la carga masiva XML genera registros cuando sus nodos entran en el ámbito y envía esos registros a Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando sus nodos salen del ámbito, los datos del registro deben estar presentes en el ámbito del nodo.  
  
 Considere el siguiente esquema XSD, en el que la relación de uno a varios entre ** \<los elementos>cliente** y ** \<>de pedido** (un cliente puede realizar muchos pedidos) se especifica mediante el ** \<elemento SQL: Relationship>** :  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"<>   
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
</xsd:schema>  
```  
  
 Cuando el ** \<cliente>** nodo de elemento entra en el ámbito, la carga masiva XML genera un registro de cliente. Este registro permanece hasta que la carga masiva XML Lee ** \</Customer>**. Al procesar el ** \<orden de>** nodo de elemento, la carga masiva XML usa ** \<SQL: Relationship>** para obtener el valor de la columna de clave externa CustomerID de la tabla CustOrder del elemento primario ** \<Customer>** , porque el ** \<elemento Order>** no especifica el atributo **CustomerID** . Esto significa que, al definir el ** \<elemento Customer>** , debe especificar el atributo **CustomerID** en el esquema antes de especificar ** \<SQL: Relationship>**. De lo contrario, cuando un ** \<pedido>** elemento entra en el ámbito, la carga masiva XML genera un registro para la tabla CustOrder y, cuando la carga masiva XML alcanza la etiqueta de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ** \<finalización/Order>** , envía el registro a sin el valor de columna de clave externa CustomerID.  
  
 Guarde el esquema que se proporciona en este ejemplo como SampleSchema.xml.  
  
### <a name="to-test-a-working-sample"></a>Para probar un ejemplo funcional  
  
1.  Cree estas tablas:  
  
    ```  
    CREATE TABLE Cust (  
                  CustomerID     int          PRIMARY KEY,  
               CompanyName    varchar(20)  NOT NULL,  
                  City           varchar(20)  DEFAULT 'Seattle')  
    GO  
    CREATE TABLE CustOrder (  
                  OrderID        varchar(10) PRIMARY KEY,  
               CustomerID     int         FOREIGN KEY REFERENCES                                          Cust(CustomerID))  
    GO  
    ```  
  
2.  Guarde los siguientes datos de ejemplo como SampleXMLData.xml:  
  
    ```  
    <ROOT>    
      <Customers>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City>NY</City>  
        <Order OrderID="1" />  
        <Order OrderID="2" />  
        <CustomerID>1111</CustomerID>  
      </Customers>  
      <Customers>  
        <CompanyName>Toms Spezialitten</CompanyName>  
         <City>LA</City>    
        <Order OrderID="3" />  
        <CustomerID>1112</CustomerID>  
      </Customers>  
      <Customers>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
        <CustomerID>1113</CustomerID>  
      </Customers>  
    </ROOT>  
    ```  
  
3.  Para ejecutar la carga masiva XML, guarde y ejecute el siguiente ejemplo de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic Scripting Edition (VBScript) como MySample.vbs:  

    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Transaction=True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
     Como resultado, la carga masiva XML inserta un valor NULL en la columna de clave externa CustomerID de la tabla CustOrder. Si revisa los datos de ejemplo XML para que el ** \<elemento secundario CustomerID>** aparezca antes que el ** \<elemento secundario Order>** , obtendrá el resultado esperado: la carga masiva XML inserta el valor de clave externa especificado en la columna.  
  
 Éste es el esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >   
   <ElementType name="CustomerID"  />  
   <ElementType name="CompanyName" />  
   <ElementType name="City"        />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust" >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
                 <sql:relationship  
                        key-relation    ="Cust"  
                        key             ="CustomerID"  
                        foreign-key     ="CustomerID"  
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
  
  
