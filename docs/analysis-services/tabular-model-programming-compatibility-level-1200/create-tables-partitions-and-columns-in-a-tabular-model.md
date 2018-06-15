---
title: Crear tablas, las particiones y columnas en un modelo Tabular | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c08fa45cbc4b77c151a002c3318dcc3dbeb2ee06
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34044169"
---
# <a name="create-tables-partitions-and-columns-in-a-tabular-model"></a>Crear tablas, las particiones y columnas en un modelo Tabular
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
En un modelo Tabular, una tabla consta de filas y columnas. Las filas se organizan en particiones para admitir la actualización de datos incrementales. Una solución Tabular puede admitir varios tipos de tablas, dependiendo de dónde provienen los datos:  

* Tablas normales, donde los datos proceden de un origen de datos relacional, a través del proveedor de datos. 

* Tablas insertadas, donde datos es "Insertar" en la tabla mediante programación. 

* Tablas calculadas, procedencia de los datos de una expresión de DAX que hace referencia a otro objeto en el modelo para sus datos.  

En el ejemplo de código siguiente, se definirá una tabla normal. 

## <a name="required-elements"></a>Elementos necesarios 

Una tabla debe tener al menos una partición. Una tabla normal también debe tener al menos una columna definida. 

Cada partición debe tener un origen de especificar el origen de datos, pero el origen se puede establecer en null. Normalmente, el origen es una expresión de consulta que define un segmento de datos en el lenguaje de consulta de base de datos relevante. 

## <a name="code-example-create-a-table-column-parition"></a>Ejemplo de código: crear una tabla, columna, partición

Las tablas se representan mediante la clase de tabla (en el espacio de nombres Microsoft.AnalysisServices.Tabular). 

En el ejemplo siguiente, se definirá una tabla normal tener una partición vinculada a un origen de datos relacionales y unas pocas columnas normales. También enviar los cambios al servidor y desencadenar una actualización de datos que pone los datos en el modelo. Esto representa el escenario más típico, cuando desea cargar datos de una base de datos relacional de SQL Server en una solución Tabular. 


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
                    server.Databases.GetNewName("Database with a Table Definition"); 
 
                // 
                // Instantiate a new  
                // Microsoft.AnalysisServices.Tabular.Database object. 
                // 
                var dbWithTable = new Database() 
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
                dbWithTable.Model = new Model() 
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
                string dataSourceName = "SQL Server Data Source Example"; 
                dbWithTable.Model.DataSources.Add(new ProviderDataSource() 
                { 
                    Name = dataSourceName, 
                    Description = "A data source definition that uses explicit Windows credentials for authentication against SQL Server.", 
                    ConnectionString = "Provider=SQLNCLI11;Data Source=localhost;Initial Catalog=AdventureWorks2014;Integrated Security=SSPI;Persist Security Info=false", 
                    ImpersonationMode = Microsoft.AnalysisServices.Tabular.ImpersonationMode.ImpersonateAccount, 
                    Account = @".\Administrator", 
                    Password = "P@ssw0rd", 
                }); 
 
                //  
                // Add a table called Individual Customers to the data model 
                // with a partition that points to a [Sales].[vIndividualCustomer] view 
                // in the underlying data source. 
                // 
                dbWithTable.Model.Tables.Add(new Table() 
                { 
                    Name = dbWithTable.Model.Tables.GetNewName("Individual Customers"), 
                    Description = "Individual customers (names and email addresses) that purchase Adventure Works Cycles products online.", 
                    Partitions = { 
                        // 
                        // Create a single partition with a QueryPartitionSource for a query 
                        // that imports all customer rows from the underlying data source. 
                        // 
                        new Partition() { 
                            Name = "All Customers", 
                            Source = new QueryPartitionSource() { 
                                DataSource = dbWithTable.Model.DataSources[dataSourceName], 
                                Query = @"SELECT   [FirstName] 
                                                    ,[MiddleName] 
                                                    ,[LastName] 
                                                    ,[PhoneNumber]  
                                                    ,[EmailAddress] 
                                                    ,[City] 
                                        FROM [Sales].[vIndividualCustomer]", 
                            } 
                        } 
                    }, 
                    Columns = 
                    { 
                        // 
                       // DataColumn objects refer to regular table columns.  
                        // Each DataColumn object corresponds to a column in the underlying data source query. 
                        // 
                        new DataColumn() { 
                            Name = "FirstName", 
                            DataType = DataType.String, 
                            SourceColumn = "FirstName", 
                        }, 
                        new DataColumn() { 
                            Name = "MiddleName", 
                            DataType = DataType.String, 
                            SourceColumn = "MiddleName", 
                        }, 
                        new DataColumn() { 
                            Name = "LastName", 
                            DataType = DataType.String, 
                            SourceColumn = "LastName", 
                        }, 
                        new DataColumn() { 
                            Name = "PhoneNumber", 
                            DataType = DataType.String, 
                            SourceColumn = "PhoneNumber", 
                        }, 
                        new DataColumn() { 
                            Name = "EmailAddress", 
                            DataType = DataType.String, 
                            SourceColumn = "EmailAddress", 
                        }, 
                        new DataColumn() { 
                            Name = "City", 
                            DataType = DataType.String, 
                            SourceColumn = "City", 
                        }, 
                    } 
                }); 
 
                // 
                // Add the new database object to the server's  
                // Databases connection and submit the changes 
                // with full expansion to the server. 
                // 
                server.Databases.Add(dbWithTable); 
 
                //  
                // Request a full refresh to import the data from the data source and 
                // and perform any necessary recalculations. 
                // The refresh operation will be performed with the next 
                // invocation of Model.SaveChanges() or Database.Update(UpdateOptions.ExpandFull). 
                dbWithTable.Model.RequestRefresh(Microsoft.AnalysisServices.Tabular.RefreshType.Full); 
                dbWithTable.Update(UpdateOptions.ExpandFull); 
 
 
                Console.Write("Database "); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                Console.Write(dbWithTable.Name); 
                Console.ResetColor(); 
                Console.WriteLine(" created successfully."); 
 
                Console.WriteLine("The data model includes the following table definitions:"); 
                Console.ForegroundColor = ConsoleColor.Yellow; 
                foreach (Table tbl in dbWithTable.Model.Tables) 
                { 
                    Console.WriteLine("\tTable name:\t\t{0}", tbl.Name); 
                    Console.WriteLine("\ttbl description:\t{0}", tbl.Description); 
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

## <a name="partitions-in-a-table"></a>Particiones en una tabla 

Las particiones se representan mediante un **partición** clase (en el espacio de nombres Microsoft.AnalysisServices.Tabular). El **partición** clase expone un **origen** propiedad de P**artitionSource** escribe, lo que proporciona una abstracción sobre los distintos enfoques para introducir datos en partición. A **partición** instancia puede tener un **origen** propiedad como null, que indica que se insertarán datos en la partición mediante el envío de fragmentos de datos al servidor como parte de inserción API de datos expuesto por Analysis Services . En SQL Server 2016, **PartitionSource** clase tiene dos clases derivadas que representan formas para enlazar datos a una partición: **QueryPartitionSource** y **CalculatedPartitionSource**. 

## <a name="columns-in-a-table"></a>Columnas de una tabla 

Las columnas se representan mediante varias clases derivadas de base **columna** clase (en el espacio de nombres Microsoft.AnalysisServices.Tabular): 

* **Objeto DataColumn** (para las columnas regulares en las tablas normales)
* **CalculatedColumn** (para las columnas respaldadas por la expresión de DAX)
* **CalculatedTableColumn** (para las columnas regulares en las tablas calculadas)
* **RowNumberColumn** (tipo especial de columna creada por SSAS para todas las tablas). 

## <a name="row-numbers-in-a-table"></a>Números de fila en una tabla 

Cada **tabla** objeto en un servidor tiene un **RowNumberColumn** usa efectos de indización. No se puede crear o agregar de forma explícita. La columna se crea automáticamente al guardar o actualizar el objeto: 

* **base de datos. SaveChanges** 

* **base de datos. Update(ExpandFull)** 

Al llamar a cualquiera de estos métodos, el servidor creará columna de número de fila automáticamente, que será visible como **RowNumberColumn** colección de columnas de la tabla. 

## <a name="calculated-tables"></a>Tablas calculadas 

Las tablas calculadas se obtienen de una expresión de DAX que modifica los datos de las estructuras de datos existentes en el modelo o de los enlaces fuera de línea. Para crear una tabla calculada mediante programación, haga lo siguiente: 

* Crear un tipo genérico **tabla**. 

* Agregar una partición en él con el origen de tipo **CalculatedPartitionSource**, donde el origen es una expresión de DAX. Origen de la partición es lo que diferencia una tabla normal de una columna calculada. 

Al guardar los cambios en el servidor, el servidor devolverá la lista deducida de **CalculatedTableColumns** (calcula las tablas se componen de las columnas de tabla calculada), visible a través de la colección de columnas de la tabla. 

## <a name="next-steps"></a>Pasos siguientes

Revise las clases usadas para controlar las excepciones en TOM: [control de errores de TOM](../../analysis-services/tabular-model-programming-compatibility-level-1200/handling-errors-in-the-tom-api-analysis-services-amo-tom.md)
  
