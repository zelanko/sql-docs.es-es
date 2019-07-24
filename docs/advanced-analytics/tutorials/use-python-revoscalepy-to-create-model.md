---
title: Uso de Python con revoscalepy para crear un modelo
description: Escritura de scripts de Python con las funciones de revoscalepy para crear modelos de ciencia de datos que se ejecutan de forma remota en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/25/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3fe398a6210936553fc40b10cc9a42f395a98785
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345807"
---
# <a name="use-python-with-revoscalepy-to-create-a-model-that-runs-remotely-on-sql-server"></a>Use Python con revoscalepy para crear un modelo que se ejecute de forma remota en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

La biblioteca de Python de [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) de Microsoft proporciona algoritmos de ciencia de datos para la exploración, la visualización, las transformaciones y el análisis de datos. Esta biblioteca tiene una importancia estratégica en escenarios de integración de Python en SQL Server. En un servidor de varios núcleos, las funciones de **revoscalepy** se pueden ejecutar en paralelo. En una arquitectura distribuida con un servidor central y estaciones de trabajo cliente (equipos físicos independientes, que tienen la misma biblioteca **revoscalepy** ), puede escribir código de Python que se inicie localmente, pero después desplazará la ejecución a una instancia de SQL Server remota. donde residen los datos.

Puede encontrar **revoscalepy** en los siguientes productos y distribuciones de Microsoft:

+ [SQL Server Machine Learning Services (in-Database)](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server (no SQL, servidor independiente)](https://docs.microsoft.com/machine-learning-server/index)
+ [Bibliotecas de Python del lado cliente (para estaciones de trabajo de desarrollo)](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) 

En este ejercicio se muestra cómo crear un modelo de regresión lineal basado en [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod), uno de los algoritmos de **revoscalepy** que acepta el contexto de cálculo como una entrada. El código que ejecutará en este ejercicio desplazará la ejecución del código de un entorno informático local a remoto, habilitado por las funciones de **revoscalepy** que habilitan un contexto de cálculo remoto.

Al completar este tutorial, obtendrá información sobre cómo:

> [!div class="checklist"]
> * Uso de **revoscalepy** para crear un modelo lineal
> * Operaciones de desplazamiento desde el contexto de cálculo local a remoto

## <a name="prerequisites"></a>Requisitos previos

Los datos de ejemplo que se usan en este ejercicio son la base de datos [**flightdata**](demo-data-airlinedemo-in-sql.md) .

Necesita un IDE para ejecutar el código de ejemplo de este artículo y el IDE debe estar vinculado al archivo ejecutable de Python.

Para practicar un cambio de contexto de proceso, necesita una [estación de trabajo local](../python/setup-python-client-tools-sql.md) y una instancia del motor de base de datos de SQL Server con [Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) y Python habilitado. 

> [!Tip]
> Si no tiene dos equipos, puede simular un contexto de cálculo remoto en un equipo físico mediante la instalación de aplicaciones relevantes. En primer lugar, una instalación de [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) funciona como la instancia "Remote". En segundo lugar, la instalación de las [bibliotecas de cliente de Python funciona](../python/setup-python-client-tools-sql.md) como el cliente. Tendrá dos copias de la misma distribución de Python y las bibliotecas de Microsoft Python en el mismo equipo. Tendrá que realizar un seguimiento de las rutas de acceso de archivo y qué copia de Python. exe usa para completar el ejercicio correctamente.

## <a name="remote-compute-contexts-and-revoscalepy"></a>Contextos de cálculo remotos y revoscalepy

Este ejemplo muestra el proceso de creación de un modelo de Python en un contexto de cálculo remoto, que le permite trabajar desde un cliente, pero elegir un entorno remoto, como SQL Server, Spark o Machine Learning Server, donde se realizan las operaciones. El objetivo del contexto de cálculo remoto es llevar el cálculo a donde residen los datos.

Para ejecutar el código de Python en SQL Server requiere el paquete **revoscalepy** . Se trata de un paquete de Python especial proporcionado por Microsoft, similar al paquete **RevoScaleR** para el lenguaje R. El paquete **revoscalepy** admite la creación de contextos de cálculo y proporciona la infraestructura para pasar datos y modelos entre una estación de trabajo local y un servidor remoto. La función **revoscalepy** que admite la ejecución de código en la base de datos es [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver).

En esta lección, se usan los datos de SQL Server para entrenar un modelo lineal basado en [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod), una función de **revoscalepy** que admite la regresión en conjuntos de datos muy grandes. 

En esta lección también se muestran los aspectos básicos de cómo configurar y usar un **contexto de proceso de SQL Server** en Python. Para obtener una explicación de cómo funcionan los contextos de cálculo con otras plataformas y qué contextos de cálculo se admiten, vea [contexto de proceso para la ejecución de scripts en machine learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context).


## <a name="run-the-sample-code"></a>Ejecutar el código de ejemplo

Una vez preparada la base de datos y contenga los datos para el entrenamiento almacenados en una tabla, abra un entorno de desarrollo de Python y ejecute el ejemplo de código.

El código realiza los pasos siguientes:

1. Importa las bibliotecas y funciones necesarias.
2. Crea una conexión a SQL Server. Crea objetos de **origen de datos** para trabajar con los datos.
3. Modifica los datos mediante transformaciones para que los pueda usar el algoritmo de regresión logística.
4. Llama `rx_lin_mod` a y define la fórmula utilizada para ajustar el modelo.
5. Genera un conjunto de predicciones basadas en los datos originales.
6. Crea un resumen basado en los valores de predicción.

Todas las operaciones se realizan utilizando una instancia de SQL Server como el contexto de cálculo.

> [!NOTE]
> Para ver una demostración de este ejemplo que se ejecuta desde la línea de comandos, vea este vídeo: [SQL Server 2017 análisis avanzado con Python](https://www.youtube.com/watch?v=FcoY795jTcc)

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

### <a name="defining-a-data-source-vs-defining-a-compute-context"></a>Definir un origen de datos frente a definir un contexto de cálculo

Un origen de datos es diferente de un contexto de cálculo. El *origen de datos* define los datos que se usan en el código. El contexto de cálculo define dónde se ejecutará el código. Sin embargo, usan parte de la misma información:

+ Las variables de Python, `sql_query` como `sql_connection_string`y, definen el origen de los datos. 

    Pase estas variables al constructor [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) para implementar el **objeto de origen** de datos `data_source`denominado.

+ Puede crear un **objeto de contexto de cálculo** mediante el constructor [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) . El **objeto de contexto de cálculo** resultante se `sql_cc`denomina.

    En este ejemplo se vuelve a usar la misma cadena de conexión que usó en el origen de datos, suponiendo que los datos están en la misma instancia de SQL Server que va a usar como el contexto de cálculo. 
    
    Sin embargo, el origen de datos y el contexto de cálculo pueden estar en servidores diferentes.
 
### <a name="changing-compute-contexts"></a>Cambiar contextos de cálculo

Después de definir un contexto de cálculo, debe establecer el **contexto de cálculo activo**. 

De forma predeterminada, la mayoría de las operaciones se ejecutan localmente, lo que significa que si no se especifica un contexto de proceso diferente, los datos se capturarán desde el origen de datos y el código se ejecutará en el entorno de Python actual.

Hay dos maneras de establecer el contexto de cálculo activo:
+ Como argumento de un método o función
+ Llamando a`rx_set_computecontext`

#### <a name="set-compute-context-as-an-argument-of-a-method-or-function"></a>Establecer el contexto de cálculo como un argumento de un método o una función

En este ejemplo, se establece el contexto de cálculo mediante un argumento de la función **RX** individual.
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

Este contexto de cálculo se reutiliza en la llamada a [rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary):

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rxsetcomputecontext"></a>Establecer un contexto de cálculo explícitamente mediante rx_set_compute_context

La función [rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) le permite alternar entre los contextos de cálculo que ya se han definido.

Después de haber establecido el contexto de cálculo activo, permanece activo hasta que lo cambie.

### <a name="using-parallel-processing-and-streaming"></a>Usar procesamiento paralelo y transmisión por secuencias

Al definir el contexto de cálculo, también puede establecer parámetros que controlen cómo se administran los datos mediante el contexto de cálculo. Estos parámetros difieren en función del tipo de origen de datos.

Para SQL Server contextos de cálculo, puede establecer el tamaño del lote o proporcionar sugerencias sobre el grado de paralelismo que se va a usar en las tareas en ejecución.

+ El ejemplo se ejecutó en un equipo con cuatro procesadores, por `num_tasks` lo que el parámetro se establece en 4 para permitir el uso máximo de los recursos. 
+ Si establece este valor en 0, SQL Server usa el valor predeterminado, que consiste en ejecutar tantas tareas en paralelo como sea posible, en la configuración de MAXDOP actual del servidor. Sin embargo, el número exacto de tareas que se pueden asignar depende de muchos otros factores, como la configuración del servidor, y otros trabajos que se están ejecutando.

## <a name="next-steps"></a>Pasos siguientes

Estos tutoriales y ejemplos adicionales de Python muestran escenarios de un extremo a otro con orígenes de datos más complejos, así como el uso de contextos de cálculo remotos.

+ [Python de bases de datos para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md)
+ [Creación de un modelo predictivo con Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
