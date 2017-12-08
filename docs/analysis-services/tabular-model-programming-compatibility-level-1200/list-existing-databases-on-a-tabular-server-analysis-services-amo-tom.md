---
title: Lista de bases de datos existentes en un servidor Tabular (Analysis Services AMO-TOM) | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: ab5eb4b8-6254-442d-a42e-2372c346d260
caps.latest.revision: "2"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 25b6f8ef54de536c47b3a5df4a6d8ed3b6d627de
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="list-existing-databases-on-a-tabular-server-analysis-services-amo-tom"></a>Lista de bases de datos existentes en un servidor Tabular (Analysis Services AMO-TOM)

[!INCLUDE[ssas-appliesto-sql2016-later-aas](../../includes/ssas-appliesto-sql2016-later-aas.md)]

Cuando haya un **Server** objeto que se conecta a una instancia de Analysis Services, puede iterar sobre **Server.Databases** colección para enumerar todas las bases de datos hospedadas por la instancia de servicios de análisis. 

El **Server.Databases** colección contiene un **base de datos** objeto para cada base de datos que se hospedan en el servidor, independientemente del modo de servidor (Multidimensional o Tabular) o el tipo de base de datos (Multidimensional, Pre-1200 tabulares, o Tabular 1200 y superior). 

Puede comprobar el tipo de base de datos a través de **Database.StorageEngineUsed** propiedad.  

Bases de datos tabulares de 1200 y versiones posteriores devolverán un valor no nulo **Database.Model** propiedad que proporciona acceso a todos los objetos de metadatos tabulares: tablas, columnas, relaciones y así sucesivamente.  

Para Multidimensional o Tabular 1103 y niveles inferiores, la Database.Model propiedad será null. En este caso, los metadatos no tabulares estará disponible en las propiedades multidimensionales (por ejemplo, Database.Cubes y Database.Dimensions), pero sólo se muestran las propiedades clase Microsoft.AnalysisServices.Database (a través de AMO), no por Microsoft.AnalysisServices.Tabular.Database (para TOM). Para obtener más información acerca de qué clase de base de datos debe utilizar, consulte [instalar, distribuir y hacer referencia a la biblioteca de cliente de TOM](../../analysis-services/tabular-model-programming-compatibility-level-1200/install-distribute-and-reference-the-tabular-object-model.md).

A menos que Database.StorageEngineUsed está establecida en TabularMetadata, no podrá usar otras clases en el espacio de nombres Tabular para leer o manipular el árbol del modelo. 

En la tabla siguiente se resume los comportamientos esperados al conectarse a un servidor o base de datos mediante una clase Microsoft.AnalysisServices.Tabular en un servidor o base de datos. 

mode | Database.Model | Database.StorageEngineUsed
-----|----------------|---------------------------
Tabular 1200, 1400 | Devuelve el nombre del modelo| StorageEngineUsed.TabularMetadata 
1103 tabulares, 1050, 1100 | Devuelve null | StorageEngineUsed.InMemory 
Multidimensional | Devuelve null | StorageEngineUsed.Traditional 

## <a name="code-example-list-existing-databases"></a>Ejemplo de código: lista de bases de datos existentes

El código siguiente muestra cómo conectarse a las bases de datos de servidor y lista alojados por servidor. 

```
using System; using Microsoft.AnalysisServices; 
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
                // List common properties for the databases on the server. 
                // 
                foreach (Database db in server.Databases) 
                { 
                    Console.WriteLine("Properties for database {0}:", db.Name); 
                    Console.ForegroundColor = ConsoleColor.Yellow; 
                    Console.WriteLine("Database ID:\t\t\t{0}", db.ID); 
                    Console.WriteLine("Database compatibility level:\t{0}", db.CompatibilityLevel); 
                    Console.WriteLine("Database collation:\t\t{0}", db.Collation); 
                    Console.WriteLine("Database created timestamp:\t{0}", db.CreatedTimestamp); 
                    Console.WriteLine("Database language ID:\t\t{0}", db.Language); 
                    Console.WriteLine("Database model type:\t\t{0}", db.ModelType); 
                    Console.WriteLine("Database state:\t\t\t{0}", db.State); 
                    Console.ResetColor(); 
                    Console.WriteLine(); 
                } 
            } 
            Console.WriteLine("Press Enter to close this console window."); 
            Console.ReadLine(); 
        } 
    } 
} 
```


## <a name="get-an-item-from-a-database"></a>Obtener un elemento de una base de datos 

El siguiente fragmento de código muestra cómo obtener una tabla o columna de una base de datos. 


```
var db = srv.Databases.GetByName("abc"); 

Column c1 = db.Model.Tables["foo"].Columns["bar"]; 
if (c1.ObjectType == ObjectType.Column) // always true 

MetadataObject obj; 

switch(obj.ObjectType) 
{ 
 case ObjectType.Table: 
  var t1 = (Table)obj; 
  break; 
} 
```

## <a name="next-steps"></a>Pasos siguientes

Comprender cómo [crear e implementar una base de datos vacía](../../analysis-services/tabular-model-programming-compatibility-level-1200/create-and-deploy-an-empty-database-analysis-services-amo-tom.md) mediante la API de TOM.

