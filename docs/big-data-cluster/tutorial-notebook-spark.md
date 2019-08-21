---
title: Ejecutar un cuaderno de ejemplo | Microsoft Docs
titleSuffix: SQL Server big data clusters
description: En este tutorial se muestra cómo puede cargar una ejecución de un cuaderno de Spark [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]de ejemplo en un.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 18e182a251e0f93127ffc376648a29c3e2d9cd02
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653267"
---
# <a name="tutorial-run-a-sample-notebook-on-a-sql-server-big-data-cluster"></a>Tutorial: ejecutar un cuaderno de ejemplo en un clúster de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este tutorial se muestra cómo cargar y ejecutar un cuaderno en Azure Data Studio en [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]un. Esto permite a los científicos de datos e ingenieros de datos ejecutar código de Python, S o Scala en el clúster.

> [!TIP]
> Si lo prefiere, puede descargar y ejecutar un script con los comandos de este tutorial. Para obtener instrucciones, vea los [ejemplos de Spark](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark) en GitHub.

## <a id="prereqs"></a> Requisitos previos

- [Herramientas de macrodatos](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **Extensión de SQL Server 2019**
- [Cargar datos de ejemplo en un clúster de macrodatos](tutorial-load-sample-data.md)

## <a name="download-the-sample-notebook-file"></a>Descargar el archivo de cuaderno de ejemplo

Siga estas instrucciones para cargar el archivo de cuaderno de ejemplo **spark-sql.ipynb** en Azure Data Studio.

1. Abra un símbolo del sistema de Bash (Linux) o Windows PowerShell.

1. Vaya al directorio donde quiera descargar el archivo del cuaderno de ejemplo.

1. Ejecute el siguiente comando de **curl** para descargar el archivo del cuaderno desde GitHub:

   ```bash
   curl 'https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/data-loading/transform-csv-files.ipynb' -o transform-csv-files.ipynb
   ```

## <a name="open-the-notebook"></a>Abrir el cuaderno

En los pasos siguientes, se muestra cómo abrir el archivo del cuaderno en Azure Data Studio:

1. En Azure Data Studio, conéctese a la instancia maestra del clúster de macrodatos. Para obtener más información, vea [Conexión a un clúster de macrodatos](connect-to-big-data-cluster.md).

1. Haga doble clic en la conexión de la puerta de enlace de HDFS/Spark de la ventana **Servidores**. Después, seleccione **Abrir cuaderno**.

   ![Abrir el cuaderno](media/tutorial-notebook-spark/azure-data-studio-open-notebook.png)

1. Espere hasta que se rellenen el **Kernel** y el contexto del destino (**Conectar a**). Establezca el **Kernel** en **PySpark3** y el valor de **Conectar a** en la dirección IP del punto de conexión del clúster de macrodatos.

   ![Establecer el Kernel y Conectar a](media/tutorial-notebook-spark/set-kernel-and-attach-to.png)

## <a name="run-the-notebook-cells"></a>Ejecutar las celdas del cuaderno

Para ejecutar cada celda del cuaderno, pulse el botón Reproducir a la izquierda de la celda. Cuando la celda termine de ejecutarse, los resultados se mostrarán en el cuaderno.

![Ejecutar la celda del cuaderno](media/tutorial-notebook-spark/run-notebook-cell.png)

Ejecute todas las celdas del cuaderno de ejemplo en sucesión. Para obtener más información sobre el uso de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]cuadernos con, consulte los siguientes recursos:

- [Cómo usar cuadernos en SQL Server 2019 versión preliminar](notebooks-guidance.md)
- [Cómo se administran los cuadernos en Azure Data Studio](notebooks-how-to-manage.md)

## <a name="next-steps"></a>Pasos siguientes

Obtenga más información sobre los cuadernos:
> [!div class="nextstepaction"]
> [Información sobre cuadernos](notebooks-guidance.md)
