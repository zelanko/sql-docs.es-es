---
title: Agregar un origen de datos al modelo Tabular (Analysis Services AMO-TOM) | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: e54a8a1b-b964-4b6e-9057-44d50af676c0
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 692de4d83bfef7a61b11079fb31bb395da8771aa
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="add-a-data-source-to-tabular-model-analysis-services-amo-tom"></a>Agregar un origen de datos al modelo Tabular (Analysis Services AMO-TOM)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

El **DataSource** clase en el espacio de nombres Microsoft.AnalysisServices.Tabular es una abstracción de un modelo Tabular origen de datos que especifica el tipo y la ubicación de los datos importados durante una operación de actualización de datos. 

Puede agregar un origen de datos al modelo Tabular creando instancias de un objeto de una clase derivada de **DataSource**y, a continuación, agréguelo a la **orígenes de datos** colección del objeto de modelo. Para confirmar los cambios en el servidor, llame a **Model.SaveChanges()** o **Database.Update(UpdateOptions.ExpandFull)**. 

En SQL Server 2016 Analysis Services admite la importación de datos solo desde bases de datos relacionales, donde el proveedor de datos expone los datos en forma de tablas y columnas. Por lo tanto, el modelo de objetos tabulares usa la clase de ProviderDataSource (derivada de origen de datos) para exponer esta funcionalidad. 

## <a name="code-example-add-a-data-source"></a>Ejemplo de código: agregar un origen de datos 

En este ejemplo se muestra cómo crear una instancia de un **ProviderDataSource** y lo agrega a un modelo de datos. 

```
using System; 
using Microsoft.AnalysisServices; 
using Microsoft.AnalysisServices.Tabular; 
 
namespace TOMSamples 
{ 
    class Program 
    { 
        static void Main(string[] args) 
        { 
            // 
            // Connect to the local default instance of Analysis Services 
            // 
            string ConnectionString = "DataSource=localhost"; 

            // 
            // The using syntax ensures the correct use of the 
            // Microsoft.AnalysisServices.Tabular.Server object. 
            // 
            using (Server server = new Server()) 
            { 
                server.Connect(ConnectionString); 
 
                // 
                // Generate a new database name and use GetNewName 
                // to ensure the database name is unique. 
                // 
                string newDatabaseName = 
                    server.Databases.GetNewName("Database with a Data Source Definition"); 
 
                // 
                // Instantiate a new  
                // Microsoft.AnalysisServices.Tabular.Database object. 
                // 
                var dbWithDataSource = new Database() 
                { 
                    Name = newDatabaseName, 
                    ID = newDatabaseName, 
                    CompatibilityLevel = 1200, 
                    StorageEngineUsed = StorageEngineUsed.TabularMetadata, 
                }; 
 
                // 
                // Add a Microsoft.AnalysisServices.Tabular.Model object to the 
                // database, which acts as a root for all other Tabular metadata objects. 
                // 
                dbWithDataSource.Model = new Model() 
                { 
                    Name = "Tabular Data Model", 
                    Description = "A Tabular data model at the 1200 compatibility level." 
                }; 
 
                // 
                // Add a Microsoft.AnalysisServices.Tabular.ProviderDataSource object 
                // to the data Model object created in the previous step. The connection 
                // string of the data source object in this example  
                // points to an instance of the AdventureWorks2014 SQL Server database. 
                // 
                dbWithDataSource.Model.DataSources.Add(new ProviderDataSource() 
                { 
                    Name = "SQL Server Data Source Example", 
                    Description = "A data source definition that uses explicit Windows credentials for authentication against SQL Server.", 
                    ConnectionString = "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=AdventureWorks2014;Integrated Security=SSPI;Persist Security Info=false", 
                    ImpersonationMode = Microsoft.AnalysisServices.Tabular.ImpersonationMode.ImpersonateAccount, 
                    Account = @".\Administrator", 
                    Password = "P@ssw0rd", 
                }); 
 
                // 
                // Add the new database object to the server's  
                // Databases connection and submit the changes 
                // with full expansion to the server. 
                // 
                server.Databases.Add(dbWithDataSource); 
                dbWithDataSource.Update(UpdateOptions.ExpandFull); 
 
                Console.Write("Database "); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                Console.Write(dbWithDataSource.Name); 
                Console.ResetColor(); 
                Console.WriteLine(" created successfully."); 
                Console.WriteLine("The data model includes the following data source definitions:"); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                foreach (DataSource ds in dbWithDataSource.Model.DataSources) 
                { 
                    Console.WriteLine("\tData source name:\t\t{0}", ds.Name); 
                    Console.WriteLine("\tData source description:\t{0}", ds.Description); 
                } 
                Console.ResetColor(); 
                Console.WriteLine(); 
            } 
            Console.WriteLine("Press Enter to close this console window."); 
            Console.ReadLine(); 
        } 
    } 
} 
```

## <a name="next-step"></a>Paso siguiente 

Dentro de un modelo, debe configurar los enlaces de datos que se asignan las columnas de origen en el origen de datos a columnas de destino en el modelo. También debe definir las particiones, como mínimo una por cada tabla, que almacenan los datos. El vínculo siguiente muestra cómo hacerlo: [crear tablas, las particiones y columnas](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-tables-partitions-and-columns-in-a-tabular-model.md) 

