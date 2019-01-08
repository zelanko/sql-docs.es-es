---
title: Ejecutar un cuaderno de ejemplo | Microsoft Docs
titleSuffix: SQL Server 2019 big data clusters
description: Este tutorial muestra cómo se puede cargar un cuaderno de Spark de ejemplo en un clúster de macrodatos de 2019 de SQL Server (versión preliminar) de una ejecución.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: tutorial
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: 55d37969ec3e03a635e948cdafb73eb1922a1795
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432558"
---
# <a name="tutorial-run-a-sample-notebook-on-a-sql-server-2019-big-data-cluster"></a>Tutorial: Ejecutar un cuaderno de ejemplo en un clúster de macrodatos de SQL Server 2019

Este tutorial muestra cómo cargar y ejecutar un cuaderno en Azure Data Studio en un clúster de macrodatos de 2019 de SQL Server (versión preliminar). Esto permite que los científicos de datos y los ingenieros de datos para ejecutar código de Python, R o Scala en el clúster.

> [!TIP]
> Si lo prefiere, puede descargar y ejecutar un script para los comandos en este tutorial. Para obtener instrucciones, consulte el [Spark ejemplos](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark) en GitHub.

## <a id="prereqs"></a> Requisitos previos

- [Herramientas de datos de gran tamaño](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **Extensión de SQL Server 2019**
- [Cargar datos de ejemplo en el clúster de macrodatos](tutorial-load-sample-data.md)

## <a name="download-the-sample-notebook-file"></a>Descargue el archivo de Bloc de notas de ejemplo

Siga las instrucciones siguientes para cargar el archivo de Bloc de notas de ejemplo **spark sql.ipynb** en Azure Data Studio.

1. Abra una línea de comandos de bash (Linux) o Windows PowerShell.

1. Desplácese hasta el directorio donde desea descargar el archivo de Bloc de notas de ejemplo.

1. Ejecute el siguiente **curl** comando para descargar el archivo de Bloc de notas desde GitHub:

   ```bash
   curl 'https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/spark-sql.ipynb' -o spark-sql.ipynb
   ```

## <a name="open-the-notebook"></a>Abra el Bloc de notas

Los pasos siguientes muestran cómo abrir el archivo de Bloc de notas en Azure Data Studio:

1. En Azure Data Studio, conéctese a la puerta de enlace de Spark o HDFS del clúster de macrodatos. Para obtener más información, consulte [conectar con la puerta de enlace de Spark o HDFS](connect-to-big-data-cluster.md#hdfs).

1. Haga doble clic en la conexión de puerta de enlace de Spark o HDFS en el **servidores** ventana. A continuación, seleccione **Abrir Bloc de notas**.

   ![Abrir Bloc de notas](media/tutorial-notebook-spark/azure-data-studio-open-notebook.png)

1. Espere a que el **Kernel** y el contexto de destino (**adjuntar a**) que se debe rellenar. Establecer el **Kernel** a **PySpark3**y establezca **adjuntar a** a la dirección IP de su punto de conexión del clúster de macrodatos.

   ![Establecer el Kernel y adjuntar a](media/tutorial-notebook-spark/set-kernel-and-attach-to.png)

## <a name="run-the-notebook-cells"></a>Ejecutando las celdas del Bloc de notas

Puede ejecutar cada celda del Bloc de notas, presione el botón de reproducción a la izquierda de la celda. Los resultados se muestran en el Bloc de notas, una vez que finaliza la ejecución de la celda.

![Ejecución de celda del Bloc de notas](media/tutorial-notebook-spark/run-notebook-cell.png)

Ejecutar cada una de las celdas del Bloc de notas de ejemplo en sucesión. Para obtener más información sobre cómo usar cuadernos con clústeres grandes de datos de SQL Server, consulte los siguientes recursos:

- [Uso de cuadernos en versión preliminar de SQL Server 2019](notebooks-guidance.md)
- [Administración de blocs de notas en Azure Data Studio](notebooks-how-to-manage.md)

## <a name="next-steps"></a>Pasos siguientes

Más información sobre los blocs de notas:
> [!div class="nextstepaction"]
> [Obtenga información sobre los blocs de notas](notebooks-guidance.md)