---
title: 'Tutorial de Python: Clasificación de usuarios por categorías'
description: En esta serie de tutoriales de cuatro partes, realizará una agrupación de clientes en clústeres con el algoritmo K-Means en una base de datos SQL mediante Python con SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 12/17/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f5d1254c6b5c478c7bcad63da0902f21f4db70a9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75306579"
---
# <a name="tutorial-categorizing-customers-using-k-means-clustering-with-sql-server-machine-learning-services"></a>Tutorial: Clasificación de clientes por categorías mediante la agrupación en clústeres k-means con SQL Server Machine Learning Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En esta serie de tutoriales de cuatro partes, usará Python para desarrollar e implementar un modelo de agrupación en clústeres k-means en [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) para agrupar en clústeres datos de clientes.

En la primera parte de esta serie, configurará los requisitos previos para el tutorial y, después, restaurará un conjunto de datos de ejemplo en una base de datos SQL. Más adelante en esta serie, usará estos datos para entrenar e implementar un modelo de agrupación en clústeres en Python con SQL Server Machine Learning Services.

En las partes dos y tres de esta serie, desarrollará scripts de Python en un cuaderno de Azure Data Studio para analizar y preparar los datos y entrenar un modelo de aprendizaje automático. Después, en la parte cuatro, ejecutará esos scripts de Python dentro de una base de datos SQL mediante los procedimientos almacenados.

*Agrupar en clústeres* es organizar datos en grupos, donde los miembros de un grupo son de alguna forma similares. Para esta serie de tutoriales, imagine que es el propietario de un negocio de venta al por menor. Usará el algoritmo **k-means** para realizar la agrupación de clientes en clústeres en un conjunto de datos de compras y devoluciones de productos. Al agrupar los clientes en clústeres, puede centrar sus actividades de marketing de forma más eficaz al dirigirse a grupos específicos.
La agrupación en clústeres k-means es un algoritmo de *aprendizaje no supervisado* que analiza patrones en datos basándose en similitudes.

En este artículo, aprenderá a:

> [!div class="checklist"]
> * Restauración de una base de datos de ejemplo en una instancia de SQL Server

En la [parte dos](python-clustering-model-prepare-data.md), aprenderá a preparar los datos de una base de datos SQL para realizar la agrupación en clústeres.

En la [parte tres](python-clustering-model-build.md), aprenderá a crear y entrenar un modelo de agrupación en clústeres k-means en Python.

En la [parte cuatro](python-clustering-model-deploy.md), aprenderá a crear un procedimiento almacenado en una base de datos SQL que pueda realizar la agrupación en clústeres en Python basándose en datos nuevos.

## <a name="prerequisites"></a>Prerrequisitos

* [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) con la opción de lenguaje de Python: siga las instrucciones de instalación en la [Guía de instalación para Windows](../install/sql-machine-learning-services-windows-install.md) o la [Guía de instalación para Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup-machine-learning?toc=%2fsql%2fadvanced-analytics%2ftoc.json&view=sql-server-linux-ver15).

* [Azure Data Studio](../../azure-data-studio/what-is.md) Usará un cuaderno en Azure Data Studio para Python y SQL. Para obtener más información sobre los cuadernos, vea [Uso de los cuadernos en Azure Data Studio](../../azure-data-studio/sql-notebooks.md).

  * Python: También puede usar su propio IDE de Python, como un cuaderno de Jupyter Notebook o [Visual Studio Code](https://code.visualstudio.com/docs) con la [extensión de Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) y la [extensión de mssql](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql).
  * SQL: También puede usar [SQL Server Management Studio](../../ssms/sql-server-management-studio-ssms.md) (SSMS).

* Paquetes de Python adicionales: en los ejemplos de esta serie de tutoriales, se usan paquetes de Python que puede que no estén instalados.

  Abra un **símbolo del sistema** y cambie a la ruta de instalación de la versión de Python que use en Azure Data Studio. Por ejemplo, `cd %LocalAppData%\Programs\Python\Python37-32`. A continuación, ejecute los siguientes comandos para instalar cualquiera de estos paquetes que no están ya instalados.

  ```console
  pip install matplotlib
  pip install pandas
  pip install pyodbc
  pip install scipy
  pip install sklearn
  ```

## <a name="restore-the-sample-database"></a>Restauración de la base de datos de ejemplo

El conjunto de datos de ejemplo usado en este tutorial se ha guardado en un archivo de copia de seguridad de base de datos **.bak** para que pueda descargarlo y usarlo. Este conjunto de datos se basa en el conjunto de datos [tpcx-bb](http://www.tpc.org/tpcx-bb/default.asp) proporcionado por [Transaction Processing Performance Council (TPC)](http://www.tpc.org/default.asp).

1. Descargue el archivo [tpcxbb_1gb.bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/tpcxbb_1gb.bak).

1. Siga las indicaciones de [Restauración de una base de datos a partir de un archivo de copia de seguridad](../../azure-data-studio/tutorial-backup-restore-sql-server.md#restore-a-database-from-a-backup-file) en Azure Data Studio con estos datos:

   * Importe el archivo **tpcxbb_1gb.bak** que ha descargado.
   * Asigne a la base de datos de destino el nombre "tpcxbb_1gb".

1. Para asegurarse de que el conjunto de datos exista después de restaurar la base de datos, ejecute la siguiente consulta en la tabla **dbo.customer**:

    ```sql
    USE tpcxbb_1gb;
    SELECT * FROM [dbo].[customer];
    ```

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no quiere continuar con este tutorial, elimine la base de datos tpcxbb_1gb de la instancia de SQL Server.

## <a name="next-steps"></a>Pasos siguientes

En la parte uno de esta serie de tutoriales, ha completado estos pasos:

* Restauración de una base de datos de ejemplo en una instancia de SQL Server

Para preparar los datos para el modelo de aprendizaje automático, siga la parte dos de esta serie de tutoriales:

> [!div class="nextstepaction"]
> [Tutorial: Preparación de los datos para realizar la agrupación en clústeres en Python con SQL Server Machine Learning Services](python-clustering-model-prepare-data.md)
