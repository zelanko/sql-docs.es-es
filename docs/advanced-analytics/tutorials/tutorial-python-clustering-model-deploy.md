---
title: 'Tutorial: Implementación de un modelo de agrupación en clústeres en Python'
description: En la primera parte de esta serie de tutoriales de cuatro partes, implementará un modelo de agrupación en clústeres en Python con SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/27/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 923fae2a6b215814888b04dc674b67e4c87bc00d
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2019
ms.locfileid: "70238686"
---
# <a name="tutorial-deploy-a-clustering-model-in-python-with-sql-server-machine-learning-services"></a>Tutorial: Implementación de un modelo de agrupación en clústeres en Python con SQL Server Machine Learning Services

En la primera parte de esta serie de tutoriales de cuatro partes, implementará un modelo de agrupación en clústeres, desarrollado en Python, en una base de datos SQL mediante SQL Server Machine Learning Services.

Para realizar la agrupación en clústeres de forma periódica, a medida que los nuevos clientes se registran, debe poder llamar al script de Python desde cualquier aplicación. Para ello, puede implementar el script de Python en SQL Server colocando el script de Python dentro de un procedimiento almacenado de SQL en la base de datos. Dado que el modelo se ejecuta en SQL Database, se puede entrenar fácilmente con los datos almacenados en la base de datos.

En esta sección, moverá el código de Python que acaba de escribir en SQL Server e implementará la agrupación en clústeres con la ayuda de SQL Server Machine Learning Services.

En este artículo, aprenderá a:

> [!div class="checklist"]
> * Crear un procedimiento almacenado que genere el modelo
> * Realizar la agrupación en clústeres en SQL Server
> * Usar la información de agrupación en clústeres

En la [primera parte](tutorial-python-clustering-model.md), instaló los requisitos previos e importó la base de datos de ejemplo.

En la [segunda parte](tutorial-python-clustering-model-prepare-data.md), aprendió a preparar los datos de una base de datos SQL para realizar la agrupación en clústeres.

En la tercera [parte](tutorial-python-clustering-model-build.md), aprendió a crear y entrenar un modelo de agrupación en clústeres K-means en Python.

## <a name="prerequisites"></a>Requisitos previos

* En la cuarta parte de esta serie de tutoriales se supone que ha cumplido los requisitos previos de la [**parte uno**](tutorial-python-clustering-model.md)y que ha completado los pasos de la [**segunda parte**](tutorial-python-clustering-model-prepare-data.md) y la tercera [**parte**](tutorial-python-clustering-model-build.md).

## <a name="create-a-stored-procedure-that-generates-the-model"></a>Crear un procedimiento almacenado que genere el modelo

Ejecute el siguiente script de T-SQL para crear el procedimiento almacenado. El procedimiento vuelve a crear los pasos desarrollados en las partes uno y dos de esta serie de tutoriales:

* Clasifique a los clientes en función de su historial de compra y devolución
* generar cuatro clústeres de clientes mediante un algoritmo de medias K

```sql
USE [tpcxbb_1gb]
GO

CREATE procedure [dbo].[py_generate_customer_return_clusters]
AS

BEGIN
    DECLARE

-- Input query to generate the purchase history & return metrics
     @input_query NVARCHAR(MAX) = N'
SELECT
  ss_customer_sk AS customer,
  CAST( (ROUND(COALESCE(returns_count / NULLIF(1.0*orders_count, 0), 0), 7) ) AS FLOAT) AS orderRatio,
  CAST( (ROUND(COALESCE(returns_items / NULLIF(1.0*orders_items, 0), 0), 7) ) AS FLOAT) AS itemsRatio,
  CAST( (ROUND(COALESCE(returns_money / NULLIF(1.0*orders_money, 0), 0), 7) ) AS FLOAT) AS monetaryRatio,
  CAST( (COALESCE(returns_count, 0)) AS FLOAT) AS frequency
FROM
  (
    SELECT
      ss_customer_sk,
      -- return order ratio
      COUNT(distinct(ss_ticket_number)) AS orders_count,
      -- return ss_item_sk ratio
      COUNT(ss_item_sk) AS orders_items,
      -- return monetary amount ratio
      SUM( ss_net_paid ) AS orders_money
    FROM store_sales s
    GROUP BY ss_customer_sk
  ) orders
  LEFT OUTER JOIN
  (
    SELECT
      sr_customer_sk,
      -- return order ratio
      count(distinct(sr_ticket_number)) as returns_count,
      -- return ss_item_sk ratio
      COUNT(sr_item_sk) as returns_items,
      -- return monetary amount ratio
      SUM( sr_return_amt ) AS returns_money
    FROM store_returns
    GROUP BY sr_customer_sk
  ) returned ON ss_customer_sk=sr_customer_sk
 '

EXEC sp_execute_external_script
      @language = N'Python'
    , @script = N'

import pandas as pd
from sklearn.cluster import KMeans

#get data from input query
customer_data = my_input_data

#We concluded in step 2 in the tutorial that 4 would be a good number of clusters
n_clusters = 4

#Perform clustering
est = KMeans(n_clusters=n_clusters, random_state=111).fit(customer_data[["orderRatio","itemsRatio","monetaryRatio","frequency"]])
clusters = est.labels_
customer_data["cluster"] = clusters

OutputDataSet = customer_data
'
    , @input_data_1 = @input_query
    , @input_data_1_name = N'my_input_data'
             with result sets (("Customer" int, "orderRatio" float,"itemsRatio" float,"monetaryRatio" float,"frequency" float,"cluster" float));
END;
GO
```

## <a name="perform-clustering-in-sql-database"></a>Realizar la agrupación en clústeres en SQL Database

Ahora que ha creado el procedimiento almacenado, ejecute el siguiente script para realizar la agrupación en clústeres mediante el procedimiento.

```sql
--Create a table to store the predictions in

DROP TABLE IF EXISTS [dbo].[py_customer_clusters];
GO

CREATE TABLE [dbo].[py_customer_clusters] (
    [Customer] [bigint] NULL
  , [OrderRatio] [float] NULL
  , [itemsRatio] [float] NULL
  , [monetaryRatio] [float] NULL
  , [frequency] [float] NULL
  , [cluster] [int] NULL
  ,
    ) ON [PRIMARY]
GO

--Execute the clustering and insert results into table
INSERT INTO py_customer_clusters
EXEC [dbo].[py_generate_customer_return_clusters];

-- Select contents of the table to verify it works
SELECT * FROM py_customer_clusters;
```

## <a name="use-the-clustering-information"></a>Usar la información de agrupación en clústeres

Dado que ha almacenado el procedimiento de agrupación en clústeres en la base de datos, puede realizar la agrupación en clústeres de forma eficaz con los datos del cliente almacenados en la misma base de datos. Puede ejecutar el procedimiento cada vez que se actualicen los datos de los clientes y usar la información actualizada de la agrupación en clústeres.

Supongamos que desea enviar un correo electrónico promocional a los clientes del clúster 0, el grupo que estaba inactivo (puede ver cómo se describen los cuatro clústeres en la tercera [parte](tutorial-python-clustering-model-build.md#analyze-the-results) de este tutorial). El código siguiente selecciona las direcciones de correo electrónico de los clientes en el clúster 0.

```sql
USE [tpcxbb_1gb]
--Get email addresses of customers in cluster 0 for a promotion campaign
SELECT customer.[c_email_address], customer.c_customer_sk
  FROM dbo.customer
  JOIN
  [dbo].[py_customer_clusters] as c
  ON c.Customer = customer.c_customer_sk
  WHERE c.cluster = 0
```

Puede cambiar el valor de **c. Cluster** para devolver las direcciones de correo electrónico de los clientes de otros clústeres.

## <a name="clean-up-resources"></a>Limpieza de recursos

Cuando haya terminado este tutorial, puede eliminar la base de datos tpcxbb_1gb de SQL Server.

## <a name="next-steps"></a>Pasos siguientes

En la cuarta parte de esta serie de tutoriales, ha completado estos pasos:

* Crear un procedimiento almacenado que genere el modelo
* Realizar la agrupación en clústeres en SQL Server
* Usar la información de agrupación en clústeres

Para obtener más información sobre el uso de Python en SQL Server Machine Learning Services, consulte:

* [Inicio rápido: Ejecutar un script de Python "Hello World" en SQL Server Machine Learning Services](quickstart-python-run-using-t-sql.md)
* [Otros tutoriales de Python para SQL Server Machine Learning Services](sql-server-python-tutorials.md)
* [Instalación de paquetes de Python con sqlmlutils](../package-management/install-additional-python-packages-on-sql-server.md)

