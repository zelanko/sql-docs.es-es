---
title: Ejecutar un DiffGram utilizando SQLXML clases administradas | Documentos de Microsoft
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
- DiffGrams [SQLXML], Managed Classes
- SQLXML Managed Classes, DiffGrams
- Managed Classes [SQLXML], DiffGrams
- SQLXML, Managed Classes
ms.assetid: 81c687ca-8c9f-4f58-801f-8dabcc508a06
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 5c5837a1709bca49f1d06429d49da67719bfc6fd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202248"
---
# <a name="executing-a-diffgram-by-using-sqlxml-managed-classes"></a>Ejecutar un DiffGram utilizando clases administradas de SQLXML
  Este ejemplo muestra cómo ejecutar un archivo DiffGram en el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] entorno de .NET Framework para aplicar los datos se actualiza a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tablas utilizando clases administradas de SQLXML (Microsoft.Data.SqlXml).  
  
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
  
 El  **\<antes >** bloque incluye un  **\<cliente >** elemento (**diffgr: ID = "Customer1"**). El  **\<DataInstance >** bloque incluye el elemento correspondiente  **\<cliente >** elemento con el mismo **identificador**. El  **\<cliente >** elemento en el  **\<NewDataSet >** también especifica **diffgr: HasChanges = "modified"**. Esto indica una operación de actualización y por lo tanto, el registro de cliente de la tabla Cust se actualiza en consecuencia. Tenga en cuenta que si el **diffgr: HasChanges** atributo no se especifica, la lógica de procesamiento de DiffGram omite este elemento y no se realizan actualizaciones.  
  
 El siguiente código es de una aplicación C# tutorial que muestra cómo utilizar las clases administradas de SQLXML para ejecutar el DiffGram anterior y actualizar dos tablas (Cust, Ord) también creará en el **tempdb** base de datos.  
  
```  
using System;  
using System.Data;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
   static string ConnString = "Provider=SQLOLEDB;Server=MyServer;database=tempdb;Integrated Security=SSPI;";  
   public static int testParams()  
   {  
      SqlXmlAdapter ad;  
      // Need a memory stream to hold diff gram temporarily  
      MemoryStream ms = new MemoryStream();  
      SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
      cmd.RootTag = "ROOT";  
      cmd.CommandStream = new FileStream("MyDiffgram.xml", FileMode.Open, FileAccess.Read);  
      cmd.CommandType = SqlXmlCommandType.DiffGram;  
      cmd.SchemaPath = "DiffGramSchema.xml";  
      // Load data set  
      DataSet ds = new DataSet();  
      ad = new SqlXmlAdapter(cmd);  
      ad.Fill(ds);  
      ad.Update(ds);  
      return 0;  
   }  
   public static int Main(String[] args)  
   {  
      testParams();  
      return 0;  
   }  
}  
```  
  
### <a name="to-test-the-application"></a>Para probar la aplicación  
  
1.  Asegúrese de que .NET Framework está instalado en su equipo.  
  
2.  Guarde el siguiente esquema XSD (DiffGramSchema.xml) en una carpeta:  
  
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
  
3.  Cree estas tablas en el **tempdb** base de datos.  
  
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
  
4.  Agregue estos datos de ejemplo:  
  
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
  
5.  Copie el DiffGram anterior y péguelo en un archivo de texto. Guarde el archivo como MyDiffGram.xml en la misma carpeta utilizada en el paso 1.  
  
6.  Guarde el código C# (DiffgramSample.cs) que se proporciona arriba en la misma carpeta en la que almacenó DiffGramSchema.xml y MyDiffGram.xml en los pasos anteriores.  
  
    > [!NOTE]  
    >  Necesitará actualizar el nombre de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la cadena de conexión de '`MyServer`' al nombre real de su instancia instalada de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
     Si almacena los archivos en otra carpeta, tendrá que modificar el código y especificar la ruta de acceso al directorio adecuada para el esquema de asignación.  
  
7.  Compile el código. Para compilar el código en el símbolo del sistema, use:  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DiffgramSample.cs  
    ```  
  
     Esto crea una aplicación ejecutable (DiffgramSample.exe).  
  
8.  En el símbolo del sistema, ejecute DiffgramSample.exe.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplos de DiffGram &#40;SQLXML 4.0&#41;](diffgram-examples-sqlxml-4-0.md)  
  
  