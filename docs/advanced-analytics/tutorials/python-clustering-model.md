---
title: Categorización de clientes mediante la agrupación en clústeres k-means
description: En esta serie de tutoriales de cuatro partes, realizará la agrupación en clústeres de clientes con el algoritmo K-means, en una base de datos SQL con Python con SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/30/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 78a5999bc0c00a72edcc631877fdfed647024bc5
ms.sourcegitcommit: 26715b4dbef95d99abf2ab7198a00e6e2c550243
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2019
ms.locfileid: "70294370"
---
# <a name="tutorial-categorizing-customers-using-k-means-clustering-with-sql-server-machine-learning-services"></a>Tutorial: Categorización de clientes mediante la agrupación en clústeres k-means con SQL Server Machine Learning Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En esta serie de tutoriales de cuatro partes, usará Python para desarrollar e implementar un modelo de agrupación en clústeres de K-means en [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) a los datos del cliente del clúster.

En la primera parte de esta serie, configurará los requisitos previos para el tutorial y, a continuación, restaurará un conjunto de datos de ejemplo en una base de datos SQL. Más adelante en esta serie, usará estos datos para entrenar e implementar un modelo de agrupación en clústeres en Python con SQL Server Machine Learning Services.

En las partes dos y tres de esta serie, va a desarrollar algunos scripts de Python en un Azure Data Studio Notebook para analizar y preparar los datos y entrenar un modelo de aprendizaje automático. A continuación, en la cuarta parte, ejecutará esos scripts de Python en una base de datos SQL mediante procedimientos almacenados.

La *agrupación en clústeres* se puede explicar como la organización de los datos en grupos en los que los miembros de un grupo son similares de algún modo. En esta serie de tutoriales, Imagine que posee un negocio minorista. Usará el algoritmo **K-means** para realizar la agrupación en clústeres de los clientes en un conjunto de conjuntos de productos que se compran y devuelven. Mediante la agrupación en clústeres de los clientes, puede centrar sus esfuerzos de marketing de manera más eficaz al dirigirse a grupos específicos.
La agrupación en clústeres K-means es un algoritmo de *aprendizaje no supervisado* que busca patrones en los datos en función de las similitudes.

En este artículo, aprenderá a:

> [!div class="checklist"]
> * Restaurar una base de datos de ejemplo en una instancia de SQL Server

En la [segunda parte](python-clustering-model-prepare-data.md), aprenderá a preparar los datos de una base de datos SQL para realizar la agrupación en clústeres.

En la tercera [parte](python-clustering-model-build.md), aprenderá a crear y entrenar un modelo de agrupación en clústeres K-means en Python.

En la [cuarta parte](python-clustering-model-deploy.md), aprenderá a crear un procedimiento almacenado en una base de datos SQL que puede realizar la agrupación en clústeres en Python en función de los nuevos datos.

## <a name="prerequisites"></a>Requisitos previos

* [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) con la opción de lenguaje Python: siga las instrucciones de instalación de la [Guía](../install/sql-machine-learning-services-windows-install.md) de instalación de Windows o la [Guía de instalación de Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup-machine-learning?toc=%2fsql%2fadvanced-analytics%2ftoc.json&view=sql-server-linux-ver15).

* IDE de Python: en este tutorial se usa un cuaderno de Python en [Azure Data Studio](../../azure-data-studio/what-is.md). Para obtener más información, consulte [uso de cuadernos en Azure Data Studio](../../azure-data-studio/sql-notebooks.md). También puede usar su propio IDE de Python, como un cuaderno de Jupyter Notebook o [Visual Studio Code](https://code.visualstudio.com/docs) con la [extensión de Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) y la [extensión MSSQL](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).

* paquete [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) : el paquete **revoscalepy** se incluye en SQL Server Machine Learning Services. Para usar el paquete en un equipo cliente, consulte [configuración de un cliente de ciencia de datos para el desarrollo de Python](../python/setup-python-client-tools-sql.md) para ver las opciones para instalar este paquete localmente.

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
  pip install matplotlib
  pip install scipy
  pip install sklearn
  ```

## <a name="restore-the-sample-database"></a>Restaurar la base de datos de ejemplo

El conjunto de datos de ejemplo utilizado en este tutorial se ha guardado en un archivo de copia de seguridad de base de datos **. bak** para que pueda descargarlo y usarlo. Este conjunto de resultados se deriva del conjunto de [tpcx-BB](http://www.tpc.org/tpcx-bb/default.asp) que proporciona el del [Consejo de rendimiento de procesamiento de transacciones (TPC)](http://www.tpc.org/default.asp).

1. Descargue el archivo [tpcxbb_1gb. bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/tpcxbb_1gb.bak).

1. Siga las instrucciones de [restauración de una base de datos a partir de un archivo de copia de seguridad](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file) en Azure Data Studio con estos detalles:

   * Importe desde el archivo **tpcxbb_1gb. bak** que descargó
   * Asignar el nombre "tpcxbb_1gb" a la base de datos de destino

1. Puede comprobar que el conjunto de datos existe después de haber restaurado la base de datos consultando la tabla **dbo. Customer** :

    ```sql
    USE tpcxbb_1gb;
    SELECT * FROM [dbo].[customer];
    ```

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no va a continuar con este tutorial, elimine la base de datos tpcxbb_1gb de SQL Server.

## <a name="next-steps"></a>Pasos siguientes

En la primera parte de esta serie de tutoriales, ha completado estos pasos:

* Restaurar una base de datos de ejemplo en una instancia de SQL Server

Para preparar los datos para el modelo de aprendizaje automático, siga la segunda parte de esta serie de tutoriales:

> [!div class="nextstepaction"]
> [Tutorial: Preparar los datos para realizar la agrupación en clústeres en Python con SQL Server Machine Learning Services](python-clustering-model-prepare-data.md)
