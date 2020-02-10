---
title: 'SQL: Overflow-Field (SQLXML 4,0) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- overflow-field annotation
- unconsumed data
- overflow data [SQLXML]
- sql:overflow-field
ms.assetid: f005182b-6151-432d-ab22-3bc025742cd3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 594ebdbad3968ba2efe7e255b28379194d2fb77f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66013469"
---
# <a name="sqloverflow-field-sqlxml-40"></a>sql:overflow-field (SQLXML 4.0)
  En un esquema, puede identificar una columna como una columna de desbordamiento para que reciba todos los datos no consumidos del documento XML. Esta columna se especifica en el esquema utilizando la anotación `sql:overflow-field`. Es posible tener varias columnas de desbordamiento.  
  
 Siempre que un nodo XML (elemento o atributo) para el que hay una anotación `sql:overflow-field` definida entra en el ámbito, la columna de desbordamiento se activa y recibe los datos no consumidos. Cuando el nodo sale del ámbito, la columna de desbordamiento deja de estar activa y Carga masiva XML activa el campo de desbordamiento anterior (si existe).  
  
 Al almacenar datos en la columna de desbordamiento, Carga masiva XML también almacena las etiquetas de cierre y apertura del elemento primario para el que se define `sql:overflow-field`.  
  
 Por ejemplo, en el esquema siguiente se describen los ** \<** ** \<elementos>** y>de los clientes de CustOrder. Cada uno de estos elementos identifica una columna de desbordamiento:  
  
```  
<?xml version="1.0" ?>  
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
 <xsd:element name="ROOT" sql:is-constant="1">  
  <xsd:complexType>  
    <xsd:sequence>   
      <xsd:element name="Customers"   
                   sql:relation="Cust"  
                   sql:overflow-field="OverflowColumn">  
        <xsd:complexType>  
             <xsd:sequence>   
             <xsd:element name="CustomerID" type="xsd:integer"/>  
             <xsd:element name="CompanyName"  type="xsd:string"/>  
             <xsd:element name="City" type="xsd:string"/>  
             <xsd:element name="Order"  
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder"  
                          sql:overflow-field="OverflowColumn">  
               <xsd:complexType>  
                 <xsd:attribute name="OrderID"/>  
                 <xsd:attribute name="CustomerID"/>  
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
  
 En el esquema, el ** \<elemento Customer>** se asigna a la tabla Cust y el ** \<elemento Order>** se asigna a la tabla CustOrder.  
  
 Los ** \<elementos>cliente** y ** \<pedido>** identifican una columna de desbordamiento. Por lo tanto, la carga masiva XML guarda todos los elementos secundarios y atributos no consumidos del elemento ** \<Customer>** en la columna Overflow de la tabla Cust, y todos los elementos secundarios y atributos no consumidos del elemento ** \<Order>** de la columna Overflow de la tabla CustOrder.  
  
### <a name="to-test-a-working-sample"></a>Para probar un ejemplo funcional  
  
1.  Guarde el esquema que se proporciona en este ejemplo como SampleSchema.xml.  
  
2.  Cree estas tablas:  
  
    ```  
    CREATE TABLE Cust (  
              CustomerID     int         PRIMARY KEY,  
              CompanyName    varchar(20) NOT NULL,  
              City           varchar(20) DEFAULT 'Seattle',  
              OverflowColumn nvarchar(200))  
    GO  
    CREATE TABLE CustOrder (  
              OrderID        int         PRIMARY KEY,  
              CustomerID     int         FOREIGN KEY REFERENCES  
                                              Cust(CustomerID),  
              OverflowColumn nvarchar(200))  
    GO  
    ```  
  
3.  Guarde los siguientes datos XML de ejemplo como SampleXMLData.xml:  
  
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
       <City><![CDATA[LA]]> </City>  
       <xyz><address>111 Maple, Seattle</address></xyz>     
       <Order OrderID="3" />  
     </Customers>  
       <Customers>  
       <CustomerID>1113</CustomerID>  
       <CompanyName>Victuailles en stock</CompanyName>  
       <Order OrderID="4" />  
      </Customers>  
    </ROOT>  
    ```  
  
4.  Para ejecutar Carga masiva XML, guarde y ejecute este ejemplo de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic Scripting Edition (VBScript) como Sample.vbs:  
  
    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
  
