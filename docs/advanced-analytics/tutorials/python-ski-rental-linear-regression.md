---
title: 'Tutorial de Python: Alquileres de esquí (regresión lineal)'
description: En este tutorial usará Python y la regresión lineal en SQL Server Machine Learning Services para predecir el número de alquileres de esquí.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 718487ba55b2b8db8f16b59df5785cf78ff501f1
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2019
ms.locfileid: "70242513"
---
# <a name="python-tutorial-predict-ski-rental-with-linear-regression-in-sql-server-machine-learning-services"></a>Tutorial de Python: Predecir el alquiler de esquí con regresión lineal en SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En esta serie de tutoriales de cuatro partes, usará Python y la regresión lineal en [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) para predecir el número de alquileres de esquí. En el tutorial se usa un [cuaderno de Python en Azure Data Studio](../../azure-data-studio/sql-notebooks.md), pero también puede usar su propio entorno de desarrollo integrado (IDE) de Python.

Imagine que posee una empresa de alquiler de esquí y desea predecir el número de alquileres que tendrá en una fecha futura. Esta información le ayudará a preparar las acciones, el personal y las instalaciones.

En la primera parte de esta serie, se configurará con los requisitos previos. En las partes dos y tres, va a desarrollar algunos scripts de Python en un cuaderno de Jupyter Notebook para preparar los datos y entrenar un modelo de aprendizaje automático. A continuación, en la tercera parte, ejecutará esos scripts de Python dentro de SQL Server mediante procedimientos almacenados de T-SQL.

En este artículo, aprenderá a:

> [!div class="checklist"]
> * Importar una base de datos de ejemplo en SQL Server 

En la [segunda parte](python-ski-rental-linear-regression-prepare-data.md), aprenderá a cargar los datos de SQL Server en una trama de datos de Python y a preparar los datos en Python.

En la tercera [parte](python-ski-rental-linear-regression-train-model.md), aprenderá a entrenar un modelo de regresión lineal en Python.

En la [cuarta parte](python-ski-rental-linear-regression-deploy-model.md), aprenderá a almacenar el modelo en SQL Server y, a continuación, creará procedimientos almacenados a partir de los scripts de Python desarrollados en las partes dos y tres. Los procedimientos almacenados se ejecutarán en SQL Server para realizar predicciones basadas en nuevos datos.

## <a name="prerequisites"></a>Requisitos previos

* SQL Server Machine Learning Services: para saber cómo instalar Machine Learning Services, consulte la [Guía de instalación de Windows](../install/sql-machine-learning-services-windows-install.md) o la [Guía de instalación de Linux](../../linux/sql-server-linux-setup-machine-learning.md?toc=%2Fsql%2Fadvanced-analytics%2Ftoc.json).

* IDE de Python: en este tutorial se usa un cuaderno de Python en [Azure Data Studio](../../azure-data-studio/what-is.md). Para obtener más información, consulte [uso de cuadernos en Azure Data Studio](../../azure-data-studio/sql-notebooks.md). 

    También puede usar su propio IDE de Python, como un cuaderno de Jupyter Notebook o [Visual Studio Code](https://code.visualstudio.com/docs) con la [extensión de Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) y la [extensión MSSQL](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql). 

* paquete [revoscalepy](../python/ref-py-revoscalepy.md) : el paquete **revoscalepy** se incluye en SQL Server Machine Learning Services. Para usar el paquete en un equipo cliente, consulte [configuración de un cliente de ciencia de datos para el desarrollo de Python](../python/setup-python-client-tools-sql.md) para ver las opciones para instalar este paquete localmente.

    Si usa un cuaderno de Python en Azure Data Studio, siga estos pasos adicionales para usar **revoscalepy**:

    1. Abra Azure Data Studio
    1. En el menú **archivo** , seleccione **preferencias** y, a continuación, **configuración** .
    1. Expanda **extensiones** y seleccione **configuración de Notebook** .
    1. En **ruta de acceso de Python**, escriba la ruta de acceso en la que instaló `C:\path-to-python-for-mls`las bibliotecas (por ejemplo,).
    1. Asegúrese de que la opción **usar Python existente** está activada
    1. Reiniciar Azure Data Studio

    Si usa un IDE de Python diferente, siga los mismos pasos para el IDE.

* Herramienta de consulta SQL: en este tutorial se da por supuesto que está usando [Azure Data Studio](../../azure-data-studio/what-is.md). También puede usar [SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md) (SSMS).

* Paquetes adicionales de Python: los ejemplos de esta serie de tutoriales usan paquetes de Python que puede haber instalado o no. Use los siguientes comandos **PIP** para instalar estos paquetes si es necesario.

    ```console
    pip install pandas
    pip install sklearn
    pip install pickle
    ```

## <a name="restore-the-sample-database"></a>Restaurar la base de datos de ejemplo

El conjunto de datos de ejemplo utilizado en este tutorial se ha guardado en un archivo de copia de seguridad de base de datos **. bak** para que pueda descargarlo y usarlo.

1. Descargue el archivo [TutorialDB. bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/TutorialDB.bak).

1. Siga las instrucciones de [restauración de una base de datos a partir de un archivo de copia de seguridad](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file) en Azure Data Studio con estos detalles:

   * Importe desde el archivo **TutorialDB. bak** que descargó
   * Asignar el nombre "TutorialDB" a la base de datos de destino

1. Puede comprobar que el conjunto de datos existe después de haber restaurado la base de datos consultando la tabla **dbo. rental_data** :

    ```sql
    USE TutorialDB;
    SELECT * FROM [dbo].[rental_data];
    ```

## <a name="next-steps"></a>Pasos siguientes

En la primera parte de esta serie de tutoriales, ha completado estos pasos:

* Se han instalado los requisitos previos
* Importar una base de datos de ejemplo en un SQL Server

Para preparar los datos de la base de datos TutorialDB, siga la segunda parte de esta serie de tutoriales:

> [!div class="nextstepaction"]
> [Tutorial de Python: Preparar los datos para entrenar un modelo de regresión lineal](python-ski-rental-linear-regression-prepare-data.md)