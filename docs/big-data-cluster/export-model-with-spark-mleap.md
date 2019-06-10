---
title: Exportar modelos de aprendizaje automático de Spark con MLeap
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo exportar modelos con MLeap de aprendizaje automático de Spark.
author: lgongmsft
ms.author: shivprashant
ms.reviewer: jroth
manager: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 7d62cc32be569bec6e1560b4b712ff0ac9cba553
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66803058"
---
# <a name="export-spark-machine-learning-models-with-mleap"></a>Exportar modelos con MLeap de aprendizaje automático de Spark

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Un escenario de aprendizaje automático típico implica el entrenamiento del modelo en Spark y la puntuación fuera de Spark. Exportar modelos en un formato portátil, que se puede usar fuera de Spark. [MLeap](https://github.com/combust/mleap) es un formato de intercambio de este tipo modelo. Permite a Spark canalizaciones de aprendizaje automático y modelos que se exportan como formatos de portátiles y usar en cualquier sistema basados en JVM con el `Mleap` en tiempo de ejecución.

Esta guía muestra cómo puede exportar los modelos de spark mediante Mleap. Los pasos se resume a continuación y se detallan con código en la sección siguiente.

1. Empiece por crear un modelo de Spark. Para este uso **el modelo de entrenamiento y de creación de aprendizaje automático con Spark [aquí.](train-and-create-machinelearning-models-with-spark.md)**
2. El siguiente paso vamos a **importar los datos training\test y el modelo**
3. **Exportar el modelo como `Mleap` agrupación**. Este paquete exportado puede usarse ahora para puntuar fuera de spark.
4. Para validar, importaremos el `Mleap` agrupar back nuevo y usarlo para puntuar en Spark.

## <a name="step-1---start-by-creating-a-spark-model"></a>Paso 1: inicio mediante la creación de un modelo de Spark
Ejecute [el modelo de entrenamiento y de creación de aprendizaje automático con Spark](train-and-create-machinelearning-models-with-spark.md) para crear conjuntos de entrenamiento y pruebas y el modelo y se conservan en el almacenamiento HDFS. El modelo debe exportarse como `AdultCensus.mml` bajo el `spark_ml` directory.

## <a name="step-2---import-the-trainingtest-data-and-the-model"></a>Paso 2: importar los datos training\test y el modelo

Paso 1 crea el `AdultCensus.mml`, que es un modelo de spark. 

En este paso, importar el modelo de spark.

```python
import mleap.pyspark
from mleap.pyspark.spark_support import SimpleSparkSerializer
from pyspark.ml import PipelineModel

model_name = "AdultCensus.mml"
model_fs = "/spark_ml/" + model_name

print("load pyspark model from hbfs")
model = PipelineModel.load(model_fs)
print("Model is " , model)
print("Model stages", model.stages)
```

## <a name="step-3---export-the-model-as-mleap-bundle"></a>Paso 3: exportar el modelo como `Mleap` agrupación

Exportar el modelo de Spark como un portátil `Mleap` modelar y conservarlos en almacenamiento local. Después de este paso, el modelo está disponible en un portátil `Mleap` dar formato y se puede usar fuera de Spark.

```python
import os

#Get the train and test datasets

# Write the train and test data sets to intermediate storage

train_data_path = "/spark_ml/AdultCensusIncomeTrain"
test_data_path = "/spark_ml/AdultCensusIncomeTest"

train = spark.read.orc(train_data_path)
test = spark.read.orc(test_data_path)

print("train: ({}, {})".format(train.count(), len(train.columns)))
train.printSchema()

print("test: ({}, {})".format(test.count(), len(test.columns)))
test.printSchema()

# serialize the model to a zip file in JSON format
model_name_export = "adult_census_pipeline.zip"
model_name_path = os.getcwd()
model_file = os.path.join(model_name_path, model_name_export)

# serialize the model to a zip file in JSON format
model_name_export = "adult_census_pipeline.zip"
model_name_path = os.getcwd()
model_file = os.path.join(model_name_path, model_name_export)

# remove an old model file, if needed.
try:
    os.remove(model_file)
except OSError:
    pass

model_file_path = "jar:file:{}".format(model_file)
model.serializeToBundle(model_file_path, model.transform(train))

```

Conservar la `Mleap` agrupación de local a hdfs

```python
print("persist the mleap bundle from local to hdfs")
from subprocess import Popen, PIPE
proc = Popen(["hadoop", "fs", "-put", "-f", model_file, os.path.join("/spark_ml", model_name_export)], stdout=PIPE, stderr=PIPE)
s_output, s_err = proc.communicate()
if(s_err):
    print("Error when storing to HDFS")
```

## <a name="step-3---validate-by-importing-the-mleap-bundle-and-scoring-in-spark"></a>Paso 3: validar por importar la `Mleap` agrupación y la puntuación en Spark
En el paso 2, ya se ha exportado el modelo a un portátil `Mleap` formato que se puede usar fuera de Spark. En este paso, se importará el `Mleap` serializado en Spark y usarlo en Spark a la puntuación en el conjunto de pruebas.
   
```python
model_deserialized = PipelineModel.deserializeFromBundle(model_file_path)
print("The deserialized model is ", model_deserialized)
print("The deserialized model stages are", model_deserialized.stages)

from pyspark.ml.evaluation import BinaryClassificationEvaluator

# make prediction
pred = model_deserialized.transform(test)


# evaluate. note only 2 metrics are supported out of the box by Spark ML.
bce = BinaryClassificationEvaluator(rawPredictionCol='rawPrediction')
au_roc = bce.setMetricName('areaUnderROC').evaluate(pred)
au_prc = bce.setMetricName('areaUnderPR').evaluate(pred)

print("Results of using the model score test set")
print("Area under ROC: {}".format(au_roc))
print("Area Under PR: {}".format(au_prc))
```

## <a name="references"></a>References

* [Introducción a los cuadernos de PySpark](notebooks-guidance.md)
* [Entrenamiento y de crear el modelo de aprendizaje automático con Spark](train-and-create-machinelearning-models-with-spark.md)
