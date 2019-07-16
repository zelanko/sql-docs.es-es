---
title: Ejecute SQL Server Machine Learning Services en un contenedor | Microsoft Docs
description: Este tutorial muestra cómo usar SQL Server Machine Learning Services en un contenedor de Linux que se ejecutan en Docker.
author: uc-msft
ms.author: umajay
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.collection: linux-container
moniker: '>= sql-server-linux-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: 484f4fc9e51bc8d6ec4ad6e2e75df88593672c28
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67941081"
---
# <a name="run-sql-server-machine-learning-services-in-a-container"></a>Ejecute SQL Server Machine Learning Services en un contenedor

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este tutorial muestra cómo crear un contenedor de Docker con SQL Server Machine Learning Services y ejecutar secuencias de comandos de Machine Learning de Transact-SQL.

> [!div class="checklist"]
> * Clone el repositorio mssql-docker.
> * Compilar imagen de contenedor de SQL Server Linux con Machine Learning Services.
> * Ejecutar la imagen de contenedor de SQL Server Linux con Machine Learning Services.
> * Ejecutar scripts de R o Python mediante instrucciones Transact-SQL.
> * Detener y quitar el contenedor de Linux de SQL Server. 

## <a name="prerequisites"></a>Requisitos previos

* Interfaz de línea de comandos de GIT.
* Motor de Docker 1.8 o versiones posteriores en cualquier distribución de Linux admitida o Docker para Mac y Windows. Para obtener más información, consulte [Instalar Docker](https://docs.docker.com/engine/installation/).
* Mínimo de 2 GB de espacio en disco.
* Mínimo de 2 GB de RAM.
* [Requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

## <a name="clone-the-mssql-docker-repository"></a>Clone el repositorio mssql-docker

1. Abra un terminal de bash en Linux o Mac o WSL terminal en Windows.

1. Cree un directorio local para mantener una copia del repositorio mssql-docker localmente.
1. Ejecute el comando de clonación de git para clonar el repositorio mssql-docker.

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-sql-server-linux-container-image-with-machine-learning-services"></a>Compilar imagen de contenedor de SQL Server Linux con Machine Learning Services

1. Cambie el directorio al directorio mssql mlservices.

    ```bash
    cd mssql-docker/linux/preview/examples/mssql-mlservices
    ```

1. Ejecute el script build.sh.

   ```bash
   ./build.sh
   ```

   > [!NOTE]
   > Creación de la imagen de docker requiere la instalación de paquetes que se encuentran varios gigabytes de tamaño. El script puede tardar hasta 20 minutos en completarse según el ancho de banda de red.

## <a name="run-sql-server-linux-container-image-with-machine-learning-services"></a>Ejecutar la imagen de contenedor de SQL Server Linux con Machine Learning Services

1. Establecer variables de entorno antes de ejecutar el contenedor. Establezca la variable de entorno PATH_TO_MSSQL en un directorio de host.

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

   Este comando crea un contenedor de SQL Server con Machine Learning Services con la edición Developer (valor predeterminado). Puerto de SQL Server **1433** se expone en el host como puerto **1401**.

   > [!NOTE]
   > El proceso para ejecutar las ediciones de SQL Server de producción en contenedores es ligeramente diferente. Para obtener más información, vea [Run production container image](sql-server-linux-configure-docker.md#production) (Ejecutar imágenes de contenedor de producción). Si usa los mismos nombres de contenedor y los puertos, el resto de este tutorial sigue funcionando con contenedores de producción.

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

## <a name="execute-r--python-scripts-from-transact-sql"></a>Ejecutar R / Python scripts de Transact-SQL

1. Conectarse a SQL Server en el contenedor y habilite la opción de configuración de script externo mediante la ejecución de la siguiente instrucción de Transact-SQL.

    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    go
    ```

1. Comprobar que Machine Learning Services funciona mediante la ejecución de la siguiente sp_execute_external_script simple de R o Python.

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
> * Clone el repositorio mssql-docker.
> * Compilar imagen de contenedor de SQL Server Linux con Machine Learning Services.
> * Ejecutar la imagen de contenedor de SQL Server Linux con Machine Learning Services.
> * Ejecutar scripts de R o Python mediante instrucciones Transact-SQL.
> * Detener y quitar el contenedor de Linux de SQL Server.

A continuación, revisar otra configuración de Docker y escenarios de solución de problemas:

> [!div class="nextstepaction"]
>[Guía de configuración de SQL Server en Docker](sql-server-linux-configure-docker.md)
