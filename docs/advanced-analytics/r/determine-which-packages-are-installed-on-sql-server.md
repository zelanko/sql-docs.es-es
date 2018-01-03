---
title: "Determinar qué paquetes de R están instalados en SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 10/09/2016
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9a7f7e43-b568-406c-9434-5a2ec64ec5f5
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c570f5643880b1111889e29e6de03bbff4b10e1d
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2017
---
# <a name="determine-which-r-packages-are-installed-on-sql-server"></a>Determinar qué paquetes de R están instalados en SQL Server

Cuando instala el aprendizaje automático en SQL Server con la opción de lenguaje R, el programa de instalación crea una biblioteca de paquetes de R asociada a la instancia. Cada instancia tiene una biblioteca de paquete independiente. Las bibliotecas de paquete son **no** se comparte entre las instancias, por lo que es posible que paquetes diferentes para instalarse en instancias diferentes.

Este artículo describe cómo se puede determinar qué paquetes de R se instalan para una instancia específica.

## <a name="generate-r-package-list-using-a-stored-procedure"></a>Generar la lista de paquetes de R mediante un procedimiento almacenado

En el ejemplo siguiente se utiliza la función de R `installed.packages()` en un [!INCLUDE [tsql](..\..\includes\tsql-md.md)] procedimiento almacenado para obtener una matriz de los paquetes que se han instalado en la biblioteca R_SERVICES para la instancia actual. Para evitar el análisis de los campos del archivo de DESCRIPCIÓN, se devuelve solo el nombre.

```SQL
EXECUTE sp_execute_external_script
@language=N'R'  
,@script = N'str(OutputDataSet);  
packagematrix <- installed.packages();  
NameOnly <- packagematrix[,1];  
OutputDataSet <- as.data.frame(NameOnly);'  
,@input_data_1 = N'SELECT 1 as col'  
WITH RESULT SETS ((PackageName nvarchar(250) ))  
```

Para obtener más información sobre la parte opcional y los campos predeterminados para el archivo de descripción del paquete de R, consulte [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file).

## <a name="verify-whether-a-package-is-installed-with-an-instance"></a>Compruebe si se instala un paquete con una instancia

Si ha instalado un paquete y para asegurarse de que está disponible para una determinada instancia de SQL Server, puede ejecutar la siguiente llamada de procedimiento almacenado para cargar el paquete y devolver solo los mensajes.

```SQL
EXEC sp_execute_external_script  @language =N'R',
@script=N'library("RevoScaleR")'
GO
```

Este ejemplo busca y carga la biblioteca de RevoScaleR.

+ Si se encuentra el paquete, el mensaje devuelto debe ser algo parecido a "Comandos completados correctamente."

+ Si el paquete no se encuentra o cargado, obtendrá un error similar al siguiente: "se produjo un error de script externo: Error en library("RevoScaleR"): no hay ningún paquete denominado RevoScaleR"

## <a name="get-a-list-of-installed-packages-using-r"></a>Obtener una lista de paquetes instalados con R

Hay varias maneras de obtener una lista de paquetes instalados o cargados mediante herramientas y funciones de R. Muchas herramientas de desarrollo de R proporcionan un examinador de objetos o una lista de paquetes que están instalados o cargados en el área de trabajo actual de R.

+ Desde una utilidad de R local, use una función de R base, como `installed.packages()`, que se incluye en el `utils` paquete. Para obtener una lista que es precisa para una instancia, debe especificar explícitamente la ruta de biblioteca o utilizar las herramientas de R asociadas a la biblioteca de la instancia.

+ Para comprobar si un paquete en un contexto de proceso específico, puede utilizar las siguientes funciones del paquete RevoScaleR. Estas funciones ayudan a identificar los paquetes en contextos de proceso especificado:

+ [rxFindPackage](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxfindpackage)

+ [rxInstalledPackages](https://msdn.microsoft.com/microsoft-r/scaler/packagehelp/rxinstalledpackages)

Por ejemplo, ejecute el siguiente código de R para obtener una lista de los paquetes disponibles en el contexto de proceso de SQL Server especificado.

```r
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
sqlPackages
```
## <a name="see-also"></a>Vea también

[Instalar paquetes de R adicionales en SQL Server](install-additional-r-packages-on-sql-server.md)
