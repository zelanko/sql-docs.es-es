---
title: Ejecutar trabajos de Spark en el Kit de herramientas de Azure para IntelliJ en clúster de macrodatos de SQL Server
titleSuffix: SQL Server big data clusters
description: Envío de trabajos de Spark en clústeres de macrodatos de SQL Server en el Kit de herramientas de Azure para IntelliJ.
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e48aebbb15b9bd684b2ed3f5d4d314191a55ba42
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59932302"
---
# <a name="submit-spark-jobs-on-sql-server-big-data-clusters-in-intellij"></a>Enviar trabajos de Spark en clústeres de macrodatos de SQL Server en IntelliJ

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Uno de los escenarios claves para los clústeres de macrodatos de SQL Server es la capacidad para enviar trabajos de Spark. La característica de envío de trabajos de Spark permite enviar archivos Jar o Py locales con referencias a los clústeres de macrodatos de SQL Server. También permite ejecutar archivos Jar o Py, ya se encuentran en el sistema de archivos HDFS. 

## <a name="prerequisites"></a>Requisitos previos

- Clúster de macrodatos de SQL Server.
- Kit de desarrollo de Java de Oracle. Puede instalarlo desde el [sitio Web de Oracle](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
- IntelliJ IDEA. Puede instalarlo desde el [sitio Web de JetBrains](https://www.jetbrains.com/idea/download/).
- Azure Toolkit for IntelliJ extension. Para obtener instrucciones de instalación, consulte [instalar Azure Toolkit for IntelliJ](https://docs.microsoft.com/azure/azure-toolkit-for-intellij-installation).

## <a name="link-sql-server-big-data-cluster"></a>Clúster de macrodatos de SQL Server de vínculo
1. Abra la herramienta de IntelliJ IDEA.

2. Si usa un certificado autofirmado, deshabilitar la validación del certificado SSL de **herramientas** menú, seleccione **Azure**, **validar un certificado de SSL de clúster de Spark**, entonces  **Deshabilitar**.

    ![vincular el clúster de macrodatos de SQL Server: deshabilitar SSL](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-disableSSL.png)

3. Abra el Explorador de Azure desde **vista** menú, seleccione **herramienta Windows**y, a continuación, seleccione **Azure Explorer**.
4. Haga clic con el botón derecho en **clúster de SQL Server macrodatos**, seleccione **clúster de macrodatos de vínculo de SQL Server**. Escriba el **Server**, **nombre de usuario**, y **contraseña**, a continuación, haga clic en **Aceptar**.

    ![vincular el clúster de Big Data: cuadro de diálogo](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-dialog.png)

5. Cuando aparezca el cuadro de diálogo de certificado de confianza del servidor, haga clic en **Accept**. Puede administrar el certificado más adelante, consulte [certificados de servidor](https://www.jetbrains.com/help/idea/settings-tools-server-certificates.html).

6. Enumera el clúster vinculado en **clúster grande de datos de SQL Server**. Puede supervisar el trabajo de spark abriendo el historial de spark la interfaz de usuario y la interfaz de usuario de Yarn, también puede desvincular, haciendo clic en el clúster.

    ![clúster de Macrodatos - menú contextual del vínculo](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-contextmenu.png)

## <a name="create-a-spark-scala-application-from-hdinsight-template"></a>Crear una aplicación Scala Spark de HDInsight plantilla

1. Inicie IntelliJ IDEA y, a continuación, cree un proyecto. En el **nuevo proyecto** cuadro de diálogo, siga estos pasos: 

   a. Seleccione **Azure Spark/HDInsight** > **despierte el proyecto con ejemplos (Scala)**.

   b. En el **herramienta de compilación** lista, seleccione cualquiera de las siguientes, según sus necesidades:

      * **Maven**, para compatibilidad con el Asistente para crear un proyecto Scala
      * **SBT**, para administrar las dependencias y compilar el proyecto de Scala

    ![El cuadro de diálogo nuevo proyecto](./media/spark-submit-job-intellij-tool-plugin/create-hdi-scala-app.png)

2. Seleccione **Siguiente**.

3. El Asistente para crear un proyecto de Scala detecta automáticamente si ha instalado el complemento Scala. Seleccione **Instalar**.

   ![Comprobación de complemento de scala](./media/spark-submit-job-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. Para descargar el complemento de Scala, seleccione **Aceptar**. Siga las instrucciones para reiniciar IntelliJ. 

   ![El cuadro de diálogo de instalación de complemento de Scala](./media/spark-submit-job-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. En el **nuevo proyecto** ventana, realice los pasos siguientes:  

    ![Selección del SDK de Spark](./media/spark-submit-job-intellij-tool-plugin/hdi-new-project.png)

   a. Escriba un nombre de proyecto y una ubicación.

   b. En el **SDK de proyecto** lista desplegable, seleccione **Java 1.8** para el clúster Spark 2.x, o bien **Java 1.7** para el clúster Spark 1.x.

   c. En el **versión Spark** lista desplegable, el Asistente para crear un proyecto Scala integra la versión correcta de SDK de Spark y el SDK de Scala. Si la versión del clúster de Spark es anterior a 2.0, seleccione **Spark 1.x**. En caso contrario, seleccione **Spark2.x**. Este ejemplo se utiliza **Spark 2.0.2 (Scala 2.11.8)**.

6. Seleccione **Finalizar**.

7. El proyecto Spark creará automáticamente un artefacto para usted. Para ver el artefacto, siga los pasos siguientes:

   a. En el **archivo** menú, seleccione **estructura del proyecto**.

   b. En el **estructura del proyecto** cuadro de diálogo, seleccione **artefactos** para ver el artefacto predeterminado que se crea. También puede crear su propio artefacto seleccionando el signo más (**+**).

      ![Información de artefacto en el cuadro de diálogo](./media/spark-submit-job-intellij-tool-plugin/default-artifact.png)
      

## <a name="submit-application-to-sql-server-big-data-cluster"></a>Enviar la aplicación en clúster de macrodatos de SQL Server
Después de vincular un clúster de macrodatos de SQL Server, puede enviar la aplicación en él.

1. Establezca la configuración en **ejecutar/depurar configuraciones** ventana, haga clic en + ->**Apache Spark en SQL Server**, seleccione ficha **ejecutar de forma remota en clúster**, establezca los parámetros como después, haga clic en Aceptar.

    ![Consola interactiva Agregar entrada de configuración](./media/spark-submit-job-intellij-tool-plugin/interactive-console-add-config-entry.png)

    ![vincular el clúster de Macrodatos - config](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-config.png)

    * Para **(solo Linux) de clústeres de Spark**, seleccione el clúster en el que desea ejecutar la aplicación.

    * Seleccione un artefacto del proyecto IntelliJ o seleccione uno en la unidad de disco duro.

    * **Nombre de la clase principal** campo: El valor predeterminado es la clase principal del archivo seleccionado. Puede cambiar la clase seleccionando el botón de puntos suspensivos (**...** ) y elija otra clase.   

    * **Las configuraciones de trabajo** campo:  Los valores predeterminados se establecen como imagen mostrado anteriormente. Puede cambiar el valor o agregar nuevos pares clave-valor para el envío de trabajos. Para obtener más información: [Livy API de REST de Apache](http://livy.incubator.apache.org./docs/latest/rest-api.html)

      ![El significado de configuración de envío de Spark diálogo cuadro trabajo](./media/spark-submit-job-intellij-tool-plugin/submit-job-configurations.png)

    * **Argumentos de línea de comandos** campo: Puede especificar los valores de argumentos que se divide por un espacio para la clase principal, si es necesario.

    * **Hace referencia a archivos JAR** y **hace referencia a archivos** campos: Puede especificar las rutas de acceso para los archivos y los archivos JAR que se hace referencia si existe. Para obtener más información: [Configuración de Apache Spark](https://spark.apache.org/docs/latest/configuration.html#runtime-environment) 

      ![Lo que significa que los archivos jar de envío de Spark diálogo cuadro](./media/spark-submit-job-intellij-tool-plugin/jar-files-meaning.png)

       > [!NOTE]  
       > Para cargar los archivos al que hace referencia y los archivos JAR de al que hace referencia, consulte: [Cómo cargar recursos de clúster](https://docs.microsoft.com/azure/storage/blobs/storage-quickstart-blobs-storage-explorer)
                         
    * **Ruta de acceso carga**: Puede indicar la ubicación de almacenamiento para el envío de los recursos del proyecto Jar o Scala. Hay varios tipos de almacenamiento compatibles: **Usar sesión interactiva de Spark para cargar** y **WebHDFS de uso para cargar**
    
2. Haga clic en **SparkJobRun** para enviar el proyecto para el clúster seleccionado. El **trabajo de Spark remoto en clúster** pestaña muestra el progreso de ejecución del trabajo en la parte inferior. Puede detener la aplicación, haga clic en el botón rojo.  

    ![clúster de Big Data Link - ejecutar](./media/spark-submit-job-intellij-tool-plugin/link-ariscluster-run.png)

## <a name="spark-console"></a>Consola de Spark
Puede ejecutar Spark Local Console(Scala) o ejecutar Console(Scala) de sesión interactivas de Spark Livy.

### <a name="spark-local-consolescala"></a>Console(Scala) Local de Spark
Asegúrese de que haber satisfecho el WINUTILS. Requisito previo EXE.

1. En la barra de menús, vaya a **ejecutar** > **editar configuraciones...** .

2. Desde el **ejecutar/depurar configuraciones** ventana, en el panel izquierdo, vaya a **Apache Spark en el clúster de SQL Server macrodatos** > **myApp [Spark en SQL]**.

3. En la ventana principal, seleccione el **ejecutar localmente** ficha.

4. Proporcione los valores siguientes y, a continuación, seleccione **Aceptar**:

    |Property |Valor |
    |----|----|
    |Clase principal del trabajo|El valor predeterminado es la clase principal del archivo seleccionado. Puede cambiar la clase seleccionando el botón de puntos suspensivos (**...** ) y elija otra clase.|
    |Variables de entorno|Asegúrese de que el valor de HADOOP_HOME es correcto.|
    |Ubicación de WINUTILS.exe|Asegúrese de que la ruta de acceso es correcta.|

    ![Configuración de la consola local](./media/spark-submit-job-intellij-tool-plugin/console-set-configuration.png)

5. En el proyecto, vaya a **myApp** > **src** > **principal** > **scala**  >  **myApp**.  

6. En la barra de menús, vaya a **herramientas** > **Spark consola** > **ejecutar Spark Local Console(Scala)**.

7. A continuación, pueden aparecer dos cuadros de diálogo para preguntar si desea auto corregir las dependencias. Si es así, seleccione **Autocorregir**.

    ![Fix1 automático de Spark](./media/spark-submit-job-intellij-tool-plugin/console-auto-fix1.png)

    ![Fix2 automático de Spark](./media/spark-submit-job-intellij-tool-plugin/console-auto-fix2.png)

8. La consola debe ser similar a la siguiente imagen. En el tipo de ventana de consola `sc.appName`y, a continuación, presione ctrl + ENTRAR.  Se mostrará el resultado. Puede finalizar la consola local, haga clic en el botón rojo.

    ![Resultado de la consola local](./media/spark-submit-job-intellij-tool-plugin/local-console-result.png)


### <a name="spark-livy-interactive-session-consolescala"></a>Spark Console(Scala) sesión interactiva de Livy
Solo se admite la Console(Scala) de sesión de Spark interactiva de Livy en IntelliJ 2018.2 y 2018.3.

1. En la barra de menús, vaya a **ejecutar** > **editar configuraciones...** .

2. Desde el **ejecutar/depurar configuraciones** ventana, en el panel izquierdo, vaya a **Apache Spark en el clúster de SQL Server macrodatos** > **myApp [Spark en SQL]**.

3. En la ventana principal, seleccione el **ejecutar de forma remota en clúster** ficha.

4. Proporcione los valores siguientes y, a continuación, seleccione **Aceptar**:

    |Property |Valor |
    |----|----|
    |Clústeres de Spark (solo Linux)|Seleccione el clúster de SQL Server Big Data en el que desea ejecutar la aplicación.|
    |Nombre de la clase principal|El valor predeterminado es la clase principal del archivo seleccionado. Puede cambiar la clase seleccionando el botón de puntos suspensivos (**...** ) y elija otra clase.|

    ![Configuración de la consola interactiva](./media/spark-submit-job-intellij-tool-plugin/interactive-console-configuration.png)

5. En el proyecto, vaya a **myApp** > **src** > **principal** > **scala**  >  **myApp**.  

6. En la barra de menús, vaya a **herramientas** > **Spark consola** > **Console(Scala) de sesión interactiva de Livy de Spark de ejecutar**.

7. La consola debe ser similar a la siguiente imagen. En el tipo de ventana de consola `sc.appName`y, a continuación, presione ctrl + ENTRAR.  Se mostrará el resultado. Puede finalizar la consola local, haga clic en el botón rojo.

    ![Resultado de la consola interactiva](./media/spark-submit-job-intellij-tool-plugin/interactive-console-result.png)

### <a name="send-selection-to-spark-console"></a>Enviar selección a la consola de Spark

Para mayor comodidad, puede ver el resultado del script mediante el envío de código a la consola Local o Console(Scala) sesión interactiva de Livy. Puede resaltar el código en el archivo de Scala y luego haga clic en **Enviar selección a la consola de Spark**. El código seleccionado se enviarán a la consola y se puede realizar. El resultado se mostrará después del código en la consola. La consola comprobará los errores si existentes.  

   ![Enviar selección a la consola de Spark](./media/spark-submit-job-intellij-tool-plugin/send-selection-to-console.png)

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre los escenarios relacionados y clúster de macrodatos de SQL Server, vea [¿cuáles son los clústeres de SQL Server 2019 macrodatos](big-data-cluster-overview.md)?
