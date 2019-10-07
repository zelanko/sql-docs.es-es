---
title: Ejecución de SQL Server Machine Learning Services en un contenedor | Microsoft Docs
description: En este tutorial se explica cómo usar SQL Server Machine Learning Services en un contenedor de Linux que se ejecuta en Docker.
author: uc-msft
ms.author: umajay
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.collection: linux-container
monikerRange: '>= sql-server-linux-ver15  || >= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 28bdf20b51769e15a887b4f9ec227f7aaf6afc95
ms.sourcegitcommit: 071065bc5433163ebfda4fdf6576349f9d195663
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/03/2019
ms.locfileid: "71923822"
---
# <a name="run-sql-server-machine-learning-services-in-a-container"></a>Ejecución de SQL Server Machine Learning Services en un contenedor

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este tutorial se muestra cómo crear un contenedor de Docker mediante SQL Server Machine Learning Services y cómo ejecutar scripts de Machine Learning desde Transact-SQL. La cobertura incluye las tareas siguientes:

> [!div class="checklist"]
> * Clonación del repositorio mssql-docker.
> * Compilación de una imagen de contenedor de SQL Server Linux con Machine Learning Services.
> * Ejecute la imagen de contenedor de SQL Server Linux con Machine Learning Services.
> * Ejecute scripts de R o Python mediante instrucciones Transact-SQL.
> * Detención y eliminación del contenedor de SQL Server Linux.

## <a name="prerequisites"></a>Prerequisites

* Interfaz de la línea de comandos de Git.
* Motor de Docker 1.8 o versiones posteriores en cualquier distribución de Linux admitida o Docker para Mac y Windows. Para obtener más información, consulte [Instalar Docker](https://docs.docker.com/engine/installation/).
* Espacio en disco de 2 gigabytes (GB) como mínimo.
* Un mínimo de 2 GB de RAM.
* [Requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

## <a name="clone-the-mssql-docker-repository"></a>Clonación del repositorio mssql-docker

1. Abra un terminal de Bash en Linux o Mac o un terminal de WSL en Windows.

1. Cree un directorio local para que contenga una copia local del repositorio mssql-docker.
1. Ejecute el comando git clone para clonar el repositorio mssql-docker:

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-a-sql-server-linux-container-image-with-machine-learning-services"></a>Compilación de una imagen de contenedor de SQL Server Linux con Machine Learning Services

1. Cambie el directorio al directorio mssql-mlservices:

    ```bash
    cd mssql-docker/linux/preview/examples/mssql-mlservices
    ```

1. Ejecute el script build.sh:

   ```bash
   ./build.sh
   ```

   > [!NOTE]
   > Para compilar la imagen de Docker, debe instalar paquetes de varios GB de tamaño. El script puede tardar hasta 20 minutos en terminar de ejecutarse, en función del ancho de banda de red.

## <a name="run-the-sql-server-linux-container-image-with-machine-learning-services"></a>Ejecución de la imagen de contenedor de SQL Server Linux con Machine Learning Services

1. Establezca las variables de entorno antes de ejecutar el contenedor. Establezca la variable de entorno PATH_TO_MSSQL en un directorio host:

   ```bash
    export MSSQL_PID='Developer'
    export ACCEPT_EULA='Y'
    export ACCEPT_EULA_ML='Y'
    export PATH_TO_MSSQL='/home/mssql/'
   ```

1. Ejecute el script run.sh:

   ```bash
   ./run.sh
   ```

   Este comando crea un contenedor de SQL Server con Machine Learning Services mediante la edición Developer (valor predeterminado). El puerto **1433** de SQL Server se expone en el host como puerto **1401**.

   > [!NOTE]
   > El proceso para ejecutar ediciones de producción de SQL Server en contenedores es ligeramente diferente. Para obtener más información, consulte [Configuración de imágenes de contenedor de SQL Server en Docker](sql-server-linux-configure-docker.md). Si usa los mismos nombres y puertos de contenedor, el resto de este tutorial funciona con los contenedores de producción.

1. Para ver los contenedores de Docker, ejecute el comando `docker ps`:

   ```bash
   sudo docker ps -a
   ```

1. Si la columna **ESTADO** muestra el estado **Activo**, SQL Server se está ejecutando en el contenedor y está escuchando en el puerto especificado en la columna **PUERTOS**. Si la columna **ESTADO** de su contenedor de SQL Server muestra **Cerrado**, consulte la [sección Solución de problemas de la guía de configuración](sql-server-linux-configure-docker.md#troubleshooting).

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

## <a name="execute-r--python-scripts-from-transact-sql"></a>Ejecución de scripts de R o Python desde Transact-SQL

1. Conéctese a SQL Server en el contenedor y ejecute la siguiente instrucción T-SQL para habilitar la opción de configuración de scripts externos:

    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    go
    ```

1. Para comprobar que Machine Learning Services funciona, ejecute el siguiente comando sp_execute_external_script sencillo de R o Python:

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
> * Clonación del repositorio mssql-docker
> * Compilación de la imagen de contenedor de SQL Server Linux con Machine Learning Services
> * Ejecución de la imagen de contenedor de SQL Server Linux con Machine Learning Services
> * Ejecución de scripts de R o Python mediante instrucciones Transact-SQL
> * Detención y eliminación del contenedor de SQL Server Linux

Después, revise otros escenarios de configuración y solución de problemas de Docker:

> [!div class="nextstepaction"]
>[Guía de configuración de SQL Server en Docker](sql-server-linux-configure-docker.md)
