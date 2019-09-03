---
title: 'Tutorial: Agrupación en clústeres en Python'
description: En esta serie de tutoriales de cuatro partes, realizará la agrupación en clústeres de clientes en una base de datos SQL mediante Python con SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/30/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: abcd13b5db24f7ffd44a21b4690f14d97645cdd5
ms.sourcegitcommit: 3de1fb410de2515e5a00a5dbf6dd442d888713ba
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/02/2019
ms.locfileid: "70211929"
---
# <a name="tutorial-perform-clustering-in-python-with-sql-server-machine-learning-services"></a>Tutorial: Realización de clústeres en Python con SQL Server Machine Learning Services

En esta serie de tutoriales de cuatro partes, usará Python para desarrollar e implementar un modelo de agrupación en clústeres de K-means en [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md) a los datos del cliente del clúster.

En la primera parte de esta serie, configurará los requisitos previos para el tutorial y, a continuación, importará un conjunto de datos de ejemplo a una base de datos SQL. Más adelante en esta serie, usará estos datos para entrenar e implementar un modelo de agrupación en clústeres en Python con SQL Server Machine Learning Services.

En las partes dos y tres de esta serie, va a desarrollar algunos scripts de Python en un Azure Data Studio Notebook para analizar y preparar los datos y entrenar un modelo de aprendizaje automático. A continuación, en la cuarta parte, ejecutará esos scripts de Python en una base de datos SQL mediante procedimientos almacenados.

La agrupación en clústeres se puede explicar como la organización de los datos en grupos en los que los miembros de un grupo son similares de algún modo. En esta serie de tutoriales, Imagine que posee un negocio minorista. Usará el algoritmo **K-means** para realizar la agrupación en clústeres de los clientes en un conjunto de conjuntos de productos que se compran y devuelven. Mediante la agrupación en clústeres de los clientes, puede centrar sus esfuerzos de marketing de manera más eficaz al dirigirse a grupos específicos.
La agrupación en clústeres K-means es un algoritmo de *aprendizaje* no supervisado que busca patrones en los datos en función de las similitudes.

En este artículo, aprenderá a:

> [!div class="checklist"]
> * Importar una base de datos de ejemplo en una instancia de SQL Server

En la [segunda parte](tutorial-python-clustering-model-prepare-data.md), aprenderá a preparar los datos de una base de datos SQL para realizar la agrupación en clústeres.

En la tercera [parte](tutorial-python-clustering-model-build.md), aprenderá a crear y entrenar un modelo de agrupación en clústeres K-means en Python.

En la [cuarta parte](tutorial-python-clustering-model-deploy.md), aprenderá a crear un procedimiento almacenado en una base de datos SQL que puede realizar la agrupación en clústeres en Python en función de los nuevos datos.

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

## <a name="import-the-sample-database"></a>Importar la base de datos de ejemplo

El conjunto de datos de ejemplo utilizado en este tutorial se ha guardado en un archivo de copia de seguridad de base de datos **. bak** para que pueda descargarlo y usarlo. Este conjunto de resultados se deriva del conjunto de [tpcx-BB](http://www.tpc.org/tpcx-bb/default.asp) que proporciona el del [Consejo de rendimiento de procesamiento de transacciones (TPC)](http://www.tpc.org/default.asp).

1. Descargue el archivo [tpcxbb_1gb. bak](https://sqlchoice.blob.core.windows.net/sqlchoice/static/tpcxbb_1gb.bak) en la carpeta de copia de seguridad de SQL Server. En la instancia de base de datos predeterminada, la carpeta es:

   `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Backup\`

1. Abra Azure Data Studio, conéctese a la instancia de SQL Server y abra una nueva ventana de consulta.

1. Ejecute los siguientes comandos para restaurar la base de datos.

   ```sql
   USE master;
   GO

   RESTORE DATABASE tpcxbb_1gb
   FROM DISK = 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\Backup\tpcxbb_1gb.bak'
   WITH MOVE 'tpcxbb_1gb' TO 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\DATA\tpcxbb_1gb.mdf'
      , MOVE 'tpcxbb_1gb_log' TO 'C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\MSSQL\DATA\tpcxbb_1gb.ldf';
   GO
   ```

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no va a continuar con este tutorial, elimine la base de datos tpcxbb_1gb de SQL Server.

## <a name="next-steps"></a>Pasos siguientes

En la primera parte de esta serie de tutoriales, ha completado estos pasos:

* Importar una base de datos de ejemplo en una instancia de SQL Server

Para preparar los datos para el modelo de aprendizaje automático, siga la segunda parte de esta serie de tutoriales:

> [!div class="nextstepaction"]
> [Tutorial: Preparar los datos para realizar la agrupación en clústeres en Python con SQL Server Machine Learning Services](tutorial-python-clustering-model-prepare-data.md)
