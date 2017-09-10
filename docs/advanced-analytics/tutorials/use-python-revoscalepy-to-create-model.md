---
title: Usar Python con revoscalepy para crear un modelo | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 07/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: 4
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6b7e166971ff74add56bce628838c82a9a6c1128
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="use-python-with-revoscalepy-to-create-a-model"></a>Usar Python con revoscalepy para crear un modelo

Este ejemplo muestra cómo puede crear un modelo de regresión logística en SQL Server, mediante un algoritmo de la **revoscalepy** paquete.

El **revoscalepy** el paquete para Python contiene objetos, transformaciones, y algoritmos similares a los que se proporcionan para que la **RevoScaleR** paquete para el lenguaje R. Con esta biblioteca, puede crear un contexto de proceso, mover datos entre los contextos de proceso, transforman datos y entrenar modelos de predicción utilizando algoritmos populares, como la regresión logística y lineal, árboles de decisión y mucho más.

Para obtener más información, vea [¿qué es revoscalepy?](../python/what-is-revoscalepy.md)

## <a name="prerequisites"></a>Requisitos previos

> [!IMPORTANT]
> Para ejecutar código de Python en SQL Server, debe tener instalado SQL Server 2017 CTP 2.0 o posterior, y debe instalar y habilitar la característica, **Machine Learning Services** con Python. Otras versiones de SQL Server no admiten la integración de Python.

## <a name="run-the-sample-code"></a>Ejecute el código de ejemplo

Este código realiza los pasos siguientes:

1. Importa las bibliotecas necesarias y funciones
2. Crea una conexión con SQL Server y crea objetos de origen de datos para trabajar con los datos
3. Modifica los datos de forma que se puede utilizar el algoritmo de regresión logística
4. Llamadas `rx_lin_mod` y define la fórmula utilizada se ajuste al modelo
5. Genera un conjunto de predicciones basados en el conjunto de datos original
6. Crea un resumen en función de los valores de predicción

Todas las operaciones se realizan con una instancia de SQL Server como el contexto de proceso.

En general, el proceso de Python que realiza la llamada en un contexto de proceso remoto es similar a la forma de que usar R en un contexto de proceso remoto. Ejecutar el ejemplo como un script de Python desde la línea de comandos o mediante el uso de un entorno de desarrollo de Python que incluye los componentes de integración de Python proporcionados en esta versión. En el código, crear y usar un objeto de contexto de proceso para indicar donde quiere que los cálculos concretos que se realice.

> [!NOTE]
> No olvide cambiar los nombres de base de datos y entorno según corresponda.
> 
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
    
    sql_connection_string = 'Driver=SQL Server;Server=' + sqlServer + ';Database=PyTestDb;Trusted_Connection=True;'
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

## <a name="discussion"></a>Discusión

Vamos a revisar el código y resaltar algunos pasos claves.

### <a name="defining-a-data-source-and-compute-context"></a>Definición de datos de origen y contexto de proceso

Un origen de datos es diferente de un contexto de proceso. El _origen de datos_ define los datos utilizados en el código. El _cálculo_ define dónde se ejecutará el código.

1. Crear variables de Python, como `sql_query` y `sql_connection_string`, que definen el origen y los datos que desea usar. Pasar estas variables para el constructor RxSqlServerData para implementar la **objeto de origen de datos** denominado `data_source`.
2. Crear un objeto de contexto de proceso mediante la **RxInSqlServer** constructor. En este ejemplo, pasar la misma cadena de conexión definida anteriormente, en la suposición de que los datos están en la misma instancia de SQL Server que va a usar como el contexto de proceso. Sin embargo, el origen de datos y el contexto de proceso pudieron encontrarse en diferentes servidores. Resultante **objeto de contexto de proceso** se denomina `sql_cc`.
3. Elegir el contexto de computación activa. De forma predeterminada, las operaciones se ejecutan localmente, lo que significa que si no se especifica un contexto de proceso diferente, se capturarán los datos del origen de datos y la conexión de modelo se ejecutará en el entorno actual de Python.

### <a name="changing-compute-contexts"></a>Cambio de contextos de proceso

En este ejemplo, se establece el contexto de cálculo mediante un argumento de la persona **rx** función.
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

Lo mismo se aplica en la llamada a **rxsummary**, donde se vuelve a usar el contexto de proceso.

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

También puede utilizar la función **rxsetcomputecontext** para alternar entre los contextos de proceso que ya se ha definido. 

### <a name="setting-the-degree-of-parallelism"></a>Establecer el grado de paralelismo

Al definir el contexto de proceso, también puede establecer parámetros que controlan cómo se gestionan los datos por el contexto del proceso. Estos parámetros varían según el tipo de origen de datos. 

Para contextos de proceso de SQL Server, puede establecer el tamaño del lote, o proporcionar sugerencias sobre el grado de paralelismo para usar en las tareas en ejecución.

El ejemplo se ejecuta en un equipo con cuatro procesadores, por lo que establecemos la *num_tasks* parámetro 4. Si establece este valor en 0, SQL Server utiliza el valor predeterminado, que se usa para ejecutar todas las tareas en paralelo como sea posible, en la configuración de MAXDOP actual para el servidor. Sin embargo, incluso en servidores con varios procesadores, el número exacto de las tareas que se pueden asignar depende de otros muchos factores, como la configuración de servidor y otros trabajos que se están ejecutando. 

Para obtener más información, consulte [RxInSqlServer](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinsqlserver).

## <a name="related-samples"></a>Ejemplos relacionados

Vea estos ejemplos de Python y tutoriales para obtener sugerencias avanzadas y demostraciones to-end.

+ [En bases de datos Python para desarrolladores de SQL](sqldev-in-database-python-for-sql-developers.md)
+ [Crear un modelo de predicción mediante Python y SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
+ [Implementar y utilizar modelos de Python](../python/publish-consume-python-code.md)

