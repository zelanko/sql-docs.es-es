---
title: 'Tutorial de Python: Implementación del modelo del clúster'
description: En la parte cuatro de esta serie de tutoriales de cuatro partes, implementará un modelo de agrupación en clústeres en Python con SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/27/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: df0fd7cb27977679a6ca879d7ae01045ed3fa8c8
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727137"
---
# <a name="tutorial-deploy-a-model-in-python-to-categorize-customers-with-sql-server-machine-learning-services"></a>Tutorial: Implementación de un modelo en Python para clasificar clientes por categorías con SQL Server Machine Learning Services

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En la parte cuatro de esta serie de tutoriales de cuatro partes, implementará un modelo de agrupación en clústeres, desarrollado en Python, en una base de datos SQL mediante SQL Server Machine Learning Services.

Para realizar la agrupación en clústeres de forma periódica cuando se registren nuevos clientes, necesita llamar al script de Python desde cualquier aplicación. Para hacerlo, puede implementar el script de Python en SQL Server si lo coloca dentro de un procedimiento almacenado en SQL en la base de datos. Como el modelo se ejecuta en la base de datos SQL, se puede entrenar fácilmente con los datos almacenados en la base de datos.

En esta sección, migrará el código de Python que acaba de escribir en SQL Server e implementará la agrupación de clústeres con la ayuda de SQL Server Machine Learning Services.

En este artículo, aprenderá a:

> [!div class="checklist"]
> * Crear un procedimiento almacenado que genere el modelo
> * Agrupar en clústeres en SQL Server
> * Usar la información de agrupación en clústeres

En la [parte uno](python-clustering-model.md), ha instalado los requisitos previos y ha restaurado la base de datos de ejemplo.

En la [parte dos](python-clustering-model-prepare-data.md), ha aprendido a preparar los datos de una base de datos SQL para realizar la agrupación en clústeres.

En la [parte tres](python-clustering-model-build.md), ha aprendido a crear y entrenar un modelo de agrupación en clústeres k-means en Python.

## <a name="prerequisites"></a>Prerequisites

* En la parte cuatro de esta serie de tutoriales, se da por hecho que ha completado los requisitos previos de la [**parte uno**](python-clustering-model.md) y que ha realizado los pasos de la [**parte dos**](python-clustering-model-prepare-data.md) y la [**parte tres**](python-clustering-model-build.md).

## <a name="create-a-stored-procedure-that-generates-the-model"></a>Creación de un procedimiento almacenado que genere el modelo

Ejecute el siguiente script de T-SQL para crear el procedimiento almacenado. El procedimiento recrea los pasos que ha desarrollado en las partes uno y dos de esta serie de tutoriales:

* clasificación de los clientes basándose en su historial de compras devoluciones
* generación de cuatro clústeres de clientes mediante un algoritmo k-means

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

## <a name="perform-clustering-in-sql-database"></a>Agrupación en clústeres en una base de datos SQL

Después de crear el procedimiento almacenado, ejecute el script siguiente para realizar la agrupación en clústeres mediante el procedimiento.

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

## <a name="use-the-clustering-information"></a>Uso de la información de agrupación en clústeres

Como ha almacenado el procedimiento de agrupación en clústeres en la base de datos, puede realizar la agrupación en clústeres de forma eficiente con los datos de cliente almacenados en la misma base de datos. Puede ejecutar el procedimiento cada vez que se actualicen los datos de clientes y usar la información de agrupación en clústeres actualizada.

Imagine que quiere enviar un correo electrónico promocional a los clientes del clúster 0, el grupo que estaba inactivo (vea una descripción de los cuatro clústeres en la [parte tres](python-clustering-model-build.md#analyze-the-results) de este tutorial). El código siguiente selecciona las direcciones de correo electrónico de los clientes en el clúster 0.

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

Puede cambiar el valor de **c.cluster** a las direcciones de correo electrónico de retorno de los clientes en otros clústeres.

## <a name="clean-up-resources"></a>Limpiar recursos

Cuando termine este tutorial, puede eliminar la base de datos tpcxbb_1gb de SQL Server.

## <a name="next-steps"></a>Pasos siguientes

En la parte cuatro de esta serie de tutoriales, ha aprendido a:

* Crear un procedimiento almacenado que genere el modelo
* Agrupar en clústeres en SQL Server
* Uso de la información de agrupación en clústeres

Para más información sobre cómo usar Python en SQL Server Machine Learning Services, vea:

* [Inicio rápido: Crear y ejecutar scripts de Python simples con SQL Server Machine Learning Services](quickstart-python-create-script.md)
* [Otros tutoriales de Python para SQL Server Machine Learning Services](sql-server-python-tutorials.md)
* [Instalación de paquetes de Python con sqlmlutils](../package-management/install-additional-python-packages-on-sql-server.md)

