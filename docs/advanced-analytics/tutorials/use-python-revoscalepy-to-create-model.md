---
title: Uso de Python para crear un modelo con revoscalepy | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 5c8ff387c3abda3f147700dce6349009a027a778
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2018
ms.locfileid: "49461961"
---
# <a name="use-python-with-revoscalepy-to-create-a-model"></a>Uso de Python con revoscalepy para crear un modelo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En esta lección, aprenderá a ejecutar código de Python desde un cliente de desarrollo remoto, para crear un modelo de regresión lineal en SQL Server. 

## <a name="prerequisites"></a>Requisitos previos

+ En esta lección se usa datos distintos a las lecciones anteriores. No es necesario completar las lecciones anteriores en primer lugar. Sin embargo, si se han completado las lecciones anteriores y tiene un servidor que ya ha configurado para la ejecución de Python, usar ese servidor y base de datos como un contexto de proceso.
+ Para ejecutar código de Python con SQL Server como un proceso contexto requiere SQL Server 2017 o posterior. Además, debe instalar explícitamente y, a continuación, habilitar la característica, **Machine Learning Services**, eligiendo la opción de lenguaje Python.

    Si instaló una versión de vista previa de SQL Server 2017, debe actualizar al menos la versión RTM. Las versiones posteriores de servicio han continuado expandir y mejorar la funcionalidad de Python. Algunas características de este tutorial podrían no funcionar en las primeras versiones preliminares.

+ Este ejemplo usa un entorno de Python predefinido, denominado `PYTEST_SQL_SERVER`. Se ha configurado el entorno para contener **revoscalepy** y otras bibliotecas necesarias. 

    Si no tiene un entorno configurado para la ejecución de Python, debe hacerlo por separado. Una explicación de cómo crear o modificar entornos de Python está fuera del ámbito de este tutorial. Para obtener más información acerca de cómo configurar un cliente de Python que contiene las bibliotecas correctas, consulte [cliente instalar Python](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) y [vínculo Python herramientas](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools).

## <a name="remote-compute-contexts-and-revoscalepy"></a>Contextos de proceso remoto y de revoscalepy

En este ejemplo se muestra el proceso de creación de un modelo de Python en un control remoto _contexto de proceso_, lo que permite trabajar desde un cliente, pero elija un entorno remoto, como SQL Server, Spark o Machine Learning Server, donde el las operaciones se realizan realmente. Usar contextos de cálculo facilita escribir código una vez e implementarlo en cualquier entorno compatible.

Para ejecutar código de Python en SQL Server requiere el **revoscalepy** paquete. Se trata de un paquete de Python especial proporcionado por Microsoft, similar a la **RevoScaleR** paquete para el lenguaje R. El **revoscalepy** paquete admite la creación de contextos de proceso y proporciona la infraestructura para pasar datos y modelos de entre una estación de trabajo local y un servidor remoto. El **revoscalepy** función que admite la ejecución de código de base de datos es [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver).

En esta lección, usar datos en SQL Server para entrenar un modelo lineal basado en [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod), una función en **revoscalepy** que admita la regresión en conjuntos de datos muy grandes. 

En esta lección también muestra los conceptos básicos de cómo configurar y, a continuación, usar un **contexto de proceso de SQL Server** en Python. Para obtener una explicación de cómo los contextos de cálculo trabajar con otras plataformas y contextos de cálculo que se admiten, consulte [contexto de proceso para la ejecución de scripts en Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)

## <a name="prepare-the-database-and-sample-data"></a>Preparar la base de datos y datos de ejemplo

1. Esta lección utiliza la base de datos **sqlpy**. Si no ha completado cualquiera de las lecciones anteriores, puede crear la base de datos ejecutando el código siguiente:

    ```sql
    CREATE DATABASE sqlpy;
    GO
    USE sqlpy;
    GO
    ```

    > [!IMPORTANT]
    > Si desea usar otra base de datos, asegúrese de editar el código de ejemplo y cambie el nombre de la base de datos en la cadena de conexión.

2. Este ejemplo utiliza el conjunto de datos de la compañía aérea, que está disponible en R y Python. Después de haber creado una base de datos para los ejemplos de Python, rellenar una tabla con los datos, como se describe aquí: [muestreo de datos en RevoScaleR](https://docs.microsoft.com/machine-learning-server/r/sample-built-in-data).

3. Cambie el nombre de este entorno para usar un entorno disponible en el cliente.

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
> Para ver una demostración de este ejemplo se ejecuta desde la línea de comandos, vea este vídeo: [SQL Server 2017 Advanced Analytics con Python](https://www.youtube.com/watch?v=FcoY795jTcc)

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

Un origen de datos es diferente de un contexto de proceso. El _origen de datos_ define los datos usados en el código. El _contexto de proceso_ define dónde se ejecutará el código. Sin embargo, usan la misma información:

+ Las variables de Python, como `sql_query` y `sql_connection_string`, definir el origen de datos. 

    Pasar estas variables para el [RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata) constructor para implementar la **objeto origen de datos** denominado `data_source`.

+ Crear un **objeto de contexto de proceso** utilizando el [RxInSqlServer](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxinsqlserverdata) constructor. Resultante **objeto de contexto de proceso** se denomina `sql_cc`.

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

Este contexto de cálculo se vuelve a usar en la llamada a [rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary):.

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rxsetcomputecontext"></a>Establecer un contexto de cálculo utilizando explícitamente rx_set_compute_context

La función [rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) le permite alternar entre los contextos que ya se han definido de proceso.

Después de haber establecido activo el contexto de cálculo, permanece activo hasta que la cambie.

### <a name="using-parallel-processing-and-streaming"></a>Uso de procesamiento en paralelo y streaming

Al definir el contexto de cálculo, también puede establecer los parámetros que controlan cómo se controlan los datos mediante el contexto de cálculo. Estos parámetros varían según el tipo de origen de datos.

Contextos de proceso de SQL Server, puede establecer el tamaño del lote, o proporcionar sugerencias sobre el grado de paralelismo para usar en las tareas en ejecución.

+ El ejemplo se ejecuta en un equipo con cuatro procesadores, por lo que el `num_tasks` parámetro se establece en 4 para permitir el uso máximo de recursos. 
+ Si establece este valor en 0, SQL Server utiliza el valor predeterminado, que consiste en ejecutar todas las tareas en paralelo como sea posible, en la configuración de MAXDOP actual para el servidor. Sin embargo, el número exacto de las tareas que se pueden asignar depende de muchos otros factores, como la configuración del servidor y otros trabajos que se ejecutan.

## <a name="related-samples"></a>Ejemplos relacionados

Estos tutoriales y ejemplos de Python adicionales muestran escenarios de extremo a otro mediante los orígenes de datos más complejos, así como el uso de contextos de cálculo remoto.

+ [Python en bases de datos para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md)
+ [Crear un modelo predictivo con Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
+ [Crear un modelo predictivo con Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
