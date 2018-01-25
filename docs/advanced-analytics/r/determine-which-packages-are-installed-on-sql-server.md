---
title: "Determinar qué paquetes de R están instalados en SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 9a7f7e43-b568-406c-9434-5a2ec64ec5f5
caps.latest.revision: "11"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: e76a42ead115c8ee4fa89599b192d722ecfbb2ee
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="determine-which-r-packages-are-installed-on-sql-server"></a>Determinar qué paquetes de R están instalados en SQL Server

Cuando instala el aprendizaje automático en SQL Server con la opción de lenguaje R, una biblioteca de paquetes de R se crea específicamente para su uso por la instancia. Cada instancia en el servidor tiene su propia biblioteca de paquete. Bibliotecas de paquete no se pueden compartir entre instancias.

Este artículo describe cómo se puede determinar qué paquetes de R se instalan para una instancia específica de SQL Server.

## <a name="generate-r-package-list-using-a-stored-procedure"></a>Generar la lista de paquetes de R mediante un procedimiento almacenado

En el ejemplo siguiente se utiliza la función de R `installed.packages()` en un [!INCLUDE [tsql](..\..\includes\tsql-md.md)] procedimiento almacenado para obtener una matriz de los paquetes que se han instalado en la biblioteca R_SERVICES para la instancia actual. Para evitar el análisis de los campos del archivo de DESCRIPCIÓN, se devuelve solo el nombre.

```SQL
EXECUTE sp_execute_external_script
@language=N'R'
,@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
NameOnly <- packagematrix[,1];
OutputDataSet <- as.data.frame(NameOnly);'
, @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250) ))
```

Para obtener más información sobre la parte opcional y los campos predeterminados para el campo de descripción del paquete de R, consulte [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file).

## <a name="verify-whether-a-package-is-installed-with-an-instance"></a>Compruebe si se instala un paquete con una instancia

Si ha instalado un paquete y para asegurarse de que está disponible para una determinada instancia de SQL Server, puede ejecutar la siguiente llamada de procedimiento almacenado para cargar el paquete y devolver solo los mensajes. Este ejemplo busca y carga la biblioteca RevoScaleR, si está disponible.

```sql
EXEC sp_execute_external_script  @language =N'R',
@script=N'library("RevoScaleR")'
GO
```

+ Si se encuentra el paquete, se devuelve un mensaje: "Comandos completados correctamente."

+ Si el paquete no se encuentra o cargado, obtendrá un error que contiene el texto: "no hay ningún paquete denominado 'MissingPackageName'"

## <a name="get-a-list-of-installed-packages-using-r"></a>Obtener una lista de paquetes instalados con R

Hay varias maneras de obtener una lista de paquetes instalados o cargados mediante herramientas y funciones de R. Muchas herramientas de desarrollo de R proporcionan un examinador de objetos o una lista de paquetes que están instalados o cargados en el área de trabajo actual de R. Esta sección proporciona algunos comandos cortos que pueden usar desde cualquier línea de comandos de R o en el Service Pack\_ejecutar\_externo\_secuencia de comandos.

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

## <a name="get-library-location-and-version"></a>Obtener la versión y la ubicación de biblioteca

En el ejemplo siguiente se obtiene la ubicación de la biblioteca de RevoScaleR en el contexto de proceso local y la versión del paquete.

```r
rxFindPackage(RevoScaleR, "local")
packageVersion("RevoScaleR")
```

## <a name="determine-path-of-library-used-by-sql-server"></a>Determinar la ruta de acceso de biblioteca utilizado por SQL Server

Si ha actualizado los componentes mediante el enlace de aprendizaje automático, puede cambiar la ruta de acceso a la biblioteca de R. Cuando esto sucede, anteriores accesos directos a herramientas de R podrían hacer referencia a una versión anterior. Para asegurarse de la versión de paquete y la ruta de acceso utilizada por SQL Server, puede ejecutar un comando como el siguiente:

```sql
EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    sql_r_path <- rxSqlLibPaths("local")
      print(sql_r_path)
    version_info <-packageVersion("RevoScaleR")
      print(version_info)'
```

**Resultado**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.2.1'
```
## <a name="see-also"></a>Vea también

[Instalar paquetes de R adicionales en SQL Server](install-additional-r-packages-on-sql-server.md)
