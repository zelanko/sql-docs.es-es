---
title: Ejecución de trabajos de Spark con Spark & Hive Tools para VS Code en un clúster de macrodatos de SQL Server
titleSuffix: SQL Server big data clusters
description: Envíe trabajos de Spark con Spark & Hive Tools para Visual Studio Code en un clúster de macrodatos de SQL Server.
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b09a5febe9bc67f04d70c4d5b7850ef26ebac750
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653728"
---
# <a name="submit-spark-jobs-on-sql-server-big-data-cluster-in-visual-studio-code"></a>Envío de trabajos de Spark en un clúster de macrodatos de SQL Server en Visual Studio Code

Obtenga información sobre cómo usar Spark & Hive Tools para Visual Studio Code para crear y enviar scripts de PySpark para Apache Spark; primero, describiremos cómo instalar Spark & Hive Tools en Visual Studio Code y, después, explicaremos cómo enviar trabajos a Spark.  

Spark & Hive Tools se puede instalar en las plataformas compatibles con Visual Studio Code, que son Windows, Linux y macOS. A continuación, encontrará los requisitos previos para las diferentes plataformas.


## <a name="prerequisites"></a>Requisitos previos

Los elementos siguientes son necesarios para completar los pasos indicados en este artículo:

- Un clúster de macrodatos de SQL Server. Vea [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](https://docs.microsoft.com/sql/big-data-cluster/big-data-cluster-overview?view=sqlallproducts-allversions).
- [Visual Studio Code](https://code.visualstudio.com/).
- [Mono](https://www.mono-project.com/docs/getting-started/install/). Mono solo es necesario para Linux y macOS.
- [Configuración del entorno interactivo de PySpark para Visual Studio Code](https://docs.microsoft.com/azure/hdinsight/set-up-pyspark-interactive-environment).
- Un directorio local denominado **SQLBDCexample**.  En este artículo se usa **C:\SQLBDC\SQLBDCexample**.

## <a name="install-spark--hive-tools"></a>Instalar Spark & Hive Tools

Después de completar los requisitos previos, puede instalar Spark & Hive Tools para Visual Studio Code.  Siga este procedimiento para instalar Spark & Hive Tools:

1. Abra Visual Studio Code.

2. En la barra de menús, vaya a **Ver** > **Extensiones**.

3. En el cuadro de búsqueda, escriba **Spark & Hive**.

4. En los resultados de la búsqueda, seleccione **Spark & Hive Tools** y, después, seleccione **Instalar**.  

   ![Instalar la extensión](./media/spark-hive-tools-vscode/extension.png)

5. Si es necesario, vuelva a cargar la aplicación.

## <a name="open-work-folder"></a>Abrir la carpeta de trabajo

Complete los pasos siguientes para abrir una carpeta de trabajo y cree un archivo en Visual Studio Code:

1. En la barra de menús, vaya a **archivo** > **Abrir carpeta...** C:\SQLBDC\SQLBDCexample y, a continuación, seleccione el botón **Seleccionar carpeta** .  >  La carpeta aparece en la vista **Explorador** a la izquierda.

2. En la vista **Explorador** , seleccione la carpeta **SQLBDCexample**y, a continuación, el icono **nuevo archivo** situado junto a la carpeta de trabajo.

   ![Nuevo archivo](./media/spark-hive-tools-vscode/new-file.png)

3. Asigne un nombre al nuevo archivo con la extensión de archivo `.py` (script de Spark).  En este ejemplo, se usa **HelloWorld.py**.
4. Copie y pegue el código siguiente en el archivo de script:
   ```python
    import sys
    from operator import add
    from pyspark.sql import SparkSession, Row
    
    spark = SparkSession\
        .builder\
        .appName("PythonWordCount")\
        .getOrCreate()
    
    data = [Row(col1='pyspark and spark', col2=1), Row(col1='pyspark', col2=2), Row(col1='spark vs hadoop', col2=2), Row(col1='spark', col2=2), Row(col1='hadoop', col2=2)]
    df = spark.createDataFrame(data)
    lines = df.rdd.map(lambda r: r[0])

    counters = lines.flatMap(lambda x: x.split(' ')) \
        .map(lambda x: (x, 1)) \
        .reduceByKey(add)
    
    output = counters.collect()
    sortedCollection = sorted(output, key = lambda r: r[1], reverse = True)
    
    for (word, count) in sortedCollection:
        print("%s: %i" % (word, count))
   ```

## <a name="link-a-sql-server-big-data-cluster"></a>Vincular un clúster de macrodatos de SQL Server

Antes de enviar scripts a los clústeres desde Visual Studio Code, necesita vincular un clúster de macrodatos de SQL Server.

1. En la barra de menús, vaya a **Ver** > **Paleta de comandos…** y escriba **Spark/Hive: Link a Cluster** (vincular un clúster).

   ![comando para vincular un clúster](./media/spark-hive-tools-vscode/link-cluster-command.png)

2. Seleccione el tipo de clúster vinculado **Macrodatos de SQL Server**.

3. Especifique el punto de conexión de macrodatos de SQL Server.

4. Especifique el nombre de usuario del clúster de macrodatos de SQL Server.

5. Escriba la contraseña del administrador de usuarios.

6. Establezca el nombre para mostrar del clúster (opcional).

7. Muestre una lista de los clústeres y revise la vista **SALIDA**.

## <a name="list-clusters"></a>Lista de clústeres

1. En la barra de menús, vaya a **Ver** > **Paleta de comandos…** y escriba **Spark/Hive: List Cluster** (lista de clústeres).

2. Revise la ventana de **SALIDA**.  En la vista, se muestran los clústeres vinculados.

    ![Establecer una configuración de clúster predeterminado](./media/spark-hive-tools-vscode/list-cluster-result.png)

## <a name="set-default-cluster"></a>Establecer el clúster predeterminado

1. Vuelva a abrir la carpeta **SQLBDCexample** creada [anteriormente](#open-work-folder) si está cerrada.  

2. Seleccione el archivo **HelloWorld.py** que ha creado [anteriormente](#open-work-folder) para abrirlo en el editor de scripts.

3. Si aún no lo ha hecho, vincule un clúster.

4. Haga clic con el botón derecho en el editor de scripts y seleccione **Spark/Hive: Set Default Cluster** (establecer clúster predeterminado).   

5. Seleccione un clúster como clúster predeterminado del archivo de script actual. Las herramientas actualizan automáticamente el archivo de configuración **.VSCode\settings.json**. 

   ![Establecer la configuración del clúster predeterminado](./media/spark-hive-tools-vscode/set-default-cluster-configuration.png)

## <a name="submit-interactive-pyspark-queries"></a>Enviar consultas de PySpark interactivas

Para enviar consultas de PySpark interactivas, siga este procedimiento:

1. Vuelva a abrir la carpeta **SQLBDCexample** creada [anteriormente](#open-work-folder) si está cerrada.  

2. Seleccione el archivo **HelloWorld.py** que ha creado [anteriormente](#open-work-folder) para abrirlo en el editor de scripts.

3. Si aún no lo ha hecho, vincule un clúster.

4. Seleccione todo el código, haga clic con el botón derecho en el editor de scripts y seleccione **Spark: PySpark Interactive** (PySpark interactivo) para enviar la consulta, o bien use el método abreviado de teclado **Ctrl + Alt + I**.

   ![menú contextual de PySpark Interactive](./media/spark-hive-tools-vscode/pyspark-interactive-right-click.png)

5. Si aún no ha especificado un clúster predeterminado, seleccione el clúster. En un momento, los resultados de **Python Interactive** se mostrarán en una pestaña nueva. Las herramientas también le permiten enviar un bloque de código, en lugar de todo el archivo de script, mediante el menú contextual. 

   ![ventana de Python Interactive de PySpark Interactive](./media/spark-hive-tools-vscode/pyspark-interactive-python-interactive-window.png) 

6. Escriba **“%%info”** y, después, presione **Mayús + Entrar** para ver la información del trabajo. (Opcional)

   ![ver la información del trabajo](./media/spark-hive-tools-vscode/pyspark-interactive-view-job-information.png)

   > [!NOTE] 
   >
   > Si la opción **Python Extension Enabled** (Extensión de Python habilitada) está desactivada en la configuración (de forma predeterminada, esta opción está activada), los resultados de la interacción de PySpark enviados se mostrarán en la ventana anterior.
   >
   > ![extensión de Python de PySpark Interactive deshabilitada](./media/spark-hive-tools-vscode/pyspark-interactive-python-extension-disabled.png)


## <a name="submit-pyspark-batch-job"></a>Envío de un trabajo por lotes de PySpark

1. Vuelva a abrir la carpeta **SQLBDCexample** creada [anteriormente](#open-work-folder) si está cerrada.  

2. Seleccione el archivo **HelloWorld.py** que ha creado [anteriormente](#open-work-folder) para abrirlo en el editor de scripts.

3. Si aún no lo ha hecho, vincule un clúster.

4. Haga clic con el botón derecho en el editor de scripts y, después, seleccione **Spark: PySpark Batch** (lote de PySpark), o bien use el método abreviado de teclado **Ctrl + Alt + H**. 

5. Si aún no ha especificado un clúster predeterminado, seleccione el clúster. Después de enviar trabajo de Python, los registros de envío se muestran en la ventana de **SALIDA** en Visual Studio Code. También se muestran la **dirección URL de interfaz de usuario de Spark** y la **dirección URL de interfaz de usuario de Yarn**. Para realizar un seguimiento del estado del trabajo, puede abrir la URL en un explorador web.

   ![Enviar el resultado de un trabajo de Python](./media/spark-hive-tools-vscode/submit-pythonjob-result.png) 

## <a name="apache-livy-configuration"></a>Configuración de Apache Livy

Se admite la configuración de [Apache Livy](https://livy.incubator.apache.org/), que puede configurarse en el archivo **.VSCode\settings.json** de la carpeta del área de trabajo. Actualmente, la configuración de Livy solo admite scripts de Python. Para obtener más información, vea [Livy README](https://github.com/cloudera/livy/blob/master/README.rst ) (LÉAME de Livy).

### <a id="triggerlivyconf"></a>**Procedimiento para desencadenar la configuración de Livy**

#### <a name="method-1"></a>Método 1

1. En la barra de menús, vaya a **Archivo** > **Preferencias** > **Configuración**.  
2. En el cuadro de texto **Configuración de la búsqueda** escriba **HDInsight Job Sumission: Livy Conf**. (Envío de trabajo de HDInsight: Livy Conf).  
3. Seleccione **Edit in settings.json** (Editar en settings.json) para el resultado de búsqueda pertinente.

#### <a name="method-2"></a>Método 2

Envíe un archivo; la carpeta `.vscode` se agregará automáticamente a la carpeta de trabajo. Para encontrar la configuración de Livy, haga clic en `.vscode\settings.json`.

+ Configuración del proyecto:

    ![Configuración de Livy](./media/spark-hive-tools-vscode/hdi-livyconfig.png)

>[!NOTE]
>En el caso de las opciones **driverMomory** y **executorMomry**, establezca el valor con una unidad (por ejemplo, “1g” o “1024m”). 

### <a name="supported-livy-configurations"></a>Configuraciones de Livy admitidas

#### <a name="post-batches"></a>POST /batches

**Cuerpo de la solicitud**

| name | description | Tipo |
| :- | :- | :- |
| file | Archivo que contiene la aplicación para ejecutar | ruta de acceso (obligatorio) |
| proxyUser | Usuario para suplantar cuando se ejecuta el trabajo | string |
| className | Clase principal de Spark o Java de la aplicación | string |
| args | Argumentos de la línea de comandos para la aplicación | lista de cadenas |
| jars | Archivos JAR que se usarán en esta sesión | Lista de cadenas |
| pyFiles | Archivos Python que se usarán en esta sesión | Lista de cadenas |
| files | Archivos que se usarán en esta sesión | Lista de cadenas |
| driverMemory | Cantidad de memoria que se usará para el proceso de controlador | string |
| driverCores | Número de núcleos que se usarán para el proceso de controlador | int |
| executorMemory | Cantidad de memoria que se usará por proceso ejecutor | string |
| executorCores | Número de núcleos que se usarán para cada ejecutor | int |
| numExecutors | Número de ejecutores para iniciar en esta sesión | int |
| archives | Archivos que se usarán en esta sesión | Lista de cadenas |
| queue | El nombre de la cola YARN a la que se envió | string |
| name | Nombre de esta sesión | string |
| conf | Propiedades de configuración de Spark. | Asignación de clave = val |

#### <a name="response-body"></a>Cuerpo de la respuesta

Objeto por lotes creado.

| name | description | Tipo |
| :- | :- | :- |
| id | Identificador de sesión | int |
| appId | Identificador de la aplicación de esta sesión | string |
| appInfo | Información detallada de la aplicación | Asignación de clave = val |
| log | Líneas de registro | lista de cadenas |
| state | Estado de lote | string |

>[!NOTE]
>La configuración de Livy asignada se mostrará en el panel de resultados al enviar el script.

## <a name="additional-features"></a>Características adicionales

Spark & Hive para Visual Studio Code admite las características siguientes:

- **Autocompletar de IntelliSense**. Emergen sugerencias para la palabra clave, los métodos, las variables, etc. Se representan diferentes tipos de objetos con distintos iconos.

    ![Tipos de objetos de IntelliSense en Spark & Hive Tools para Visual Studio Code](./media/spark-hive-tools-vscode/hdinsight-for-vscode-auto-complete-objects.png)
- **Marcador de error de IntelliSense**. El servicio de lenguaje subraya los errores de edición del script de Hive.     
- **Aspectos destacados de la sintaxis**. El servicio de lenguaje usa distintos colores para diferenciar variables, palabras clave, tipos de datos, funciones, etc. 

    ![Sintaxis resaltada de Spark & Hive Tools para Visual Studio Code](./media/spark-hive-tools-vscode/hdinsight-for-vscode-syntax-highlights.png)

## <a name="unlink-cluster"></a>Desvincular clúster

1. En la barra de menús, vaya a **Ver** > **Paleta de comandos…** y escriba **Spark/Hive: desvincular un clúster**.  

2. Seleccione el clúster que desea desvincular.  

3. Revise la vista **SALIDA**.  

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre SQL Server clúster de macrodatos y escenarios relacionados [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](https://docs.microsoft.com/sql/big-data-cluster/big-data-cluster-overview?view=sqlallproducts-allversions), vea.
