---
title: paquete de Python de revoscalepy
description: Introducción al módulo revoscalepy en SQL Server Machine Learning Services con Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 76c68d0753c4ba29387b3378c1086ce9bce4f53b
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715777"
---
# <a name="revoscalepy-python-module-in-sql-server"></a>revoscalepy (módulo de Python en SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

**revoscalepy** es un módulo compatible con Python35 de Microsoft que admite computación distribuida, contextos de cálculo remotos y algoritmos de ciencia de datos de alto rendimiento. Se basa en el paquete **RevoScaleR** para R (distribuido con Microsoft R Server y SQL Server R Services), lo que ofrece una funcionalidad similar a la siguiente:

+ Contextos de cálculo locales y remotos en sistemas que tienen la misma versión de **revoscalepy**
+ Funciones de visualización y transformación de datos
+ Funciones de ciencia de datos, escalables a través del procesamiento en paralelo o distribuido
+ Rendimiento mejorado, incluido el uso de las bibliotecas matemáticas de Intel

Los orígenes de datos y los contextos de cálculo que se crean en **revoscalepy** también se pueden usar en algoritmos de aprendizaje automático. Para obtener una introducción a estos algoritmos, vea [Microsoftml Python Module in SQL Server](ref-py-microsoftml.md).

## <a name="full-reference-documentation"></a>Documentación de referencia completa

La biblioteca **revoscalepy** se distribuye en varios productos de Microsoft, pero el uso es el mismo si se obtiene la biblioteca en SQL Server u otro producto. Dado que las funciones son iguales, la [documentación de las funciones individuales de revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) se publica en una sola ubicación en la [referencia de Python](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) para Microsoft machine learning Server. Si hay algún comportamiento específico del producto, las discrepancias se anotarán en la página de ayuda de la función.

## <a name="versions-and-platforms"></a>Versiones y plataformas

El módulo **revoscalepy** se basa en Python 3,5 y solo está disponible cuando se instala uno de los siguientes productos o descargas de Microsoft:

+ [Servicios de aprendizaje de máquina SQL Server](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 o posterior](https://docs.microsoft.com/machine-learning-server/)
+ [Bibliotecas de cliente de Python para un cliente de ciencia de datos](setup-python-client-tools-sql.md)

> [!NOTE]
> Las versiones completas del producto son solo de Windows, empezando por SQL Server 2017. La compatibilidad con Linux para **revoscalepy** es nueva en [SQL Server vista previa de 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="functions-by-category"></a>Funciones por categoría

En esta sección se enumeran las funciones por categoría para darle una idea de cómo se usa cada una de ellas. También puede usar la [tabla de contenido](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) para buscar funciones en orden alfabético.

## <a name="1-data-source-and-compute"></a>1: origen de datos y proceso

**revoscalepy** incluye funciones para crear orígenes de datos y establecer la ubicación, o el *contexto de cálculo*, de dónde se realizan los cálculos. En la tabla siguiente se enumeran las funciones relevantes para SQL Server escenarios.

En algunos casos, SQL Server y Python usan tipos de datos diferentes. Para obtener una lista de las asignaciones entre los tipos de datos de SQL y Python, vea [tipos de datos de Python a SQL](python-libraries-and-data-types.md).

| Función| Descripción|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) |  Cree un objeto de contexto de cálculo SQL Server para enviar los cálculos a una instancia remota. Varias funciones **revoscalepy** toman el contexto de cálculo como argumento. Para obtener un ejemplo de cambio de contexto, consulte [crear un modelo con revoscalepy](../tutorials/use-python-revoscalepy-to-create-model.md).|
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxsqlserverdata) | Cree un objeto de datos basado en una consulta o tabla de SQL Server. |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxodbcdata)| Cree un origen de datos basado en una conexión ODBC. |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxxdfdata) | Cree un origen de datos basado en un archivo XDF local. Los archivos XDF se usan a menudo para descargar los datos en memoria en el disco. Un archivo XDF puede ser útil cuando se trabaja con más datos de los que se pueden transferir de la base de datos en un lote, o más datos de los que caben en la memoria. Por ejemplo, si mueve regularmente grandes cantidades de datos de una base de datos a una estación de trabajo local, en lugar de consultar la base de datos varias veces para cada operación de R, puede usar el archivo XDF como un tipo de caché para guardar los datos localmente y, después, trabajar con ellos en el área de trabajo de R. |

> [!TIP]
> Si no está familiarizado con la idea de orígenes de datos o contextos de cálculo, se recomienda empezar con la [informática distribuida](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing) en la documentación de Microsoft machine learning Server.

## <a name="2-data-manipulation-etl"></a>2: manipulación de datos (ETL)

| Función | Descripción |
|----------|-------------|
|[rx_import](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-import) | Importe los datos en un archivo. xdf o una trama de datos.|
|[rx_data_step](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-data-step) | Transforme los datos de un conjunto de datos de entrada en un conjunto de datos de salida.|

<a name="bkmk_algorithms"></a>

## <a name="3-training-and-summarization"></a>3-aprendizaje y Resumen

| Función| Descripción|
| ------- | ---------- |
|[rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) | Ajustar los árboles de decisión impulsados por gradiente estocástico|
|[rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) | Ajustar la clasificación y los bosques de decisión de regresión|
|[rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) | Ajustar los árboles de clasificación y regresión |
|[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) | Crear un modelo de regresión lineal|
|[rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) | Crear un modelo de regresión logística|
|[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) | Generar resúmenes de univariante de objetos en revoscalepy.|

También debe revisar las funciones de [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) para ver otros enfoques.

<a name="ml-scoring"></a>

## <a name="4-scoring-functions"></a>4: funciones de puntuación

| Función| Descripción|
| ------- | ---------- |
| [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | Generar predicciones a partir de un modelo entrenado|) | Genera predicciones a partir de un modelo entrenado y se puede usar para la puntuación en tiempo real. |
|[rx_predict_default](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-default) | Calcule valores de predicción y residuos con los objetos rx_lin_mod y rx_logit. |
|[rx_predict_rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dforest) | Calcular los valores previstos o ajustados para un conjunto de datos de un objeto rx_dforest o rx_btrees. |
|[rx_predict_rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dtree) | Calcular los valores previstos o ajustados para un conjunto de datos de un objeto rx_dtree. |

## <a name="how-to-work-with-revoscalepy"></a>Cómo trabajar con revoscalepy

Se puede llamar a las funciones de **revoscalepy** en el código de Python encapsulado en procedimientos almacenados. La mayoría de los desarrolladores compilan soluciones **revoscalepy** localmente y, después, migran el código Python finalizado a procedimientos almacenados como un ejercicio de implementación.

Cuando se ejecuta localmente, normalmente se ejecuta un script de Python desde la línea de comandos o desde un entorno de desarrollo de Python, y se especifica un contexto de proceso de SQL Server mediante una de las funciones de **revoscalepy** . Puede usar el contexto de cálculo remoto para todo el código o para funciones individuales. Por ejemplo, puede que desee descargar el entrenamiento del modelo en el servidor para usar los datos más recientes y evitar el movimiento de datos.

Cuando esté preparado para encapsular el script de Python dentro de un procedimiento almacenado, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), se recomienda volver a escribir el código como una sola función que tiene entradas y salidas claramente definidas. 

Las entradas y salidas deben ser tramas de datos **pandas** . Una vez hecho esto, puede llamar al procedimiento almacenado desde cualquier cliente que admita T-SQL, pasar fácilmente las consultas SQL como entradas y guardar los resultados en tablas SQL. Para obtener un ejemplo, consulte [aprendizaje de análisis de Python en base de datos para desarrolladores de SQL](../tutorials/sqldev-in-database-python-for-sql-developers.md).

### <a name="using-revoscalepy-with-microsoftml"></a>Uso de revoscalepy con microsoftml

Las funciones de Python para [microsoftml](ref-py-microsoftml.md) se integran con los contextos de cálculo y los orígenes de datos que se proporcionan en revoscalepy. Al llamar a funciones desde microsoftml, por ejemplo, al definir y entrenar un modelo, use las funciones revoscalepy para ejecutar el código de Python localmente o en un contexto de cálculo remoto de SQl Server.

En el ejemplo siguiente se muestra la sintaxis para la importación de módulos en el código de Python. Después, puede hacer referencia a las funciones individuales que necesite.

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>Vea también

+ [Tutoriales de Python](../tutorials/sql-server-python-tutorials.md)
+ [Tutorial: Inserción de código de Python en T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Referencia de Python (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)
