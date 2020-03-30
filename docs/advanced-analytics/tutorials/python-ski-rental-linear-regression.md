---
title: 'Tutorial de Python: Alquileres de esquíes'
description: En la tercera parte de esta serie de tutoriales de cuatro partes, creará un modelo de regresión lineal en Python para predecir los alquileres de esquíes en SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/02/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fe8a0c9af06d39ce183677adb86f30d9fc197d67
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75681756"
---
# <a name="python-tutorial-predict-ski-rental-with-linear-regression-in-sql-server-machine-learning-services"></a>Tutorial de Python: Predicción de alquileres de esquíes con regresión lineal en SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En esta serie de tutoriales de cuatro partes, usará Python y una regresión lineal en [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) para predecir el número de alquileres de esquíes. El tutorial usa un [cuaderno de Python en Azure Data Studio](../../azure-data-studio/sql-notebooks.md), pero también puede usar su propio entorno de desarrollo integrado (IDE) de Python.

Imagine que es el propietario de una empresa de alquiler de esquíes y quiere predecir el número de alquileres que tendrá en una fecha futura. Esta información le ayudará a preparar las existencias, el personal y las instalaciones.

En la primera parte de esta serie, configurará los requisitos previos. En las partes dos y tres, desarrollará scripts de Python en un cuaderno de Jupyter para preparar sus datos y entrenar un modelo de aprendizaje automático. Después, en la parte tres, ejecutará esos scripts de Python en SQL Server con procedimientos almacenados en T-SQL.

En este artículo, aprenderá a:

> [!div class="checklist"]
> * Importar una base de datos de ejemplo en SQL Server 

En la [parte dos](python-ski-rental-linear-regression-prepare-data.md), aprenderá a cargar los datos desde SQL Server en una trama de datos de Python y a preparar los datos en Python.

En la [parte tres](python-ski-rental-linear-regression-train-model.md), aprenderá a entrenar un modelo de regresión lineal en Python.

En la [parte cuatro](python-ski-rental-linear-regression-deploy-model.md), aprenderá a almacenar el modelo en SQL Server y, después, creará procedimientos almacenados de los scripts de Python que ha desarrollado en las partes dos y tres. Los procedimientos almacenados se ejecutarán en SQL Server para realizar predicciones basándose en datos nuevos.

## <a name="prerequisites"></a>Prerrequisitos

* SQL Server Machine Learning Services: para obtener información sobre cómo instalar Machine Learning Services, vea la [Guía de instalación para Windows](../install/sql-machine-learning-services-windows-install.md) o la [Guía de instalación para Linux](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fadvanced-analytics%2Ftoc.json).

* IDE de Python: en este tutorial, se usa un cuaderno de Python en [Azure Data Studio](../../azure-data-studio/what-is.md). Para más información, vea [Uso de cuadernos en Azure Data Studio](../../azure-data-studio/sql-notebooks.md). 

    También puede usar su propio IDE de Python, como un cuaderno de Jupyter o [Visual Studio Code](https://code.visualstudio.com/docs) con la [extensión de Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) y la [extensión de mssql](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql). 

* Herramienta de consultas SQL: en este tutorial, se da por hecho que usa [Azure Data Studio](../../azure-data-studio/what-is.md). También puede usar [SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md) (SSMS).

* Paquetes de Python adicionales: en los ejemplos de esta serie de tutoriales, se usan los paquetes de Python siguiente que puede que no estén instalados de manera predeterminada:

  * Pandas
  * pyodbc
  * sklearn

  Para instalar estos paquetes:
  1. En Azure Data Studio, seleccione **Administrar paquetes**.
  2. En el panel **Administrar paquetes**, seleccione la pestaña **Agregar nuevo**.
  3. Para cada uno de los paquetes siguientes, escriba el nombre del paquete, haga clic en **Buscar** y, a continuación, haga clic en **instalar**.

  Como alternativa, puede abrir un **símbolo del sistema**, cambiar a la ruta de instalación de la versión de Python que usa en Azure Data Studio (por ejemplo, `cd %LocalAppData%\Programs\Python\Python37-32`) y, a continuación, ejecutar `pip install` para cada paquete.

## <a name="restore-the-sample-database"></a>Restauración de la base de datos de ejemplo

La base de datos de ejemplo usada en este tutorial se ha guardado en un archivo de copia de seguridad de base de datos **.bak** para que pueda descargarlo y usarlo.

1. Descargue el archivo [TutorialDB.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/TutorialDB.bak).

1. Siga las indicaciones de [Restauración de una base de datos a partir de un archivo de copia de seguridad](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file) en Azure Data Studio con estos datos:

   * Importación del archivo **TutorialDB.bak** que ha descargado
   * Asignación del nombre "TutorialDB" a la base de datos de destino

1. Para comprobar que la base de datos restaurada existe, consulte la tabla **DBO.rental_data**:

   ```sql
   USE TutorialDB;
   SELECT * FROM [dbo].[rental_data];
   ```

Para habilitar los scripts externos, ejecute los comandos SQL siguientes:

  ```sql
  sp_configure 'external scripts enabled', 1;
  RECONFIGURE WITH override;
  ```

## <a name="next-steps"></a>Pasos siguientes

En la parte uno de esta serie de tutoriales, ha completado estos pasos:

* Instalación de los requisitos previos
* Importación de una base de datos de ejemplo en una instancia de SQL Server

Para preparar los datos de la base de datos TutorialDB, siga la parte dos de esta serie de tutoriales:

> [!div class="nextstepaction"]
> [Tutorial de Python: Preparación de los datos para entrenar un modelo de regresión lineal](python-ski-rental-linear-regression-prepare-data.md)