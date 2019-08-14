---
title: Ingestión de datos con trabajos de Spark
titleSuffix: SQL Server big data clusters
description: En este tutorial, se muestra cómo ingerir datos en el grupo de datos de un clúster de macrodatos de SQL Server 2019 (versión preliminar) con trabajos de Spark en Azure Data Studio.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: shivsood
ms.date: 06/26/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6d0ea6d4fb7a3aea9788c089ad68cb3bf523837f
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67957816"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-spark-jobs"></a>Tutorial: Ingestión de datos en un grupo de datos de SQL Server con trabajos de Spark

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este tutorial, se muestra cómo usar trabajos de Spark para cargar datos en el [grupo de datos](concept-data-pool.md) de un clúster de macrodatos de SQL Server 2019 (versión preliminar). 

En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Crear una tabla externa en el grupo de datos.
> * Crea un trabajo de Spark para cargar datos desde HDFS.
> * Consultar los resultados en la tabla externa.

> [!TIP]
> Si lo prefiere, puede descargar y ejecutar un script con los comandos de este tutorial. Para obtener instrucciones, vea los [Ejemplos de grupos de datos](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool) en GitHub.

## <a id="prereqs"></a> Requisitos previos

- [Herramientas de macrodatos](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **Extensión de SQL Server 2019**
- [Cargar datos de ejemplo en un clúster de macrodatos](tutorial-load-sample-data.md)

## <a name="create-an-external-table-in-the-data-pool"></a>Crear una tabla externa en el grupo de datos

Siga este procedimiento para crear una tabla externa en el grupo de datos denominada **web_clickstreams_spark_results**. Después, esta tabla se puede usar como una ubicación para ingerir datos en el clúster de macrodatos.

1. En Azure Data Studio, conéctese a la instancia maestra de SQL Server del clúster de macrodatos. Para obtener más información, vea [Conectarse a una instancia maestra de SQL Server](connect-to-big-data-cluster.md#master).

1. Haga doble clic en la conexión de la ventana **Servidores** para mostrar el panel del servidor de la instancia maestra de SQL Server. Seleccione **Nueva consulta**.

   ![Consultar una instancia maestra de SQL Server](./media/tutorial-data-pool-ingest-spark/sql-server-master-instance-query.png)

1. Cree un origen de datos externo al grupo de datos (si aún no existe).

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
     CREATE EXTERNAL DATA SOURCE SqlDataPool
     WITH (LOCATION = 'sqldatapool://controller-svc/default');
   ```

1. Cree una tabla externa denominada **web_clickstreams_spark_results** en el grupo de datos.

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
  
1. En CTP 3.1, la creación del grupo de datos es asincrónica, pero aún no se puede determinar cuándo se ha completado. Espere dos minutos para asegurarse de que se haya creado el grupo de datos antes de continuar.

## <a name="start-a-spark-streaming-job"></a>Iniciar un trabajo de streaming de Spark

El paso siguiente es crear un trabajo de streaming de Spark que cargue datos de secuencias de clics web desde el grupo de almacenamiento (HDFS) en la tabla externa que ha creado en el grupo de datos.

1. En Azure Data Studio, conéctese a la instancia maestra del clúster de macrodatos. Para obtener más información, vea [Conexión a un clúster de macrodatos](connect-to-big-data-cluster.md).

1. Haga doble clic en la conexión de la puerta de enlace de HDFS/Spark de la ventana **Servidores**. Después, seleccione **Nuevo trabajo de Spark**.

   ![Nuevo trabajo de Spark](media/tutorial-data-pool-ingest-spark/hdfs-new-spark-job.png)

1. En la ventana **Nuevo trabajo**, escriba un nombre en el campo **Nombre del trabajo**.

1. En el menú desplegable **Archivo jar/py**, seleccione **HDFS**. Después, escriba la siguiente ruta del archivo JAR:

   ```text
   /jar/mssql-spark-lib-assembly-1.0.jar
   ```

1. En el campo **Clase principal**, escriba `FileStreaming`.

1. En el campo **Argumentos**, escriba el texto siguiente y especifique la contraseña para la instancia maestra de SQL Server en el marcador de posición `<your_password>`. 

   ```text
   --server mssql-master-pool-0.service-master-pool --port 1433 --user sa --password <your_password> --database sales --table web_clickstreams_spark_results --source_dir hdfs:///clickstream_data --input_format csv --enable_checkpoint false --timeout 380000
   ```

   En la tabla siguiente, se describen los distintos argumentos:

   | Argumento | Descripción |
   |---|---|
   | nombre de servidor | SQL Server lo usa para leer el esquema de la tabla |
   | número de puerto | Puerto en el que escucha SQL Server (de forma predeterminada, 1433) |
   | username | Nombre de usuario de inicio de sesión de SQL Server |
   | password | Contraseña de inicio de sesión de SQL Server |
   | El nombre de la base de datos | Base de datos de destino |
   | external table name | Tabla que se usará para los resultados |
   | source directory for streaming | Tiene que ser un URI completo, como “hdfs:///datos_secuencia_clics” |
   | input format | Puede ser “csv”, “parquet” o “json”. |
   | enable checkpoint | true o false |
   | timeout | Hora a la que se ejecutará el trabajo en milisegundos antes de cerrarse |

1. Pulse **Enviar** para enviar el trabajo.

   ![Envío de trabajo de Spark](media/tutorial-data-pool-ingest-spark/spark-new-job-settings.png)

## <a name="query-the-data"></a>Consultar los datos

En los pasos siguientes, se muestra que el trabajo de streaming de Spark ha cargado los datos de HDFS en el grupo de datos.

1. Antes de consultar los datos ingeridos, vea el resultado del historial de la tarea para comprobar si el trabajo se ha completado.

   ![Historial de trabajos de Spark](media/tutorial-data-pool-ingest-spark/spark-task-history.png)

1. Vuelva a la ventana de consultas de la instancia maestra de SQL Server que ha abierto al principio de este tutorial.

1. Ejecute la consulta siguiente para inspeccionar los datos ingeridos.

   ```sql
   USE Sales
   GO
   SELECT count(*) FROM [web_clickstreams_spark_results];
   SELECT TOP 10 * FROM [web_clickstreams_spark_results];
   ```

## <a name="clean-up"></a>Limpieza

Use este comando para quitar los objetos de la base de datos creados en este tutorial.

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstreams_spark_results];
```

## <a name="next-steps"></a>Pasos siguientes

Obtenga información sobre cómo ejecutar un cuaderno de ejemplo en Azure Data Studio:
> [!div class="nextstepaction"]
> [Ejecutar un cuaderno de ejemplo](tutorial-notebook-spark.md)
