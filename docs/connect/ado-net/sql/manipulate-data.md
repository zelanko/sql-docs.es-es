---
title: Manipulación de datos
description: Proporciona ejemplos de codificación de aplicaciones de MARS.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 51096a2e-8b38-4c4d-a523-799bfdb7ec69
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: bb0d7fe3519c5f86c6d1d750afaa36c08341a8ca
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924336"
---
# <a name="manipulating-data"></a>Manipulación de datos

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Antes de la introducción de conjuntos de resultados activos múltiples (MARS), los desarrolladores tenían que usar varias conexiones o cursores del lado servidor para resolver determinados escenarios. Además, al usar varias conexiones en una situación transaccional, se necesitaban conexiones enlazadas (con **sp_getbindtoken** y **sp_bindsession**). En los siguientes escenarios se muestra cómo usar una conexión habilitada para MARS en lugar de varias conexiones.  
  
## <a name="using-multiple-commands-with-mars"></a>Uso de varios comandos con MARS  
La siguiente aplicación de consola muestra cómo usar dos objetos <xref:Microsoft.Data.SqlClient.SqlDataReader> con dos objetos <xref:Microsoft.Data.SqlClient.SqlCommand> y un único objeto <xref:Microsoft.Data.SqlClient.SqlConnection> con MARS habilitado.  
  
### <a name="example"></a>Ejemplo  
En el ejemplo se abre una única conexión a la base de datos **AdventureWorks**. Con un objeto <xref:Microsoft.Data.SqlClient.SqlCommand>, se crea <xref:Microsoft.Data.SqlClient.SqlDataReader>. Cuando se utiliza el lector, se abre un segundo <xref:Microsoft.Data.SqlClient.SqlDataReader>, utilizando los datos del primer <xref:Microsoft.Data.SqlClient.SqlDataReader> como entrada de la cláusula WHERE para el segundo lector.  
  
> [!NOTE]
>  En el siguiente ejemplo se usa la base de datos de ejemplo **AdventureWorks** que se incluye con SQL Server. La cadena de conexión proporcionada en el código de ejemplo da por sentado que la base de datos está instalada y disponible en el equipo local. Modifique la cadena de conexión según sea necesario para el entorno.  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
class Class1  
{  
static void Main()  
{  
  // By default, MARS is disabled when connecting  
  // to a MARS-enabled host.  
  // It must be enabled in the connection string.  
  string connectionString = GetConnectionString();  
  
  int vendorID;  
  SqlDataReader productReader = null;  
  string vendorSQL =   
    "SELECT VendorId, Name FROM Purchasing.Vendor";  
  string productSQL =   
    "SELECT Production.Product.Name FROM Production.Product " +  
    "INNER JOIN Purchasing.ProductVendor " +  
    "ON Production.Product.ProductID = " +   
    "Purchasing.ProductVendor.ProductID " +  
    "WHERE Purchasing.ProductVendor.VendorID = @VendorId";  
  
  using (SqlConnection awConnection =   
    new SqlConnection(connectionString))  
  {  
    SqlCommand vendorCmd = new SqlCommand(vendorSQL, awConnection);  
    SqlCommand productCmd =   
      new SqlCommand(productSQL, awConnection);  
  
    productCmd.Parameters.Add("@VendorId", SqlDbType.Int);  
  
    awConnection.Open();  
    using (SqlDataReader vendorReader = vendorCmd.ExecuteReader())  
    {  
      while (vendorReader.Read())  
      {  
        Console.WriteLine(vendorReader["Name"]);  
  
        vendorID = (int)vendorReader["VendorId"];  
  
        productCmd.Parameters["@VendorId"].Value = vendorID;  
        // The following line of code requires  
        // a MARS-enabled connection.  
        productReader = productCmd.ExecuteReader();  
        using (productReader)  
        {  
          while (productReader.Read())  
          {  
            Console.WriteLine("  " +  
              productReader["Name"].ToString());  
          }  
        }  
      }  
  }  
      Console.WriteLine("Press any key to continue");  
      Console.ReadLine();  
    }  
  }  
  private static string GetConnectionString()  
  {  
    // To avoid storing the connection string in your code,  
    // you can retrieve it from a configuration file.  
    return "Data Source=(local);Integrated Security=SSPI;" +   
      "Initial Catalog=AdventureWorks;MultipleActiveResultSets=True";  
  }  
}  
```  
  
## <a name="reading-and-updating-data-with-mars"></a>Lectura y actualización de datos con MARS  
MARS permite usar una conexión para operaciones de lectura y de lenguaje de manipulación de datos (DML) con más de una operación pendiente. Esta característica elimina la necesidad de que una aplicación se ocupe de los errores de conexión ocupada. Además, MARS puede reemplazar el usuario de los cursores del lado servidor, que normalmente consumen más recursos. Finalmente, dado que es posible realizar varias operaciones con una sola conexión, pueden compartir el mismo contexto de transacción, lo que elimina la necesidad de usar los procedimientos almacenados del sistema **sp_getbindtoken** y **sp_bindsession**.  
  
### <a name="example"></a>Ejemplo  
La siguiente aplicación de consola muestra cómo usar dos objetos <xref:Microsoft.Data.SqlClient.SqlDataReader> con tres objetos <xref:Microsoft.Data.SqlClient.SqlCommand> y un único objeto <xref:Microsoft.Data.SqlClient.SqlConnection> con MARS habilitado. El primer objeto de comando recupera una lista de proveedores cuya clasificación crediticia es 5. El segundo objeto de comando utiliza el identificador de proveedor proporcionado a partir de <xref:Microsoft.Data.SqlClient.SqlDataReader> para cargar el segundo <xref:Microsoft.Data.SqlClient.SqlDataReader> con todos los productos de ese proveedor en particular. El segundo <xref:Microsoft.Data.SqlClient.SqlDataReader> visita cada registro del producto. Para determinar cuál debe ser la nueva **OnOrderQty**, se realiza un cálculo. Luego, se usa el tercer objeto de comando para actualizar la tabla **ProductVendor** con el nuevo valor. Este proceso completo tiene lugar dentro de una única transacción, que se revierte al final.  
  
> [!NOTE]
>  En el siguiente ejemplo se usa la base de datos de ejemplo **AdventureWorks** que se incluye con SQL Server. La cadena de conexión proporcionada en el código de ejemplo da por sentado que la base de datos está instalada y disponible en el equipo local. Modifique la cadena de conexión según sea necesario para el entorno.  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Text;  
using System.Data;  
using Microsoft.Data.SqlClient;  
  
class Program  
{  
static void Main()  
{  
  // By default, MARS is disabled when connecting  
  // to a MARS-enabled host.  
  // It must be enabled in the connection string.  
  string connectionString = GetConnectionString();  
  
  SqlTransaction updateTx = null;  
  SqlCommand vendorCmd = null;  
  SqlCommand prodVendCmd = null;  
  SqlCommand updateCmd = null;  
  
  SqlDataReader prodVendReader = null;  
  
  int vendorID = 0;  
  int productID = 0;  
  int minOrderQty = 0;  
  int maxOrderQty = 0;  
  int onOrderQty = 0;  
  int recordsUpdated = 0;  
  int totalRecordsUpdated = 0;  
  
  string vendorSQL =  
      "SELECT VendorID, Name FROM Purchasing.Vendor " +   
      "WHERE CreditRating = 5";  
  string prodVendSQL =  
      "SELECT ProductID, MaxOrderQty, MinOrderQty, OnOrderQty " +  
      "FROM Purchasing.ProductVendor " +   
      "WHERE VendorID = @VendorID";  
  string updateSQL =  
      "UPDATE Purchasing.ProductVendor " +   
      "SET OnOrderQty = @OrderQty " +  
      "WHERE ProductID = @ProductID AND VendorID = @VendorID";  
  
  using (SqlConnection awConnection =   
    new SqlConnection(connectionString))  
  {  
    awConnection.Open();  
    updateTx = awConnection.BeginTransaction();  
  
    vendorCmd = new SqlCommand(vendorSQL, awConnection);  
    vendorCmd.Transaction = updateTx;  
  
    prodVendCmd = new SqlCommand(prodVendSQL, awConnection);  
    prodVendCmd.Transaction = updateTx;  
    prodVendCmd.Parameters.Add("@VendorId", SqlDbType.Int);  
  
    updateCmd = new SqlCommand(updateSQL, awConnection);  
    updateCmd.Transaction = updateTx;  
    updateCmd.Parameters.Add("@OrderQty", SqlDbType.Int);  
    updateCmd.Parameters.Add("@ProductID", SqlDbType.Int);  
    updateCmd.Parameters.Add("@VendorID", SqlDbType.Int);  
  
    using (SqlDataReader vendorReader = vendorCmd.ExecuteReader())  
    {  
      while (vendorReader.Read())  
      {  
        Console.WriteLine(vendorReader["Name"]);  
  
        vendorID = (int) vendorReader["VendorID"];  
        prodVendCmd.Parameters["@VendorID"].Value = vendorID;  
        prodVendReader = prodVendCmd.ExecuteReader();  
  
        using (prodVendReader)  
        {  
          while (prodVendReader.Read())  
          {  
            productID = (int) prodVendReader["ProductID"];  
  
            if (prodVendReader["OnOrderQty"] == DBNull.Value)  
            {  
              minOrderQty = (int) prodVendReader["MinOrderQty"];  
              onOrderQty = minOrderQty;  
            }  
            else  
            {  
              maxOrderQty = (int) prodVendReader["MaxOrderQty"];  
              onOrderQty = (int)(maxOrderQty / 2);  
            }  
  
            updateCmd.Parameters["@OrderQty"].Value = onOrderQty;  
            updateCmd.Parameters["@ProductID"].Value = productID;  
            updateCmd.Parameters["@VendorID"].Value = vendorID;  
  
            recordsUpdated = updateCmd.ExecuteNonQuery();  
            totalRecordsUpdated += recordsUpdated;  
          }  
        }  
      }  
    }  
    Console.WriteLine("Total Records Updated: " +   
      totalRecordsUpdated.ToString());  
    updateTx.Rollback();  
    Console.WriteLine("Transaction Rolled Back");  
  }  
  
  Console.WriteLine("Press any key to continue");  
  Console.ReadLine();  
}  
private static string GetConnectionString()  
{  
  // To avoid storing the connection string in your code,  
  // you can retrieve it from a configuration file.  
  return "Data Source=(local);Integrated Security=SSPI;" +   
    "Initial Catalog=AdventureWorks;" +   
    "MultipleActiveResultSets=True";  
  }  
}  
```  
  
## <a name="next-steps"></a>Pasos siguientes
- [Conjuntos de resultados activos múltiples (MARS)](multiple-active-result-sets-mars.md)
