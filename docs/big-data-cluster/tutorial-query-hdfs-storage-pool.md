---
title: Cómo consulta HDFS en un clúster de macrodatos de SQL Server | Microsoft Docs
description: Este tutorial muestra cómo consultar datos HDFS en un clúster de macrodatos de 2019 de SQL Server (versión preliminar). Crear una tabla externa a través de los datos en el grupo de almacenamiento y, a continuación, ejecutar una consulta.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/11/2018
ms.topic: tutorial
ms.prod: sql
ms.openlocfilehash: c6f0f01936d5b6e570c2bff53d19ae7a64f151ab
ms.sourcegitcommit: 38f35b2f7a226ded447edc6a36665eaa0376e06e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/23/2018
ms.locfileid: "49644248"
---
# <a name="tutorial-query-hdfs-in-a-sql-server-big-data-cluster"></a>Tutorial: Consulta de HDFS en un clúster de macrodatos de SQL Server

Este tutorial muestra cómo consultar datos HDFS en un clúster de macrodatos de SQL Server 2019.

En este tutorial, obtendrá información sobre cómo:

> [!div class="checklist"]
> * Crear una tabla externa que apunte a los datos HDFS en un clúster de macrodatos.
> * Únase a estos datos con datos de gran valor en la instancia maestra.

> [!TIP]
> Si lo prefiere, puede descargar y ejecutar un script para los comandos en este tutorial. Para obtener instrucciones, consulte el [ejemplos de datos de virtualización](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/data-virtualization) en GitHub.

## <a name="prerequisites"></a>Requisitos previos

- [Implementar un clúster de macrodatos en Kubernetes](deployment-guidance.md).
- [Instalar Data Studio de Azure y la extensión de SQL Server 2019](deploy-big-data-tools.md).
- [Cargar datos de ejemplo en el clúster](#sampledata).

[!INCLUDE [Load sample data](../includes/big-data-cluster-load-sample-data.md)]

## <a name="create-an-external-table-to-hdfs"></a>Crear una tabla HDFS externa

El grupo de almacenamiento contiene datos de la secuencia de clics de web en un archivo CSV que se almacenan en HDFS. Use los pasos siguientes para definir una tabla externa que puede tener acceso a los datos en ese archivo.

1. En Azure Data Studio, conéctese a la instancia principal de SQL Server del clúster de macrodatos. Para obtener más información, consulte [conectar a la instancia principal de SQL Server](deploy-big-data-tools.md#master).

2. Haga doble clic en la conexión en el **servidores** ventana para mostrar el panel del servidor para la instancia principal de SQL Server. Seleccione **nueva consulta**.

   ![Consulta de la instancia principal de SQL Server](./media/tutorial-query-hdfs-storage-pool/sql-server-master-instance-query.png)

3. Ejecute el siguiente comando de Transact-SQL para cambiar el contexto para el **ventas** base de datos en la instancia maestra.

   ```sql
   USE Sales
   GO
   ```

4. Definir el formato del archivo CSV para leer de HDFS. Presione F5 para ejecutar la instrucción.

   ```sql
   CREATE EXTERNAL FILE FORMAT csv_file
   WITH (
       FORMAT_TYPE = DELIMITEDTEXT,
       FORMAT_OPTIONS(
           FIELD_TERMINATOR = ',',
           STRING_DELIMITER = '"',
           FIRST_ROW = 2,
           USE_TYPE_DEFAULT = TRUE)
   );
   ```

5. Crear una tabla externa que puede leer el `/clickstream_data` del bloque de almacenamiento. El **SqlStoragePool** es accesible desde la instancia principal de un clúster de macrodatos.

   ```sql
   CREATE EXTERNAL TABLE [web_clickstreams_hdfs]
   ("wcs_click_date_sk" BIGINT , "wcs_click_time_sk" BIGINT , "wcs_sales_sk" BIGINT , "wcs_item_sk" BIGINT , "wcs_web_page_sk" BIGINT , "wcs_user_sk" BIGINT)
   WITH
   (
       DATA_SOURCE = SqlStoragePool,
       LOCATION = '/clickstream_data',
       FILE_FORMAT = csv_file
   );
   GO
   ```

## <a name="query-the-data"></a>Consultar los datos

Ejecute la siguiente consulta para unir los datos HDFS en el `web_clickstream_hdfs` tabla externa con los datos relacionales locales `Sales` base de datos.

```sql
SELECT  
    wcs_user_sk,
    SUM( CASE WHEN i_category = 'Books' THEN 1 ELSE 0 END) AS book_category_clicks,
    SUM( CASE WHEN i_category_id = 1 THEN 1 ELSE 0 END) AS [Home & Kitchen],
    SUM( CASE WHEN i_category_id = 2 THEN 1 ELSE 0 END) AS [Music],
    SUM( CASE WHEN i_category_id = 3 THEN 1 ELSE 0 END) AS [Books],
    SUM( CASE WHEN i_category_id = 4 THEN 1 ELSE 0 END) AS [Clothing & Accessories],
    SUM( CASE WHEN i_category_id = 5 THEN 1 ELSE 0 END) AS [Electronics],
    SUM( CASE WHEN i_category_id = 6 THEN 1 ELSE 0 END) AS [Tools & Home Improvement],
    SUM( CASE WHEN i_category_id = 7 THEN 1 ELSE 0 END) AS [Toys & Games],
    SUM( CASE WHEN i_category_id = 8 THEN 1 ELSE 0 END) AS [Movies & TV],
    SUM( CASE WHEN i_category_id = 9 THEN 1 ELSE 0 END) AS [Sports & Outdoors]
  FROM [dbo].[web_clickstreams_hdfs]
  INNER JOIN item it ON (wcs_item_sk = i_item_sk
                        AND wcs_user_sk IS NOT NULL)
GROUP BY  wcs_user_sk;
GO
```

## <a name="clean-up"></a>Limpiar

Use el siguiente comando para quitar la tabla externa que se usa en este tutorial.

```sql
DROP EXTERNAL TABLE [dbo].[web_clickstreams_hdfs];
GO
```

## <a name="next-steps"></a>Pasos siguientes

Avance al siguiente artículo para obtener información sobre cómo realizar consultas de Oracle desde un clúster de macrodatos.
> [!div class="nextstepaction"]
> [Consultar datos externos en Oracle](tutorial-query-oracle.md)
