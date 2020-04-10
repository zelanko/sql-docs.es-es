---
title: Generación de previsiones y predicciones
description: Use rxPredict, o sp_rxPredict para la puntuación en tiempo real o PREDICT T-SQL para la puntuación nativa de predicciones y previsiones en R y Python en SQL Server Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/30/2020
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c07a5b8d3e1b34c0bb33f44a20ab5fff867db922
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2020
ms.locfileid: "81117628"
---
# <a name="how-to-generate-forecasts-and-predictions-using-machine-learning-models-in-sql-server"></a>Cómo generar previsiones y predicciones mediante modelos de aprendizaje automático en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

El uso de un modelo existente para pronosticar o predecir los resultados de nuevas entradas de datos es una tarea principal del aprendizaje automático. En este artículo se enumeran los métodos para generar predicciones en SQL Server. Entre los distintos enfoques están las metodologías de procesamiento interno para las predicciones de alta velocidad, donde la velocidad se basa en las reducciones incrementales de las dependencias de tiempo de ejecución. Menos dependencias significan predicciones más rápidas.

El uso de la infraestructura de procesamiento interno (puntuación en tiempo real o nativa) incluye requisitos de biblioteca. Las funciones deben ser de las bibliotecas de Microsoft. El código de R o Python que llama a funciones de código abierto o de terceros no se admite en extensiones de C++ o CLR.

En la tabla siguiente se resumen los marcos de puntuación de previsiones y predicciones. 

| Metodología           | Interfaz         | Requisitos de biblioteca | Velocidades de procesamiento |
|-----------------------|-------------------|----------------------|----------------------|
| Marco de extensibilidad | [rxPredict (R)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) <br/>[rx_predict (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | Ninguno. Los modelos se pueden basar en cualquier función de R o Python. | Cientos de milisegundos. <br/>La carga de un entorno de runtime tiene un costo fijo, con un promedio de 3 a 600 milisegundos, antes de que se puntúen los datos nuevos. |
| [Extensión CLR de puntuación en tiempo real](../real-time-scoring.md) | [sp_rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) en un modelo serializado | R: RevoScaleR, MicrosoftML <br/>Python: revoscalepy, microsoftml | Decenas de milisegundos de promedio. |
| [Extensión de C++ de puntuación nativa](../sql-native-scoring.md) | [Función PREDICT de T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) en un modelo serializado | R: RevoScaleR <br/>Python: revoscalepy | Menos de 20 milisegundos de promedio. | 

La velocidad de procesamiento y no el componente de la salida es la característica diferenciadora. Teniendo en cuenta las mismas funciones y entradas, la salida puntuada no debe variar en función del enfoque usado.

El modelo se debe crear con una función compatible y, a continuación, serializarse en una secuencia de bytes sin formato guardada en el disco o almacenada en formato binario en una base de datos. Mediante el uso de un procedimiento almacenado o T-SQL, se puede cargar y usar un modelo binario sin la sobrecarga de un entorno de runtime de lenguaje R o Python, con lo que se consigue que la generación de puntuación en nuevas entradas sea más rápida.

La importancia de las extensiones de C++ y CLR es la proximidad al propio motor de base de datos. El lenguaje nativo del motor de base de datos es C++, lo que significa que las extensiones escritas en C++ se ejecutan con menos dependencias. En cambio, las extensiones de CLR dependen de .NET Core. 

Como cabría esperar, la compatibilidad con la plataforma se ve afectada por estos entornos de runtime. Las extensiones nativas del motor de base de datos se ejecutan en cualquier lugar donde se admita la base de datos relacional: Windows, Linux y Azure. Las extensiones de CLR que requieren .NET Core son solo de Windows.

## <a name="scoring-overview"></a>Información general sobre puntuación

La _puntuación_ es un proceso de dos pasos. En primer lugar, especifique un modelo ya entrenado para cargarlo desde una tabla. En segundo lugar, pase nuevos datos de entrada a la función para generar valores de predicción (o _puntuaciones_). La entrada suele ser una consulta T-SQL, que devuelve filas tabulares o únicas. Puede optar por generar un valor de columna único que represente una probabilidad, o puede generar varios valores, como un intervalo de confianza, un error u otro complemento útil para la predicción.

Volviendo atrás, el proceso general de preparación del modelo y la generación de puntuaciones se pueden resumir de esta manera:

1. Cree un modelo con un algoritmo compatible. La compatibilidad varía según la metodología de puntuación que elija.
2. Entrene el modelo.
3. Serialice el modelo con un formato binario especial.
3. Guarde el modelo en SQL Server. Normalmente, esto significa almacenar el modelo serializado en una tabla de SQL Server.
4. Llame a la función o al procedimiento almacenado, especificando el modelo y las entradas de datos como parámetros.

Cuando la entrada incluye muchas filas de datos, normalmente es más rápido insertar los valores de predicción en una tabla como parte del proceso de puntuación. Generar una sola puntuación es más habitual en un escenario en el que se obtienen los valores de entrada de un formulario o una solicitud de usuario, y se devuelve la puntuación a una aplicación cliente. Para mejorar el rendimiento al generar puntuaciones sucesivas, SQL Server podría almacenar en caché el modelo para que se pueda volver a cargar en la memoria.

## <a name="compare-methods"></a>Comparación de métodos

Para conservar la integridad de los procesos principales del motor de base de datos, la compatibilidad con R y Python está habilitada en una arquitectura dual que aísla el procesamiento de idiomas del procesamiento RDBMS. A partir de SQL Server 2016, Microsoft ha agregado un marco de extensibilidad que permite ejecutar scripts de R desde T-SQL. En SQL Server 2017 se agregó la integración con Python. 

El marco de extensibilidad es compatible con cualquier operación que pueda realizar en R o Python, desde funciones sencillas hasta el entrenamiento de modelos de aprendizaje automático complejos. Sin embargo, la arquitectura de dos procesos requiere invocar un proceso de R o Python externo para cada llamada, independientemente de la complejidad de la operación. Cuando la carga de trabajo implica la carga de un modelo previamente entrenado a partir de una tabla y su puntuación en los datos que ya están en SQL Server, la sobrecarga de llamar a los procesos externos agrega latencia que puede ser inaceptable en determinadas circunstancias. Por ejemplo, la detección de fraudes requiere que la puntuación rápida sea relevante.

Para aumentar las velocidades de puntuación de escenarios como la detección de fraudes, SQL Server ha agregado bibliotecas de puntuación integradas como extensiones de CLR y C++ que eliminan la sobrecarga de los procesos de inicio de R y Python.

[**La puntuación en tiempo real**](../real-time-scoring.md) era la primera solución para la puntuación de alto rendimiento. Introducida en las anteriores versiones de SQL Server 2017 y las actualizaciones posteriores a SQL Server 2016, la puntuación en tiempo real se basa en las bibliotecas de CLR que sustituyen el procesamiento de R y Python en las funciones controladas por Microsoft en RevoScaleR, MicrosoftML (R), revoscalepy y microsoftml (Python). Las bibliotecas de CLR se invocan mediante el procedimiento almacenado **sp_rxPredict** para generar puntuaciones de cualquier tipo de modelo admitido, sin llamar al entorno de runtime de R o Python.

[**La puntuación nativa**](../sql-native-scoring.md) es una característica SQL Server 2017, implementada como biblioteca nativa de C++, pero solo para los modelos RevoScaleR y revoscalepy. Es el enfoque más rápido y seguro, pero admite un conjunto más pequeño de funciones en relación con otras metodologías.

## <a name="choose-a-scoring-method"></a>Elección de un método de puntuación

Los requisitos de la plataforma a menudo determinan la metodología de puntuación que se va a usar.

| Versión y plataforma del producto | Metodología |
|------------------------------|-------------|
| SQL Server 2017 en Windows, SQL Server 2017 Linux y Azure SQL Database | **Puntuación nativa** con PREDICT de T-SQL |
| SQL Server 2017 (solo Windows), SQL Server 2016 R Services en SP1 o versiones posteriores | **Puntuación en tiempo real** con el procedimiento almacenado sp\_rxPredict |

Se recomienda la puntuación nativa con la función PREDICT. El uso de sp\_rxPredict requiere la habilitación de la integración de SQLCLR. Tenga en cuenta las implicaciones de seguridad antes de habilitar esta opción.

## <a name="serialization-and-storage"></a>Serialización y almacenamiento

Para usar un modelo con cualquiera de las opciones de puntuación rápida, guarde el modelo con un formato serializado especial, que se haya optimizado teniendo en cuenta el tamaño y la eficacia de la puntuación.

+ Llame a [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) para escribir un modelo compatible con el formato **raw**.
+ Llame a [rxUnserializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) para reconstituir el modelo para su uso en otro código R o para ver el modelo.

**Usar SQL**

Desde código SQL, puede entrenar el modelo mediante [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) e insertar directamente los modelos entrenados en una tabla, en una columna de tipo **varbinary(max)** . Para ver un ejemplo sencillo, consulte [Creación de un modelo de predicción en R](../tutorials/quickstart-r-train-score-model.md)

**Usar R**

Desde código R, llame a la función [rxWriteObject](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxwriteobject) desde el paquete RevoScaleR para escribir el modelo directamente en la base de datos. La función **rxWriteObject()** puede recuperar objetos de R de un origen de datos ODBC como SQL Server, o escribir objetos en SQL Server. La API se modela según un almacén de clave-valor simple.
  
Si usa esta función, asegúrese de serializar el modelo utilizando primero [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel). Después, establezca el argumento *serialize* en **rxWriteObject** en FALSE para evitar repetir el paso de serialización.

Serializar un modelo a un formato binario es útil, pero no es necesario si va a puntuar las predicciones con el entorno de runtime de R y Python en el marco de extensibilidad. Puede guardar un modelo en formato de bytes sin procesar en un archivo y, después, leer el archivo en SQL Server. Esta opción puede ser útil si va a mover o copiar modelos entre entornos.

## <a name="scoring-in-related-products"></a>Puntuación en productos relacionados

Si usa el [servidor independiente](r-server-standalone.md) o [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), tiene otras opciones para generar predicciones rápidamente aparte de los procedimientos almacenados y las funciones de T-SQL. Tanto el servidor independiente como Machine Learning Server admiten el concepto de un *servicio web* para la implementación del código. Puede agrupar un modelo previamente entrenado en R o Python como servicio web, al que se llama en tiempo de ejecución para evaluar nuevas entradas de datos. Para obtener más información, consulte estos artículos:

+ [¿Qué son los servicios web en Machine Learning Server?](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [¿Qué es la operacionalización?](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)
+ [Implementación de un modelo de Python como servicio web con azureml-model-management-sdk](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [Publicación de un bloque de código R o un modelo en tiempo real como un servicio web nuevo](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [Paquete mrsdeploy para R](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)


## <a name="see-also"></a>Consulte también

+ [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)  
+ [rxRealTimeScoring](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxrealtimescoring)
+ [sp-rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)
+ [PREDICT T-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)