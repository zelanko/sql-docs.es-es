---
title: Usar Python con revoscalepy para crear un modelo | Documentos de Microsoft
titleSuffix: SQL Server
ms.date: 02/28/2018
mms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 02e4592398e0558ff01a968bef7c3d1dd199666c
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2018
---
# <a name="use-python-with-revoscalepy-to-create-a-model"></a>Usar Python con revoscalepy para crear un modelo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En esta lección, aprenderá a ejecutar código Python de un cliente de desarrollo remoto, puede crear un modelo de regresión lineal en SQL Server. 

## <a name="prerequisites"></a>Requisitos previos

+ Esta lección utiliza datos diferentes de las lecciones anteriores. No es necesario completar las lecciones anteriores en primer lugar. Sin embargo, si ha completado las lecciones anteriores y tiene un servidor ya configurado para ejecutarse Python, use dicho servidor y base de datos como un contexto de proceso.

+ Para ejecutar el código Python con SQL Server como un proceso contexto requiere SQL Server 2017 o una versión posterior. Además, debe instalar explícitamente y, a continuación, habilita la característica, **Machine Learning Services**, elegir la opción de lenguaje de Python.

    Si instaló una versión preliminar de SQL Server 2017, debe actualizar al menos la versión RTM. Las versiones posteriores de servicio han continuado expandir y mejorar la funcionalidad de Python. Algunas características de este tutorial podrían no funcionar en las primeras versiones preliminares.

+ Este ejemplo usa un entorno de Python predefinido, denominado `PYTEST_SQL_SERVER`. Se ha configurado el entorno para contener **revoscalepy** y otras bibliotecas necesarias. 

    Si no tiene un entorno configurado para ejecutarse Python, debe hacerlo por separado. La explicación de cómo crear o modificar entornos de Python queda fuera del ámbito de este tutorial. Para obtener más información acerca de cómo configurar un cliente de Python que contenga las bibliotecas correctas, consulte [cliente instalar Python](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) y [vínculo Python herramientas](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools).

## <a name="remote-compute-contexts-and-revoscalepy"></a>Revoscalepy y contextos de proceso remoto

En este ejemplo se muestra el proceso de creación de un modelo de Python en un equipo remoto _contexto de proceso_, que permite trabajar desde un cliente, pero elija un entorno remoto, como SQL Server, Spark o servidor de aprendizaje de máquina, donde el las operaciones se realizan en realidad. Uso contextos de proceso hace que sea más fácil escribir el código una vez e implementarla en cualquier entorno compatible con.

Para ejecutar el código de Python en SQL Server requiere la **revoscalepy** paquete. Se trata de un paquete de Python especial suministrado por Microsoft, similar a la **RevoScaleR** paquete para el lenguaje R. El **revoscalepy** paquete es compatible con la creación de contextos de proceso y proporciona la infraestructura para pasar los datos y modelos entre una estación de trabajo local y un servidor remoto. El **revoscalepy** función compatible con la ejecución de código de base de datos está [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver).

En esta lección, utiliza datos de SQL Server para entrenar un modelo lineal basado en [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod), una función en **revoscalepy** que admite la regresión en grandes conjuntos de datos. 

En esta lección también muestra los conceptos básicos de cómo configurar y, a continuación, usar un **contexto de proceso de SQL Server** en Python. Para obtener una explicación de cómo contextos de proceso de trabajo con otras plataformas y contextos de proceso que se admiten, consulte [contexto de proceso para la ejecución de scripts en el servidor de aprendizaje de máquina](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)

## <a name="prepare-the-database-and-sample-data"></a>Preparar los datos de ejemplo y la base de datos

1. Esta lección utiliza la base de datos `sqlpy`. Si no ha finalizado cualquiera de las lecciones anteriores, puede crear la base de datos cuando se ejecuta el código siguiente:

    ```sql
    CREATE DATABASE sqlpy;
    GO;
    USE sqlpy;
    GO;
    ```

    > [!IMPORTANT]
    > Si desea utilizar otra base de datos, asegúrese de editar el código de ejemplo y cambiar el nombre de la base de datos en la cadena de conexión.

2. Este ejemplo utiliza el conjunto de datos Airline, que está disponible en R y Python. Una vez haya creado una base de datos para los ejemplos de Python, rellenar una tabla con los datos tal como se describe aquí: [muestreo de los datos en RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/sample-built-in-data).

3. Cambiar el nombre de este entorno para usar un entorno disponible en el cliente.

## <a name="run-the-sample-code"></a>Ejecute el código de ejemplo

Después de haber preparado la base de datos y con los datos de entrenamiento almacenados en una tabla, abra un entorno de desarrollo de Python y ejecutar el ejemplo de código.

El código realiza los pasos siguientes:

1. Importa las funciones y las bibliotecas necesarias.
2. Crea una conexión a SQL Server. Crea **origen de datos** objetos para trabajar con los datos.
3. Modifica los datos mediante **transformaciones** para que se puede utilizar el algoritmo de regresión logística.
4. Llamadas `rx_lin_mod` y define la fórmula utilizada se ajuste al modelo.
5. Genera un conjunto de predicciones basados en los datos originales.
6. Crea un resumen en función de los valores de predicción.

Todas las operaciones se realizan con una instancia de SQL Server como el contexto de proceso.

> [!NOTE]
> Para ver una demostración de este ejemplo ejecuta desde la línea de comandos, vea este vídeo: [SQL Server 2017 Advanced Analytics con Python](https://www.youtube.com/watch?v=FcoY795jTcc)

### <a name="sample-code"></a>Código de ejemplo

```python
from revoscalepy import RxComputeContext, RxInSqlServer, RxSqlServerData
from revoscalepy import rx_lin_mod, rx_predict, rx_summary
from revoscalepy import RxOptions, rx_import

from pandas import Categorical
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

### <a name="defining-a-data-source-vs-defining-a-compute-context"></a>Definir un origen de datos frente a definir un contexto de proceso

Un origen de datos es diferente de un contexto de proceso. El _origen de datos_ define los datos utilizados en el código. El _cálculo_ define dónde se ejecutará el código. Sin embargo, usan parte de la misma información:

+ Variables de Python, como `sql_query` y `sql_connection_string`, definir el origen de los datos. 

    Pasar estas variables para el [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) constructor para implementar la **objeto de origen de datos** denominado `data_source`.

+ Crear un **objeto de contexto de proceso** mediante el uso de la [RxInSqlServer](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxinsqlserverdata) constructor. Resultante **objeto de contexto de proceso** se denomina `sql_cc`.

    Este ejemplo vuelve a utiliza la misma cadena de conexión que utilizó en el origen de datos, con la suposición de que los datos están en la misma instancia de SQL Server que va a usar como el contexto de proceso. 
    
    Sin embargo, el origen de datos y el contexto de proceso pudieron encontrarse en diferentes servidores.
 
### <a name="changing-compute-contexts"></a>Cambio de contextos de proceso

Después de definir un contexto de proceso, debe establecer el **contexto de computación activa**. 

De forma predeterminada, la mayoría de las operaciones se ejecutan localmente, lo que significa que si no se especifica un contexto de proceso diferente, se capturarán los datos del origen de datos y el código se ejecutará en el entorno actual de Python.

Hay dos maneras de establecer el contexto de computación activa:
+ Como un argumento de un método o función
+ Mediante una llamada a `rx_set_computecontext`

#### <a name="set-compute-context-as-an-argument-of-a-method-or-function"></a>Establecer contexto de proceso como un argumento de un método o función

En este ejemplo, se establece el contexto de cálculo mediante un argumento de la persona **rx** función.
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

Este contexto de cálculo se vuelve a usar en la llamada a [rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary):.

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rxsetcomputecontext"></a>Establecer un contexto de proceso de forma explícita mediante rx_set_compute_context

La función [rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) le permite alternar entre los contextos que ya se ha definido de proceso.

Después de establecer contexto de proceso activo, permanece activo hasta que la cambie.

### <a name="using-parallel-processing-and-streaming"></a>Uso de transmisión por secuencias y procesamiento en paralelo

Al definir el contexto de proceso, también puede establecer parámetros que controlan cómo se gestionan los datos por el contexto del proceso. Estos parámetros varían según el tipo de origen de datos.

Para contextos de proceso de SQL Server, puede establecer el tamaño del lote, o proporcionar sugerencias sobre el grado de paralelismo para usar en las tareas en ejecución.

+ El ejemplo se ejecuta en un equipo con cuatro procesadores, por lo que el `num_tasks` parámetro se establece en 4 para permitir el uso máximo de recursos. 
+ Si establece este valor en 0, SQL Server utiliza el valor predeterminado, que se usa para ejecutar todas las tareas en paralelo como sea posible, en la configuración de MAXDOP actual para el servidor. Sin embargo, el número exacto de las tareas que se pueden asignar depende de otros muchos factores, como la configuración de servidor y otros trabajos que se están ejecutando.

## <a name="related-samples"></a>Ejemplos relacionados

Estos ejemplos de Python y tutoriales adicionales muestran los escenarios de extremo a extremo mediante orígenes de datos más complejos, así como el uso de contextos de proceso remoto.

+ [En bases de datos de Python para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md)
+ [Crear un modelo de predicción mediante Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
+ [Crear un modelo de predicción mediante Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
