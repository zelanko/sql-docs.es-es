---
title: 'Tutorial de Python: Preparar datos'
description: En este tutorial, usará Python y una regresión lineal en SQL Server Machine Learning Services para predecir el número de alquileres de esquíes. Preparará los datos de una base de datos de SQL Server mediante Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6424a453bff2f0f6d62caa8c9870ccc2ec10d578
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727057"
---
# <a name="python-tutorial-prepare-data-to-train-a-linear-regression-model-in-sql-server-machine-learning-services"></a>Tutorial de Python: Preparación de datos para entrenar un modelo de regresión lineal en SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En la parte dos de esta serie de tutoriales de cuatro partes, preparará los datos de una base de datos de SQL Server mediante Python. Más adelante en esta serie, usará estos datos para entrenar e implementar un modelo de regresión lineal en Python con SQL Server Machine Learning Services.

En este artículo, aprenderá a:

> [!div class="checklist"]
> * Cargar los datos desde la base de datos de SQL Server en una trama de datos de **pandas**
> * Quitar columnas para preparar los datos en Python

En la [parte uno](python-ski-rental-linear-regression.md), ha aprendido a restaurar la base de datos de ejemplo.

En la [parte tres](python-ski-rental-linear-regression-train-model.md), aprenderá a entrenar un modelo de aprendizaje automático de regresión lineal en Python.

En la [parte cuatro](python-ski-rental-linear-regression-deploy-model.md), aprenderá a almacenar el modelo en SQL Server y, después, creará procedimientos almacenados de los scripts de Python que ha desarrollado en las partes dos y tres. Los procedimientos almacenados se ejecutarán en SQL Server para realizar predicciones basándose en datos nuevos.

## <a name="prerequisites"></a>Prerequisites

* En la parte dos de este tutorial, se da por hecho que ha completado la [parte uno](python-ski-rental-linear-regression.md) y los requisitos previos.

## <a name="explore-and-prepare-the-data"></a>Exploración y preparación de los datos

Para usar los datos en Python, cargará los datos de la base de datos de SQL Server en una trama de datos de pandas.

Cree un cuaderno de Python en Azure Data Studio y ejecute el script siguiente. Reemplace `<SQL Server>` por el nombre de su instancia de SQL Server.

El script de Python siguiente importa el conjunto de datos de la tabla **dbo.rental_data** de la base de datos en una trama de datos de pandas **df**.

```python
import pandas as pd
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from revoscalepy import RxComputeContext, RxInSqlServer, RxSqlServerData
from revoscalepy import rx_import

# Connection string to your SQL Server instance
conn_str = 'Driver=SQL Server;Server=<SQL Server>;Database=TutorialDB;Trusted_Connection=True;'

# Define the columns you will import
 column_info = {
         "Year" : { "type" : "integer" },
         "Month" : { "type" : "integer" },
         "Day" : { "type" : "integer" },
         "RentalCount" : { "type" : "integer" },
         "WeekDay" : {
             "type" : "factor",
             "levels" : ["1", "2", "3", "4", "5", "6", "7"]
         },
         "Holiday" : {
             "type" : "factor",
             "levels" : ["1", "0"]
         },
         "Snow" : {
             "type" : "factor",
             "levels" : ["1", "0"]
         }
     }

# Get the data from the SQL Server table
data_source = RxSqlServerData(table="dbo.rental_data",
                               connection_string=conn_str, column_info=column_info)
computeContext = RxInSqlServer(
     connection_string = conn_str,
     num_tasks = 1,
     auto_cleanup = False
)

RxInSqlServer(connection_string=conn_str, num_tasks=1, auto_cleanup=False)

# import data source and convert to pandas dataframe
df = pd.DataFrame(rx_import(input_data = data_source))
print("Data frame:", df)

# Get all the columns from the dataframe.
columns = df.columns.tolist()

# Filter the columns to remove ones we don't want to use in the training
columns = [c for c in columns if c not in ["Year"]]
```

Se mostrarán resultados similares a los siguientes.

```results
Rows Processed: 453
Data frame:      Day  Holiday  Month  RentalCount  Snow  WeekDay  Year
0     20        1      1          445     2        2  2014
1     13        2      2           40     2        5  2014
2     10        2      3          456     2        1  2013
3     31        2      3           38     2        2  2014
4     24        2      4           23     2        5  2014
5     11        2      2           42     2        4  2015
6     28        2      4          310     2        1  2013
...
[453 rows x 7 columns]
```

## <a name="next-steps"></a>Pasos siguientes

En la parte dos de esta serie de tutoriales, ha completado estos pasos:

* Cargar los datos desde la base de datos de SQL Server en una trama de datos de **pandas**
* Quitar columnas para preparar los datos en Python

Para entrenar un modelo de aprendizaje automático que use datos de la base de datos TutorialDB, siga la parte tres de esta serie de tutoriales:

> [!div class="nextstepaction"]
> [Tutorial de Python: Entrenamiento de un modelo de regresión lineal](python-ski-rental-linear-regression-train-model.md)