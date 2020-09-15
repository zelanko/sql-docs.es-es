---
title: revoscalepy (paquete de Python)
description: revoscalepy es un paquete de Python de Microsoft que admite computación distribuida, contextos de cálculo remoto y algoritmos de ciencia de datos de alto rendimiento.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 07/14/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c5932a335dc1789256932f327ba9dab58c6afaf7
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178629"
---
# <a name="revoscalepy-python-package-in-sql-server-machine-learning-services"></a>revoscalepy (paquete de Python en SQL Server Machine Learning Services)
[!INCLUDE [SQL Server 2017 and later](../../includes/applies-to-version/sqlserver2017.md)]

**revoscalepy** es un paquete de Python de Microsoft que admite computación distribuida, contextos de cálculo remoto y algoritmos de ciencia de datos de alto rendimiento. El paquete se incluye en [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md).

El paquete ofrece la capacidad siguiente:

+ Contextos de cálculo local y remoto en sistemas que tienen la misma versión de **revoscalepy**
+ Funciones de visualización y transformación de datos
+ Funciones de ciencia de datos, escalables a través del procesamiento paralelo o distribuido
+ Rendimiento mejorado, incluido el uso de las bibliotecas matemáticas de Intel

Los orígenes de datos y los contextos de cálculo que se creen en **revoscalepy** también se pueden usar en algoritmos de aprendizaje automático. Para obtener una introducción a estos algoritmos, consulte [módulo microsoftml de Python en SQL Server](ref-py-microsoftml.md).

## <a name="full-reference-documentation"></a>Documentación de referencia completa

El paquete de **revoscalepy** se distribuye en varios productos de Microsoft, pero el uso es el mismo, se obtenga el paquete en SQL Server o en otro producto. Dado que las funciones son las mismas, la [documentación de las funciones individuales de revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) se publica en una sola ubicación en la [referencia de Python](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) para Microsoft Machine Learning Server. Si existe algún comportamiento específico del producto, las discrepancias se anotarán en la página de ayuda de la función.

## <a name="versions-and-platforms"></a>Versiones y plataformas

El módulo de **revoscalepy** se basa en Python 3.5 y solo está disponible cuando se instala uno de los siguientes productos o descargas de Microsoft:

+ [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 o posterior](https://docs.microsoft.com/machine-learning-server/)
+ [Bibliotecas de cliente de Python para un cliente de ciencia de datos](setup-python-client-tools-sql.md)

> [!NOTE]
> En SQL Server 2017, las versiones completas del producto son solo para Windows. Para **revoscalepy** en [SQL Server 2019](../../linux/sql-server-linux-setup-machine-learning.md) y versiones posteriores, se admiten tanto Windows como Linux.

## <a name="functions-by-category"></a>Funciones por categoría

En esta sección se enumeran las funciones por categoría, para darle una idea del uso de cada una de ellas. También puede usar la [tabla de contenido](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) para ver las funciones en orden alfabético.

## <a name="1-data-source-and-compute"></a>1- Origen de datos y cálculo

**revoscalepy** incluye funciones para crear orígenes de datos y establecer la ubicación, o el *contexto de proceso*, de dónde se realizan los cálculos. En la tabla siguiente se enumeran las funciones relevantes para los escenarios de SQL Server.

En algunos casos, SQL Server y Python usan tipos de datos diferentes. Para obtener una lista de las asignaciones entre los tipos de datos de SQL y Python, vea [tipos de datos entre Python y SQL](python-libraries-and-data-types.md).

| Función| Descripción|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) |  Cree un objeto de contexto de proceso de SQL Server para enviar los cálculos a una instancia remota. Varias funciones de **revoscalepy** toman el contexto de proceso como argumento. Para obtener un ejemplo de cambio de contexto, vea [Crear un modelo con revoscalepy](../tutorials/use-python-revoscalepy-to-create-model.md).|
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxsqlserverdata) | Cree un objeto de datos basado en una consulta o una tabla de SQL Server. |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxodbcdata)| Cree un origen de datos basado en una conexión ODBC. |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxxdfdata) | Cree un origen de datos basado en un archivo XDF local. Los archivos XDF a menudo se usan para descargar en el disco los datos en memoria. Un archivo XDF puede ser útil al trabajar con más datos de los que se pueden transferir desde la base de datos en un lote o con más datos de los que caben en la memoria. Por ejemplo, si suele mover grandes cantidades de datos de una base de datos a una estación de trabajo local, en lugar de consultar la base de datos varias veces para cada operación de R, puede usar el archivo XDF a modo de memoria caché para guardar los datos localmente y, después, trabajar con ellos en el área de trabajo de R. |

> [!TIP]
> Si no está familiarizado con la idea de los orígenes de datos o los contextos de cálculo, le recomendamos que comience con la [computación distribuida](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing) en la documentación de Microsoft Machine Learning Server.

## <a name="2-data-manipulation-etl"></a>2- Manipulación de datos (ETL)

| Función | Descripción |
|----------|-------------|
|[rx_import](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-import) | Importe los datos en un archivo .xdf o una trama de datos.|
|[rx_data_step](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-data-step) | Transforme los datos de un conjunto de datos de entrada en un conjunto de datos de salida.|

<a name="bkmk_algorithms"></a>

## <a name="3-training-and-summarization"></a>3- Aprendizaje y resumen

| Función| Descripción|
| ------- | ---------- |
|[rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) | Ajustar los árboles de decisión impulsados por gradiente estocástico|
|[rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) | Ajustar los bosques de decisión de regresión clasificación|
|[rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) | Ajustar los bosques de regresión y clasificación |
|[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) | Crear un modelo de regresión lineal|
|[rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) | Crear un modelo de regresión logística|
|[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) | Generar resúmenes de variable única de objetos en revoscalepy|

También debe revisar las funciones de [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) para ver otros enfoques.

<a name="ml-scoring"></a>

## <a name="4-scoring-functions"></a>4- Funciones de puntuación

| Función| Descripción|
| ------- | ---------- |
| [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | Generar predicciones a partir de un modelo entrenado|) | Genera predicciones a partir de un modelo entrenado y se puede usar para obtener la puntuación en tiempo real. |
|[rx_predict_default](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-default) | Calcular valores y valores residuales previstos mediante objetos rx_lin_mod y rx_logit |
|[rx_predict_rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dforest) | Calcular los valores previstos o ajustados para un conjunto de datos a partir de un objeto rx_dforest o rx_btrees |
|[rx_predict_rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dtree) | Calcular los valores previstos o ajustados para un conjunto de datos a partir de un objeto rx_dtree |

## <a name="how-to-work-with-revoscalepy"></a>Cómo trabajar con revoscalepy

Las funciones de **revoscalepy** se pueden llamar en código de Python encapsulado en procedimientos almacenados. La mayoría de los desarrolladores compilan soluciones de **revoscalepy** localmente y, después, migran el código de Python final a los procedimientos almacenados como un ejercicio de implementación.

Cuando se ejecuta localmente, normalmente se ejecuta un script de Python desde la línea de comandos o desde un entorno de desarrollo de Python, y se especifica un contexto de proceso de SQL Server mediante una de las funciones de **revoscalepy**. Puede usar el contexto de proceso remoto para todo el código o para funciones individuales. Por ejemplo, puede que quiera descargar el entrenamiento del modelo en el servidor para usar los datos más recientes y evitar el movimiento de datos.

Cuando esté preparado para encapsular el script de Python dentro de un procedimiento almacenado, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), se recomienda que vuelva a escribir el código como una sola función que tenga las entradas y salidas definidas con claridad. 

Las entradas y salidas deben ser tramas de datos **Pandas**. Una vez hecho esto, puede llamar al procedimiento almacenado desde cualquier cliente que admita T-SQL, pasar fácilmente las consultas SQL como entradas y guardar los resultados en tablas SQL. Para obtener un ejemplo, vea [Análisis de Python en base de datos para desarrolladores de SQL](../tutorials/python-taxi-classification-introduction.md).

### <a name="using-revoscalepy-with-microsoftml"></a>Uso de revoscalepy con microsoftml

Las funciones de Python para [microsoftml](ref-py-microsoftml.md) se integran con los contextos de cálculo y los orígenes de datos que se proporcionan en revoscalepy. Al llamar a funciones desde microsoftml —por ejemplo, al definir y entrenar un modelo—, use las funciones de revoscalepy para ejecutar el código de Python localmente o en un contexto de proceso remoto de SQL Server.

En el ejemplo siguiente se muestra la sintaxis para la importación de módulos en el código de Python. Después, puede hacer referencia a las funciones individuales que necesite.

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>Consulte también

+ [Tutoriales de Python](../tutorials/sql-server-python-tutorials.md)
+ [Referencia de Python (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)
