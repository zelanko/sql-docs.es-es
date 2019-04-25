---
title: Generar predicciones con modelos de aprendizaje automático - SQL Server Machine Learning Services y previsiones
description: Use rxPredict o sp_rxPredict para puntuar en tiempo real o PREDECIR Transact-SQL para la puntuación para las predicciones nativo y la previsión de R y Pythin en SQL Server Machine Learning.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/30/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 001b90eafd26c90f730e5647f0dc62d756ca9d1b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62503770"
---
# <a name="how-to-generate-forecasts-and-predictions-using-machine-learning-models-in-sql-server"></a>Cómo generar predicciones con modelos de aprendizaje automático de SQL Server y previsiones
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Con un modelo existente para prever o predecir los resultados de las nuevas entradas de datos es una tarea esencial en machine learning. En este artículo se enumera los métodos para generar predicciones en SQL Server. Entre los métodos se ejecutan las metodologías de procesamiento interno para las predicciones de alta velocidad, donde la velocidad se basa en reducciones incrementales de las dependencias de tiempo. Menos dependencias significan predicciones más rápidas.

Mediante la infraestructura de procesamiento interno (puntuación en tiempo real o nativo) incluye requisitos de la biblioteca. Las funciones deben ser de las bibliotecas de Microsoft. Código de R o Python llamar a funciones de código abierto o de terceros no se admite en las extensiones de CLR o C++.

En la tabla siguiente se resume los marcos de puntuación para la previsión y predicciones. 

| Metodología           | Interfaz         | Requisitos de la biblioteca | Velocidades de procesamiento |
|-----------------------|-------------------|----------------------|----------------------|
| Marco de extensibilidad | [rxPredict (R)](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) <br/>[rx_predict (Python)](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) | Ninguno. Los modelos se pueden basar en cualquier función de R o Python | Cientos de milisegundos. <br/>Carga de un entorno en tiempo de ejecución tiene un costo fijo, calcular el promedio de tres a seis cientos de milisegundos, antes de que se usa para puntuar nuevos datos. |
| [Extensión CLR de puntuación en tiempo real](../real-time-scoring.md) | [sp_rxPredict](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql) en un modelo serializado | R: RevoScaleR, MicrosoftML <br/>Python: revoscalepy, microsoftml | Decenas de milisegundos por término medio. |
| [Extensión de C++ puntuación nativa](../sql-native-scoring.md) | [Función T-SQL PREDECIR](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) en un modelo serializado | R: RevoScaleR <br/>Python: revoscalepy | Menos de 20 milisegundos, en promedio. | 

Velocidad de procesamiento y no la sustancia de la salida es la característica distintiva. La salida con puntuación suponiendo que las mismas funciones y entradas, no debería variar según el enfoque que utilice.

El modelo debe creado mediante una función admitida y luego se serializa en una secuencia de bytes sin procesar guardados en disco o almacenados en formato binario en una base de datos. Con Transact-SQL o un procedimiento almacenado, puede cargar y usar un modelo binario sin la sobrecarga de un tiempo de ejecución de lenguaje R o Python, resultante en un tiempo más rápido hasta su finalización al generar puntuaciones de predicción en nuevas entradas.

La importancia de las extensiones de CLR y C++ está cerca del propio motor de base de datos. El lenguaje nativo del motor de base de datos es de C++, lo que significa que las extensiones escritas en C++ que se ejecute con menos dependencias. En cambio, las extensiones CLR dependen de .NET Core. 

Como cabría esperar, compatibilidad con la plataforma se ve afectado por estos entornos de tiempo de ejecución. Extensiones de motor de base de datos nativa ejecutan desde cualquier lugar que es compatible la base de datos relacional: Windows, Linux, Azure. Extensiones CLR con el requisito de .NET Core solo está actualmente Windows.

## <a name="scoring-overview"></a>Información general de puntuación

_Puntuación_ es un proceso en dos pasos. En primer lugar, especifique un modelo ya entrenado para cargar desde una tabla. En segundo lugar, pase nuevos datos de entrada en la función para generar valores de predicción (o _puntuaciones_). La entrada a menudo es una consulta Transact-SQL, y devuelve filas tabulares o únicas. Puede elegir como resultado un valor de columna única que representa una probabilidad, o pueden generar varios valores, como un intervalo de confianza, error u otro complemento útil para la predicción.

Cómo dar un paso hacer una copia, el proceso general de la preparación del modelo y, a continuación, generar puntuaciones puede resumirse así:

1. Crear un modelo usando un algoritmo compatible. Compatibilidad con varía según la metodología de puntuación que elija.
2. Entrenar el modelo.
3. Serializa el modelo utilizando un formato binario especial.
3. Guardar el modelo en SQL Server. Normalmente, esto significa que almacenar el modelo serializado en una tabla de SQL Server.
4. Llame a la función o procedimiento almacenado, especificar las entradas de modelo y datos como parámetros.

Cuando la entrada incluye muchas filas de datos, es normalmente más rápido insertar los valores de predicción en una tabla como parte del proceso de puntuación. Generar una puntuación única es más habitual en un escenario donde obtener los valores de entrada de una solicitud de formulario o de usuario y devolver la puntuación a una aplicación cliente. Para mejorar el rendimiento al generar puntuaciones sucesivas, SQL Server puede almacenar en caché el modelo para que se puede volver a cargar en la memoria.

## <a name="compare-methods"></a>Comparación de métodos

Para conservar la integridad de los procesos de motor de base de datos principales, compatibilidad con R y Python está habilitado en una arquitectura dual que aísla el procesamiento de lenguaje de procesamiento de RDBMS. A partir de SQL Server 2016, Microsoft agregó un marco de extensibilidad que permite que los scripts de R que se ejecutará desde T-SQL. En SQL Server 2017, se agregó integración de Python. 

El marco de extensibilidad admite cualquier operación que podría realizar en R o Python, comprendido entre funciones sencillas y entrenamiento complejos modelos de machine learning. Sin embargo, la arquitectura de doble proceso requiere invocar un proceso externo de R o Python para todas las llamadas, independientemente de la complejidad de la operación. Cuando la carga de trabajo implica cargar un modelo previamente entrenado de una tabla y la puntuación en el mismo en los datos ya incluidos en SQL Server, la sobrecarga de la llamada a los procesos externos agrega latencia a los que puede ser inaceptable en determinadas circunstancias. Por ejemplo, la detección de fraudes requiere puntuación rápida para que sea relevante.

Para aumentar las velocidades de puntuación para escenarios como la detección de fraudes, SQL Server agrega las bibliotecas integradas de puntuación como extensiones de C++ y CLR que eliminan la sobrecarga de procesos de inicio de R y Python.

[**Puntuación en tiempo real** ](../real-time-scoring.md) fue la primera solución para la puntuación de alto rendimiento. Se introdujo en las versiones anteriores de SQL Server 2017 y las actualizaciones posteriores a SQL Server 2016, puntuación en tiempo real se basa en las bibliotecas CLR que representan R y Python de procesamiento a través de funciones controladas por Microsoft en RevoScaleR, MicrosoftML (R), revoscalepy, y microsoftml (Python). Bibliotecas CLR se invocan mediante el **sp_rxPredict** procedimiento almacenado que genera las puntuaciones desde cualquier tipo de modelo admitidos, sin llamar en tiempo de ejecución de R o Python.

[**Puntuación nativa** ](../sql-native-scoring.md) es una característica de SQL Server 2017, implementada como una biblioteca de C++ nativa, pero solo para modelos de RevoScaleR y revoscalepy. Es el enfoque más rápido y más seguro, pero es compatible con un conjunto más pequeño de funciones en relación con otras metodologías.

## <a name="choose-a-scoring-method"></a>Elija un método de puntuación

Requisitos de la plataforma a menudo determinan qué puntuación metodología que se va a usar.

| Plataforma y versión del producto | Metodología |
|------------------------------|-------------|
| SQL Server 2017 en Windows, SQL Server 2017 para Linux y Azure SQL Database | **Puntuación nativa** con T-SQL PREDECIR |
| SQL Server 2017 (solo Windows), SQL Server 2016 R Services SP1 o superior | **Puntuación en tiempo real** con sp\_rxPredict procedimiento almacenado |

Se recomienda la puntuación nativa con la función PREDICT. Con sp\_rxPredict requiere que habilite la integración de SQLCLR. Antes de habilitar esta opción, tenga en cuenta las implicaciones de seguridad.

## <a name="serialization-and-storage"></a>Almacenamiento y serialización

Para usar un modelo con cualquiera de las opciones rápidas de puntuación, guarde el modelo con un formato serializado especial, que se ha optimizado para el tamaño y la eficacia de puntuación.

+ Llame a [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) para escribir un modelo compatible para la **raw** formato.
+ Llame a [rxUnserializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)' para reconstituir el modelo para su uso en otro código de R, o para ver el modelo.

**Uso de SQL**

Desde el código SQL, puede entrenar el modelo mediante [sp_execute_external_script](https://docs.microsoft.com//sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)e insertar directamente los modelos entrenados en una tabla, en una columna de tipo **varbinary (max)**. Para obtener un ejemplo simple, vea [crear un modelo preditive en R](../tutorials/rtsql-create-a-predictive-model-r.md)

**Uso de R**

Desde el código de R, llame a la [rxWriteObject](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxwriteobject) función del paquete RevoScaleR para escribir el modelo directamente en la base de datos. El **rxWriteObject()** función puede recuperar objetos de R desde un origen de datos ODBC, como SQL Server, o escribir objetos en SQL Server. La API se modela después de un almacén de pares clave-valor simple.
  
Si usa esta función, asegúrese de serializar el modelo mediante [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel) primero. A continuación, establezca el *serializar* argumento en **rxWriteObject** en FALSE para evitar repetir el paso de serialización.

Serializar un modelo a un formato binario es útil, pero no es necesario si está puntuando predicciones que usan R y Python ejecuta el entorno de tiempo en el marco de extensibilidad. Puede guardar un modelo en formato de bytes sin procesar en un archivo y, a continuación, se leen desde el archivo en SQL Server. Esta opción puede ser útil si va a mover o copiar modelos entre entornos.

## <a name="scoring-in-related-products"></a>Puntuación en productos relacionados

Si usas el [servidor independiente](r-server-standalone.md) o un [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/what-is-machine-learning-server), tiene otras opciones además de procedimientos almacenados y funciones de Transact-SQL para generar predicciones rápidamente. El servidor independiente y el servidor de Machine Learning admiten el concepto de un *servicio web* para la implementación de código. Puede agrupar un R o Python modelo previamente entrenado como un servicio web, que se llama en tiempo de ejecución para evaluar las nuevas entradas de datos. Para más información, vea estos artículos:

+ [¿Cuáles son los servicios web en Machine Learning Server?](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [¿Qué es la puesta en marcha?](https://docs.microsoft.com/machine-learning-server/what-is-operationalization)
+ [Implementar un modelo de Python como un servicio web con Azure ml-model-management-sdk](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [Publicar un modelo en tiempo real o un bloque de código de R como un servicio web nuevo](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [paquete de mrsdeploy para R](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)


## <a name="see-also"></a>Vea también

+ [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)  
+ [rxRealTimeScoring](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxrealtimescoring)
+ [sp-rxPredict](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-rxpredict-transact-sql)
+ [PREDECIR TRANSACT-SQL](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)