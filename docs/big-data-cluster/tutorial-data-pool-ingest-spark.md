---
title: Ingesta de datos con los trabajos de Spark
titleSuffix: SQL Server 2019 big data clusters
description: Este tutorial muestra cómo introducir datos en el grupo de datos de un clúster de macrodatos de 2019 de SQL Server (versión preliminar) mediante trabajos de Spark en Azure Data Studio.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/27/2018
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 1611a8b0513e8f1a9e50d3cc612b114c88698df5
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58491908"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-spark-jobs"></a>Tutorial: Introducir datos en un grupo de datos de SQL Server con trabajos de Spark

Este tutorial muestra cómo usar trabajos de Spark para cargar datos en el [grupo datos](concept-data-pool.md) de un clúster de macrodatos de 2019 de SQL Server (versión preliminar). 

En este tutorial, obtendrá información sobre cómo:

> [!div class="checklist"]
> * Crear una tabla externa en el grupo de datos.
> * Crear un trabajo de Spark para cargar datos desde HDFS.
> * Consultar los resultados en la tabla externa.

> [!TIP]
> Si lo prefiere, puede descargar y ejecutar un script para los comandos en este tutorial. Para obtener instrucciones, consulte el [ejemplos de grupos de datos](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool) en GitHub.

## <a id="prereqs"></a> Requisitos previos

- [Herramientas de datos de gran tamaño](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **Extensión de SQL Server 2019**
- [Cargar datos de ejemplo en el clúster de macrodatos](tutorial-load-sample-data.md)

## <a name="create-an-external-table-in-the-data-pool"></a>Crear una tabla externa en el grupo de datos

Los pasos siguientes crean una tabla externa en el grupo de datos llamado **web_clickstreams_spark_results**. Esta tabla, a continuación, se utiliza como una ubicación para la ingesta de datos en el clúster de macrodatos.

1. En Azure Data Studio, conéctese a la instancia principal de SQL Server del clúster de macrodatos. Para obtener más información, consulte [conectar a la instancia principal de SQL Server](connect-to-big-data-cluster.md#master).

1. Haga doble clic en la conexión en el **servidores** ventana para mostrar el panel del servidor para la instancia principal de SQL Server. Seleccione **nueva consulta**.

   ![Consulta de la instancia principal de SQL Server](./media/tutorial-data-pool-ingest-spark/sql-server-master-instance-query.png)

1. Crear un origen de datos externo para el grupo de datos si aún no existe.

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
     CREATE EXTERNAL DATA SOURCE SqlDataPool
     WITH (LOCATION = 'sqldatapool://service-mssql-controller:8080/datapools/default');
   ```

1. Crear una tabla externa denominada **web_clickstreams_spark_results** en el grupo de datos.

   ```sql
   USE Sales
   GO
   IF NOT EXISTS(SELECT * FROM sys.external_tables WHERE name = 'web_clickstreams_spark_results')
      CREATE EXTERNAL TABLE [web_clickstreams_spark_results]
      ("wcs_click_date_sk" BIGINT , "wcs_click_time_sk" BIGINT , "wcs_sales_sk" BIGINT , "wcs_item_sk" BIGINT , "wcs_web_page_sk" BIGINT , "wcs_user_sk" BIGINT)
      WITH
      (
         DATA_SOURCE = SqlDataPool,
         DISTRIBUTION = ROUND_ROBIN
      );
   ```
  
1. En CTP 2.4, la creación del grupo de datos es asincrónica, pero no hay ninguna manera de determinar si aún termina. Espere dos minutos para asegurarse de que se crea el grupo de datos antes de continuar.

## <a name="start-a-spark-streaming-job"></a>Iniciar un trabajo de streaming de Spark

El siguiente paso es crear un trabajo de Spark streaming que carga los datos de secuencia de clics de web del grupo de almacenamiento (HDFS) en la tabla externa que creó en el grupo de datos.

1. En Azure Data Studio, conéctese a la **puerta de enlace de Spark o HDFS** del clúster de macrodatos. Para obtener más información, consulte [conectar con la puerta de enlace de Spark o HDFS](connect-to-big-data-cluster.md#hdfs).

1. Haga doble clic en la conexión de puerta de enlace de Spark o HDFS en el **servidores** ventana. A continuación, seleccione **nuevo trabajo de Spark**.

   ![Nuevo trabajo de Spark](media/tutorial-data-pool-ingest-spark/hdfs-new-spark-job.png)

1. En el **nuevo trabajo** ventana, escriba un nombre en el **nombre del trabajo** campo.

1. En el **archivo Jar/py** lista desplegable, seleccione **HDFS**. A continuación, escriba la ruta del archivo jar siguiente:

   ```text
   /jar/mssql-spark-lib-assembly-1.0.jar
   ```

1. En el **clase principal** , introduzca `FileStreaming`.

1. En el **argumentos** , escriba el texto siguiente, especificando la contraseña a la instancia principal de SQL Server en el `<your_password>` marcador de posición. 

   ```text
   --server mssql-master-pool-0.service-master-pool --port 1433 --user sa --password <your_password> --database sales --table web_clickstreams_spark_results --source_dir hdfs:///clickstream_data --input_format csv --enable_checkpoint false --timeout 380000
   ```

   La tabla siguiente describe cada argumento:

   | Argumento | Descripción |
   |---|---|
   | nombre de servidor | Uso de SQL Server para leer el esquema de tabla |
   | número de puerto | Puerto de SQL Server está escuchando en (predeterminado: 1433) |
   | username | Nombre de usuario de inicio de sesión de SQL Server |
   | password | Contraseña de inicio de sesión de SQL Server |
   | El nombre de la base de datos | Base de datos de destino |
   | nombre de tabla externa | Tabla que se usará para los resultados |
   | Directorio de origen para streaming | Esto debe ser un URI completo, como "hdfs: / / / clickstream_data" |
   | formato de entrada | Esto puede ser "csv", "parquet" o "json" |
   | Habilitar punto de control | true o false |
   | timeout | tiempo para ejecutar el trabajo para en milisegundos antes de salir |

1. Presione **enviar** para enviar el trabajo.

   ![Envío de trabajos de Spark](media/tutorial-data-pool-ingest-spark/spark-new-job-settings.png)

## <a name="query-the-data"></a>Consultar los datos

Los pasos siguientes muestran que el trabajo de streaming de Spark había cargado los datos de HDFS en el grupo de datos.

1. Antes de consultar los datos ingeridos, examine la salida del historial de tareas para ver el trabajo se completó.

   ![Historial de trabajos de Spark](media/tutorial-data-pool-ingest-spark/spark-task-history.png)

1. Volver a la ventana de consulta de instancia principal de SQL Server que abrió al principio de este tutorial.

1. Ejecute la siguiente consulta para inspeccionar los datos ingeridos.

   ```sql
   USE Sales
   GO
   SELECT count(*) FROM [web_clickstreams_spark_results];
   SELECT TOP 10 * FROM [web_clickstreams_spark_results];
   ```

## <a name="clean-up"></a>Limpiar

Use el siguiente comando para quitar los objetos de base de datos creados en este tutorial.

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstreams_spark_results];
```

## <a name="next-steps"></a>Pasos siguientes

Obtenga información sobre cómo ejecutar un cuaderno de ejemplo en Azure Data Studio:
> [!div class="nextstepaction"]
> [Ejecutar un cuaderno de ejemplo](tutorial-notebook-spark.md)
