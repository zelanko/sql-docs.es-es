---
title: Cómo introducir datos en un grupo de datos de SQL Server con Transact-SQL | Microsoft Docs
description: Este tutorial muestra cómo introducir datos en el grupo de datos de un clúster de macrodatos de 2019 de SQL Server (versión preliminar) con el procedimiento almacenado de sp_data_pool_table_insert_data.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/06/2018
ms.topic: tutorial
ms.prod: sql
ms.openlocfilehash: 1f585a354175ff893869cef7f2f47b12fe244634
ms.sourcegitcommit: cb73d60db8df15bf929ca17c1576cf1c4dca1780
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2018
ms.locfileid: "51221701"
---
# <a name="tutorial-ingest-data-into-a-sql-server-data-pool-with-transact-sql"></a>Tutorial: Introducción de datos en un grupo de datos de SQL Server con Transact-SQL

Este tutorial muestra cómo utilizar Transact-SQL para cargar datos en el [grupo datos](concept-data-pool.md) de un clúster de macrodatos de 2019 de SQL Server (versión preliminar). Con los clústeres de macrodatos de SQL Server, pueden ingeridos datos desde una variedad de orígenes y distribuirse entre las instancias del grupo de datos.

En este tutorial, obtendrá información sobre cómo:

> [!div class="checklist"]
> * Crear una tabla externa en el grupo de datos.
> * Insertar datos de secuencia de clics de web de ejemplo en la tabla de grupo de datos.
> * Combinar datos en la tabla de grupo de datos con tablas locales.

> [!TIP]
> Si lo prefiere, puede descargar y ejecutar un script para los comandos en este tutorial. Para obtener instrucciones, consulte el [ejemplos de grupos de datos](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-pool) en GitHub.

## <a id="prereqs"></a> Requisitos previos

* [Implementar un clúster de macrodatos en Kubernetes](deployment-guidance.md).
* [Instalar Data Studio de Azure y la extensión de SQL Server 2019](deploy-big-data-tools.md).
* [Cargar datos de ejemplo en el clúster](#sampledata).

[!INCLUDE [Load sample data](../includes/big-data-cluster-load-sample-data.md)]

## <a name="create-an-external-table-in-the-data-pool"></a>Crear una tabla externa en el grupo de datos

Los pasos siguientes crean una tabla externa en el grupo de datos llamado **web_clickstream_clicks_data_pool**. Esta tabla, a continuación, se utiliza como una ubicación para la ingesta de datos en el clúster de macrodatos.

1. En Azure Data Studio, conéctese a la instancia principal de SQL Server del clúster de macrodatos. Para obtener más información, consulte [conectar a la instancia principal de SQL Server](deploy-big-data-tools.md#master).

1. Haga doble clic en la conexión en el **servidores** ventana para mostrar el panel del servidor para la instancia principal de SQL Server. Seleccione **nueva consulta**.

   ![Consulta de la instancia principal de SQL Server](./media/tutorial-data-pool-ingest-sql/sql-server-master-instance-query.png)

1. Ejecute el siguiente comando de Transact-SQL para cambiar el contexto para el **ventas** base de datos en la instancia maestra.

   ```sql
   USE Sales
   GO
   ```

1. Crear una tabla externa denominada **web_clickstream_clicks_data_pool** en el grupo de datos. El `SqlDataPool` origen de datos es un tipo de origen de datos especial que puede utilizarse desde la instancia principal de cualquier clúster de macrodatos.

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
  
1. En CTP 2.1, la creación del grupo de datos es asincrónica, pero no hay ninguna manera de determinar si aún termina. Espere dos minutos para asegurarse de que se crea el grupo de datos antes de continuar.

## <a name="load-data"></a>Cargar datos

Los pasos siguientes ingieren datos de secuencia de clics de web de ejemplo en el grupo de datos utilizando la tabla externa creada en los pasos anteriores.

1. Defina variables para la consulta que desea usar para insertar datos en el grupo de datos. A continuación, utilice el **modelo... sp_data_pool_table_insert_data** procedimiento almacenado para insertar los resultados de la consulta en el grupo de datos (el **web_clickstream_clicks_data_pool** tabla externa).

   ```sql
   DECLARE @db_name SYSNAME = 'Sales'
   DECLARE @schema_name SYSNAME = 'dbo'
   DECLARE @table_name SYSNAME = 'web_clickstream_clicks_data_pool'
   DECLARE @query NVARCHAR(MAX) = '
   SELECT wcs_user_sk, i_category_id, COUNT_BIG(*) as clicks
   FROM sales.dbo.web_clickstreams
   INNER JOIN sales.dbo.item it ON (wcs_item_sk = i_item_sk
      AND wcs_user_sk IS NOT NULL)
   GROUP BY wcs_user_sk, i_category_id
   HAVING COUNT_BIG(*) > 100;'

   EXEC model..sp_data_pool_table_insert_data @db_name, @schema_name, @table_name, @query
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

## <a name="clean-up"></a>Limpiar

Use el siguiente comando para quitar los objetos de base de datos creados en este tutorial.

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstream_clicks_data_pool];
```

## <a name="next-steps"></a>Pasos siguientes

Obtenga información sobre cómo introducir datos en el grupo de datos con los trabajos de Spark:
> [!div class="nextstepaction"]
> [Ingesta de datos con los trabajos de Spark](tutorial-data-pool-ingest-spark.md)
