---
title: 'Tutorial: Preparar los datos para realizar la agrupación en clústeres en Python'
description: En la segunda parte de esta serie de tutoriales de cuatro partes, va a preparar los datos de una base de datos SQL Server para realizar la agrupación en clústeres en Python con SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/30/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 16291c059efc34f270f6705fb17fa538e55e7459
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2019
ms.locfileid: "70238674"
---
# <a name="tutorial-prepare-data-to-perform-clustering-in-python-with-sql-server-machine-learning-services"></a>Tutorial: Preparar los datos para realizar la agrupación en clústeres en Python con SQL Server Machine Learning Services

En la segunda parte de esta serie de tutoriales de cuatro partes, importará y preparará los datos de una base de datos SQL mediante python. Más adelante en esta serie, usará estos datos para entrenar e implementar un modelo de agrupación en clústeres en Python con SQL Server Machine Learning Services.

En este artículo, aprenderá a:

> [!div class="checklist"]
> * Separe a los clientes a lo largo de diferentes dimensiones mediante Python
> * Carga de datos de SQL Database en una trama de datos de Python

En la [primera parte](tutorial-python-clustering-model.md), instaló los requisitos previos e importó la base de datos de ejemplo.

En la tercera [parte](tutorial-python-clustering-model-build.md), aprenderá a crear y entrenar un modelo de agrupación en clústeres K-means en Python.

En la [cuarta parte](tutorial-python-clustering-model-deploy.md), aprenderá a crear un procedimiento almacenado en una base de datos SQL que puede realizar la agrupación en clústeres en Python en función de los nuevos datos.

## <a name="prerequisites"></a>Requisitos previos

* En la segunda parte de este tutorial se supone que ha cumplido los requisitos previos de la [**parte uno**](tutorial-python-clustering-model.md).

## <a name="separate-customers"></a>Clientes independientes

Para prepararse para los clientes de agrupación en clústeres, primero deberá separar a los clientes en las siguientes dimensiones:

* **orderRatio** = proporción del orden de retorno (número total de pedidos parcialmente o totalmente devueltos frente al número total de pedidos)
* **itemsRatio** = relación de los elementos devueltos (número total de elementos devueltos frente al número de elementos comprados)
* **monetaryRatio** = proporción del importe de retorno (importe monetario total de los artículos devueltos frente al importe adquirido)
* **Frequency** = frecuencia de devolución

Abra un nuevo cuaderno en Azure Data Studio y escriba el script siguiente.

En la cadena de conexión, reemplace los detalles de conexión según sea necesario.

```python
# Load packages.
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import revoscalepy as revoscale
from scipy.spatial import distance as sci_distance
from sklearn import cluster as sk_cluster

################################################################################################

## Connect to DB and select data

################################################################################################

# Connection string to connect to SQL Server named instance.
conn_str = 'Driver=SQL Server;Server=localhost;Database=tpcxbb_1gb;Trusted_Connection=True;'

input_query = '''SELECT
ss_customer_sk AS customer,
ROUND(COALESCE(returns_count / NULLIF(1.0*orders_count, 0), 0), 7) AS orderRatio,
ROUND(COALESCE(returns_items / NULLIF(1.0*orders_items, 0), 0), 7) AS itemsRatio,
ROUND(COALESCE(returns_money / NULLIF(1.0*orders_money, 0), 0), 7) AS monetaryRatio,
COALESCE(returns_count, 0) AS frequency
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
GROUP BY sr_customer_sk ) returned ON ss_customer_sk=sr_customer_sk'''


# Define the columns we wish to import.
column_info = {
    "customer": {"type": "integer"},
    "orderRatio": {"type": "integer"},
    "itemsRatio": {"type": "integer"},
    "frequency": {"type": "integer"}
}
```

## <a name="load-the-data-into-a-data-frame"></a>Cargar los datos en una trama de datos

Los resultados de la consulta se devuelven a Python mediante la función **RxSqlServerData** de revoscalepy. Como parte del proceso, usará la información de columna que definió en el script anterior.

```python
data_source = revoscale.RxSqlServerData(sql_query=input_query, column_Info=column_info,
                                        connection_string=conn_str)
revoscale.RxInSqlServer(connection_string=conn_str, num_tasks=1, auto_cleanup=False)
# import data source and convert to pandas dataframe.
customer_data = pd.DataFrame(revoscale.rx_import(data_source))
```

Ahora, muestre el principio de la trama de datos para comprobar que parece correcta.

```python
print("Data frame:", customer_data.head(n=5))
```

```results
Rows Read: 37336, Total Rows Processed: 37336, Total Chunk Time: 0.172 seconds
Data frame:     customer  orderRatio  itemsRatio  monetaryRatio  frequency
0    29727.0    0.000000    0.000000       0.000000          0
1    97643.0    0.068182    0.078176       0.037034          3
2    57247.0    0.000000    0.000000       0.000000          0
3    32549.0    0.086957    0.068657       0.031281          4
4     2040.0    0.000000    0.000000       0.000000          0
```

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no va a continuar con este tutorial, elimine la base de datos tpcxbb_1gb de SQL Server.

## <a name="next-steps"></a>Pasos siguientes

En la segunda parte de esta serie de tutoriales, ha completado estos pasos:

* Separe a los clientes a lo largo de diferentes dimensiones mediante Python
* Carga de datos de SQL Database en una trama de datos de Python

Para crear un modelo de aprendizaje automático que use estos datos de cliente, siga la tercera parte de esta serie de tutoriales:

> [!div class="nextstepaction"]
> [Tutorial: Creación de un modelo predictivo en Python con SQL Server Machine Learning Services](tutorial-python-clustering-model-build.md)
