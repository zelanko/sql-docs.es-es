---
title: Instalación en Docker
titleSuffix: SQL Server Machine Learning Services
description: Obtenga información sobre cómo instalar SQL Server Machine Learning Services (Python y R) en Docker.
author: cawrites
ms.author: chadam
ms.reviewer: davidph
manager: cgronlun
ms.date: 03/23/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: machine-learning
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: eb42a3b63c06e1d436bfac8f727c87ce201bd4ec
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664380"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-docker"></a>Instalación de SQL Server Machine Learning Services (Python y R) en Docker

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se explica cómo instalar SQL Server Machine Learning Services en Docker. Puede usar Machine Learning Services para ejecutar scripts de Python y R en la base de datos. No se proporcionan contenedores generados previamente con Machine Learning Services. Puede crear uno a partir de los contenedores de SQL Server mediante [una plantilla de ejemplo disponible en GitHub](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices).

## <a name="prerequisites"></a>Prerrequisitos

- Interfaz de la línea de comandos de Git.

- Motor de Docker 1.8 o versiones posteriores en cualquier distribución de Linux admitida o Docker para Mac y Windows. Para más información, vea [Get Docker](https://docs.docker.com/get-docker/) (Obtención de Docker).

- Vea también los [requisitos del sistema para SQL Server en Linux](sql-server-linux-setup.md#system).

## <a name="clone-the-mssql-docker-repository"></a>Clonación del repositorio mssql-docker

El comando siguiente clona el repositorio git `mssql-docker` en un directorio local.

1. Abra un terminal de Bash en Linux o Mac, o bien un terminal de Subsistema de Windows para Linux en Windows.

2. Cree un directorio para almacenar una copia local del repositorio mssql-docker.

3. Ejecute el comando git clone para clonar el repositorio mssql-docker:

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-a-sql-server-linux-container-image"></a>Compilación de una imagen de contenedor de Linux de SQL Server

Complete los pasos siguientes para compilar la imagen de Docker:

1. Cambie el directorio al directorio mssql-mlservices:

2. En el mismo directorio, ejecute el comando siguiente:

    ```bash
    docker builds -t mssql-server-mlservices
    ```

3. Ejecute el comando:

    ```bash
    docker runs -d -e MSSQL_PID=Developer -e ACCEPT_EULA=Y -e ACCEPT_EULA_ML=Y -e SA_PASSWORD=<your_sa_password> -v OS>:/var/opt/mssql -p 1433:1433 mssql-server-mlservices
    ```

    Cambie `<your_sa_password>` en `SA_PASSWORD=<your_sa_password>` y cambie la ruta de acceso de `-v`. 

4. Ejecute el comando siguiente para confirmarlo:

    ```bash
    docker ps -a
    ```

   > [!NOTE]
   > Para compilar la imagen de Docker, debe instalar paquetes de varios GB de tamaño. El script puede tardar algún tiempo en terminar de ejecutarse, en función del ancho de banda de red.

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

4. Si en la columna **ESTADO** se muestra el estado **Activo**, SQL Server se ejecuta en el contenedor y escucha en el puerto especificado en la columna **PUERTOS**. Si la columna **ESTADO** de su contenedor de SQL Server muestra **Cerrado**, consulte la [sección Solución de problemas de la guía de configuración](sql-server-linux-configure-docker.md#troubleshooting).

   ```bash
   $ sudo docker ps -a
   ```

    Salida:

    ```
    CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
    941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour     0.0.0.0:1401->1433/tcp   sql1
    ```

## <a name="enable-machine-learning-services"></a>Habilitar Machine Learning Services

Para habilitar Machine Learning Services, conéctese a la instancia de SQL Server y ejecute la siguiente instrucción de T-SQL:

```sql
EXEC sp_configure  'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE
```

## <a name="next-steps"></a>Pasos siguientes

Los desarrolladores de Python pueden aprender a usar Python con SQL Server con estos tutoriales:

+ [Tutorial de Python: Predicción de alquileres de esquíes con regresión lineal en SQL Server Machine Learning Services](../machine-learning/tutorials/python-ski-rental-linear-regression-deploy-model.md)
+ [Tutorial de Python: Clasificación de clientes por categorías mediante la agrupación en clústeres k-means con SQL Server Machine Learning Services](../machine-learning/tutorials/python-clustering-model.md)

Los desarrolladores de R pueden empezar con algunos ejemplos sencillos y conocer los aspectos básicos del funcionamiento de R con SQL Server. Para conocer el siguiente paso, vea los vínculos siguientes:

+ [Inicio rápido: Ejecutar R en T-SQL](../machine-learning/tutorials/quickstart-r-create-script.md)
+ [Tutorial: Análisis en base de datos para desarrolladores de R](../machine-learning/tutorials/sqldev-in-database-r-for-sql-developers.md)
