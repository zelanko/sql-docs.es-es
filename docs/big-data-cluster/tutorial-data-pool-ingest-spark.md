---
title: Ingestión de datos con trabajos de Spark
titleSuffix: SQL Server big data clusters
description: En este tutorial se muestra cómo introducir datos en el grupo de datos de una [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] mediante trabajos de Spark en Azure Data Studio.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: shivsood
ms.date: 08/21/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5ffc2773144d2b1a170e2f087d7abf607af99ef6
ms.sourcegitcommit: 4fb6bc7c81a692a2df706df063d36afad42816af
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/29/2019
ms.locfileid: "73049856"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-spark-jobs"></a>Tutorial: introducción de datos en un grupo de datos de SQL Server con trabajos de Spark

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este tutorial se muestra cómo usar trabajos de Spark para cargar datos en el [grupo de datos](concept-data-pool.md) de un [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]. 

En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Crear una tabla externa en el grupo de datos.
> * Crea un trabajo de Spark para cargar datos desde HDFS.
> * Consultar los resultados en la tabla externa.

> [!TIP]
> Si lo prefiere, puede descargar y ejecutar un script con los comandos de este tutorial. Para obtener instrucciones, vea los [Ejemplos de grupos de datos](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool) en GitHub.

## <a id="prereqs"></a> Prerequisites

- [Herramientas de macrodatos](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **Extensión de SQL Server 2019**
- [Cargar datos de ejemplo en un clúster de macrodatos](tutorial-load-sample-data.md)

## <a name="create-an-external-table-in-the-data-pool"></a>Crear una tabla externa en el grupo de datos

Siga este procedimiento para crear una tabla externa en el grupo de datos denominada **web_clickstreams_spark_results**. Después, esta tabla se puede usar como una ubicación para ingerir datos en el clúster de macrodatos.

1. En Azure Data Studio, conéctese a la instancia maestra de SQL Server del clúster de macrodatos. Para obtener más información, vea [Conectarse a una instancia maestra de SQL Server](connect-to-big-data-cluster.md#master).

1. Haga doble clic en la conexión de la ventana **Servidores** para mostrar el panel del servidor de la instancia maestra de SQL Server. Seleccione **Nueva consulta**.

   ![Consulta de la instancia maestra de SQL Server](./media/tutorial-data-pool-ingest-spark/sql-server-master-instance-query.png)

1. Cree un origen de datos externo al grupo de datos (si aún no existe).

   ```sql
   USE Sales
   GO
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

El paso siguiente es crear un trabajo de streaming de Spark que cargue datos de secuencias de clics web desde el grupo de almacenamiento (HDFS) en la tabla externa que ha creado en el grupo de datos. Estos datos se agregaron a/clickstream_data en [cargar datos de ejemplo en el clúster de Big Data](tutorial-load-sample-data.md).

1. En Azure Data Studio, conéctese a la instancia maestra del clúster de macrodatos. Para obtener más información, vea [Conexión a un clúster de macrodatos](connect-to-big-data-cluster.md).

2. Cree un nuevo cuaderno y seleccione Spark | Scala como kernel.

3. Ejecución del trabajo de ingesta de Spark
   1. Configuración de los parámetros del conector de Spark-SQL
      ```
      import org.apache.spark.sql.types._
      import org.apache.spark.sql.{SparkSession, SaveMode, Row, DataFrame}

      // Change per your installation
      val user= "username"
      val password= "****"
      val database =  "MyTestDatabase"
      val sourceDir = "/clickstream_data"
      val datapool_table = "web_clickstreams_spark_results"
      val datasource_name = "SqlDataPool"
      val schema = StructType(Seq(
      StructField("wcs_click_date_sk",IntegerType,true), StructField("wcs_click_time_sk",IntegerType,true), StructField("wcs_sales_sk",IntegerType,true), StructField("wcs_item_sk",IntegerType,true), 
      StructField("wcs_web_page_sk",IntegerType,true), StructField("wcs_user_sk",IntegerType,true)
      ))

      val hostname = "master-0.master-svc"
      val port = 1433
      val url = s"jdbc:sqlserver://${hostname}:${port};database=${database};user=${user};password=${password};"
      ```
   2. Definir y ejecutar el trabajo de Spark
      * Cada trabajo tiene dos partes: readStream y writeStream. A continuación, se crea una trama de datos con el esquema definido anteriormente y, a continuación, se escribe en la tabla externa del grupo de datos.
      ```
      import org.apache.spark.sql.{SparkSession, SaveMode, Row, DataFrame}
      
      val df = spark.readStream.format("csv").schema(schema).option("header", true).load(sourceDir)
      val query = df.writeStream.outputMode("append").foreachBatch{ (batchDF: DataFrame, batchId: Long) => 
                batchDF.write
                 .format("com.microsoft.sqlserver.jdbc.spark")
                 .mode("append")
                  .option("url", url)
                  .option("dbtable", datapool_table)
                  .option("user", user)
                  .option("password", password)
                  .option("dataPoolDataSource",datasource_name).save()
               }.start()

      query.processAllAvailable()
      query.awaitTermination(40000)
      ```
## <a name="query-the-data"></a>Consulta de los datos

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
1. Los datos también se pueden consultar en Spark. Por ejemplo, el código siguiente imprime el número de registros de la tabla:
   ```
   def df_read(dbtable: String,
                url: String,
                dataPoolDataSource: String=""): DataFrame = {
        spark.read
             .format("com.microsoft.sqlserver.jdbc.spark")
             .option("url", url)
             .option("dbtable", dbtable)
             .option("user", user)
             .option("password", password)
             .option("dataPoolDataSource", dataPoolDataSource)
             .load()
             }

   val new_df = df_read(datapool_table, url, dataPoolDataSource=datasource_name)
   println("Number of rows is " +  new_df.count)
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
