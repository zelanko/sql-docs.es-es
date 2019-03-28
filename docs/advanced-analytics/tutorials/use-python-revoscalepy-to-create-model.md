---
title: 'Uso de Python con revoscalepy para crear un modelo: SQL Server Machine Learning'
description: Escribir el script de Python con las funciones de revoscalepy para crear modelos de ciencia de datos que se ejecutan de forma remota en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/25/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: f0d9916414514e0ad0d73c3bb849b9c6e546289d
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58512461"
---
# <a name="use-python-with-revoscalepy-to-create-a-model-that-runs-remotely-on-sql-server"></a>Uso de Python con revoscalepy para crear un modelo que se ejecuta de forma remota en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

El [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) biblioteca de Python de Microsoft proporciona algoritmos de ciencia de datos para análisis, transformaciones, visualización y exploración de datos. Esta biblioteca tiene una importancia estratégica en escenarios de integración de Python en SQL Server. En un servidor de núcleo múltiple, **revoscalepy** funciones se pueden ejecutar en paralelo. En una arquitectura distribuida con una estación de trabajo cliente y servidor central (separar los equipos físicos, todos tienen el mismo **revoscalepy** biblioteca), puede escribir código de Python que se inicia localmente, pero, a continuación, la ejecución se desplaza una instancia remota de SQL Server donde residen los datos.

Puede encontrar **revoscalepy** en los siguientes productos de Microsoft y las distribuciones:

+ [SQL Server Machine Learning Services (en bases de datos)](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server (que no sea de SQL, servidor independiente)](https://docs.microsoft.com/machine-learning-server/index)
+ [Bibliotecas de Python del lado cliente (para las estaciones de trabajo de desarrollo)](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) 

Este ejercicio muestra cómo crear un modelo de regresión lineal basado en [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod), uno de los algoritmos en **revoscalepy** que acepta un contexto de cálculo como entrada. El código que se va a ejecutar en este ejercicio cambia la ejecución de código de una variable local a remoto entorno informático, habilitado de forma **revoscalepy** contexto de cálculo de las funciones que permiten un control remoto.

Al completar este tutorial, obtendrá información sobre cómo:

> [!div class="checklist"]
> * Use **revoscalepy** para crear un modelo lineal
> * Desplazar las operaciones de local al contexto de proceso remoto

## <a name="prerequisites"></a>Requisitos previos

Datos de ejemplo utilizados en este ejercicio están la [ **flightdata** ](demo-data-airlinedemo-in-sql.md) base de datos.

Necesita un IDE para ejecutar el código de ejemplo en este artículo y el IDE debe estar vinculado a la versión de Python ejecutable.

Para poner en práctica un cambio de contexto de proceso, necesita un [estación de trabajo local](../python/setup-python-client-tools-sql.md) y una instancia del motor de base de datos de SQL Server con [Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) y Python habilitado. 

> [!Tip]
> Si no tiene dos equipos, puede simular un contexto de proceso remoto en un equipo físico mediante la instalación de las aplicaciones pertinentes. Primero, una instalación de [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) funciona como la instancia "remota". Segundo, una instalación de la [bibliotecas de cliente de Python funciona](../python/setup-python-client-tools-sql.md) como el cliente. Tendrá dos copias de la misma distribución de Python y las bibliotecas de Python de Microsoft en el mismo equipo. Tendrá que realizar un seguimiento de las rutas de acceso de archivo y qué copia de la Python.exe usa para completar el ejercicio correctamente.

## <a name="remote-compute-contexts-and-revoscalepy"></a>Contextos de proceso remoto y de revoscalepy

Este ejemplo muestra el proceso de creación de un modelo de Python en un contexto de cálculo remoto, lo que permite trabajar desde un cliente, pero elija un entorno remoto, como SQL Server, Spark o Machine Learning Server, donde realmente se realizan las operaciones. El objetivo de contexto de cálculo remoto es poner el cálculo de donde residen los datos.

Para ejecutar código de Python en SQL Server requiere el **revoscalepy** paquete. Se trata de un paquete de Python especial proporcionado por Microsoft, similar a la **RevoScaleR** paquete para el lenguaje R. El **revoscalepy** paquete admite la creación de contextos de proceso y proporciona la infraestructura para pasar datos y modelos de entre una estación de trabajo local y un servidor remoto. El **revoscalepy** función que admite la ejecución de código de base de datos es [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver).

En esta lección, usar datos en SQL Server para entrenar un modelo lineal basado en [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod), una función en **revoscalepy** que admita la regresión en conjuntos de datos muy grandes. 

En esta lección también muestra los conceptos básicos de cómo configurar y, a continuación, usar un **contexto de proceso de SQL Server** en Python. Para obtener una explicación de cómo los contextos de cálculo trabajar con otras plataformas y contextos de cálculo que se admiten, consulte [contexto de proceso para la ejecución de scripts en Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context).


## <a name="run-the-sample-code"></a>Ejecute el código de ejemplo

Después de haber preparado la base de datos y con los datos de entrenamiento que se almacenan en una tabla, abra un entorno de desarrollo de Python y ejecute el ejemplo de código.

El código realiza los pasos siguientes:

1. Importa las bibliotecas necesarias y funciones.
2. Crea una conexión a SQL Server. Crea **origen de datos** objetos para trabajar con los datos.
3. Modifica los datos mediante **transformaciones** para que se puede usar el algoritmo de regresión logística.
4. Las llamadas `rx_lin_mod` y define la fórmula que se usa para ajustar el modelo.
5. Genera un conjunto de predicciones basados en los datos originales.
6. Crea un resumen basado en los valores de predicción.

Todas las operaciones se realizan con una instancia de SQL Server como contexto de proceso.

> [!NOTE]
> Para ver una demostración de este ejemplo se ejecuta desde la línea de comandos, vea este vídeo: [Análisis avanzado de SQL Server 2017 con Python](https://www.youtube.com/watch?v=FcoY795jTcc)

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

Un origen de datos es diferente de un contexto de proceso. El *origen de datos* define los datos usados en el código. El contexto de proceso define dónde se ejecutará el código. Sin embargo, usan la misma información:

+ Las variables de Python, como `sql_query` y `sql_connection_string`, definir el origen de datos. 

    Pasar estas variables para el [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) constructor para implementar la **objeto origen de datos** denominado `data_source`.

+ Crear un **objeto de contexto de proceso** utilizando el [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver) constructor. Resultante **objeto de contexto de proceso** se denomina `sql_cc`.

    Este ejemplo utiliza volver a la misma cadena de conexión que usó en el origen de datos, en la suposición de que los datos están en la misma instancia de SQL Server que se va a usar como contexto de proceso. 
    
    Sin embargo, podrían ser el origen de datos y el contexto de cálculo en servidores diferentes.
 
### <a name="changing-compute-contexts"></a>Cambiar contextos de cálculo

Después de definir un contexto de proceso, debe establecer el **contexto de cálculo activo**. 

De forma predeterminada, la mayoría de las operaciones se ejecutan localmente, lo que significa que si no se especifica un contexto de proceso diferentes, se obtendrán los datos del origen de datos y el código se ejecutará en el entorno de Python actual.

Hay dos maneras de establecer el contexto de cálculo activo:
+ Como un argumento de un método o función
+ Mediante una llamada a `rx_set_computecontext`

#### <a name="set-compute-context-as-an-argument-of-a-method-or-function"></a>Establece el contexto de proceso como un argumento de un método o función

En este ejemplo, establecer el contexto de cálculo mediante un argumento de la persona **rx** función.
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

Este contexto de cálculo se vuelve a usar en la llamada a [rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary):

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rxsetcomputecontext"></a>Establecer un contexto de cálculo utilizando explícitamente rx_set_compute_context

La función [rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) le permite alternar entre los contextos que ya se han definido de proceso.

Después de haber establecido activo el contexto de cálculo, permanece activo hasta que la cambie.

### <a name="using-parallel-processing-and-streaming"></a>Uso de procesamiento en paralelo y streaming

Al definir el contexto de cálculo, también puede establecer los parámetros que controlan cómo se controlan los datos mediante el contexto de cálculo. Estos parámetros varían según el tipo de origen de datos.

Contextos de proceso de SQL Server, puede establecer el tamaño del lote, o proporcionar sugerencias sobre el grado de paralelismo para usar en las tareas en ejecución.

+ El ejemplo se ejecuta en un equipo con cuatro procesadores, por lo que el `num_tasks` parámetro se establece en 4 para permitir el uso máximo de recursos. 
+ Si establece este valor en 0, SQL Server utiliza el valor predeterminado, que consiste en ejecutar todas las tareas en paralelo como sea posible, en la configuración de MAXDOP actual para el servidor. Sin embargo, el número exacto de las tareas que se pueden asignar depende de muchos otros factores, como la configuración del servidor y otros trabajos que se ejecutan.

## <a name="next-steps"></a>Pasos siguientes

Estos tutoriales y ejemplos de Python adicionales muestran escenarios de extremo a otro mediante los orígenes de datos más complejos, así como el uso de contextos de cálculo remoto.

+ [Python en bases de datos para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md)
+ [Crear un modelo predictivo con Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
