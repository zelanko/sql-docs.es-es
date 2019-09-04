---
title: 'Tutorial de Python: Preparar datos (regresión lineal)'
description: En este tutorial usará Python y la regresión lineal en SQL Server Machine Learning Services para predecir el número de alquileres de esquí. Va a preparar los datos de una base de datos SQL Server mediante python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c6c4d5fb4ffc5049f7e1325267b7623dc195e9d8
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2019
ms.locfileid: "70242503"
---
# <a name="python-tutorial-prepare-data-to-train-a-linear-regression-model-in-sql-server-machine-learning-services"></a>Tutorial de Python: Preparar los datos para entrenar un modelo de regresión lineal en SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En la segunda parte de esta serie de tutoriales de cuatro partes, va a preparar los datos de una base de datos de SQL Server con Python. Más adelante en esta serie, usará estos datos para entrenar e implementar un modelo de regresión lineal en Python con SQL Server Machine Learning Services.

En este artículo, aprenderá a:

> [!div class="checklist"]
> * Carga de los datos de la base de datos SQL Server en una trama de datos **pandas**
> * Preparar los datos en Python quitando algunas columnas

En la [primera parte](python-ski-rental-linear-regression.md), aprendió a restaurar la base de datos de ejemplo.

En la tercera [parte](python-ski-rental-linear-regression-train-model.md), aprenderá a entrenar un modelo de aprendizaje automático de regresión lineal en Python.

En la [cuarta parte](python-ski-rental-linear-regression-deploy-model.md), aprenderá a almacenar el modelo en SQL Server y, a continuación, creará procedimientos almacenados a partir de los scripts de Python desarrollados en las partes dos y tres. Los procedimientos almacenados se ejecutarán en SQL Server para realizar predicciones basadas en nuevos datos.

## <a name="prerequisites"></a>Requisitos previos

* En la segunda parte de este tutorial se supone que ha completado la [parte uno](python-ski-rental-linear-regression.md) y sus requisitos previos.

## <a name="explore-and-prepare-the-data"></a>Explorar y preparar los datos

Para usar los datos en Python, cargará los datos de la SQL Server base de datos en una trama de datos pandas.

Cree un nuevo cuaderno de Python en Azure Data Studio y ejecute el script siguiente. Reemplace `<SQL Server>` por su propio nombre de SQL Server.

El siguiente script de Python importa el conjunto de datos de la tabla **dbo. rental_data** de la base de datos a un **DF**de trama de datos pandas.

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

Debería ver resultados similares a los siguientes.

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

En la segunda parte de esta serie de tutoriales, ha completado estos pasos:

* Carga de los datos de la base de datos SQL Server en una trama de datos **pandas**
* Preparar los datos en Python quitando algunas columnas

Para entrenar un modelo de aprendizaje automático que use datos de la base de datos TutorialDB, siga la tercera parte de esta serie de tutoriales:

> [!div class="nextstepaction"]
> [Tutorial de Python: Entrenar un modelo de regresión lineal](python-ski-rental-linear-regression-train-model.md)