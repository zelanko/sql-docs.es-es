---
title: "Crear e implementar una base de datos vacía (Analysis Services AMO-TOM) | Documentos de Microsoft"
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
ms.assetid: dcb916e9-97c5-47e0-922a-404891423b2a
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f8aafa733ba61563072e304cf77945203df7585d
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-and-deploy-an-empty-database-analysis-services-amo-tom"></a>Crear e implementar una base de datos vacía (Analysis Services AMO-TOM)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

Un escenario de programación común para AMO TOM consiste en generar las bases de datos y modelos sobre la marcha. Este artículo le guiará por los pasos necesarios para crear una base de datos. 

Para las soluciones tabulares, hay una correspondencia uno a uno entre una base de datos y un modelo, con un modelo por base de datos. Por lo general puede especificar uno u otro, y el motor deducirá el objeto que falta. 

Crear e implementar una nueva base de datos son una tarea de tres partes: 

* Crear una instancia de un **base de datos** de objeto y establecer sus propiedades, incluido un nombre. 

* Agregar el **base de datos** el objeto a un **Server.Databases** colección. 

* Llame a la **actualización** método en el **base de datos** objeto que se va a guardar para el **Server**. 

## <a name="code-example-create-empty-database"></a>Ejemplo de código: crear la base de datos vacía 

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
                    server.Databases.GetNewName("New Empty Database"); 
 
                // 
                // Instantiate a new  
                // Microsoft.AnalysisServices.Tabular.Database object. 
                // 
                var blankDatabase = new Database() 
                { 
                    Name = newDatabaseName, 
                    ID = newDatabaseName, 
                    CompatibilityLevel = 1200, 
                    StorageEngineUsed = StorageEngineUsed.TabularMetadata, 
                }; 
                // 
                // Add the new database object to the server's  
                // Databases connection and submit the changes 
                // with full expansion to the server. 
                // 
                server.Databases.Add(blankDatabase); 
                blankDatabase.Update(UpdateOptions.ExpandFull); 

                Console.Write("Database "); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                Console.Write(blankDatabase.Name); 
                Console.ResetColor(); 
                Console.WriteLine(" created successfully."); 
                Console.WriteLine(); 
            } 
            Console.WriteLine("Press Enter to close this console window."); 
            Console.ReadLine(); 
        } 
    } 
} 
```

## <a name="next-steps"></a>Pasos siguientes 

Una vez que se crea una base de datos, puede agregar objetos de modelo: 

- [Agregar un origen de datos a un modelo Tabular](../../analysis-services/tabular-model-programming-compatibility-level-1200/add-a-data-source-to-tabular-model-analysis-services-amo-tom.md)
- [Crear tablas, las particiones y columnas en un modelo Tabular](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-tables-partitions-and-columns-in-a-tabular-model.md)
 

