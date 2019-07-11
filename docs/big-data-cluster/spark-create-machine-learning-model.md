---
title: Crear y exportar modelos con MLeap de aprendizaje automático de Spark
titleSuffix: SQL Server big data clusters
description: Usar PySpark para entrenar y crear modelos de aprendizaje automático con Spark en clústeres de macrodatos de SQL Server (versión preliminar). Exportar con MLeap y, a continuación, Puntuar el modelo con Java en SQL Server.
author: lgongmsft
ms.author: lgong
ms.reviewer: mikeray
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: aa4c31eca725e8e662937259f078cf00a3441915
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727376"
---
# <a name="create-export-and-score-spark-machine-learning-models-on-sql-server-big-data-clusters"></a>Crear, exportar y puntuar modelos de aprendizaje automático de Spark en clústeres de macrodatos de SQL Server

El ejemplo siguiente muestra cómo crear un modelo con [Sparkml](https://spark.apache.org/docs/latest/ml-guide.html), exportar el modelo a [MLeap](http://mleap-docs.combust.ml/)y puntuación del modelo en SQL Server con su [extensión del lenguaje Java](../language-extensions/language-extensions-overview.md). Esto se hace en el contexto de un clúster de macrodatos de SQL Server 2019.

El siguiente diagrama ilustra el trabajo realizado en este ejemplo:

![Exportación de puntuación "Train" con spark](./media/spark-create-machine-learning-model/train-score-export-with-spark.png)

## <a name="prerequisites"></a>Requisitos previos

Todos los archivos de este ejemplo se encuentran en [ https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml ](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml).

Para ejecutar el ejemplo, también debe tener los siguientes requisitos previos:

- Un [clúster grande de datos de SQL Server](deploy-get-started.md)

- [Herramientas de datos de gran tamaño](deploy-big-data-tools.md)
   - **kubectl**
   - **curl**
   - **Azure Data Studio**

## <a name="model-training-with-spark-ml"></a>Entrenamiento del modelo de aprendizaje automático de Spark

Para este ejemplo, los datos del censo (**AdultCensusIncome.csv**) se usa para crear un modelo de canalización de aprendizaje automático de Spark.

1. Use la [mleap_sql_test/setup.sh](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/setup.sh) archivo para descargar el conjunto de datos de internet y colocarlo en HDFS en el clúster de macrodatos de SQL Server. Esto le permite tener acceso a Spark.

1. A continuación, descargue el notebook de ejemplo [train_score_export_ml_models_with_spark.ipynb](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb). Desde una línea de comandos de PowerShell o bash, ejecute el comando siguiente para descargar el Bloc de notas:

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb"
   ```

   Este bloc de notas contiene celdas con los comandos necesarios para esta sección del ejemplo.

1. Abra el Bloc de notas en Azure Data Studio y ejecute cada bloque de código. Para obtener más información sobre cómo trabajar con equipos portátiles, consulte [para usar cuadernos en versión preliminar de SQL Server 2019](notebooks-guidance.md).

En primer lugar, los datos se leen en Spark y división en entrenamiento y conjuntos de datos de prueba. A continuación, el código entrena un modelo de canalización con los datos de entrenamiento. Por último, exporta el modelo a una agrupación MLeap.

> [!TIP]
> También puede revisar o ejecutar el código de Python asociado con estos pasos fuera el Bloc de notas en el [mleap_sql_test/mleap_pyspark.py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/mleap_pyspark.py) archivo.

## <a name="model-scoring-with-sql-server"></a>Modelo de puntuación con SQL Server

Ahora que el modelo de canalización de aprendizaje automático de Spark está en una serialización comunes [MLeap agrupación](http://mleap-docs.combust.ml/core-concepts/mleap-bundles.html) formato, puede Puntuar el modelo en Java sin la presencia de Spark. 

Este ejemplo se utiliza el [extensión del lenguaje Java](../language-extensions/language-extensions-overview.md) en SQL Server. A fin de Puntuar el modelo en SQL Server, primero deberá crear una aplicación de Java que puede cargar el modelo en Java y puntuarlo. Puede encontrar el código de ejemplo para esta aplicación de Java en el [carpeta mssql-mleap-app](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mssql-mleap-app).

Después de compilar el ejemplo, puede utilizar Transact-SQL para llamar a la aplicación de Java y puntuar el modelo con una tabla de base de datos. Esto puede verse en tres [mleap_sql_test/mleap_sql_tests.py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/mleap_sql_tests.py) archivo de código fuente.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de datos de gran tamaño, vea [cómo implementar grandes de datos de SQL Server a clústeres de Kubernetes](deployment-guidance.md)
