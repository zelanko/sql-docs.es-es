---
title: Introducir datos en un grupo de datos de SQL Server
titleSuffix: SQL Server big data clusters
description: Este tutorial muestra cómo introducir datos en el grupo de datos de un clúster de macrodatos de 2019 de SQL Server (versión preliminar).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 06/26/2019
ms.topic: tutorial
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 52881f5102125cc008c1a35278b9bf46bef289f4
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728358"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-transact-sql"></a>Tutorial: Introducir datos en un grupo de datos de SQL Server con Transact-SQL

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este tutorial muestra cómo utilizar Transact-SQL para cargar datos en el [grupo datos](concept-data-pool.md) de un clúster de macrodatos de 2019 de SQL Server (versión preliminar). Con los clústeres de macrodatos de SQL Server, pueden ingeridos datos desde una variedad de orígenes y distribuirse entre las instancias del grupo de datos.

En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Crear una tabla externa en el grupo de datos.
> * Insertar datos de secuencia de clics de web de ejemplo en la tabla de grupo de datos.
> * Combinar datos en la tabla de grupo de datos con tablas locales.

> [!TIP]
> Si lo prefiere, puede descargar y ejecutar un script para los comandos en este tutorial. Para obtener instrucciones, consulte el [ejemplos de grupos de datos](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool) en GitHub.

## <a id="prereqs"></a> Requisitos previos

- [Herramientas de datos de gran tamaño](deploy-big-data-tools.md)
   - **kubectl**
   - **Azure Data Studio**
   - **Extensión de SQL Server 2019**
- [Cargar datos de ejemplo en el clúster de macrodatos](tutorial-load-sample-data.md)

## <a name="create-an-external-table-in-the-data-pool"></a>Crear una tabla externa en el grupo de datos

Los pasos siguientes crean una tabla externa en el grupo de datos llamado **web_clickstream_clicks_data_pool**. Esta tabla, a continuación, se utiliza como una ubicación para la ingesta de datos en el clúster de macrodatos.

1. En Azure Data Studio, conéctese a la instancia principal de SQL Server del clúster de macrodatos. Para obtener más información, consulte [conectar a la instancia principal de SQL Server](connect-to-big-data-cluster.md#master).

1. Haga doble clic en la conexión en el **servidores** ventana para mostrar el panel del servidor para la instancia principal de SQL Server. Seleccione **nueva consulta**.

   ![Consulta de la instancia principal de SQL Server](./media/tutorial-data-pool-ingest-sql/sql-server-master-instance-query.png)

1. Ejecute el siguiente comando de Transact-SQL para cambiar el contexto para el **ventas** base de datos en la instancia maestra.

   ```sql
   USE Sales
   GO
   ```

1. Crear un origen de datos externo para el grupo de datos si aún no existe.

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_data_sources WHERE name = 'SqlDataPool')
     CREATE EXTERNAL DATA SOURCE SqlDataPool
     WITH (LOCATION = 'sqldatapool://controller-svc/default');
   ```

1. Crear una tabla externa denominada **web_clickstream_clicks_data_pool** en el grupo de datos.

   ```sql
   IF NOT EXISTS(SELECT * FROM sys.external_tables WHERE name = 'web_clickstream_clicks_data_pool')
      CREATE EXTERNAL TABLE [web_clickstream_clicks_data_pool]
      ("wcs_user_sk" BIGINT , "i_category_id" BIGINT , "clicks" BIGINT)
      WITH
      (
         DATA_SOURCE = SqlDataPool,
         DISTRIBUTION = ROUND_ROBIN
      );
   ```
  
1. En CTP 3.1, la creación del grupo de datos es asincrónica, pero no hay ninguna manera de determinar si aún termina. Espere dos minutos para asegurarse de que se crea el grupo de datos antes de continuar.

## <a name="load-data"></a>Carga de datos

Los pasos siguientes ingieren datos de secuencia de clics de web de ejemplo en el grupo de datos utilizando la tabla externa creada en los pasos anteriores.

1. Use un `INSERT INTO` instrucción para insertar los resultados de la consulta en el grupo de datos (el **web_clickstream_clicks_data_pool** tabla externa).

   ```sql
   INSERT INTO web_clickstream_clicks_data_pool
   SELECT wcs_user_sk, i_category_id, COUNT_BIG(*) as clicks
     FROM sales.dbo.web_clickstreams_hdfs_parquet
   INNER JOIN sales.dbo.item it ON (wcs_item_sk = i_item_sk
                           AND wcs_user_sk IS NOT NULL)
   GROUP BY wcs_user_sk, i_category_id
   HAVING COUNT_BIG(*) > 100;
   ```

1. Inspeccione los datos insertados con dos consultas SELECT.

   ```sql
   SELECT count(*) FROM [dbo].[web_clickstream_clicks_data_pool]
   SELECT TOP 10 * FROM [dbo].[web_clickstream_clicks_data_pool]  
   ```

## <a name="query-the-data"></a>Consultar los datos

Únase a los resultados almacenados en la consulta en el grupo de datos con datos locales en el **ventas** tabla.

```sql
SELECT TOP (100)
   w.wcs_user_sk,
   SUM( CASE WHEN i.i_category = 'Books' THEN 1 ELSE 0 END) AS book_category_clicks,
   SUM( CASE WHEN w.i_category_id = 1 THEN 1 ELSE 0 END) AS [Home & Kitchen],
   SUM( CASE WHEN w.i_category_id = 2 THEN 1 ELSE 0 END) AS [Music],
   SUM( CASE WHEN w.i_category_id = 3 THEN 1 ELSE 0 END) AS [Books],
   SUM( CASE WHEN w.i_category_id = 4 THEN 1 ELSE 0 END) AS [Clothing & Accessories],
   SUM( CASE WHEN w.i_category_id = 5 THEN 1 ELSE 0 END) AS [Electronics],
   SUM( CASE WHEN w.i_category_id = 6 THEN 1 ELSE 0 END) AS [Tools & Home Improvement],
   SUM( CASE WHEN w.i_category_id = 7 THEN 1 ELSE 0 END) AS [Toys & Games],
   SUM( CASE WHEN w.i_category_id = 8 THEN 1 ELSE 0 END) AS [Movies & TV],
   SUM( CASE WHEN w.i_category_id = 9 THEN 1 ELSE 0 END) AS [Sports & Outdoors]
FROM [dbo].[web_clickstream_clicks_data_pool] as w
INNER JOIN (SELECT DISTINCT i_category_id, i_category FROM item) as i
   ON i.i_category_id = w.i_category_id
GROUP BY w.wcs_user_sk;
```

## <a name="clean-up"></a>Limpieza

Use el siguiente comando para quitar los objetos de base de datos creados en este tutorial.

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstream_clicks_data_pool];
```

## <a name="next-steps"></a>Pasos siguientes

Obtenga información sobre cómo introducir datos en el grupo de datos con los trabajos de Spark:
> [!div class="nextstepaction"]
> [Ingesta de datos con los trabajos de Spark](tutorial-data-pool-ingest-spark.md)
