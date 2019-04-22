---
title: Ejecutar trabajos de Spark en Azure Data Studio
titleSuffix: SQL Server big data clusters
description: Enviar trabajos de Spark en clústeres de macrodatos de SQL Server en Azure Data Studio.
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: d5354927ff0c7e1c61bf358ad73312611c18f317
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "58860456"
---
# <a name="submit-spark-jobs-on-sql-server-big-data-clusters-in-azure-data-studio"></a>Enviar trabajos de Spark en clústeres de macrodatos de SQL Server en Azure Data Studio

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Uno de los escenarios claves para los clústeres de datos de gran tamaño es la capacidad para enviar trabajos de Spark para la versión preliminar de SQL Server 2019. La característica de envío de trabajos de Spark permite enviar archivos Jar o Py locales con las referencias al clúster de macrodatos de SQL Server 2019. También permite ejecutar archivos Jar o Py, ya se encuentran en el sistema de archivos HDFS. 

## <a name="prerequisites"></a>Requisitos previos

- [Herramientas de SQL Server 2019 macrodatos](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **Extensión de SQL Server 2019**
   - **kubectl**

- [Conectarse a Azure Data Studio a la puerta de enlace de Spark o HDFS del clúster de macrodatos](connect-to-big-data-cluster.md).

## <a name="open-spark-job-submission-dialog"></a>Abrir cuadro de diálogo de envío de trabajos de Spark
Hay varias maneras de abrir el cuadro de diálogo de envío de trabajos de Spark. Las formas de incluyen el panel, menú contextual en el Explorador de objetos y la paleta de comandos.

+ Haga clic en **nuevo trabajo de Spark** en el panel para abrir el cuadro de diálogo de envío de trabajos de Spark.

    ![Envío de menú, haga clic en el panel](./media/submit-spark-job/new-spark-job.png)
 
+ Haga doble clic en el clúster en el Explorador de objetos y seleccione **Submit Spark Job** en el menú contextual. Se abrirá el cuadro de diálogo de envío de trabajos de Spark.  
 
    ![Enviar el menú contextual clúster](./media/submit-spark-job/submit-spark-job.png)

+ Haga doble clic en un archivo Jar/Py en el Explorador de objetos y seleccione **Submit Spark Job** en el menú contextual. Se abrirá el cuadro de diálogo del envío de trabajo de Spark con el campo Jar/Py se rellene previamente. 
 
    ![Menú contextual archivo de envío](./media/submit-spark-job/submit-spark-job-2.png)

+ Use el comando **Submit Spark Job** desde la paleta de comandos escribiendo Ctrl + Mayús + P (en Windows) y Cmd + Mayús + P (en Mac).

    ![Enviar la paleta de comandos de menú en windows](./media/submit-spark-job/submit-spark-job-3.png)

    ![Enviar la paleta de comandos de menú en mac](./media/submit-spark-job/submit-spark-job-4.png)
  
 
## <a name="submit-spark-job"></a>Enviar trabajo de Spark 
Se muestra el cuadro de diálogo de envío de trabajos de Spark como la siguiente. Escriba el nombre del trabajo, ruta del archivo JAR/Py, clase principal y otros campos. El archivo Jar / Py origen de archivo podría ser local o de HDFS. Si el trabajo tiene de Spark hacen referencia a archivos JAR, Py archivos o archivos adicionales, haga clic en **avanzadas** pestaña y escriba las rutas de acceso de archivo correspondiente. Haga clic en **enviar** al enviar el trabajo de Spark.
 
![Nuevo cuadro de diálogo de trabajo de spark](./media/submit-spark-job/submit-spark-job-section.png)

![Cuadro de diálogo Opciones avanzada](./media/submit-spark-job/submit-spark-job-section-1.png)

## <a name="monitor-spark-job-submission"></a>Supervisar el envío de trabajos de Spark
Después de enviar el trabajo de Spark, la información de estado de envío y la ejecución de trabajos de Spark se muestran en el historial de tareas de la izquierda. Y obtener más información sobre el progreso y los registros también se muestra en el **salida** ventana en la parte inferior.
+ Cuando el trabajo de Spark está en curso, el **historial de tareas** panel y **salida** están actualizando con el progreso de la ventana.

![Trabajo del Monitor de spark en curso](./media/submit-spark-job/monitor-spark-job-submission.png)

+ Cuando se encuentra el trabajo de Spark en completa con éxito, puede ver vínculos de la interfaz de usuario de Spark y la interfaz de usuario de Yarn en el **salida** ventana. Puede hacer clic en los vínculos para obtener más información.

![Vínculo de salida del trabajo de Spark](./media/submit-spark-job/monitor-spark-job-submission-2.png)

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre los escenarios relacionados y clúster de macrodatos de SQL Server, vea [¿qué es el clúster de SQL Server macrodatos](big-data-cluster-overview.md)?

