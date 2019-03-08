---
title: Modelos de aprendizaje automático de Train/Create con Spark
titleSuffix: SQL Server 2019 big data clusters
description: Usar PySpark para entrenar y crear modelos de aprendizaje automático con Spark en clústeres de macrodatos de SQL Server (versión preliminar).
author: lgongmsft
ms.author: shivprashant
ms.manager: craigg
ms.reviewer: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 1ef8f66d220561407c0bcafedde8a402f871924a
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/07/2019
ms.locfileid: "57578115"
---
# <a name="train-and-create-machine-learning-models-with-spark"></a>Entrenar y crear modelos de aprendizaje automático con Spark

Spark en clústeres de macrodatos de SQL Server permite la inteligencia artificial y aprendizaje automático. El ejemplo muestra cómo para entrenar un modelo de aprendizaje automático con Python en Spark (PySpark) con datos almacenados en HDFS. 

El ejemplo es una guía paso a paso con fragmentos de código que se puede usar desde un cuaderno de Studio datos de Azure y cada paso de una ejecución de celda a la vez. Para obtener más información sobre cómo conectar con Spark desde Bloc de notas [aquí](notebooks-guidance.md)

En el ejemplo:

1. Comience con **comprender los datos y la predicción deseado**
2. **Cargar los datos en HDFS y preparar los datos** para crear el modelo
3. **Seleccione las características que se utilizará**
4. **Dividir los datos como conjunto de entrenamiento y prueba**
5. Juntar un **canalización ml y un modelo de compilación**
6. Utilice el modelo creado para **realizar predicciones**
7. Como paso final, **conservar el modelo creado para usar después**.

Aprendizaje automático de E2E implica varios pasos adicionales, p. ej., exploración de datos, análisis de componentes de selección y una entidad de característica, selección del modelo. Muchos de estos pasos se omiten aquí por razones de brevedad.

## <a name="step-1---understanding-the-data-and-prediction-desired"></a>Paso 1: descripción de los datos y la predicción deseado

Este ejemplo utiliza datos de ingresos del censo de adultos de [aquí]( https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv ). En `AdultCensusIncome.csv`, cada fila representa el intervalo de ingresos y otras características como la edad, horas por semana, educación, ocupación etcetera para un adulto determinado. Crear un modelo que puede predecir si el intervalo de ingresos. El modelo tomará la edad y horas por semana como características y predecir si los ingresos sería > 50 K o < 50 K. 

## <a name="step-2---upload-the-data-to-hdfs-and-basic-explorations-on-data"></a>Paso 2: cargar los datos en HDFS y exploraciones básicas en los datos
Conectarse a la puerta de enlace de Spark o HDFS desde Azure Data Studio y cree un directorio denominado `spark_ml` en HDFS. Descargar [AdultCensusIncome.csv]( https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv ) a su equipo local y la carga en HDFS. Cargar `AdultCensusIncome.csv` a la carpeta que creó.


Ahora, escribir algo de código. Puede copiar el código siguiente y péguelo en celdas individuales de un cuaderno en Azure Data Studio. 

El código siguiente lee el archivo CSV de trama de datos de Spark. Más allá de los que se cuenta el número de filas y columnas y mostrar los datos cargados.

```python
datafile = "/spark_ml/AdultCensusIncome.csv"

#Read the data to a spark data frame.
data_all = spark.read.format('csv').options(header='true', inferSchema='true', ignoreLeadingWhiteSpace='true', ignoreTrailingWhiteSpace='true').load(datafile)
print("Number of rows: {},  Number of coulumns : {}".format(data_all.count(), len(data_all.columns)))

#Replace "-" with "_" in column names
columns_new = [col.replace("-", "_") for col in data_all.columns]
data_all = data_all.toDF(*columns_new)

#Print Schema and show top 5 row
data_all.printSchema() 
data_all.show(5)
```

## <a name="step-3---select-features-to-use"></a>Paso 3: seleccionar características para usar

En este paso, use los siguientes dos términos
1. `Label`    -Hace referencia al valor que desea predecir. Esto se representa como una columna en los datos.  
2. `Features` -Hace referencia a las características de datos para predecir. También se conoce algún tiempo como `predictors` 

En este ejemplo `Label`, es el **ingresos** columna. Por motivos de simplicidad, elija **age** y **hours_per_week** como `Features`. En realidad se eligen características aplicando algunas técnicas de correlación para entender mejor lo que caracterizan a la etiqueta predicting.

```python
# Choose feature columns and the label column.
label = "income"
xvars = ["age", "hours_per_week"] #all numeric

print("label = {}".format(label))
print("features = {}".format(xvars))

select_cols = xvars
select_cols.append(label)
data = data_all.select(select_cols)

```

## <a name="step-4---split-as-training-and-test-set"></a>Paso 4: dividir como conjunto de entrenamiento y prueba

Utilice el 75% de las filas para entrenar el modelo y el resto del 25% para evaluar el modelo. Además, conservar el entrenamiento y probar los conjuntos de datos en el almacenamiento HDFS. El paso no es necesario, pero se muestra para demostrar cómo guardar y cargar con el formato ORC. Otros formatos, por ejemplo, `Parquet` también pueden usarse.

Registrar este paso que debería ver dos directorios creados con el nombre AdultCensusIncomeTrain y AdultCensusIncomeTest

```python

# Split data into train and test.
train, test = data.randomSplit([0.75, 0.25], seed=123)

print("train ({}, {})".format(train.count(), len(train.columns)))
print("test ({}, {})".format(test.count(), len(test.columns)))

train_data_path = "/spark_ml/AdultCensusIncomeTrain"
test_data_path = "/spark_ml/AdultCensusIncomeTest"

train.write.mode('overwrite').orc(train_data_path)
test.write.mode('overwrite').orc(test_data_path)
print("train and test datasets saved to {} and {}".format(train_data_path, test_data_path))

```

## <a name="step-5---put-together-a-pipeline-and-build-a-model"></a>Paso 5: elaborado una canalización y generar un modelo
[Canalización Spark ML](https://spark.apache.org/docs/2.3.1/ml-pipeline.html) permitir que todos los pasos de secuencia como un flujo de trabajo y que sea más fácil experimentar con distintos algoritmos y sus parámetros. El siguiente código crea primero las fases y, a continuación, reúne estas fases de canalización de aprendizaje automático.  LogisticRegression se utiliza para crear el modelo.

```python
from pyspark.ml import Pipeline, PipelineModel
from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler
from pyspark.ml.classification import LogisticRegression

reg = 0.1
print("Using LogisticRegression model with Regularization Rate of {}.".format(reg))

# create a new Logistic Regression model.
lr = LogisticRegression(regParam=reg)

dtypes = dict(train.dtypes)
dtypes.pop(label)

si_xvars = []
ohe_xvars = []
featureCols = []
for idx,key in enumerate(dtypes):
    if dtypes[key] == "string":
        featureCol = "-".join([key, "encoded"])
        featureCols.append(featureCol)
        
        tmpCol = "-".join([key, "tmp"])
        si_xvars.append(StringIndexer(inputCol=key, outputCol=tmpCol, handleInvalid="skip")) #, handleInvalid="keep"
        ohe_xvars.append(OneHotEncoder(inputCol=tmpCol, outputCol=featureCol))
    else:
        featureCols.append(key)

# string-index the label column into a column named "label"
si_label = StringIndexer(inputCol=label, outputCol='label')

# assemble the encoded feature columns in to a column named "features"
assembler = VectorAssembler(inputCols=featureCols, outputCol="features")

```

Ahora, elaborado la canalización. 

```python
# put together the pipeline
stages = []
stages.extend(si_xvars)
stages.extend(ohe_xvars)
stages.append(si_label)
stages.append(assembler)
stages.append(lr)
pipe = Pipeline(stages=stages)
print("Pipeline Created")

```

Ahora que se crea la canalización, usarlo para entrenar el modelo.

```python
# train the model
model = pipe.fit(train)
print("Model Trained")
print("Model is ", model)
print("Model Stages", model.stages)

```

## <a name="step-6---predict-using-the-model-and-evaluate-the-model-accuracy"></a>Paso 6: predecir usando el modelo y evaluar la precisión del modelo
El código siguiente usa el conjunto de datos de prueba para predecir el resultado con el modelo creado en el paso anterior. Mide la precisión del modelo con `areaUnderROC` y `areaUnderPR` métrica.

```python
from pyspark.ml.evaluation import BinaryClassificationEvaluator
# make prediction
pred = model.transform(test)

# evaluate. note only 2 metrics are supported out of the box by Spark ML.
bce = BinaryClassificationEvaluator(rawPredictionCol='rawPrediction')
au_roc = bce.setMetricName('areaUnderROC').evaluate(pred)
au_prc = bce.setMetricName('areaUnderPR').evaluate(pred)

print("Area under ROC: {}".format(au_roc))
print("Area Under PR: {}".format(au_prc))
```


## <a name="step-7---persist-the-models-to-hdfs"></a>Paso 7: conservar los modelos de HDFS
Por último, conservar el modelo en HDFS para su uso posterior. Registrar este paso en el modelo creado se guardan como /spark_ml/AdultCensus.mml

```python
##NOTE: by default the model is saved to and loaded from path

model_name = "AdultCensus.mml"
model_fs = "/spark_ml/" + model_name

model.write().overwrite().save(model_fs)
print("saved model to {}".format(model_fs))

# load the model file (from dbfs)
model2 = PipelineModel.load(model_fs)
assert str(model2) == str(model)
print("loaded model from {}".format(model_fs))
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre cómo empezar a trabajar con cuadernos de PySpark, consulte [para usar cuadernos](notebooks-guidance.md).