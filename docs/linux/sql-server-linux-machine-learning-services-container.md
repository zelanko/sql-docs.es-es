---
title: Ejecutar SQL Server Machine Learning Services en un contenedor | Microsoft Docs
description: En este tutorial se muestra cómo usar SQL Server Machine Learning Services en un contenedor de Linux que se ejecuta en Docker.
author: uc-msft
ms.author: umajay
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.collection: linux-container
moniker: '>= sql-server-linux-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: f3d3774adf4bee07269b25c3359b031ca24eb99e
ms.sourcegitcommit: ef7834ed0f38c1712f45737018a0bfe892e894ee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2019
ms.locfileid: "68300422"
---
# <a name="run-sql-server-machine-learning-services-in-a-container"></a>Ejecutar SQL Server Machine Learning Services en un contenedor

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este tutorial se muestra cómo crear un contenedor de Docker con SQL Server Machine Learning Services y ejecutar scripts de Machine Learning desde Transact-SQL.

> [!div class="checklist"]
> * Clone el repositorio MSSQL-Docker.
> * Cree SQL Server imagen de contenedor de Linux con Machine Learning Services.
> * Ejecute SQL Server imagen de contenedor de Linux con Machine Learning Services.
> * Ejecutar scripts de R o Python mediante instrucciones Transact-SQL.
> * Detenga y quite el contenedor de SQL Server Linux. 

## <a name="prerequisites"></a>Requisitos previos

* Interfaz de la línea de comandos de Git.
* Motor de Docker 1.8 o versiones posteriores en cualquier distribución de Linux admitida o Docker para Mac y Windows. Para obtener más información, consulte [Instalar Docker](https://docs.docker.com/engine/installation/).
* Mínimo de 2 GB de espacio en disco.
* Mínimo de 2 GB de RAM.
* [Requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

## <a name="clone-the-mssql-docker-repository"></a>Clonación del repositorio MSSQL-Docker

1. Abra un terminal de bash en Linux/Mac o terminal WSL en Windows.

1. Cree un directorio local para que contenga una copia del repositorio MSSQL-Docker localmente.
1. Ejecute el comando git clone para clonar el repositorio MSSQL-Docker.

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-sql-server-linux-container-image-with-machine-learning-services"></a>Cree SQL Server imagen de contenedor de Linux con Machine Learning Services

1. Cambie el directorio al directorio MSSQL-mlservices.

    ```bash
    cd mssql-docker/linux/preview/examples/mssql-mlservices
    ```

1. Ejecute el script build.sh.

   ```bash
   ./build.sh
   ```

   > [!NOTE]
   > La creación de la imagen de Docker requiere la instalación de paquetes de varios GB de tamaño. El script puede tardar hasta 20 minutos en completarse, en función del ancho de banda de red.

## <a name="run-sql-server-linux-container-image-with-machine-learning-services"></a>Ejecute SQL Server imagen de contenedor de Linux con Machine Learning Services

1. Establezca las variables de entorno antes de ejecutar el contenedor. Establezca la variable de entorno PATH_TO_MSSQL en un directorio host.

   ```bash
    export MSSQL_PID='Developer'
    export ACCEPT_EULA='Y'
    export ACCEPT_EULA_ML='Y'
    export PATH_TO_MSSQL='/home/mssql/'
   ```

1. Ejecute el script run.sh.

   ```bash
   ./run.sh
   ```

   Este comando crea un contenedor de SQL Server con Machine Learning Services con Developer Edition (valor predeterminado). SQL Server puerto **1433** se expone en el host como el puerto **1401**.

   > [!NOTE]
   > El proceso de ejecución de las ediciones de SQL Server de producción en contenedores es ligeramente diferente. Para obtener más información, consulte [configuración de imágenes de contenedor de SQL Server en Docker](sql-server-linux-configure-docker.md). Si usa los mismos puertos y nombres de contenedor, el resto de este tutorial sigue funcionando con los contenedores de producción.

1. Para ver los contenedores de Docker, use el comando `docker ps`.

   ```bash
   sudo docker ps -a
   ```

1. Si la columna **ESTADO** muestra el estado **Activo**, esto indica que SQL Server se está ejecutando en el contenedor y que está escuchando en el puerto especificado en la columna **PUERTOS**. Si la columna **ESTADO** de su contenedor de SQL Server muestra **Cerrado**, consulte la [sección Solución de problemas de la guía de configuración](sql-server-linux-configure-docker.md#troubleshooting).

   ```bash
   $ sudo docker ps -a
   ```

    Salida: 
    
    ```
    CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
    941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour     0.0.0.0:1401->1433/tcp   sql1
    ```

## <a name="change-the-sa-password"></a>Cambiar la contraseña de SA

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="execute-r--python-scripts-from-transact-sql"></a>Ejecutar scripts de R/Python desde Transact-SQL

1. Conéctese a SQL Server en el contenedor y habilite la opción de configuración de script externo ejecutando la siguiente instrucción T-SQL.

    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    go
    ```

1. Para comprobar Machine Learning Services funciona, ejecute el siguiente sp_execute_external_script sencillo de R/Python.

    ```sql
    execute sp_execute_external_script 
    @language = N'R',
    @script = N'
    print("Hello World!")
    print(R.version)
    print(Revo.version)
    OutputDataSet <- InputDataSet', 
    @input_data_1 = N'select 1'
    with result sets((i int));
    go
    ```

    ```sql
    execute sp_execute_external_script 
    @language = N'Python',
    @script = N'
    import sys
    print(sys.version)
    print("Hello World!")
    OutputDataSet = InputDataSet',
    @input_data_1 = N'select 1'
    with result sets((i int));
    go 
    ```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido a hacer lo siguiente:

> [!div class="checklist"]
> * Clone el repositorio MSSQL-Docker.
> * Cree SQL Server imagen de contenedor de Linux con Machine Learning Services.
> * Ejecute SQL Server imagen de contenedor de Linux con Machine Learning Services.
> * Ejecutar scripts de R o Python mediante instrucciones Transact-SQL.
> * Detenga y quite el contenedor de SQL Server Linux.

A continuación, revise otros escenarios de solución de problemas y configuración de Docker:

> [!div class="nextstepaction"]
>[Guía de configuración para SQL Server en Docker](sql-server-linux-configure-docker.md)
