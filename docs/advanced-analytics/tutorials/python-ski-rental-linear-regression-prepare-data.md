---
title: 'Tutorial de Python: Preparación de los datos'
description: En la segunda parte de esta serie de tutoriales de cuatro partes, usará Python para preparar los datos para predecir los alquileres de esquíes en SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/02/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9aeefb0b6fd9ca1a744d132fccf1eedfedbaa6e7
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75681754"
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

## <a name="prerequisites"></a>Prerrequisitos

* En la parte dos de este tutorial, se da por hecho que ha completado la [parte uno](python-ski-rental-linear-regression.md) y los requisitos previos.

## <a name="explore-and-prepare-the-data"></a>Exploración y preparación de los datos

Para usar los datos en Python, cargará los datos de la base de datos de SQL Server en una trama de datos de pandas.

Cree un cuaderno de Python en Azure Data Studio y ejecute el script siguiente. Reemplace `<SQL Server>` por el nombre de su instancia de SQL Server.

El script de Python siguiente importa el conjunto de datos de la tabla **dbo.rental_data** de la base de datos en una trama de datos de pandas **df**.

En la cadena de conexión, reemplace los detalles de conexión según corresponda.

```python
import pyodbc
import pandas
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error

# Connection string to your SQL Server instance
conn_str = pyodbc.connect('DRIVER={ODBC Driver 17 for SQL Server}; SERVER=localhost; DATABASE=TutorialDB; Trusted_Connection=yes')

query_str = 'SELECT Year, Month, Day, Rentalcount, Weekday, Holiday, Snow FROM dbo.rental_data'

df = pandas.read_sql(sql=query_str, con=conn_str)

print("Data frame:", df)

# Get all the columns from the dataframe.
columns = df.columns.tolist()

# Filter the columns to remove ones we don't want to use in the training
columns = [c for c in columns if c not in ["Year"]]
```

Se mostrarán resultados similares a los siguientes.

```results
Data frame:      Year  Month  Day  RentalCount  WeekDay  Holiday  Snow
0    2014      1   20          445        2        1     0
1    2014      2   13           40        5        0     0
2    2013      3   10          456        1        0     0
3    2014      3   31           38        2        0     0
4    2014      4   24           23        5        0     0
..    ...    ...  ...          ...      ...      ...   ...
448  2013      2   19           57        3        0     1
449  2015      3   18           26        4        0     0
450  2015      3   24           29        3        0     1
451  2014      3   26           50        4        0     1
452  2015     12    6          377        1        0     1

[453 rows x 7 columns]
```

## <a name="next-steps"></a>Pasos siguientes

En la parte dos de esta serie de tutoriales, ha completado estos pasos:

* Cargar los datos desde la base de datos de SQL Server en una trama de datos de **pandas**
* Quitar columnas para preparar los datos en Python

Para entrenar un modelo de aprendizaje automático que use datos de la base de datos TutorialDB, siga la parte tres de esta serie de tutoriales:

> [!div class="nextstepaction"]
> [Tutorial de Python: Entrenamiento de un modelo de regresión lineal](python-ski-rental-linear-regression-train-model.md)