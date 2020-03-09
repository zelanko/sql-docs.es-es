---
title: Especificar valores XML como parámetros
description: Muestra cómo pasar datos XML como un parámetro a un comando.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 2c4d08b8-fc29-4614-97fa-29c8ff7ca5b3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: b4d0f31c8f5fbb282c880abaee62f05dc190bbfc
ms.sourcegitcommit: 610e49c3e1fa97056611a85e31e06ab30fd866b1
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/07/2020
ms.locfileid: "78896652"
---
# <a name="specifying-xml-values-as-parameters"></a>Especificar valores XML como parámetros

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Si una consulta requiere un parámetro cuyo valor es una cadena XML, los desarrolladores pueden proporcionar ese valor mediante una instancia del tipo de datos **SqlXml**. En realidad no se trata de ningún truco; las columnas XML de SQL Server aceptan valores de parámetro exactamente igual que otros tipos de datos.  
  
## <a name="example"></a>Ejemplo  
En la siguiente aplicación de consola se crea una nueva tabla en la base de datos **AdventureWorks**. La nueva tabla incluye una columna denominada **SalesID** y una columna XML de nombre **SalesInfo**.  
  
> [!NOTE]
>  De forma predeterminada, la base de datos de ejemplo **AdventureWorks** no se instala al instalar SQL Server. Puede instalarlo mediante la ejecución del programa de instalación de SQL Server.  
  
En el ejemplo se prepara un objeto <xref:Microsoft.Data.SqlClient.SqlCommand> para insertar una fila en la nueva tabla. Un archivo guardado proporciona los datos XML necesarios para la columna **SalesInfo**.  
  
Para crear el archivo necesario para que se ejecute el ejemplo, cree un archivo de texto en la misma carpeta que el proyecto. Asigne al archivo el nombre MyTestStoreData.xml. Abra el archivo en el Bloc de notas y copie y pegue el texto siguiente:  
  
```xml  
<StoreSurvey xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
  <AnnualSales>300000</AnnualSales>  
  <AnnualRevenue>30000</AnnualRevenue>  
  <BankName>International Bank</BankName>  
  <BusinessType>BM</BusinessType>  
  <YearOpened>1970</YearOpened>  
  <Specialty>Road</Specialty>  
  <SquareFeet>7000</SquareFeet>  
  <Brands>3</Brands>  
  <Internet>T1</Internet>  
  <NumberEmployees>2</NumberEmployees>  
</StoreSurvey>  
```  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.Data.SqlClient;  
using System.Xml;  
using System.Data.SqlTypes;  
  
class Class1  
{  
    static void Main()  
    {  
        using (SqlConnection connection = new SqlConnection(GetConnectionString()))  
       {  
        connection.Open();  
        //  Create a sample table (dropping first if it already  
        //  exists.)  
  
        string commandNewTable =   
            "IF EXISTS (SELECT * FROM dbo.sysobjects " +   
            "WHERE id = " +  
                  "object_id(N'[dbo].[XmlDataTypeSample]') " +   
            "AND OBJECTPROPERTY(id, N'IsUserTable') = 1) " +   
            "DROP TABLE [dbo].[XmlDataTypeSample];" +   
            "CREATE TABLE [dbo].[XmlDataTypeSample](" +   
            "[SalesID] [int] IDENTITY(1,1) NOT NULL, " +   
            "[SalesInfo] [xml])";  
        SqlCommand commandAdd =   
                   new SqlCommand(commandNewTable, connection);  
        commandAdd.ExecuteNonQuery();  
        string commandText =   
            "INSERT INTO [dbo].[XmlDataTypeSample] " +   
            "([SalesInfo] ) " +   
            "VALUES(@xmlParameter )";  
        SqlCommand command =   
                  new SqlCommand(commandText, connection);  
  
        //  Read the saved XML document as a   
        //  SqlXml-data typed variable.  
        SqlXml newXml =   
            new SqlXml(new XmlTextReader("MyTestStoreData.xml"));  
  
        //  Supply the SqlXml value for the value of the parameter.  
        command.Parameters.AddWithValue("@xmlParameter", newXml);  
  
        int result = command.ExecuteNonQuery();  
        Console.WriteLine(result + " row was added.");  
        Console.WriteLine("Press Enter to continue.");  
        Console.ReadLine();  
    }  
  }  
  
    private static string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,              
        // you can retrieve it from a configuration file.   
        return "Data Source=(local);Integrated Security=true;" +  
        "Initial Catalog=AdventureWorks; ";  
    }  
}  
```  
  
## <a name="next-steps"></a>Pasos siguientes
- <xref:System.Data.SqlTypes.SqlXml>
- [Datos XML en SQL Server](xml-data-sql-server.md)
