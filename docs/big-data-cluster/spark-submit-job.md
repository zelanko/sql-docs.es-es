---
title: Enviar a trabajo de Spark en clústeres de macrodatos de SQL Server en Azure Data Studio
description: Enviar a trabajo de Spark en clústeres de macrodatos de SQL Server en Azure Data Studio
services: SQL Server 2019 big data cluster spark
ms.service: SQL Server 2019 big data cluster spark
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.custom: ''
ms.topic: conceptual
ms.date: 10/01/2018
ms.openlocfilehash: 0787663b0c2eccfed33bf5c2cc681be4f2ef5edc
ms.sourcegitcommit: 182d77997133a6e4ee71e7a64b4eed6609da0fba
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2018
ms.locfileid: "50050847"
---
# <a name="submit-spark-job-on-sql-server-big-data-clusters-in-azure-data-studio"></a>Enviar a trabajo de Spark en clústeres de macrodatos de SQL Server en Azure Data Studio

Uno de los escenarios claves es la capacidad de enviar el trabajo de Spark para SQL Server de 2019 CTP 2.0. La característica de envío de trabajos de Spark permite enviar archivos Jar o Py locales con las referencias al clúster de macrodatos de SQL Server 2019. También permite ejecutar archivos Jar o Py, ya se encuentran en el sistema de archivos HDFS. 

## <a name="prerequisite"></a>Requisito previo 
Instalar herramientas de macrodatos para SQL Server y conéctese a un clúster de macrodatos antes de poder enviar trabajo de Spark. Para obtener detalles de la instalación, consulte para vincular [implementar herramientas de macrodatos](deploy-big-data-tools.md).

## <a name="open-spark-job-submission-dialog"></a>Abrir cuadro de diálogo de envío de trabajos de Spark
Hay varias maneras de abrir el cuadro de diálogo de envío de trabajos de Spark. Las formas de incluyen el panel, menú contextual en el Explorador de objetos y la paleta de comandos.

+ Haga clic en **nuevo trabajo de Spark** en el panel para abrir el cuadro de diálogo de envío de trabajos de Spark.

    ![Envío de menú, haga clic en el panel ](./media/submit-spark-job/new-spark-job.png)
 
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

