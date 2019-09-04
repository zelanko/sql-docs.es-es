---
title: 'Tutorial de Python: Entrenar modelo (regresión lineal)'
description: En este tutorial usará Python y la regresión lineal en SQL Server Machine Learning Services para predecir el número de alquileres de esquí. Entrenará un modelo de regresión lineal en Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 30f390681dc63d6de9a95e805b6cc8f273b2b8d7
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/04/2019
ms.locfileid: "70242553"
---
# <a name="python-tutorial-train-a-linear-regression-model-in-sql-server-machine-learning-services"></a>Tutorial de Python: Entrenar un modelo de regresión lineal en SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En la tercera parte de esta serie de tutoriales de cuatro partes, entrenaremos un modelo de regresión lineal en Python. En la siguiente parte de esta serie, implementará este modelo en una base de datos de SQL Server con Machine Learning Services.

En este artículo, aprenderá a:

> [!div class="checklist"]
> * Entrenar un modelo de regresión lineal
> * Crear predicciones usando el modelo de regresión lineal

En la [primera parte](python-ski-rental-linear-regression.md), aprendió a restaurar la base de datos de ejemplo.

En la [segunda parte](python-ski-rental-linear-regression-prepare-data.md), ha aprendido a cargar los datos de SQL Server en una trama de datos de Python y a preparar los datos en Python.

En la [cuarta parte](python-ski-rental-linear-regression-deploy-model.md), aprenderá a almacenar el modelo en SQL Server y, a continuación, creará procedimientos almacenados a partir de los scripts de Python desarrollados en las partes dos y tres. Los procedimientos almacenados se ejecutarán en SQL Server para realizar predicciones basadas en nuevos datos.

## <a name="prerequisites"></a>Requisitos previos

* En la tercera parte de este tutorial se supone que ha completado la [parte uno](python-ski-rental-linear-regression.md) y sus requisitos previos.

## <a name="train-the-model"></a>Entrenar el modelo

Para predecir, tiene que buscar una función (modelo) que describa mejor la dependencia entre las variables de nuestro conjunto de resultados. Esto llamó al entrenamiento del modelo. El conjunto de datos de entrenamiento será un subconjunto del conjunto de datos completo desde el **DF** de trama de datos pandas que creó en la segunda parte de esta serie.

Entrenará el modelo **lin_model** mediante un algoritmo de regresión lineal.

```python
# Store the variable we'll be predicting on.
target = "RentalCount"

# Generate the training set.  Set random_state to be able to replicate results.
train = df.sample(frac=0.8, random_state=1)

# Select anything not in the training set and put it in the testing set.
test = df.loc[~df.index.isin(train.index)]

# Print the shapes of both sets.
print("Training set shape:", train.shape)
print("Testing set shape:", test.shape)

# Initialize the model class.
lin_model = LinearRegression()

# Fit the model to the training data.
lin_model.fit(train[columns], train[target])
```

Debería ver resultados similares a los siguientes.

```results
Training set shape: (362, 7)
Testing set shape: (91, 7)
```

## <a name="make-predictions"></a>Hacer predicciones

Use una función de predicción para predecir los recuentos de alquiler mediante el modelo **lin_model**.

```python
# Generate our predictions for the test set.
lin_predictions = lin_model.predict(test[columns])
print("Predictions:", lin_predictions)
# Compute error between our test predictions and the actual values.
lin_mse = mean_squared_error(lin_predictions, test[target])
print("Computed error:", lin_mse)
```

```results
Predictions: [  40.   38.  240.   39.  514.   48.  297.   25.  507.   24.   30.   54.
   40.   26.   30.   34.   42.  390.  336.   37.   22.   35.   55.  350.
  252.  370.  499.   48.   37.  494.   46.   25.  312.  390.   35.   35.
  421.   39.  176.   21.   33.  452.   34.   28.   37.  260.   49.  577.
  312.   24.   24.  390.   34.   64.   26.   32.   33.  358.  348.   25.
   35.   48.   39.   44.   58.   24.  350.  651.   38.  468.   26.   42.
  310.  709.  155.   26.  648.  617.   26.  846.  729.   44.  432.   25.
   39.   28.  325.   46.   36.   50.   63.]
Computed error: 3.59831533436e-26
```

## <a name="next-steps"></a>Pasos siguientes

En la tercera parte de esta serie de tutoriales, ha completado estos pasos:

* Entrenar un modelo de regresión lineal
* Crear predicciones usando el modelo de regresión lineal

Para implementar el modelo de aprendizaje automático que ha creado, siga la cuarta parte de esta serie de tutoriales:

> [!div class="nextstepaction"]
> [Tutorial de Python: Implementación de un modelo de aprendizaje automático](python-ski-rental-linear-regression-deploy-model.md)