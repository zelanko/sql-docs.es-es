---
title: Ejemplos de DiffGram (SQLXML)
description: Vea ejemplos de DiffGrams en SQLXML 4,0 que realizan operaciones de inserción, actualización y eliminación en una base de datos.
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], examples
- examples [SQLXML], DiffGram
- diffgr:parentID
- parentID annotation
ms.assetid: fc148583-dfd3-4efb-a413-f47b150b0975
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c4681c4babe25ec9c683d78e583ddd2c1a4d91fe
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97415354"
---
# <a name="diffgram-examples-sqlxml-40"></a>Ejemplos de DiffGram (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Los ejemplos de este tema incluyen de una serie de DiffGram que realizan operaciones de inserción, actualización y eliminación en la base de datos. Antes de usar los ejemplos, tenga en cuenta lo siguiente:  
  
-   Los ejemplos usan dos tablas (Cust y Ord) que deberá crear si desea probar los ejemplos de DiffGram:  
  
    ```  
    Cust(CustomerID, CompanyName, ContactName)  
    Ord(OrderID, CustomerID)  
    ```  
  
-   La mayoría de los ejemplos de este tema usan el siguiente esquema XSD:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
    <xsd:annotation>  
      <xsd:documentation>  
        Diffgram Customers/Orders Schema.  
      </xsd:documentation>  
      <xsd:appinfo>  
           <sql:relationship name="CustomersOrders"   
                      parent="Cust"  
                      parent-key="CustomerID"  
                      child-key="CustomerID"  
                      child="Ord"/>  
      </xsd:appinfo>  
    </xsd:annotation>  
  
    <xsd:element name="Customer" sql:relation="Cust">  
      <xsd:complexType>  
        <xsd:sequence>  
          <xsd:element name="CompanyName"    type="xsd:string"/>  
          <xsd:element name="ContactName"    type="xsd:string"/>  
           <xsd:element name="Order" sql:relation="Ord" sql:relationship="CustomersOrders">  
            <xsd:complexType>  
              <xsd:attribute name="OrderID" type="xsd:int" sql:field="OrderID"/>  
              <xsd:attribute name="CustomerID" type="xsd:string"/>  
            </xsd:complexType>  
          </xsd:element>  
        </xsd:sequence>  
        <xsd:attribute name="CustomerID" type="xsd:string" sql:field="CustomerID"/>  
      </xsd:complexType>  
    </xsd:element>  
  
    </xsd:schema>     
    ```  
  
     Guarde este esquema como DiffGramSchema.xml en la misma carpeta donde haya guardado los demás archivos que se utilizan en los ejemplos.  
  
## <a name="a-deleting-a-record-by-using-a-diffgram"></a>A. Eliminar un registro mediante un DiffGram  
 El DiffGram de este ejemplo elimina un registro de cliente (cuyo CustomerID es ALFKI) de la tabla Cust y elimina el registro de pedido correspondiente (cuyo OrderID es 1) de la tabla Ord.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
           xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
           xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance/>  
  
    <diffgr:before>  
        <Order diffgr:id="Order1"   
               msdata:rowOrder="0"   
               CustomerID="ALFKI"   
               OrderID="1"/>  
        <Customer diffgr:id="Customer1"   
                  msdata:rowOrder="0"   
                  CustomerID="ALFKI">  
           <CompanyName>Alfreds Futterkiste</CompanyName>  
           <ContactName>Maria Anders</ContactName>  
        </Customer>  
    </diffgr:before>  
    <msdata:errors/>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 En el **\<before>** bloque, hay un **\<Order>** elemento (**diffgr: ID = "Order1"**) y un **\<Customer>** elemento (**diffgr: ID = "Customer1"**). Estos elementos representan registros existentes en la base de datos. El **\<DataInstance>** elemento no tiene los registros correspondientes (con el mismo **diffgr: ID**). Esto indica una operación de eliminación.  
  
#### <a name="to-test-the-diffgram"></a>Para probar el DiffGram:  
  
1.  Cree estas tablas en la base de datos **tempdb** .  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  Agregue estos datos de ejemplo:  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  Copie el DiffGram anterior y péguelo en un archivo de texto. Guarde el archivo como MyDiffGram.xml en la misma carpeta utilizada en el paso anterior.  
  
4.  Copie el DiffGramSchema proporcionado anteriormente en este tema y péguelo en un archivo de texto. Guarde el archivo como DiffGramSchema.xml.  
  
5.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar el DiffGram.  
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="b-inserting-a-record-by-using-a-diffgram"></a>B. Insertar un registro mediante un DiffGram  
 En este ejemplo, el DiffGram inserta un registro en la tabla Cust y otro registro en la tabla Ord.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql"   
      sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
          xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
          xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
       <Customer diffgr:id="Customer1" msdata:rowOrder="0"    
                 diffgr:hasChanges="inserted" CustomerID="ALFKI">  
        <CompanyName>C3Company</CompanyName>  
        <ContactName>C3Contact</ContactName>  
        <Order diffgr:id="Order1"   
               msdata:rowOrder="0"  
               diffgr:hasChanges="inserted"   
               CustomerID="ALFKI" OrderID="1"/>  
      </Customer>  
    </DataInstance>  
  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 En este DiffGram **\<before>** , no se especifica el bloque (no se identificó ningún registro de base de datos existente). Hay dos instancias de registro (identificadas por **\<Customer>** los **\<Order>** elementos y del **\<DataInstance>** bloque) que se asignan a las tablas CUST y Ord, respectivamente. Ambos elementos especifican el atributo **diffgr: hasChanges** (**hasChanges = "Inserted"**). Esto indica una operación de inserción. En este DiffGram, si se especifica **hasChanges = "Modified"**, se indica que desea modificar un registro que no existe, lo que genera un error.  
  
#### <a name="to-test-the-diffgram"></a>Para probar el DiffGram:  
  
1.  Cree estas tablas en la base de datos **tempdb** .  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  Agregue estos datos de ejemplo:  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  Copie el DiffGram anterior y péguelo en un archivo de texto. Guarde el archivo como MyDiffGram.xml en la misma carpeta utilizada en el paso anterior.  
  
4.  Copie el DiffGramSchema proporcionado anteriormente en este tema y péguelo en un archivo de texto. Guarde el archivo como DiffGramSchema.xml.  
  
5.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar el DiffGram.  
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="c-updating-an-existing-record-by-using-a-diffgram"></a>C. Actualizar un registro existente mediante un DiffGram  
 En este ejemplo, el DiffGram actualiza la información del cliente ALFKI (CompanyName y ContactName).  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
           xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
           xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
      <Customer diffgr:id="Customer1"   
                msdata:rowOrder="0" diffgr:hasChanges="modified"   
                CustomerID="ALFKI">  
          <CompanyName>Bottom Dollar Markets</CompanyName>  
          <ContactName>Antonio Moreno</ContactName>  
      </Customer>  
    </DataInstance>  
  
    <diffgr:before>  
     <Customer diffgr:id="Customer1"   
               msdata:rowOrder="0"   
               CustomerID="ALFKI">  
        <CompanyName>Alfreds Futterkiste</CompanyName>  
        <ContactName>Maria Anders</ContactName>  
      </Customer>  
    </diffgr:before>  
  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 El **\<before>** bloque incluye un **\<Customer>** elemento (**diffgr: ID = "Customer1"**). El **\<DataInstance>** bloque incluye el **\<Customer>** elemento correspondiente con el mismo **identificador**. El **\<customer>** elemento de **\<NewDataSet>** también especifica **diffgr: hasChanges = "Modified"**. Esto indica una operación de actualización y el registro del cliente en la tabla **Cust** se actualiza en consecuencia. Tenga en cuenta que si no se especifica el atributo **diffgr: hasChanges** , la lógica de procesamiento de DiffGram omite este elemento y no se realiza ninguna actualización.  
  
#### <a name="to-test-the-diffgram"></a>Para probar el DiffGram:  
  
1.  Cree estas tablas en la base de datos **tempdb** .  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  Agregue estos datos de ejemplo:  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  Copie el DiffGram anterior y péguelo en un archivo de texto. Guarde el archivo como MyDiffGram.xml en la misma carpeta utilizada en el paso anterior.  
  
4.  Copie el DiffGramSchema proporcionado anteriormente en este tema y péguelo en un archivo de texto. Guarde el archivo como DiffGramSchema.xml.  
  
5.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar el DiffGram.  
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="d-inserting-updating-and-deleting-records-by-using-a-diffgram"></a>D. Insertar, actualizar y eliminar registros mediante un DiffGram  
 En este ejemplo, se usa un DiffGram relativamente complejo para realizar operaciones de inserción, actualización y eliminación.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
         xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
         xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
      <Customer diffgr:id="Customer2" msdata:rowOrder="1"   
                diffgr:hasChanges="modified"   
                CustomerID="ANATR">  
          <CompanyName>Bottom Dollar Markets</CompanyName>  
          <ContactName>Elizabeth Lincoln</ContactName>  
          <Order diffgr:id="Order2" msdata:rowOrder="1"   
               msdata:hiddenCustomerID="ANATR"   
               CustomerID="ANATR" OrderID="2"/>  
      </Customer>  
  
      <Customer diffgr:id="Customer3" msdata:rowOrder="2"   
                CustomerID="ANTON">  
         <CompanyName>Chop-suey Chinese</CompanyName>  
         <ContactName>Yang Wang</ContactName>  
         <Order diffgr:id="Order3" msdata:rowOrder="2"   
               msdata:hiddenCustomerID="ANTON"   
               CustomerID="ANTON" OrderID="3"/>  
      </Customer>  
      <Customer diffgr:id="Customer4" msdata:rowOrder="3"   
                diffgr:hasChanges="inserted"   
                CustomerID="AROUT">  
         <CompanyName>Around the Horn</CompanyName>  
         <ContactName>Thomas Hardy</ContactName>  
         <Order diffgr:id="Order4" msdata:rowOrder="3"   
                diffgr:hasChanges="inserted"   
                msdata:hiddenCustomerID="AROUT"   
               CustomerID="AROUT" OrderID="4"/>  
      </Customer>  
    </DataInstance>  
    <diffgr:before>  
      <Order diffgr:id="Order1" msdata:rowOrder="0"   
             msdata:hiddenCustomerID="ALFKI"   
             CustomerID="ALFKI" OrderID="1"/>  
      <Customer diffgr:id="Customer1" msdata:rowOrder="0"   
                CustomerID="ALFKI">  
        <CompanyName>Alfreds Futterkiste</CompanyName>  
        <ContactName>Maria Anders</ContactName>  
      </Customer>  
      <Customer diffgr:id="Customer2" msdata:rowOrder="1"   
                CustomerID="ANATR">  
        <CompanyName>Ana Trujillo Emparedados y helados</CompanyName>  
        <ContactName>Ana Trujillo</ContactName>  
      </Customer>  
    </diffgr:before>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 La lógica de DiffGram procesa este DiffGram del modo siguiente:  
  
-   De acuerdo con la lógica de procesamiento de DiffGram, todos los elementos de nivel superior del **\<before>** bloque se asignan a las tablas correspondientes, tal y como se describe en el esquema de asignación.  
  
-   El **\<before>** bloque tiene un **\<Order>** elemento (**dffgr: ID = "Order1"**) y un **\<Customer>** elemento (**diffgr: ID = "Customer1"**) para los que no hay ningún elemento correspondiente en el **\<DataInstance>** bloque (con el mismo identificador). Esto indica una operación de eliminación y los registros se eliminan de las tablas Cust y Ord.  
  
-   El **\<before>** bloque tiene un **\<Customer>** elemento (**diffgr: ID = "Customer2"**) para el que hay un **\<Customer>** elemento correspondiente en el **\<DataInstance>** bloque (con el mismo identificador). El elemento del **\<DataInstance>** bloque especifica **diffgr: hasChanges = "Modified"**. Se trata de una operación de actualización en la que para Customer ANATR, la información de CompanyName y ContactName se actualiza en la tabla Cust con los valores que se especifican en el **\<DataInstance>** bloque.  
  
-   El **\<DataInstance>** bloque tiene un **\<Customer>** elemento (**diffgr: ID = "Customer3"**) y un **\<Order>** elemento (**diffgr: ID = "Order3"**). Ninguno de estos elementos especifica el atributo **diffgr: hasChanges** . Por lo tanto, la lógica de procesamiento de DiffGram omite estos elementos.  
  
-   El **\<DataInstance>** bloque tiene un **\<Customer>** elemento (**diffgr: ID = "Customer4"**) y un **\<Order>** elemento (**diffgr: ID = "Order4"**) para los que no hay elementos correspondientes en el \<before> bloque. Estos elementos del **\<DataInstance>** bloque especifican **diffgr: hasChanges = "Inserted"**. Por lo tanto, se agrega un nuevo registro a la tabla Cust y a la tabla Ord.  
  
#### <a name="to-test-the-diffgram"></a>Para probar el DiffGram:  
  
1.  Cree las tablas siguientes en la base de datos **tempdb** .  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  Agregue estos datos de ejemplo:  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  Copie el DiffGram anterior y péguelo en un archivo de texto. Guarde el archivo como MyDiffGram.xml en la misma carpeta utilizada en el paso anterior.  
  
4.  Copie el DiffGramSchema proporcionado anteriormente en este tema y péguelo en un archivo de texto. Guarde el archivo como DiffGramSchema.xml.  
  
5.  Cree y use el script de prueba SQLXML 4.0 (Sqlxml4test.vbs) para ejecutar el DiffGram.  
  
     Para obtener más información, vea [usar ado para ejecutar consultas SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="e-applying-updates-by-using-a-diffgram-with-the-diffgrparentid-annotation"></a>E. Aplicar actualizaciones mediante un DiffGram con la anotación diffgr:parentID  
 En este ejemplo se muestra cómo se utiliza la anotación **parentId** que se especifica en el **\<before>** bloque del DiffGram para aplicar las actualizaciones.  
  
```  
<NewDataSet />  
<diffgr:before>  
   <Order diffgr:id="Order1" msdata:rowOrder="0" OrderID="2" />  
   <Order diffgr:id="Order3" msdata:rowOrder="2" OrderID="4" />  
  
   <OrderDetail diffgr:id="OrderDetail1"   
                diffgr:parentId="Order1"   
                msdata:rowOrder="0"   
                ProductID="13"   
                OrderID="2" />  
   <OrderDetail diffgr:id="OrderDetail3"   
                diffgr:parentId="Order3"  
                ProductID="77"  
                OrderID="4"/>  
</diffgr:before>  
</diffgr:diffgram>  
```  
  
 Este DiffGram especifica una operación de eliminación porque solo hay un **\<before>** bloque. En el DiffGram, la anotación **parentId** se usa para especificar una relación de elementos primarios y secundarios entre los pedidos y los detalles del pedido. Cuando SQLXML elimina los registros, elimina los registros de la tabla secundaria que se identifica mediante esta relación y, a continuación, elimina los registros de la tabla primaria correspondiente.  
  
  
