---
title: Envío de trabajos de Spark en clústeres de macrodatos de SQL Server en Azure Data Studio
titleSuffix: SQL Server big data clusters
description: Envíe trabajos de Spark [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] en Azure Data Studio.
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ccaa9fbb10359791eb1d07ef8392a11977ae31db
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653338"
---
# <a name="submit-spark-jobs-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-in-azure-data-studio"></a>Enviar trabajos de Spark [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] en Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Uno de los escenarios clave para clústeres de macrodatos es la capacidad de enviar trabajos de Spark para la versión preliminar de SQL Server 2019. La característica de envío de trabajos de Spark permite enviar archivos Jar o Py locales con referencias a clústeres de macrodatos de SQL Server 2019. También permite ejecutar archivos Jar o Py, que ya se encuentran en el sistema de archivos HDFS. 

## <a name="prerequisites"></a>Requisitos previos

- [Herramientas de macrodatos de SQL Server 2019](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Extensión de SQL Server 2019**
   - **kubectl**

- [Conexión de Azure Data Studio a la puerta de enlace de HDFS/Spark del clúster de macrodatos](connect-to-big-data-cluster.md).

## <a name="open-spark-job-submission-dialog"></a>Apertura del cuadro de diálogo de envío de trabajos de Spark

Hay varias maneras de abrir el cuadro de diálogo de envío de trabajos de Spark. Las distintas formas incluyen el panel, el menú contextual del Explorador de objetos y la paleta de comandos.

- Para abrir el cuadro de diálogo de envío de trabajos de Spark, haga clic en **New Spark Job** (Nuevo trabajo de Spark) en el panel.

    ![Menú de envío al hacer clic en el panel](./media/submit-spark-job/new-spark-job.png)

- O bien, haga clic con el botón derecho en el Explorador de objetos y seleccione **Submit Spark Job** (Enviar trabajo de Spark) en el menú contextual.

    ![Menú de envío al hacer clic con el botón derecho en el archivo](./media/submit-spark-job/submit-spark-job-1.png)


- Para abrir el cuadro de diálogo de envío de trabajos de Spark con los campos Jar o Py rellenados previamente, haga clic con el botón derecho en un archivo Jar o Py en el Explorador de objetos y seleccione **Submit Spark Job** (Enviar trabajo de Spark) en el menú contextual.  

    ![Menú de envío al hacer clic con el botón derecho en el clúster](./media/submit-spark-job/submit-spark-job.png)

- Use **Submit Spark Job** (Enviar trabajo de Spark) en la paleta de comandos al escribir **Ctrl + Mayús + P** (en Windows) y **Cmd + Mayús + P** (en Mac).

    ![Paleta de comandos del menú de envío en Windows](./media/submit-spark-job/submit-spark-job-3.png)

    ![Paleta de comandos del menú de envío en Mac](./media/submit-spark-job/submit-spark-job-4.png)
  
 
## <a name="submit-spark-job"></a>Envío de trabajo de Spark 

El cuadro de diálogo de envío de trabajos de Spark se muestra así. Escriba el nombre del trabajo, la ruta de acceso del archivo JAR o Py, la clase principal y otros campos. El origen del archivo Jar o Py puede ser Local o HDFS. Si el trabajo de Spark tiene archivos de referencia Jar, Py u otros, haga clic en la pestaña **OPCIONES AVANZADAS** y escriba las rutas de acceso de archivo correspondientes. Haga clic en **Enviar** para enviar el trabajo de Spark.

![Cuadro de diálogo Nuevo trabajo de Spark](./media/submit-spark-job/submit-spark-job-section.png)

![Cuadro de diálogo Opciones avanzadas](./media/submit-spark-job/submit-spark-job-section-1.png)

## <a name="monitor-spark-job-submission"></a>Supervisar el envío de trabajos de Spark

Una vez enviado el trabajo de Spark, la información de estado del envío y la ejecución de Spark se muestra en el historial de tareas de la izquierda. Los detalles sobre el progreso y los registros también se muestran en la ventana **SALIDA** de la parte inferior.

- Cuando el trabajo de Spark está en curso, el panel **Historial de tareas** y la ventana **SALIDA** se actualizan con el progreso.

    ![Supervisión del trabajo de Spark en curso](./media/submit-spark-job/monitor-spark-job-submission.png)

- Cuando el trabajo de Spark se completa correctamente, los vínculos de la interfaz de usuario de Spark y de Yarn aparecen en la ventana **SALIDA**. Haga clic en los vínculos para obtener más información.

    ![Vínculo del trabajo de Spark en la salida](./media/submit-spark-job/monitor-spark-job-submission-2.png)

## <a name="next-steps"></a>Pasos siguientes

Vea [¿Qué son los clústeres de macrodatos de SQL Server?](big-data-cluster-overview.md) para obtener más información sobre el clúster de macrodatos de SQL Server y los escenarios relacionados.