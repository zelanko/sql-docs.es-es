---
title: Con la carga masiva SQLXML en el entorno .NET | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQLXML, XML Bulk Load
- XML Bulk Load [SQLXML], .NET environment
- .NET Framework [SQLXML], XML Bulk Load
- bulk load [SQLXML], .NET environment
ms.assetid: b85df83b-ba56-43bf-bcdf-b2a6fca43276
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8133a762b1bc0f687529ee375bd8e9c5699051b4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37307485"
---
# <a name="using-sqlxml-bulk-load-in-the-net-environment"></a>Usar la carga masiva SQLXML en el entorno .NET
  En este tema se explica cómo se puede usar la funcionalidad de carga masiva XML en el entorno .NET. Para obtener información detallada acerca de la carga masiva XML, vea [realizar carga masiva de datos XML &#40;SQLXML 4.0&#41;](bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md).  
  
 Para utilizar el objeto COM de carga masiva SQLXML desde un entorno administrado, tiene que agregar una referencia de proyecto a este objeto. Esto genera una interfaz de contenedor administrado para el objeto COM de carga masiva.  
  
> [!NOTE]  
>  La carga masiva XML administrada no funciona con flujos administrados y requiere un contenedor para los flujo nativos. El componente Carga masiva SQLXML no se ejecutará en un entorno multiproceso (atributo ' [MTAThread]'). Si intenta ejecutar el componente carga masiva en un entorno multiproceso, obtendrá una excepción InvalidCastException con la siguiente información adicional: "Error de QueryInterface para la interfaz SQLXMLBULKLOADLib.ISQLXMLBulkLoad". La solución consiste en hacer que el objeto que contiene la carga masiva objeto único subproceso accesible (por ejemplo, mediante el **[STAThread]** atributo tal como se muestra en el ejemplo).  
  
 En este tema se proporciona una aplicación de ejemplo funcional en C# para realizar la carga masiva de los datos XML de la base de datos. Para crear un ejemplo funcional, siga estos pasos:  
  
1.  Cree las tablas siguientes:  
  
    ```  
    CREATE TABLE Ord (  
             OrderID     int identity(1,1)  PRIMARY KEY,  
             CustomerID  varchar(5))  
    GO  
    CREATE TABLE Product (  
             ProductID   int identity(1,1) PRIMARY KEY,  
             ProductName varchar(20))  
    GO  
    CREATE TABLE OrderDetail (  
           OrderID     int FOREIGN KEY REFERENCES Ord(OrderID),  
           ProductID   int FOREIGN KEY REFERENCES Product(ProductID),  
                       CONSTRAINT OD_key PRIMARY KEY (OrderID, ProductID))  
    GO  
    ```  
  
2.  Guarde el esquema siguiente en un archivo (schema.xml):  
  
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
  
3.  Guarde el documento XML de ejemplo siguiente en un archivo (data.xml):  
  
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
  
4.  Inicie Visual Studio.  
  
5.  Cree una aplicación de consola de C#.  
  
6.  Desde el **proyecto** menú, seleccione **Agregar referencia**.  
  
7.  En el **COM** ficha, seleccione **biblioteca de tipos de Microsoft SQLXML Bulkload 4.0** (xblkld4.dll) y haga clic en **Aceptar**. Verá el **Interop.SQLXMLBULKLOADLib** ensamblado creado en el proyecto.  
  
8.  Reemplace el método Main() por el código siguiente. Actualización de la **ConnectionString** propiedad y la ruta de acceso a los archivos de esquema y los datos.  
  
    ```  
    [STAThread]  
       static void Main(string[] args)  
       {     
             try  
             {  
                SQLXMLBULKLOADLib.SQLXMLBulkLoad4Class objBL = new SQLXMLBULKLOADLib.SQLXMLBulkLoad4Class();  
                objBL.ConnectionString = "Provider=sqloledb;server=server;database=databaseName;integrated security=SSPI";  
                objBL.ErrorLogFile = "error.xml";  
                objBL.KeepIdentity = false;  
                objBL.Execute ("schema.xml","data.xml");  
             }  
             catch(Exception e)  
             {  
             Console.WriteLine(e.ToString());  
             }  
       }  
    ```  
  
9. Para cargar el XML en la tabla creada, genere y ejecute el proyecto.  
  
    > [!NOTE]  
    >  La referencia al componente Carga masiva (xblkld4.dll) también se puede agregar utilizando la herramienta tlbimp.exe, que está disponible como parte de .NET Framework. Esta herramienta crea un contenedor administrado para la DLL nativa (xblkld4.dll), que se puede utilizar después en cualquier proyecto de .NET. Por ejemplo:  
  
    ```  
    c:\>tlbimp xblkld4.dll  
    ```  
  
     Esto crea la DLL del contenedor administrado (SQLXMLBULKLOADLib.dll) que puede utilizar en el proyecto de .NET Framework. En .NET Framework, puede agregar la referencia del proyecto a la DLL recién creada.  
  
## <a name="see-also"></a>Vea también  
 [Realizar la carga masiva de datos XML &#40;SQLXML 4.0&#41;](bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)  
  
  
