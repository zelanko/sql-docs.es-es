---
title: Creación y exportación de modelos de aprendizaje automático de Spark con MLeap
titleSuffix: SQL Server big data clusters
description: Use PySpark para entrenar y crear modelos de aprendizaje automático con Spark [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] en (versión preliminar). Exportar con MLeap y puntuar el modelo con Java en SQL Server.
author: RogPodge
ms.author: roliu
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: bba570a4ac68cf5a4d1405d4152669ed9ed211a0
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2019
ms.locfileid: "69653412"
---
# <a name="create-export-and-score-spark-machine-learning-models-on-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd"></a>Crear, exportar y puntuar modelos de aprendizaje automático de Spark en[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

En el ejemplo siguiente se muestra cómo crear un modelo con los [ml de Spark](https://spark.apache.org/docs/latest/ml-guide.html), exportar el modelo a [MLeap](http://mleap-docs.combust.ml/)y puntuar el modelo en SQL Server con su [extensión de lenguaje Java](../language-extensions/language-extensions-overview.md). Esto se hace en el contexto de un clúster de macrodatos SQL Server 2019.

En el siguiente diagrama se ilustra el trabajo realizado en este ejemplo:

![Entrenar la exportación de la puntuación con Spark](./media/spark-create-machine-learning-model/train-score-export-with-spark.png)

## <a name="prerequisites"></a>Requisitos previos

Todos los archivos de este ejemplo se encuentran [https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml)en.

Para ejecutar el ejemplo, también debe cumplir los siguientes requisitos previos:

- Un [clúster de macrodatos SQL Server](deploy-get-started.md)

- [Herramientas de macrodatos](deploy-big-data-tools.md)
   - **kubectl**
   - **curl**
   - **Azure Data Studio**

## <a name="model-training-with-spark-ml"></a>Entrenamiento de modelos con Spark ML

En este ejemplo, los datos de censo (**AdultCensusIncome. csv**) se usan para crear un modelo de canalización de aprendizaje automático de Spark.

1. Use el archivo [mleap_sql_test/Setup. sh](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/mleap_sql_test/setup.sh) para descargar el conjunto de datos de Internet y colocarlo en HDFS en el clúster de macrodatos de SQL Server. Esto permite que Spark tenga acceso a él.

1. A continuación, descargue el Notebook de ejemplo [train_score_export_ml_models_with_spark. ipynb](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb). Desde una línea de comandos de PowerShell o Bash, ejecute el siguiente comando para descargar el cuaderno:

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb"
   ```

   Este cuaderno contiene celdas con los comandos necesarios para esta sección del ejemplo.

1. Abra el cuaderno en Azure Data Studio y ejecute cada bloque de código. Para obtener más información sobre el trabajo con cuadernos, vea [Uso de los cuadernos en la versión preliminar de SQL Server 2019](notebooks-guidance.md).

Los datos se leen primero en Spark y se dividen en conjuntos de datos de entrenamiento y de prueba. A continuación, el código entrena un modelo de canalización con los datos de entrenamiento. Por último, exporta el modelo a un conjunto de MLeap.

> [!TIP]
> También puede revisar o ejecutar el código de Python asociado a estos pasos fuera del cuaderno en el archivo [mleap_sql_test/mleap_pyspark. py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/mleap_sql_test/mleap_pyspark.py) .

## <a name="model-scoring-with-sql-server"></a>Puntuación del modelo con SQL Server

Ahora que el modelo de canalización de aprendizaje automático de Spark se encuentra en un formato común de agrupación de [MLeap](http://mleap-docs.combust.ml/core-concepts/mleap-bundles.html) de serialización, puede puntuar el modelo en Java sin la presencia de Spark. 

En este ejemplo se utiliza la [extensión del lenguaje Java](../language-extensions/language-extensions-overview.md) en SQL Server. Para puntuar el modelo en SQL Server, primero debe compilar una aplicación Java que pueda cargar el modelo en Java y puntuarlo. Puede encontrar el código de ejemplo para esta aplicación de Java en la [carpeta MSSQL-mleap-App](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/mssql-mleap-app).

Después de generar el ejemplo, puede usar Transact-SQL para llamar a la aplicación Java y puntuar el modelo con una tabla de base de datos. Esto puede verse en el archivo de código fuente [mleap_sql_test/mleap_sql_tests. py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/mleap_sql_test/mleap_sql_tests.py) .

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de Big Data, consulte [How to deploy [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] on Kubernetes](deployment-guidance.md)
