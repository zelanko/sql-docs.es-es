---
title: paquete de Python revoscalepy - SQL Server Machine Learning Services
description: Introducción al módulo revoscalepy en Machine Learning Services de SQL Server 2017 con Python.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/12/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3482a15392fa04f7f10d2acbb0843d124e27dc21
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962743"
---
# <a name="revoscalepy-python-module-in-sql-server"></a>revoscalepy (módulo de Python en SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**revoscalepy** es un módulo Python35 compatible de Microsoft que admite la informática distribuida, contextos de cálculo remotos y los algoritmos de ciencia de datos de alto rendimiento. Se basa en el **RevoScaleR** paquete de R (que se distribuye con Microsoft R Server y SQL Server R Services), que ofrece una funcionalidad similar:

+ Contextos en los sistemas que tienen la misma versión de proceso local y remoto **revoscalepy**
+ Funciones de transformación y la visualización de datos
+ Funciones de ciencia de datos, escalables a través de procesamiento paralelo o distribuido
+ Rendimiento mejorado, incluido el uso de las bibliotecas de matemáticas de Intel

Orígenes de datos y contextos de cálculo que se crean en **revoscalepy** también puede utilizarse en algoritmos de aprendizaje automático. Para obtener una introducción a estos algoritmos, vea [microsoftml módulo de Python en SQL Server](ref-py-microsoftml.md).

## <a name="full-reference-documentation"></a>Documentación de referencia completa

El **revoscalepy** library se distribuye en varios productos de Microsoft, pero el uso es el mismo si obtener la biblioteca de SQL Server u otro producto. Dado que las funciones son los mismos, [documentación para las funciones individuales revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) se publica en una sola ubicación en la [referencia de Python](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) para Microsoft Machine Learning Server. Debe cualquier producto específico comportamientos existen, se anotará discrepancias en la página de Ayuda de la función.

## <a name="versions-and-platforms"></a>Las versiones y plataformas

El **revoscalepy** módulo se basa en Python 3.5 y está disponible solo al instalar uno de los siguientes productos de Microsoft o descargas:

+ [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server 9.2.0 o posterior](https://docs.microsoft.com/machine-learning-server/)
+ [Bibliotecas de cliente de Python para un cliente de ciencia de datos](setup-python-client-tools-sql.md)

> [!NOTE]
> Versiones de lanzamiento de producto completo son sólo Windows, a partir de SQL Server 2017. Linux support para **revoscalepy** es nuevo en [versión preliminar de SQL Server de 2019](../../linux/sql-server-linux-setup-machine-learning.md).

## <a name="functions-by-category"></a>Funciones por categoría

En esta sección se enumera las funciones por categoría para darle una idea de cómo se usa cada uno de ellos. También puede usar el [tabla de contenido](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference) para buscar las funciones en orden alfabético.

## <a name="1-data-source-and-compute"></a>Proceso y el origen de datos 1

**revoscalepy** incluye funciones para crear orígenes de datos y configuración de la ubicación, o *contexto de proceso*, de donde se realizan los cálculos. Las funciones pertinentes para escenarios de SQL Server aparecen en la tabla siguiente.

SQL Server y Python usa diferentes tipos de datos en algunos casos. Para obtener una lista de asignaciones entre tipos de datos SQL y Python, consulte [tipos de datos de Python para SQL](python-libraries-and-data-types.md).

| Función| Descripción|
| ------- | ---------- |
| [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) |  Crear un objeto de contexto de proceso de SQL Server para enviar los cálculos a una instancia remota. Varios **revoscalepy** funciones toman el contexto de proceso como un argumento. Para obtener un ejemplo de cambio de contexto, vea [crear un modelo usando revoscalepy](../tutorials/use-python-revoscalepy-to-create-model.md).|
| [RxSqlServerData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxsqlserverdata) | Crear un objeto de datos basado en una consulta de SQL Server o la tabla. |
| [RxOdbcData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxodbcdata)| Crear un origen de datos basado en una conexión ODBC. |
| [RxXdfData](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxxdfdata) | Crear un origen de datos basado en un archivo XDF local. A menudo se usan archivos XDF para descargar datos en memoria en el disco. Un archivo XDF puede ser útil al trabajar con más datos que se pueden transferir desde la base de datos en un lote o más datos que pueden caber en memoria. Por ejemplo, si suele mover grandes cantidades de datos desde una base de datos a una estación de trabajo local, en lugar de consultar la base de datos varias veces para cada operación de R, se puede usar el archivo XDF como una especie de caché para guardar los datos localmente y, a continuación, trabajar con ellos en el área de trabajo de R. |

> [!TIP]
> Si está familiarizado con la idea de los orígenes de datos o contextos de proceso, se recomienda que comience con [informática distribuida](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-distributed-computing) en la documentación de Microsoft Machine Learning Server.

## <a name="2-data-manipulation-etl"></a>Manipulación de datos de 2 (ETL)

| Función | Descripción |
|----------|-------------|
|[rx_import](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-import) | Importar datos en una trama de datos o de archivos xdf.|
|[rx_data_step](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-data-step) | Transformar los datos de un conjunto de datos de entrada a un conjunto de datos de salida.|

<a name="bkmk_algorithms"></a>

## <a name="3-training-and-summarization"></a>3 cursos y resumen

| Función| Descripción|
| ------- | ---------- |
|[rx_btrees](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-btrees) | Árboles de decisión incrementados de ajuste de gradiente estocástico|
|[rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dforest) | Bosques de decisión de clasificación y regresión con ajuste|
|[rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-dtree) | Árboles de clasificación y regresión con ajuste |
|[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) | Crear un modelo de regresión lineal|
|[rx_logit](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-logit) | Crear un modelo de regresión logística|
|[rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) | Generar resúmenes de una variable de objetos de revoscalepy.|

También debe revisar las funciones de [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) enfoques adicionales.

<a name="ml-scoring"></a>

## <a name="4-scoring-functions"></a>Funciones de puntuación de 4

| Función| Descripción|
| ------- | ---------- |
| [rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | Generar predicciones con un modelo entrenado|) | Genera predicciones a partir de un modelo entrenado y puede usarse para puntuar en tiempo real. |
|[rx_predict_default](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-default) | Calcular valores de predicción y valores residuales mediante objetos rx_lin_mod y rx_logit. |
|[rx_predict_rx_dforest](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dforest) | Calcular los valores de predicción o ajustados de un conjunto de datos desde un objeto rx_dforest o rx_btrees. |
|[rx_predict_rx_dtree](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict-rx-dtree) | Calcular los valores de predicción o ajustados de un conjunto de datos de un objeto rx_dtree. |

## <a name="how-to-work-with-revoscalepy"></a>Cómo trabajar con revoscalepy

Las funciones de **revoscalepy** son invocables en código de Python encapsulada en procedimientos almacenados. La mayoría de los desarrolladores crear **revoscalepy** soluciones localmente, y, a continuación, migrar código de Python terminado a los procedimientos almacenados como un ejercicio de implementación.

Cuando se ejecuta localmente, normalmente ejecutar un script de Python desde la línea de comandos o desde un entorno de desarrollo de Python y especificar un contexto de proceso de SQL Server mediante uno de los **revoscalepy** funciones. Puede usar el contexto de cálculo remoto para todo el código, o para funciones individuales. Por ejemplo, es posible que desea descargar el entrenamiento del modelo en el servidor para usar los datos más recientes y evitar el movimiento de datos.

Cuando esté listo para encapsular el script de Python dentro de un procedimiento almacenado, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), se recomienda volver a escribir el código como una sola función que se haya definido claramente las entradas y salidas. 

Deben ser entradas y salidas **pandas** tramas de datos. Cuando esto sucede, puede llamar al procedimiento almacenado desde cualquier cliente que admita T-SQL, fácilmente pasar una consulta SQL como entradas y guardar los resultados en las tablas SQL. Para obtener un ejemplo, vea [Obtenga información sobre análisis de Python en bases de datos para desarrolladores de SQL](../tutorials/sqldev-in-database-python-for-sql-developers.md).

### <a name="using-revoscalepy-with-microsoftml"></a>Uso de revoscalepy con microsoftml

Funciones de la versión de Python para [microsoftml](ref-py-microsoftml.md) se integran con los orígenes de datos y contextos de proceso que se proporcionan en revoscalepy. Al llamar a funciones de microsoftml, por ejemplo al definir y entrenar un modelo, use las funciones de revoscalepy para ejecutar la versión de Python código ya sea localmente o contexto de proceso en un servidor SQl remoto.

El ejemplo siguiente muestra la sintaxis para la importación de módulos en el código de Python. A continuación, puede hacer referencia a las funciones individuales que necesita.

```python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

## <a name="see-also"></a>Vea también

+ [Tutoriales de Python](../tutorials/sql-server-python-tutorials.md)
+ [Tutorial: Insertar código de Python en T-SQL](../tutorials/run-python-using-t-sql.md)
+ [Referencia de Python (Microsoft Machine Learning Server)](https://docs.microsoft.com/machine-learning-server/python-reference/introducing-python-package-reference)
