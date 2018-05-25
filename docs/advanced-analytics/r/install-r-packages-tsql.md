---
title: Usar T-SQL (crear biblioteca externa) para instalar paquetes de R en los servicios de aprendizaje de máquina de SQL Server | Documentos de Microsoft
description: Agregar nuevos paquetes de R para SQL Server de 2017 Machine Learning Services (In-Database)
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/20/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: bbc1adf4868cbfbd02afe5cae3a38fd6223e2d4d
ms.sourcegitcommit: b5ab9f3a55800b0ccd7e16997f4cd6184b4995f9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2018
---
# <a name="use-t-sql-create-external-library-to-install-r-packages-on-sql-server-2017-machine-learning-services"></a>Usar T-SQL (crear biblioteca externa) para instalar paquetes de R en servicios de aprendizaje de máquina de SQL Server de 2017
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se describe cómo instalar nuevos paquetes de R a una instancia de SQL Server donde está habilitado el aprendizaje automático. Existen varios enfoques que puede elegir. Este enfoque funciona mejor para los administradores del servidor que no estén familiarizados con R.

**Se aplica a:**  [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

El [crear biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) instrucción hace posible agregar un paquete o un conjunto de paquetes a una instancia o una base de datos sin ejecutar código R o directamente el código Python. Sin embargo, este método requiere la preparación del paquete y los permisos de base de datos adicional.

+ Todos los paquetes deben estar disponibles como un archivo comprimido local, en lugar de se descargan a petición desde internet.

+ Todas las dependencias deben ser identificadas por el nombre y la versión e incluidas en el archivo zip. La instrucción produce un error si los paquetes necesarios no están disponibles, incluidas las dependencias de paquete de nivel inferior. 

+ Debe tener los permisos necesarios en la base de datos. Para obtener más información, consulte [crear biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

## <a name="download-packages-in-archive-format"></a>Descargar los paquetes en formato de archivo

Si va a instalar un único paquete, descargue el paquete en formato comprimido.

Si el paquete requiere otros paquetes, debe comprobar que los paquetes necesarios están disponibles. Puede usar miniCRAN para analizar el paquete de destino e identificar todas sus dependencias. Se recomienda usar [ **miniCRAN** ](create-a-local-package-repository-using-minicran.md) o [ **igraph** ](http://igraph.org/r/) para analizar las dependencias de paquetes. Instalar una versión incorrecta del paquete o dependencia del paquete, también puede producir un error en la instrucción. 

## <a name="copy-the-file-to-a-local-folder"></a>Copie el archivo en una carpeta local

Copie el archivo comprimido que contiene todos los paquetes en una carpeta local en el servidor. Si no tiene acceso al sistema de archivos en el servidor, también puede pasar un paquete completo como una variable, usando un formato binario. Para obtener más información, consulte [crear biblioteca externa](../../t-sql/statements/create-external-library-transact-sql.md).

## <a name="run-the-statement-to-upload-packages"></a>Ejecute la instrucción para cargar paquetes

Abra un **consulta** ventana, con una cuenta con privilegios administrativos.

Ejecute la instrucción de T-SQL `CREATE EXTERNAL LIBRARY` para cargar la recopilación del paquete comprimido en la base de datos.

    For example, the following statement names as the package source a miniCRAN repository containing the **randomForest** package, together with its dependencies. 

    ```R
    CREATE EXTERNAL LIBRARY randomForest
    FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
    WITH (LANGUAGE = 'R');
    ```

    You cannot use an arbitrary name; the external library name must have the same name that you expect to use when loading or calling the package.

## <a name="verify-package-installation"></a>Comprobar la instalación del paquete

Si la biblioteca se haya creado correctamente, puede ejecutar el paquete en SQL Server, si lo llaman dentro de un procedimiento almacenado.
    
    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    library(randomForest)'
    ```

