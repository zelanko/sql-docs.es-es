---
title: Introducción a revoscalepy el paquete de Python en SQL Server Machine Learning | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8b2e217f599112019e96f3e20b727456b9da607f
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51697573"
---
# <a name="introducing-revoscalepy-in-sql-server-machine-learning"></a>Introducción a revoscalepy en SQL Server Machine Learning
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**revoscalepy** es una nueva biblioteca de Python proporcionado por Microsoft para admitir el procesamiento distribuido, remoto contextos de equipos y los algoritmos de alto rendimiento para desarrolladores de Python.

Se basa en el **RevoScaleR** paquete de R, que se proporcionó en Microsoft R Server y SQL Server R Services y pretende proporcionar la misma funcionalidad:

+ Es compatible con varios contextos de proceso, locales y remotos
+ Proporciona funciones equivalentes a las de RevoScaleR para visualización y la transformación de datos
+ Proporciona versiones de Python de RevoScaleR algoritmos de aprendizaje automático para el procesamiento paralelo o distribuido
+ Rendimiento mejorado, incluido el uso de las bibliotecas de matemáticas de Intel

También se proporcionan paquetes de MicrosoftML para R y Python. Para obtener más información, consulte [utilizando MicrosoftML en SQL Server](../using-the-microsoftml-package.md)

## <a name="versions-and-supported-platforms"></a>Las versiones y plataformas compatibles

El **revoscalepy** módulo está disponible cuando se instala uno de los siguientes productos de Microsoft:

+ Machine Learning Services en SQL Server 2017
+ Microsoft Machine Learning Server 9.2.0 o posterior

Para obtener la versión más reciente de revoscalepy, instale actualización acumulativa 1 para SQL Server 2017. Incluye muchas mejoras en Python, incluidos:

+ Una nueva función de Python, `rx_create_col_info`, que obtiene información del esquema de un origen de datos de SQL Server, como [rxCreateColInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcreatecolinfo) para 
+ Mejoras de [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec) para admitir escenarios paralelos mediante el `RxLocalParallel` contexto de proceso. 

## <a name="supported-functions-and-data-types"></a>Tipos de datos y funciones admitidos

Esta sección proporciona información general de los tipos de datos de Python y nuevas funciones de Python que se admiten en el **revoscalepy** módulo, a partir de la versión de SQL Server 2017 CTP 2.0. 

Para obtener la lista más reciente de las funciones de las bibliotecas de Python publicadas hasta la fecha, consulte estos vínculos:

+ [revoscalepy para Python](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)

+ [microsoftml para Python](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)

### <a name="data-types-data-sources-and-compute-contexts"></a>Tipos de datos, orígenes de datos y contextos de cálculo

SQL Server y Python usa diferentes tipos de datos en algunos casos. Para obtener una lista de asignaciones entre tipos de datos SQL y Python, consulte [extensión Python](../concepts/extension-python.md).

Orígenes de datos admitidos para el aprendizaje automático con Python en SQL Server incluye los archivos locales, incluidos los archivos XDF, base de datos de SQL Server y orígenes de datos ODBC.

Cree el objeto de origen de datos mediante el uso de funciones que se enumeran en la tabla siguiente. Después de definir el origen de datos, cargar o transformar los datos mediante un adecuado [función ETL](#bkmk_etl).

> [!IMPORTANT]
> Muchos de los nombres de función han cambiado desde la versión inicial de Python en CTP 2.0.

**Datos de SQL Server**

+ Use [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) para definir un origen de datos de una tabla o consulta
+ Use [RxInSqlServer](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxinsqlserver) para crear un contexto de proceso de SQL Server
+ Use [RxOdbcData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxodbcdata) para crear un origen de datos desde una conexión de ODBC

**revoscalepy** también admite la [origen de datos XDF](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxxdfdata), que se usa para mover datos entre la memoria y otros orígenes de datos.

> [!TIP]
> Si está familiarizado con la idea de los orígenes de datos o contextos de proceso, se recomienda que comience por leer sobre cómo funciona la informática distribuida para el aprendizaje automático en [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction).


### <a name="bkmk_algorithms"></a>Aprendizaje automático y las funciones de resumen

Se incluyen los siguientes algoritmos de aprendizaje automático y el resumen de funciones de RevoScaleR en SQL Server 2017, a partir de CTP 2.0.

| Función| Descripción|Notas|
| ------ | ------ |------ |
|`rx_btrees` | Árboles de decisión incrementados de ajuste de gradiente estocástico|`rx_btrees_ex` en CTP 2.0|
|`rx_dforest` | Bosques de decisión de clasificación y regresión con ajuste|`rx_dforest_ex` en CTP 2.0|
|`rx_dtree` | Árboles de clasificación y regresión con ajuste |`rx_dtree_ex` en CTP 2.0|
|`rx_lin_mod` | Crear un modelo lineal|`rx_lin_mod_ex` en CTP 2.0|
|`rx_logit` | Crear un modelo de regresión logística|`rx_logit_ex` en CTP 2.0|
|`rx_predict` | Generar predicciones con un modelo entrenado|`rx_predict_ex` en CTP 2.0|
|`rx_summary` | Generar un resumen del modelo||

También se proporcionan los nuevos algoritmos de aprendizaje automático con la versión de Python de [MicrosoftML](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package):

| Función| Descripción|
| ------ | ------ |
|`rx_fast_forest` |Crear un modelo de bosque de decisión|
|`rx_fast_linear` | Regresión lineal con estocástico dual ascenso de coordenadas|
|`rx_fast_trees` | Crear un modelo de árbol ampliado |
|`rx_logistic_regression` | Crear un modelo de regresión logística|
|`rx_neural_network` | Crear un modelo de red neuronal personalizable |
|`rx_oneclass_svm` | Crea un modelo SVM en un conjunto de datos desequilibrado, para su uso en la detección de anomalías|

> [!TIP]
> Muchos de estos algoritmos ya se proporcionan como módulos en Azure Machine Learning.

MicrosoftML para Python también incluye una variedad de transformaciones y funciones auxiliares, como:

+ `rx_predict` genera predicciones a partir de un modelo entrenado y puede usarse para puntuar en tiempo real
+ funciones de características de imagen
+ funciones para la extracción de procesamiento y la opinión del texto

Para obtener más información, consulte [Introducción a MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)


> [!NOTE]
> La Comunidad de Python usa las convenciones de codificación que pueden ser distintas del que está acostumbrado, incluidas todas las letras minúsculas y caracteres de subrayado en lugar de mayúsculas y minúsculas tipo camel para los nombres de parámetro. Además, quizás haya observado que la **revoscalepy** biblioteca siempre está en minúscula. ¡Así es! Otra convención de Python.
> 
> Consulte las sugerencias en la documentación de referencia de Python para Microsoft R: [ayuda con la función Python][funciones Python](https://docs.microsoft.com/r-server/python-reference/introducing-python-package-reference)

## <a name="examples"></a>Ejemplos

Puede ejecutar código que incluya **revoscalepy** funciona localmente o en un contexto de cálculo remoto. También puede ejecutar Python en SQL Server mediante la inserción de código de Python en un procedimiento almacenado.

Cuando se ejecuta localmente, normalmente ejecutar un script de Python desde la línea de comandos o desde un entorno de desarrollo de Python y especificar un contexto de proceso de SQL Server mediante uno de los **revoscalepy** funciones. Puede usar el contexto de cálculo remoto para todo el código, o para funciones individuales. Por ejemplo, es posible que desea descargar el entrenamiento del modelo en el servidor para usar los datos más recientes y evitar el movimiento de datos.

Si desea crear un script de Python completo dentro del procedimiento almacenado, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), se recomienda que vuelva a escribir el código como una sola función que se haya definido claramente las entradas y salidas. Deben ser entradas y salidas **pandas** tramas de datos. Cuando esto sucede, puede llamar al procedimiento almacenado desde cualquier cliente que admita T-SQL, fácilmente pasar una consulta SQL como entradas y guardar los resultados en las tablas SQL. Para obtener un ejemplo, vea [en bases de datos de análisis de Python para desarrolladores de SQL](../tutorials/sqldev-in-database-python-for-sql-developers.md).

### <a name="using-remote-compute-contexts"></a>Usar contextos de cálculo remoto

+ [Crear un modelo mediante revoscalepy](../tutorials/use-python-revoscalepy-to-create-model.md)

  Este ejemplo muestra cómo ejecutar Python mediante una instancia de SQL Server como contexto de proceso.

### <a name="using-a-stored-procedure"></a>Mediante un procedimiento almacenado

+ [Ejecutar Python mediante T-SQL](../tutorials/run-python-using-t-sql.md)

  En este ejemplo se muestra el mecanismo básico de llamar al script de Python que se incrusta en un procedimiento almacenado.

### <a name="using-revoscalepy-with-microsoftml"></a>Uso de revoscalepy con MicrosoftML

Las funciones de Python para MicrosoftML se integran con los contextos de cálculo y los orígenes de datos que se proporcionan en revoscalepy. Por lo tanto, podría usar un algoritmo de MicrosoftML para definir y entrenar un modelo en Python y utilizar las funciones de revoscalepy para ejecutar el código de Python, ya sea localmente o en un contexto de proceso de SQl Server.

Importar los módulos en el código de Python y, a continuación, hacer referencia a las funciones individuales que necesita.

```Python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

### <a name="requirements"></a>Requisitos

Para ejecutar código de Python en SQL Server, debe tener instalado SQL Server 2017 junto con la característica **Machine Learning Services**y habilita el lenguaje Python. Las versiones anteriores de SQL Server no admiten la integración de Python.

> [!NOTE]
> Distribuciones de código abierto de Python no se admiten los contextos de cálculo de SQL Server. Sin embargo, si tiene que publicar y consumir aplicaciones de Python desde Windows, puede instalar a Microsoft Machine Learning Server sin necesidad de instalar SQL Server. Para obtener más información, consulte [instalar SQL Server 2017 Machine Learning Server (independiente)](../install/sql-machine-learning-standalone-windows-install.md).

## <a name="get-more-help"></a>Obtener más ayuda

Documentación completa de estas API estará disponible cuando se lance el producto. Mientras tanto, se recomienda que haga referencia a la función correspondiente en las bibliotecas de RevoScaleR o MicrosoftML.

+ [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler).
+ [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml)

Puede obtener ayuda en cualquier función de Python mediante la importación del módulo y, a continuación, llamar a `help()`. Por ejemplo, ejecutar `help(revoscalepy)` desde el IDE de Python, devuelve una lista de todas las funciones del módulo de revoscalepy, con sus firmas.

Si usa herramientas de Python para Visual Studio, puede usar IntelliSense para obtener ayuda de la sintaxis y el argumento. Para obtener más información, consulte [compatibilidad con Python en Visual Studio](https://docs.microsoft.com/visualstudio/python/installation)y descargar la extensión que coincida con su versión de Visual Studio. Puede usar Python con Visual Studio 2015 y 2017 o versiones anteriores.

## <a name="see-also"></a>Vea también

[Tutoriales de Python](../tutorials/sql-server-python-tutorials.md)
