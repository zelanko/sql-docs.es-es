---
title: Ejecución de trabajos de Spark con Spark & herramientas de Hive para VS Code en SQL Server clúster de macrodatos
titleSuffix: SQL Server big data clusters
description: Envíe un trabajo de Spark con las herramientas de Spark & Hive para Visual Studio Code en SQL Server clúster de macrodatos.
author: jejiang
ms.author: jejiang
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4458666792d7f4629b4e1820e98e2dbb9901c2b6
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68425985"
---
# <a name="submit-spark-jobs-on-sql-server-big-data-cluster-in-visual-studio-code"></a>Envío de trabajos de Spark en SQL Server clúster de Big Data en Visual Studio Code

Aprenda a usar las herramientas de Spark & Hive para Visual Studio Code para crear y enviar scripts de PySpark para Apache Spark. en primer lugar, describiremos cómo instalar las herramientas de Spark & Hive en Visual Studio Code y, a continuación, veremos cómo enviar trabajos a Spark.  

Spark & herramientas de Hive se puede instalar en plataformas compatibles con Visual Studio Code, entre las que se incluyen Windows, Linux y macOS. A continuación encontrará los requisitos previos de cada plataforma.


## <a name="prerequisites"></a>Requisitos previos

Para completar los pasos de este artículo, se requieren los elementos siguientes:

- Un clúster de macrodatos de SQL Server. Consulte [SQL Server](https://docs.microsoft.com/sql/big-data-cluster/big-data-cluster-overview?view=sqlallproducts-allversions)de clústeres de macrodatos.
- [Visual Studio Code](https://code.visualstudio.com/).
- [Mono](https://www.mono-project.com/docs/getting-started/install/). Mono solo es obligatorio para Linux y macOS.
- [Configuración del entorno interactivo de PySpark para Visual Studio Code](https://docs.microsoft.com/azure/hdinsight/set-up-pyspark-interactive-environment).
- Un directorio local llamado **HDexample**.  En este artículo se usa **C:\HD\HDexample**.

## <a name="install-spark--hive-tools"></a>Instalación de Spark & herramientas de Hive

Una vez que haya completado los requisitos previos, puede instalar Spark & herramientas de Hive para Visual Studio Code.  Complete los pasos siguientes para instalar Spark & herramientas de Hive:

1. Abra Visual Studio Code.

2. En la barra de menús, vaya a **Vista** > **Extensiones**.

3. En el cuadro de búsqueda, escriba **Spark & Hive**.

4. Seleccione **Spark & herramientas de Hive** en los resultados de la búsqueda y, a continuación, seleccione **instalar**.  

   ![Instalar extensión](./media/spark-hive-tools-vscode/extension.png)

5. Vuelva a cargar cuando sea necesario.

## <a name="open-work-folder"></a>Abrir carpeta de trabajo

Complete los pasos siguientes para abrir una carpeta de trabajo y cree un archivo en Visual Studio Code:

1. En la barra de menús, vaya a **Archivo** > **Abrir carpeta...**  > **C:\HD\HDexample** y, a continuación, seleccione el botón **Seleccionar carpeta**. La carpeta aparece en la vista **Explorador** a la izquierda.

2. En la vista **Explorador**, seleccione la carpeta, **HDexample** y, a continuación, el icono **Nuevo archivo** situado junto a la carpeta de trabajo.

   ![Nuevo archivo](./media/spark-hive-tools-vscode/new-file.png)

3. Asigne al nuevo archivo el nombre `.py` con la extensión de archivo (script de Spark).  En este ejemplo se usa **HelloWorld.py**.
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

## <a name="link-a-sql-server-big-data-cluster"></a>Vinculación de un clúster de macrodatos SQL Server

Antes de poder enviar scripts a los clústeres desde Visual Studio Code, debe vincular un clúster de Big Data SQL Server.

1. En la barra de menús, vaya a **Ver** > **paleta de comandos...** y escriba **Spark/Hive: Link a Cluster** (HDInsight: vincular un clúster).

   ![comando de clúster de vinculación](./media/spark-hive-tools-vscode/link-cluster-command.png)

2. Seleccione el tipo de clúster vinculado **SQL Server Big Data**.

3. Escriba SQL Server punto de conexión de Big Data.

4. Escriba SQL Server nombre de usuario del clúster de Big Data.

5. Escriba la contraseña del administrador de usuarios.

6. Establezca el nombre para mostrar del clúster (opcional).

7. Enumerar clústeres, revise la vista de **salida** para la comprobación.

## <a name="list-clusters"></a>Enumerar clústeres

1. En la barra de menús, vaya a **Ver** > **paleta de comandos...** y escriba **Spark/Hive: List Cluster** (HDInsight: enumeración de clústeres).

2. Revise la vista **SALIDA**.  La vista mostrará los clústeres vinculados.

    ![Establecer la configuración de un clúster predeterminado](./media/spark-hive-tools-vscode/list-cluster-result.png)

## <a name="set-default-cluster"></a>Establecer el clúster predeterminado

1. Vuelva a abrir la carpeta **HDexample** creada [anteriormente](#open-work-folder) si se ha cerrado.  

2. Seleccione el archivo **HelloWorld.py** creado [anteriormente](#open-work-folder) y se abrirá en el editor de scripts.

3. Vincular un clúster si todavía no lo ha hecho.

4. Haga clic con el botón derecho en el editor **de scripts y seleccione Spark/Hive: Set Default Cluster** (HDInsight: establecer el clúster predeterminado).   

5. Seleccione un clúster como clúster predeterminado del archivo de script actual. Las herramientas actualizan automáticamente el archivo de configuración **.VSCode\settings.json**. 

   ![Establecer la configuración de un clúster predeterminado](./media/spark-hive-tools-vscode/set-default-cluster-configuration.png)

## <a name="submit-interactive-pyspark-queries"></a>Envíe consultas de PySpark interactivas

Puede enviar consultas de PySpark interactivas siguiendo estos pasos:

1. Vuelva a abrir la carpeta **HDexample** creada [anteriormente](#open-work-folder) si se ha cerrado.  

2. Seleccione el archivo **HelloWorld.py** creado [anteriormente](#open-work-folder) y se abrirá en el editor de scripts.

3. Vincular un clúster si todavía no lo ha hecho.

4. Elija todo el código y haga clic con el botón derecho en el **editor de scripts, seleccione Spark: PySpark Interactive** (HDInsight: PySpark interactivo) para enviar la consulta, o bien use el acceso directo **Ctrl + Alt + I**.

   ![menú contextual interactivo de pyspark](./media/spark-hive-tools-vscode/pyspark-interactive-right-click.png)

5. Seleccione el clúster si no ha especificado un clúster predeterminado. Transcurridos unos instantes, los resultados interactivos de **Python** aparecen en una nueva pestaña. Las herramientas también permiten enviar un bloque de código, en lugar del archivo de script completo mediante el menú contextual. 

   ![ventana interactiva de Python interactiva pyspark](./media/spark-hive-tools-vscode/pyspark-interactive-python-interactive-window.png) 

6. Escriba **"%% info"** y, a continuación, presione **MAYÚS + entrar** para ver la información del trabajo. (Opcional)

   ![ver información del trabajo](./media/spark-hive-tools-vscode/pyspark-interactive-view-job-information.png)

   > [!NOTE] 
   >
   > Cuando la **extensión de Python habilitada** está desactivada en la configuración (la configuración predeterminada está activada), los resultados de interacción de pyspark enviados usarán la ventana anterior.
   >
   > ![extensión de Python interactiva de pyspark deshabilitada](./media/spark-hive-tools-vscode/pyspark-interactive-python-extension-disabled.png)


## <a name="submit-pyspark-batch-job"></a>Envío de un trabajo por lotes de PySpark

1. Vuelva a abrir la carpeta **HDexample** creada [anteriormente](#open-work-folder) si se ha cerrado.  

2. Seleccione el archivo **HelloWorld.py** creado [anteriormente](#open-work-folder) y se abrirá en el editor de scripts.

3. Vincular un clúster si todavía no lo ha hecho.

4. Haga clic con el botón derecho en el editor de **scripts y seleccione Spark: PySpark Batch** (HDInsight: lote de PySpark), o bien use el acceso directo **Ctrl + Alt + H**. 

5. Seleccione el clúster si no ha especificado un clúster predeterminado. Después de enviar un trabajo de Python, los registros de envío aparecen en la ventana **SALIDA** de Visual Studio Code. También se muestran la **dirección URL de interfaz de usuario de Spark** y la **dirección URL de interfaz de usuario de Yarn**. Puede abrir la dirección URL en un explorador web para realizar el seguimiento de estado del trabajo.

   ![Enviar el resultado del trabajo de Python](./media/spark-hive-tools-vscode/submit-pythonjob-result.png) 

## <a name="apache-livy-configuration"></a>Configuración de Apache Livy

Se admite la configuración de [Apache Livy](https://livy.incubator.apache.org/); se puede establecer en **.VSCode\settings.json** en la carpeta del área de trabajo. Actualmente, la configuración de Livy solo admite el script de Python. Para obtener más información, consulte el archivo [léame de Livy](https://github.com/cloudera/livy/blob/master/README.rst ).

### <a id="triggerlivyconf"></a>**Cómo desencadenar la configuración de Livy**

#### <a name="method-1"></a>Método 1

1. En la barra de menús, vaya a **Archivo** > **Preferencias** > **Configuración**.  
2. En el cuadro de texto **Configuración de la búsqueda** escriba **HDInsight Job Sumission: Livy Conf**. (Envío de trabajo de HDInsight: Livy Conf).  
3. Seleccione **Edit in settings.json** (Editar en settings.json) para el resultado de búsqueda pertinente.

#### <a name="method-2"></a>Método 2

Enviar un archivo, observe que `.vscode` la carpeta se agrega automáticamente a la carpeta de trabajo. Para encontrar la configuración de Livy, haga `.vscode\settings.json`clic en.

+ Configuración de proyecto:

    ![Configuración de Livy](./media/spark-hive-tools-vscode/hdi-livyconfig.png)

>[!NOTE]
>Para las opciones **driverMomory** y **executorMomry**, establezca el valor con la unidad, por ejemplo, 1 g o 1024 m. 

### <a name="supported-livy-configurations"></a>Configuraciones admitidas de Livy

#### <a name="post-batches"></a>POST/batches

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

#### <a name="response-body"></a>Cuerpo de respuesta

Objeto de lote creado.

| name | description | Tipo |
| :- | :- | :- |
| id | Identificador de sesión | int |
| appId | Identificador de la aplicación de esta sesión | string |
| appInfo | Información detallada de la aplicación | Asignación de clave = val |
| log | Líneas de registro | lista de cadenas |
| state | Estado de lote | string |

>[!NOTE]
>La configuración de Livy asignada se mostrará en el panel de salida cuando se envíe el script.

## <a name="additional-features"></a>Características adicionales

Spark & Hive para Visual Studio Code admite las siguientes características:

- Autocompletar de **IntelliSense**. Emergen sugerencias para la palabra clave, los métodos, las variables, etc. Los distintos iconos representan diferentes tipos de objetos.

    ![Herramientas de Spark & Hive para Visual Studio Code tipos de objetos de IntelliSense](./media/spark-hive-tools-vscode/hdinsight-for-vscode-auto-complete-objects.png)
- **Marcador de error de IntelliSense**. El servicio de lenguaje subraya los errores de edición del script de Hive.     
- **Aspectos destacados de la sintaxis**. El servicio de lenguaje usa colores diferentes para diferenciar las variables, palabras clave, tipos de datos, funciones, etc. 

    ![Características destacadas de la sintaxis de Spark & Hive Tools for Visual Studio Code](./media/spark-hive-tools-vscode/hdinsight-for-vscode-syntax-highlights.png)

## <a name="unlink-cluster"></a>Desvinculación del clúster

1. En la barra de menús, vaya a **Ver** > **paleta de comandos...** y **, a continuación, escriba Spark/Hive: Unlink a Cluster** (HDInsight: desvincular un clúster).  

2. Seleccione el clúster que desea desvincular.  

3. Revise la vista **SALIDA** para comprobarlo todo.  

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre SQL Server clúster de macrodatos y escenarios relacionados, consulte SQL Server de los clústeres de [Big Data](https://docs.microsoft.com/sql/big-data-cluster/big-data-cluster-overview?view=sqlallproducts-allversions).
