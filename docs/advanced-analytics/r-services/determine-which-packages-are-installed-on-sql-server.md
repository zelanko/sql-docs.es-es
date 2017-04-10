---
title: "Determinaci&#243;n de los paquetes instalados en SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "08/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9a7f7e43-b568-406c-9434-5a2ec64ec5f5
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# Determinaci&#243;n de los paquetes instalados en SQL Server
  Este tema describe cómo determinar qué paquetes de R están instalados en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia.  
  
De forma predeterminada, la instalación de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] crea una biblioteca de paquete R asociada a cada instancia. Por lo tanto, para saber qué paquetes están instalados en un equipo, debe ejecutar esta consulta en cada instancia independiente que está instalado servicios de R. Tenga en cuenta que las bibliotecas de paquete es **no** se comparte entre las instancias, por lo que es posible que paquetes diferentes para instalarse en distintas instancias.

Para obtener información acerca de cómo determinar la ubicación de la biblioteca predeterminada para una instancia, consulte [instalación y administración de paquetes de R](../../advanced-analytics/r-services/installing-and-managing-r-packages.md).   
   
 
## Obtener una lista de paquetes instalados con R  
 Hay varias maneras de obtener una lista de paquetes instalados o cargados mediante herramientas de R y funciones de R.  
  
+   Muchas herramientas de desarrollo de R proporcionan un examinador de objetos o una lista de paquetes que están instalados o cargados en el área de trabajo actual de R.  

+ Recomendamos las siguientes funciones del paquete RevoScaleR que se proporcionan específicamente para la administración de paquetes en contextos de proceso:
  - [rxFindPackage](https://msdn.microsoft.com/microsoft-r/scaler/rxfindpackage)
  - [rxInstalledPackages](https://msdn.microsoft.com/microsoft-r/scaler/rxInstalledPackages)   
  
+   Puede usar una función de R, como `installed.packages()`, que se incluye en el paquete `utils` instalado. La función analiza los archivos de descripción de cada paquete que se encontró en la biblioteca especificada y devuelve una matriz de nombres de paquete, las rutas de acceso de la biblioteca y los números de versión.  
 
### Ejemplos  
En el ejemplo siguiente se utiliza la función `rxInstalledPackages` para obtener una lista de los paquetes disponibles en el contexto del proceso de SQL Server especificado.

~~~~
sqlServerCompute <- RxInSqlServer(connectionString = 
"Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
     sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
     sqlPackages
~~~~

 En el ejemplo siguiente se utiliza la función R base `installed.packages()` en un [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimiento almacenado para obtener una matriz de los paquetes que se han instalado en la biblioteca R_SERVICES para la instancia actual. Para evitar el análisis de los campos del archivo de DESCRIPCIÓN, se devuelve solo el nombre.  
  
```  
EXECUTE sp_execute_external_script  
@language=N'R'  
,@script = N'str(OutputDataSet);  
packagematrix <- installed.packages();  
NameOnly <- packagematrix[,1];  
OutputDataSet <- as.data.frame(NameOnly);'  
,@input_data_1 = N'SELECT 1 as col'  
WITH RESULT SETS ((PackageName nvarchar(250) ))  
```  
  
 Para obtener más información acerca de los predeterminados y los campos opcionales en el archivo de descripción del paquete de R, consulte [https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file](https://cran.r-project.org/doc/manuals/R-exts.html).  
  
## Vea también  
 [Instalación de paquetes de R adicionales en SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)  
  
  