---
title: 'Creación de un modelo de Python: revoscalepy'
description: Escritura de scripts de Python con las funciones de revoscalepy para crear modelos de ciencia de datos que se ejecutan de forma remota en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/25/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 5faa8688f3036f80b947ccc5d99c09c4612f26fb
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2020
ms.locfileid: "81116028"
---
# <a name="use-python-with-revoscalepy-to-create-a-model-that-runs-remotely-on-sql-server"></a>Usar Python con revoscalepy para crear un modelo que se ejecute de forma remota en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La biblioteca [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) para Python de Microsoft proporciona algoritmos de ciencia de datos para la exploración, la visualización, las transformaciones y el análisis de datos. Esta biblioteca tiene una importancia estratégica en escenarios de integración de Python en SQL Server. En un servidor de varios núcleos, las funciones de **revoscalepy** se pueden ejecutar en paralelo. En una arquitectura distribuida con un servidor central y estaciones de trabajo cliente (equipos físicos independientes, todos ellos con la misma biblioteca de **revoscalepy**), se puede escribir código de Python que se inicie localmente, pero que después pase a ejecutarse en una instancia de SQL Server remota en la que residen los datos.

**revoscalepy** se encuentra en los siguientes productos y distribuciones de Microsoft:

+ [SQL Server Machine Learning Services (en base de datos)](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server (servidor independiente que no es de SQL)](https://docs.microsoft.com/machine-learning-server/index)
+ [Bibliotecas de Python del lado cliente (para estaciones de trabajo de desarrollo)](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) 

En este ejercicio se muestra cómo crear un modelo de regresión lineal basado en [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod), uno de los algoritmos de **revoscalepy** que acepta el contexto de proceso como una entrada. El código que ejecutará en este ejercicio desplazará la ejecución del código de un entorno informático local a uno remoto, habilitado por las funciones de **revoscalepy** que habilitan un contexto de proceso remoto.

En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Usar **revoscalepy** para crear un modelo lineal
> * Desplazar operaciones desde un contexto de proceso local a uno remoto

## <a name="prerequisites"></a>Prerrequisitos

Como datos de ejemplo de este ejercicio, se usa la base de datos [**flightdata**](demo-data-airlinedemo-in-sql.md).

Necesita un IDE para ejecutar el código de ejemplo de este artículo y el IDE debe estar vinculado al archivo ejecutable de Python.

Para practicar un cambio de contexto de proceso, necesita una [estación de trabajo local](../python/setup-python-client-tools-sql.md) y una instancia del motor de base de datos de SQL Server con [Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) y Python habilitados. 

> [!Tip]
> Si no tiene dos equipos, puede instalar las aplicaciones pertinentes que le permitan simular un contexto de proceso remoto en un equipo físico. En primer lugar, una instalación de [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) funciona como instancia "remota". En segundo lugar, la instalación de las [bibliotecas de cliente de Python funciona](../python/setup-python-client-tools-sql.md) como cliente. En el mismo equipo, tendrá dos copias de la misma distribución de Python y las bibliotecas de Python de Microsoft. Para completar el ejercicio correctamente, tendrá que realizar un seguimiento de las rutas de acceso de archivo y de la copia de Python.exe que se utiliza.

## <a name="remote-compute-contexts-and-revoscalepy"></a>Contextos de proceso remotos y revoscalepy

En este ejemplo se muestra el proceso de creación de un modelo de Python en un contexto de proceso remoto que le permite trabajar desde un cliente, pero elegir un entorno remoto en el que se realizan las operaciones, como SQL Server, Spark o Machine Learning Server. El objetivo del contexto de proceso remoto es llevar el proceso a donde residen los datos.

Para ejecutar el código de Python en SQL Server, se necesita el paquete **revoscalepy**. Se trata de un paquete de Python especial proporcionado por Microsoft, similar al paquete **RevoScaleR** para el lenguaje R. El paquete **revoscalepy** admite la creación de contextos de proceso y proporciona la infraestructura para pasar datos y modelos entre una estación de trabajo local y un servidor remoto. La función de **revoscalepy** que admite la ejecución de código en la base de datos es [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver).

En esta lección, se usarán los datos de SQL Server para entrenar un modelo lineal basado en [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod), una función de **revoscalepy** que admite la regresión en conjuntos de datos muy grandes. 

En esta lección también se muestran los aspectos básicos de cómo configurar y usar un **contexto de proceso de SQL Server** en Python. Para obtener una descripción de cómo funcionan los contextos de proceso con otras plataformas y qué contextos de proceso se admiten, consulte [Contexto de proceso para la ejecución de scripts en Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context).


## <a name="run-the-sample-code"></a>Ejecución del código de ejemplo

Una vez que haya preparado la base de datos y tenga los datos para el entrenamiento almacenados en una tabla, abra un entorno de desarrollo de Python y ejecute el ejemplo de código.

Este código realiza los pasos siguientes:

1. Importa las bibliotecas y funciones necesarias.
2. Crea una conexión a SQL Server. Crea objetos de **origen de datos** para trabajar con los datos.
3. Modifica los datos mediante **transformaciones** de modo que el algoritmo de regresión logística pueda usarlos.
4. Llama a `rx_lin_mod` y define la fórmula utilizada para ajustar el modelo.
5. Genera un conjunto de predicciones basadas en los datos originales.
6. Crea un resumen basado en la predicción de valores.

Todas las operaciones se realizan utilizando una instancia de SQL Server como contexto de proceso.

> [!NOTE]
> Para ver una demo de este ejemplo ejecutándose desde la línea de comandos, vea este vídeo: [Análisis avanzado de SQL Server 2017 con Python](https://www.youtube.com/watch?v=FcoY795jTcc)

### <a name="sample-code"></a>Código de ejemplo

```python
from revoscalepy import RxComputeContext, RxInSqlServer, RxSqlServerData
from revoscalepy import rx_lin_mod, rx_predict, rx_summary
from revoscalepy import RxOptions, rx_import

import os

def test_linmod_sql():
    sql_server = os.getenv('PYTEST_SQL_SERVER', '.')
    
    sql_connection_string = 'Driver=SQL Server;Server=' + sqlServer + ';Database=sqlpy;Trusted_Connection=True;'
    print("connectionString={0!s}".format(sql_connection_string))

    data_source = RxSqlServerData(
        sql_query = "select top 10 * from airlinedemosmall",
        connection_string = sql_connection_string,

        column_info = {
            "ArrDelay" : { "type" : "integer" },
            "DayOfWeek" : {
                "type" : "factor",
                "levels" : [ "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday" ]
            }
        })

    sql_compute_context = RxInSqlServer(
        connection_string = sql_connection_string,
        num_tasks = 4,
        auto_cleanup = False
        )

    #
    # Run linmod locally
    #
    linmod_local = rx_lin_mod("ArrDelay ~ DayOfWeek", data = data_source)
    #
    # Run linmod remotely
    #
    linmod = rx_lin_mod("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)

    # Predict results
    # 
    predict = rx_predict(linmod, data = rx_import(input_data = data_source))
    summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)
```

### <a name="defining-a-data-source-vs-defining-a-compute-context"></a>Definición de un origen de datos y definición de un contexto de proceso

Un origen de datos es diferente de un contexto de proceso. El *origen de datos* define los datos que se usan en el código. El contexto de proceso define dónde se ejecutará el código. Pero se usa parte de la misma información:

+ Las variables de Python, como `sql_query` y `sql_connection_string`, definen el origen de los datos. 

    Pase estas variables al constructor [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) para implementar el **objeto de origen de datos** denominado `data_source`.

+ Se crea un **objeto de contexto de proceso** mediante el constructor [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver). El **objeto de contexto de proceso** resultante se denomina `sql_cc`.

    En este ejemplo se vuelve a usar la misma cadena de conexión que se usó en el origen de datos, suponiendo que los datos están en la misma instancia de SQL Server que va a usar como el contexto de proceso. 
    
    No obstante, el origen de datos y el contexto de proceso pueden estar en servidores diferentes.
 
### <a name="changing-compute-contexts"></a>Cambio de los contextos de proceso

Después de definir un contexto de proceso, debe establecer el **contexto de proceso activo**. 

De forma predeterminada, la mayoría de las operaciones se ejecutan localmente, lo que significa que si no se especifica un contexto de proceso diferente, los datos se capturarán en el origen de datos y el código se ejecutará en el entorno de Python actual.

Hay dos maneras de establecer el contexto de proceso activo:
+ Como argumento de un método o función
+ Mediante una llamada a `rx_set_computecontext`

#### <a name="set-compute-context-as-an-argument-of-a-method-or-function"></a>Establecimiento del contexto de proceso como un argumento de un método o una función

En este ejemplo, se establece el contexto de proceso mediante un argumento de la función individual **rx**.
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

Este contexto de proceso se reutiliza en la llamada a [rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary):

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rx_set_compute_context"></a>Establecimiento explícito de un contexto de proceso mediante rx_set_compute_context

La función [rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) permite alternar entre los contextos de proceso que ya se han definido.

Después de establecer un contexto de proceso, este permanece activo hasta que se cambie.

### <a name="using-parallel-processing-and-streaming"></a>Uso de streaming y procesamiento en paralelo

Al definir el contexto de proceso, también puede establecer parámetros que controlen la forma en que el contexto de proceso administra los datos. Estos parámetros difieren en función del tipo de origen de datos.

Para contextos de proceso de SQL Server, puede establecer el tamaño del lote o proporcionar sugerencias sobre el grado de paralelismo que se va a usar en las tareas en ejecución.

+ El ejemplo se ejecutó en un equipo con cuatro procesadores, por lo que el parámetro `num_tasks` está establecido en 4 para permitir el uso máximo de recursos. 
+ Si establece este valor en 0, SQL Server usa el valor predeterminado, que consiste en ejecutar tantas tareas en paralelo como sea posible, según la configuración actual de MAXDOP para el servidor. Pero el número exacto de tareas que se pueden asignar depende de muchos otros factores, como la configuración del servidor y otros trabajos que se estén ejecutando.

## <a name="next-steps"></a>Pasos siguientes

Estos tutoriales y ejemplos adicionales de Python muestran escenarios de un extremo a otro con orígenes de datos más complejos, así como el uso de contextos de proceso remotos.

+ [Python para desarrolladores de SQL en base de datos](sqldev-in-database-python-for-sql-developers.md)
+ [Compilación de un modelo predictivo con Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
