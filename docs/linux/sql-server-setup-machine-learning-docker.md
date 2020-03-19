---
title: Instalación en Docker
titleSuffix: SQL Server Machine Learning Services
description: Obtenga información sobre cómo instalar SQL Server Machine Learning Services (Python y R) en Docker.
author: cawrites
ms.author: chadam
ms.reviewer: davidph
manager: cgronlun
ms.date: 02/18/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 767df0ec19f0749eab78a757db5bc92eb66cab49
ms.sourcegitcommit: 39d8d2d504d0ab70bac5ae3e981657e15dfb7bee
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/10/2020
ms.locfileid: "78964523"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-docker"></a>Instalación de SQL Server Machine Learning Services (Python y R) en Docker

En este artículo se explica cómo instalar SQL Server Machine Learning Services en Docker. Puede usar Machine Learning Services para ejecutar scripts de Python y R en la base de datos. No se proporcionan contenedores generados previamente con Machine Learning Services. Puede crear uno a partir de los contenedores de SQL Server mediante [una plantilla de ejemplo disponible en GitHub](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices).

## <a name="prerequisites"></a>Prerrequisitos

- Interfaz de la línea de comandos de Git.
- Motor de Docker 1.8 o versiones posteriores en cualquier distribución de Linux admitida o Docker para Mac y Windows. Para obtener más información, consulte [Instalar Docker](https://docs.docker.com/engine/install/).
- [Requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

## <a name="clone-the-mssql-docker-repository"></a>Clonación del repositorio mssql-docker

1. Abra un terminal de Bash en Linux o Mac, o bien un terminal de Subsistema de Windows para Linux en Windows.

2. Cree un directorio local para que contenga una copia local del repositorio mssql-docker.

3. Ejecute el comando git clone para clonar el repositorio mssql-docker:

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-a-sql-server-linux-container-image"></a>Compilación de una imagen de contenedor de Linux de SQL Server

1. Cambie el directorio al directorio mssql-mlservices:

2. En el mismo directorio, ejecute el comando siguiente:

    ```bash
       docker builds -t mssql-server-mlservices
    ```

3. Ejecute el comando:

    ```bash
       docker runs -d -e MSSQL_PID=Developer -e ACCEPT_EULA=Y -e ACCEPT_EULA_ML=Y -e SA_PASSWORD=  -v OS>:/var/opt/mssql -p 1433:1433 mssql-server-mlservices
    ```

    Modifique para agregar SA_PASSWORD y la ruta de acceso -v. 

4. Ejecute el comando siguiente para confirmarlo:

    ```bash
       docker ps -a
    ```

   > [!NOTE]
   > Para compilar la imagen de Docker, debe instalar paquetes de varios GB de tamaño. El script puede tardar hasta 20 minutos en terminar de ejecutarse, en función del ancho de banda de red.

## <a name="run-the-sql-server-linux-container-image"></a>Ejecución de la imagen de contenedor de SQL Server para Linux

1. Establezca las variables de entorno antes de ejecutar el contenedor. Establezca la variable de entorno PATH_TO_MSSQL en un directorio host:

   ```bash
    export MSSQL_PID='Developer'
    export ACCEPT_EULA='Y'
    export ACCEPT_EULA_ML='Y'
    export PATH_TO_MSSQL='/home/mssql/'
   ```

2. Ejecute el script run.sh:

   ```bash
   ./run.sh
   ```

   Este comando crea un contenedor de SQL Server con Machine Learning Services mediante la edición Developer (valor predeterminado). El puerto **1433** de SQL Server se expone en el host como puerto **1401**.

   > [!NOTE]
   > El proceso para ejecutar ediciones de producción de SQL Server en contenedores es ligeramente diferente. Para obtener más información, consulte [Configuración de imágenes de contenedor de SQL Server en Docker](sql-server-linux-configure-docker.md). Si usa los mismos nombres y puertos de contenedor, el resto de este tutorial funciona con los contenedores de producción.

3. Para ver los contenedores de Docker, ejecute el comando `docker ps`:

   ```bash
   sudo docker ps -a
   ```

4. Si la columna **ESTADO** muestra el estado **Activo**, SQL Server se está ejecutando en el contenedor y está escuchando en el puerto especificado en la columna **PUERTOS**. Si la columna **ESTADO** de su contenedor de SQL Server muestra **Cerrado**, consulte la [sección Solución de problemas de la guía de configuración](sql-server-linux-configure-docker.md#troubleshooting).

   ```bash
   $ sudo docker ps -a
   ```
    Salida:

    ```
    CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
    941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour     0.0.0.0:1401->1433/tcp   sql1
    ```

## <a name="run-in-a-container"></a>Ejecución en un contenedor

[Ejecución de imágenes de contenedor de SQL Server con Docker](quickstart-install-connect-docker.md).

## <a name="connect-to-linux-sql-server-in-the-container"></a>Conexión a SQL Server de Linux en el contenedor

```sql
EXEC sp_configure  'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE
```

## <a name="next-steps"></a>Pasos siguientes

Los desarrolladores de Python pueden aprender a usar Python con SQL Server con estos tutoriales:

+ [Tutorial: Ejecutar Python en T-SQL](../advanced-analytics/tutorials/run-python-using-t-sql.md)
+ [Tutorial: Análisis en base de datos para desarrolladores de Python](../advanced-analytics/tutorials/sqldev-in-database-python-for-sql-developers.md)

Para obtener ejemplos de Machine Learning basados en escenarios del mundo real, vea los [tutoriales sobre Machine Learning](../advanced-analytics/tutorials/machine-learning-services-tutorials.md).

Los desarrolladores de R pueden empezar con algunos ejemplos sencillos y conocer los aspectos básicos del funcionamiento de R con SQL Server. Para conocer el siguiente paso, vea los vínculos siguientes:

+ [Tutorial: Ejecutar R en T-SQL](../advanced-analytics/tutorials/quickstart-r-create-script.md)
+ [Tutorial: Análisis en base de datos para desarrolladores de R](../advanced-analytics/tutorials/sqldev-in-database-r-for-sql-developers.md)
