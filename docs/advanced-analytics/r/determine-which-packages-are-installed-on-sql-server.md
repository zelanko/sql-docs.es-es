---
title: "Determinación de los paquetes instalados en SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 08/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9a7f7e43-b568-406c-9434-5a2ec64ec5f5
caps.latest.revision: 11
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 90e7146bde123ca8ac8a8e6ff3e11d212fd4a35a
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="determine-which-packages-are-installed-on-sql-server"></a>Determinación de los paquetes instalados en SQL Server
  En este tema se describe cómo determinar qué paquetes de R están instalados en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
De forma predeterminada, la instalación de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] crea una biblioteca de paquetes de R asociada a cada instancia. Por tanto, para saber qué paquetes están instalados en un equipo, debe ejecutar esta consulta en cada instancia independiente donde esté instalado R Services. Tenga en cuenta que las bibliotecas de paquete **no** se comparten entre las instancias, por lo que es posible instalar paquetes diferentes en distintas instancias.

Para obtener información sobre cómo determinar la ubicación de la biblioteca predeterminada para una instancia, vea [Instalación y administración de paquetes de R](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)   
   
 
## <a name="get-a-list-of-installed-packages-using-r"></a>Obtener una lista de paquetes instalados con R  
 Hay varias maneras de obtener una lista de paquetes instalados o cargados mediante herramientas y funciones de R.  
  
+   Muchas herramientas de desarrollo de R proporcionan un examinador de objetos o una lista de paquetes que están instalados o cargados en el área de trabajo actual de R.  

+ Recomendamos las siguientes funciones del paquete RevoScaleR que se proporcionan específicamente para la administración de paquetes en contextos de cálculo:
  - [rxFindPackage](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxfindpackage)
  - [rxInstalledPackages](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxinstalledpackages)   
  
+   Puede usar una función de R, como `installed.packages()`, que se incluye en el paquete `utils` instalado. La función analiza los archivos de DESCRIPCIÓN de cada paquete que se encontró en la biblioteca especificada y devuelve una matriz de nombres de paquete, rutas de acceso de biblioteca y números de versión.  
 
### <a name="examples"></a>Ejemplos  
En el ejemplo siguiente se usa la función `rxInstalledPackages` para obtener una lista de los paquetes disponibles en el contexto de cálculo de SQL Server proporcionado.

~~~~
sqlServerCompute <- RxInSqlServer(connectionString = 
"Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
     sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
     sqlPackages
~~~~

 En el ejemplo siguiente se usa la función base de R `installed.packages()` en un procedimiento almacenado [!INCLUDE[tsql](../../includes/tsql-md.md)] para obtener una matriz de los paquetes que se han instalado en la biblioteca R_SERVICES para la instancia actual. Para evitar el análisis de los campos del archivo de DESCRIPCIÓN, se devuelve solo el nombre.  
  
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
  
 Para más información, vea la descripción de los campos opcionales y predeterminados para el archivo de DESCRIPCIÓN del paquete de R, en [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file).  
  
## <a name="see-also"></a>Vea también  
 [Instalación de paquetes de R adicionales en SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)  
  
  

