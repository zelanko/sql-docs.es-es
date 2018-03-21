---
title: "Introducción a revoscalepy | Documentos de Microsoft"
ms.custom: 
ms.date: 10/05/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 2649596abecfd92d40a860e743c867e0ff80ed26
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/21/2018
---
# <a name="introducing-revoscalepy"></a>Introducción a revoscalepy
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

**revoscalepy** es una nueva biblioteca proporcionados por Microsoft para admitir la computación distribuida, de proceso remoto contextos y algoritmos de alto rendimiento para Python.

Se basa en el **RevoScaleR** paquete de R, que se proporcionó en Microsoft R Server y SQL Server R Services y pretende proporcionar la misma funcionalidad:

+ Admite varios contextos de proceso, locales y remotos
+ Proporciona funciones equivalentes a las de RevoScaleR para visualización y transformación de datos
+ Proporciona versiones de Python RevoScaleR algoritmos de aprendizaje automático para el procesamiento distribuido o en paralelo
+ Mejorar el rendimiento, incluido el uso de las bibliotecas de matemáticas de Intel

También se proporcionan MicrosoftML paquetes de R y Python. Para obtener más información, vea [utilizando MicrosoftML en SQL Server](../using-the-microsoftml-package.md)

## <a name="versions-and-supported-platforms"></a>Las versiones y plataformas compatibles

El **revoscalepy** módulo está disponible cuando se instala uno de los siguientes productos de Microsoft:

+ Servicios de SQL Server de 2017 de aprendizaje automático
+ Aprendizaje de máquina de Microsoft Server 9.2.0 o posterior

Para obtener la versión más reciente de revoscalepy, instale la actualización acumulativa 1 para SQL Server 2017. Incluye muchas mejoras en Python, incluidos:

+ Una nueva función de Python, `rx_create_col_info`, que obtiene información del esquema de un origen de datos de SQL Server, como [rxCreateColInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcreatecolinfo) para 
+ Mejoras en [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec) para admitir escenarios paralelos usando el `RxLocalParallel` contexto de proceso. 

## <a name="supported-functions-and-data-types"></a>Tipos admitidos de funciones y datos

Esta sección proporciona información general de los tipos de datos de Python y nuevas funciones de Python que se admiten en el **revoscalepy** módulo, a partir de la versión 2.0 de CTP de SQL Server de 2017. 

Para obtener la lista más reciente de las funciones de las bibliotecas de Python publicadas hasta la fecha, vea los siguientes vínculos:

+ [revoscalepy para Python](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package)

+ [microsoftml para Python](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)

### <a name="data-types-data-sources-and-compute-contexts"></a>Tipos de datos, orígenes de datos y contextos de proceso

SQL Server y Python utiliza diferentes tipos de datos en algunos casos. Para obtener una lista de asignaciones entre tipos de datos SQL y Python, consulte [Python bibliotecas y tipos de datos](python-libraries-and-data-types.md).

Orígenes de datos admitidos para el aprendizaje automático con Python en SQL Server incluye archivos locales, incluidos los archivos xdf., orígenes de datos ODBC y base de datos de SQL Server.

Crear el objeto de origen de datos mediante el uso de funciones que se enumeran en la tabla siguiente. Después de definir el origen de datos, cargar o transformar los datos mediante una adecuada [función ETL](#bkmk_etl).

> [!IMPORTANT]
> Muchos de los nombres de función han cambiado desde la versión inicial de Python en CTP 2.0.

**Datos de SQL Server**

+ Use [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) para definir un origen de datos de una tabla o consulta
+ Use [RxInSqlServer](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxinsqlserver) para crear un contexto de proceso de SQL Server
+ Use [RxOdbcData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxodbcdata) para crear un origen de datos desde una conexión de ODBC

**revoscalepy** también admite la [origen de datos xdf.](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxxdfdata), que se usa para mover datos entre la memoria y otros orígenes de datos.

> [!TIP]
> Si está familiarizado con la idea de orígenes de datos o contextos de proceso, es recomendable que comience por leer sobre works informática distribuida para el aprendizaje automático en [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-introduction).


### <a name="bkmk_algorithms"></a>Aprendizaje automático y funciones de resumen

Se incluyen los siguientes algoritmos de aprendizaje automático y el resumen de las funciones de RevoScaleR en SQL Server de 2017 desde CTP 2.0.

| Función| Description|Notas|
| ------ | ------ |------ |
|`rx_btrees` | Árboles de decisión incrementados de gradiente estocástico ajuste|`rx_btrees_ex` en CTP 2.0|
|`rx_dforest` | Bosques de decisión de clasificación y regresión de ajuste|`rx_dforest_ex` en CTP 2.0|
|`rx_dtree` | Ajuste de los árboles de clasificación y regresión |`rx_dtree_ex` en CTP 2.0|
|`rx_lin_mod` | Crear un modelo lineal|`rx_lin_mod_ex` en CTP 2.0|
|`rx_logit` | Crear un modelo de regresión logística|`rx_logit_ex` en CTP 2.0|
|`rx_predict` | Generar predicciones de un modelo entrenado|`rx_predict_ex` en CTP 2.0|
|`rx_summary` | Generar un resumen del modelo||

Nuevos algoritmos de aprendizaje automático también se proporcionan con la versión de Python de [MicrosoftML](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package):

| Función| Description|
| ------ | ------ |
|`rx_fast_forest` |Crea un modelo de bosque de decisión|
|`rx_fast_linear` | Regresión lineal con estocástico ascenso coordenada dual|
|`rx_fast_trees` | Crear un modelo de árbol incrementado |
|`rx_logistic_regression` | Crear un modelo de regresión logística|
|`rx_neural_network` | Crear un modelo de red neuronal personalizable |
|`rx_oneclass_svm` | Crea un modelo SVM en un conjunto de datos equilibrado, para su uso en la detección de anomalías|

> [!TIP]
> Muchos de estos algoritmos ya se proporcionan como módulos de aprendizaje automático de Azure.

MicrosoftML para Python también incluye una serie de transformaciones y funciones auxiliares, como:

+ `rx_predict` genera predicciones a partir de un modelo entrenado y puede usarse para puntuar en tiempo real
+ funciones de características de imagen
+ funciones para la extracción de opiniones y procesamiento de texto

Para obtener más información, vea [Introducción a MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)


> [!NOTE]
> La Comunidad de Python usa las convenciones de codificación que pueden ser distintas del que está acostumbrado, incluidas todas las letras en minúsculas y caracteres de subrayado en lugar de grafía camel para los nombres de parámetro. Además, puede ser haya observado que el **revoscalepy** biblioteca siempre está en minúscula. ¡Así es! Otra convención de Python.
> 
> Consulte las sugerencias en la documentación de referencia de Python para Microsoft R: [Ayuda de la función de Python][funciones Python](https://docs.microsoft.com/r-server/python-reference/introducing-python-package-reference)

## <a name="examples"></a>Ejemplos

Puede ejecutar código que incluya **revoscalepy** funciona localmente o en un contexto de proceso remoto. También puede ejecutar Python dentro de SQL Server mediante la inserción de código de Python en un procedimiento almacenado.

Cuando se ejecuta localmente, normalmente ejecutar un script de Python desde la línea de comandos o desde un entorno de desarrollo de Python y especificar un contexto de proceso de SQL Server mediante uno de los **revoscalepy** funciones. Puede usar el contexto de proceso remoto para todo el código, o para las funciones individuales. Por ejemplo, puede descargar el entrenamiento del modelo en el servidor para usar los datos más recientes y evita los movimientos de datos.

Si desea colocar un script de Python completo dentro del procedimiento almacenado, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), se recomienda que vuelva a escribir el código como una única función que haya definido claramente entradas y salidas. Entradas y salidas deben estar **pandas** tramas de datos. Cuando esto sucede, puede llamar al procedimiento almacenado desde cualquier cliente que admita T-SQL, fácilmente pasar consultas SQL como entradas y guardar los resultados en las tablas SQL. Para obtener un ejemplo, vea [en bases de datos de análisis de Python para desarrolladores de SQL](../tutorials/sqldev-in-database-python-for-sql-developers.md).

### <a name="using-remote-compute-contexts"></a>Uso de contextos de proceso remoto

+ [Crear un modelo usando revoscalepy](../tutorials/use-python-revoscalepy-to-create-model.md)

  Este ejemplo muestra cómo ejecutar Python utilizando una instancia de SQL Server como el contexto de proceso.

### <a name="using-a-stored-procedure"></a>Mediante un procedimiento almacenado

+ [Ejecución de Python mediante T-SQL](../tutorials/run-python-using-t-sql.md)

  En este ejemplo se muestra el mecanismo básico de llamar al script de Python que se incrusta en un procedimiento almacenado.

### <a name="using-revoscalepy-with-microsoftml"></a>Uso de revoscalepy con MicrosoftML

Las funciones de Python para MicrosoftML se integran con los contextos de proceso y orígenes de datos que se proporcionan en revoscalepy. Por lo tanto, podría usar un algoritmo MicrosoftML para definir y entrenar un modelo de Python y utilizar las funciones de revoscalepy para ejecutar el código de Python, ya sea localmente o en un contexto de proceso de SQl Server.

Importar solo los módulos en el código Python y, a continuación, hacer referencia a las funciones individuales que necesita.

```Python
from microsoftml.modules.logistic_regression.rx_logistic_regression import rx_logistic_regression
from revoscalepy.functions.RxSummary import rx_summary
from revoscalepy.etl.RxImport import rx_import_datasource
```

### <a name="requirements"></a>Requisitos

Para ejecutar código de Python en SQL Server, debe tener instalado SQL Server 2017 junto con la característica **Machine Learning Services**y ha habilitado el idioma de Python. Las versiones anteriores de SQL Server no admiten la integración de Python.

> [!NOTE]
> Distribuciones de código abierto de Python no son compatibles con los contextos de proceso de SQL Server. Sin embargo, si tiene que publicar y consumir las aplicaciones de Python de Windows, puede instalar a Microsoft máquina aprendizaje Server sin necesidad de instalar SQL Server. Para obtener más información, consulte [instalar SQL Server de 2017 máquina aprendizaje Server (independiente)](../install/sql-machine-learning-standalone-windows-install.md).

## <a name="get-more-help"></a>Obtener más ayuda

La documentación completa de estas API estará disponible cuando se publica el producto. Mientras tanto, se recomienda que haga referencia a la función correspondiente en las bibliotecas de RevoScaleR o MicrosoftML.

+ [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler).
+ [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml)

Puede obtener ayuda sobre cualquier función de Python importando el módulo y, a continuación, llamar a `help()`. Por ejemplo, ejecutar `help(revoscalepy)` desde el IDE de Python devuelve una lista de todas las funciones en el módulo revoscalepy, con sus firmas.

Si usas Python Tools para Visual Studio, puede usar IntelliSense para obtener ayuda de la sintaxis y el argumento especificados. Para obtener más información, consulte [compatibilidad con Python en Visual Studio](http://docs.microsoft.com/visualstudio/python/installation)y descargar la extensión que coincida con su versión de Visual Studio. Puede utilizar Python con Visual Studio 2015 y 2017 o versiones anteriores.

## <a name="see-also"></a>Vea también

[Tutoriales de Python](../tutorials/sql-server-python-tutorials.md)
