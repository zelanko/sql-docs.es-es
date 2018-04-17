---
title: Ejemplos de DiffGram (SQLXML 4.0) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], examples
- examples [SQLXML], DiffGram
- diffgr:parentID
- parentID annotation
ms.assetid: fc148583-dfd3-4efb-a413-f47b150b0975
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6e9d54edb652ab38ff92de8d439507555b1401d9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="diffgram-examples-sqlxml-40"></a>Ejemplos de DiffGram (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
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
  
 En el  **\<antes >** bloquear, hay un  **\<orden >** elemento (**diffgr: ID = "Order1"**) y un  **\< Cliente >** elemento (**diffgr: ID = "Customer1"**). Estos elementos representan registros existentes en la base de datos. El  **\<DataInstance >** elemento no tiene los registros correspondientes (con el mismo **diffgr: ID**). Esto indica una operación de eliminación.  
  
#### <a name="to-test-the-diffgram"></a>Para probar el DiffGram:  
  
1.  Cree estas tablas en el **tempdb** base de datos.  
  
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
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
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
  
 En este DiffGram el  **\<antes >** no se especifica el bloque (no existente de base de datos identifican registros). Hay dos instancias de registro (identificada por el  **\<cliente >** y  **\<orden >** elementos en la  **\<DataInstance >** bloque) que se asignan a las tablas Cust y Ord, respectivamente. Ambos de estos elementos especifican el **diffgr: HasChanges** atributo (**hasChanges = "inserted"**). Esto indica una operación de inserción. En este DiffGram, si especifica **hasChanges = "modified"**, está indicando que va a modificar un registro que no existe, lo que produce un error.  
  
#### <a name="to-test-the-diffgram"></a>Para probar el DiffGram:  
  
1.  Cree estas tablas en el **tempdb** base de datos.  
  
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
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
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
  
 El  **\<antes >** bloque incluye un  **\<cliente >** elemento (**diffgr: ID = "Customer1"**). El  **\<DataInstance >** bloque incluye el elemento correspondiente  **\<cliente >** elemento con el mismo **identificador**. El  **\<cliente >** elemento en el  **\<NewDataSet >** también especifica **diffgr: HasChanges = "modified"**. Esto indica una operación de actualización y el registro del cliente en el **Cust** tabla se actualiza en consecuencia. Tenga en cuenta que si el **diffgr: HasChanges** atributo no se especifica, la lógica de procesamiento de DiffGram omite este elemento y no se realizan actualizaciones.  
  
#### <a name="to-test-the-diffgram"></a>Para probar el DiffGram:  
  
1.  Cree estas tablas en el **tempdb** base de datos.  
  
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
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
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
  
-   Con arreglo a la lógica de procesamiento de DiffGram, todos los elementos de nivel superior de la  **\<antes >** bloquear se asignan a las tablas correspondientes, como se describe en el esquema de asignación.  
  
-   El  **\<antes >** bloque tiene un  **\<orden >** elemento (**dffgr:id = "Order1"**) y un  **\<cliente >** elemento (**diffgr: ID = "Customer1"**) para que no hay ningún elemento correspondiente en el  **\<DataInstance >** bloque (con el mismo ID). Esto indica una operación de eliminación y los registros se eliminan de las tablas Cust y Ord.  
  
-   El  **\<antes >** bloque tiene un  **\<cliente >** elemento (**diffgr: ID = "Customer2"**) para que no hay un correspondiente **\<Cliente >** elemento en el  **\<DataInstance >** bloque (con el mismo ID). El elemento en el  **\<DataInstance >** bloque especifica **diffgr: HasChanges = "modified"**. Se trata de una operación de actualización en la que del cliente ANATR, la información de CompanyName y ContactName se actualiza en la tabla Cust mediante los valores que se especifican en el  **\<DataInstance >** bloque.  
  
-   El  **\<DataInstance >** bloque tiene un  **\<cliente >** elemento (**diffgr: ID = "Customer3"**) y un  **\<Orden >** elemento (**diffgr: ID = "Order3"**). Ninguno de estos elementos especifican el **diffgr: HasChanges** atributo. Por lo tanto, la lógica de procesamiento de DiffGram omite estos elementos.  
  
-   El  **\<DataInstance >** bloque tiene un  **\<cliente >** elemento (**diffgr: ID = "Customer4"**) y un  **\<Orden >** elemento (**diffgr: ID = "Order4"**) para que no hay ningún elemento correspondiente en el \<antes > bloque. Estos elementos en el  **\<DataInstance >** bloque especifica **diffgr: HasChanges = "inserted"**. Por lo tanto, se agrega un nuevo registro a la tabla Cust y a la tabla Ord.  
  
#### <a name="to-test-the-diffgram"></a>Para probar el DiffGram:  
  
1.  Cree las siguientes tablas en la **tempdb** base de datos.  
  
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
  
     Para obtener más información, consulte [utilizar ADO para ejecutar consultas de SQLXML 4.0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="e-applying-updates-by-using-a-diffgram-with-the-diffgrparentid-annotation"></a>E. Aplicar actualizaciones mediante un DiffGram con la anotación diffgr:parentID  
 Este ejemplo se muestra cómo el **parentID** anotación que se especifica en el  **\<antes >** bloque del DiffGram, se utiliza para aplicar las actualizaciones.  
  
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
  
 Este DiffGram especifica una operación de eliminación porque solo hay un  **\<antes >** bloque. En el DiffGram, el **parentID** anotación se utiliza para especificar una relación de elementos primarios y secundarios entre los pedidos y detalles del pedido. Cuando SQLXML elimina los registros, elimina los registros de la tabla secundaria que se identifica mediante esta relación y, a continuación, elimina los registros de la tabla primaria correspondiente.  
  
  
