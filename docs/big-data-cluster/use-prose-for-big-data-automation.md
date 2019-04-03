---
title: Generar código para tareas de tratamiento de datos
titleSuffix: Azure Data Studio
description: En este artículo se describe cómo usar el Acelerador de código de PROSE en Azure Data Studio para generar automáticamente código para tareas comunes de tratamiento de datos.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 705d3b5230faf69ca9eb9de2f7f0cc21b42a8955
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860086"
---
# <a name="data-wrangling-using-prose-code-accelerator"></a>Uso del Acelerador de código de PROSE de Wrangling de datos

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Acelerador de código PROSE genera código de Python legible para las tareas de tratamiento de datos. Puede mezclar el código generado con el código escrito a mano de forma transparente mientras trabaja en un bloc de notas en Azure Data Studio. En este artículo se proporciona información general de cómo puede usar el Acelerador de código.

 > [!NOTE]
 > Programa Synthesis using Examples, también conocido como PROSE, es una tecnología de Microsoft que genera el código legible mediante inteligencia artificial. Lo hace mediante el análisis de un usuario intención, así como datos, generar varios programas de candidato y el mejor programa mediante algoritmos de clasificación de selección. Para obtener más información sobre la tecnología PROSE, visite la [página principal PROSE](https://microsoft.github.io/prose/).

El Acelerador de código viene preinstalado con Azure Data Studio. Se puede importar como cualquier otro paquete de Python en el Bloc de notas. Por convención, se importa como cx para abreviar.

```python
import prose.codeaccelerator as cx
```

En la versión actual, el Acelerador de código de forma inteligente puede generar código de Python para las tareas siguientes:

- Leer archivos de datos en un Pandas o trama de datos de Pyspark.
- Corrección de los tipos de datos en una trama de datos.
- Búsqueda de expresiones regulares que representa los patrones en una lista de cadenas.

Para obtener una visión general de los métodos de Acelerador de código, consulte el [documentación](https://aka.ms/prose-codeaccelerator-overview).

## <a name="reading-data-from-a-file-to-a-dataframe"></a>Leer datos desde un archivo a una trama de datos

Lectura de archivos a una trama de datos implica a menudo, mirando el contenido del archivo y determinar los parámetros correctos para pasar a una biblioteca de carga de datos. Según la complejidad del archivo, que identifica los parámetros correctos puede requerir varias iteraciones.

Acelerador de código PROSE soluciona este problema al analizar la estructura del archivo de datos y generar automáticamente código para cargar el archivo. En la mayoría de los casos, el código generado analiza los datos correctamente. En algunos casos, es posible que deberá ajustar el código para satisfacer sus necesidades.

Considere el ejemplo siguiente:

 ```python
import prose.codeaccelerator as cx

# Call the ReadCsvBuilder builder to analyze the file content and generate code to load it
builder = cx.ReadCsvBuilder(r'C:/911.txt')

#Set target to pyspark if generating code to use pyspark library
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
 ```

El bloque de código anterior imprime el siguiente código de python para leer un archivo delimitado. Tenga en cuenta cómo PROSE calcula automáticamente el número de líneas que se omitirán los encabezados, quotechars, delimitadores, etcetera.

 ```python
import pandas as pd

def read_file(file):
    names = ["lat",
             "lng",
             "desc",
             "zip",
             "title"]

    df = pd.read_csv(file,
        skiprows = 11,
        header = None,
        names = names,
        quotechar = "\"",
        delimiter = "|",
        index_col = False,
        dtype = str,
        na_values = [],
        keep_default_na = False,
        skipinitialspace = True)
    return df
 ```

Acelerador de código puede generar código carga delimitados, JSON y archivos de ancho fijo a una trama de datos. Para leer archivos de ancho fijo, el `ReadFwfBuilder` opcionalmente toma un archivo de esquema de lenguaje natural que puede analizar para obtener las posiciones de columna. Para obtener más información, consulte el [documentación](https://aka.ms/prose-codeaccelerator-docs).

## <a name="fixing-data-types-in-a-dataframe"></a>Corrección de los tipos de datos en una trama de datos

Es habitual tener un pandas o pyspark trama de datos con tipos de datos incorrecto. A menudo, esto sucede debido a unos no conforme los valores en una columna. Como resultado, se leen enteros como Float o cadenas, y se leen las fechas como cadenas. El esfuerzo necesario para corregir manualmente los tipos de datos es proporcional al número de columnas.

Puede usar el `DetectTypesBuilder` en estas situaciones. Analiza los datos y, en lugar de corregir los tipos de datos de una forma de caja negra, genera código para corregir los tipos de datos. El código sirve como punto de partida. Puede revisar, usar o modifíquelo según sea necesario.

```python
import prose.codeaccelerator as cx

builder = cx.DetectTypesBuilder(df)

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

#Get the code generated to fix the data types
builder.learn().code()
```

Para obtener más información, consulte el [documentación](https://aka.ms/prose-codeaccelerator-fixtypes).

## <a name="identifying-patterns-in-strings"></a>Identificación de patrones en cadenas

Otro escenario común es detectar patrones en una columna de cadena con el fin de limpieza o de agrupación. Por ejemplo, puede tener una columna de fecha con fechas en varios formatos diferentes. Con el fin de normalizar los valores, puede escribir instrucciones condicionales mediante expresiones regulares.


|   |Name                      |BirthDate      |
|---|:-------------------------|:--------------|
| 0 |Bertram du Plessis        |1995           |
| 1 |Naiara Moravcikova        |Desconocido        |
| 2 |Jihoo Spel                |2014           |
| 3 |Viachaslau Gordan Hilario |22-Abr-67      |
| 4 |Maya de Villiers          |19-Mar-60      |

Según el volumen y la diversidad de datos, la escritura de expresiones regulares para patrones diferentes en la columna puede ser una tarea que consumen mucho tiempo. El `FindPatternsBuilder` es una herramienta de aceleración de código eficaz que resuelve el problema anterior mediante la generación de expresiones regulares para obtener una lista de cadenas.

```python
import prose.codeaccelerator as cx

builder = cx.FindPatternsBuilder(df['BirthDate'])

#Set target to pyspark if working with pyspark
#builder.Target = "pyspark"

builder.learn().regexes
```

Estas son las expresiones regulares generadas por el `FindPatternsBuilder` para los datos descritos anteriormente.

```
^[0-9]{2}-[A-Z][a-z]+-[0-9]{2}$
^[0-9]{2}[\s][A-Z][a-z]+[\s][0-9]{4}$
^[0-9]{4}$
^Unknown$
```

Además de generar expresiones regulares, `FindPatternsBuilder` también puede generar código para la agrupación en clústeres los valores basados en regexes generado. También puede afirmar que todos los valores de una columna se ajustan a las expresiones regulares generadas. Para obtener más información y ver otros escenarios útiles, vea el [documentación](https://aka.ms/prose-codeaccelerator-findpatterns).
