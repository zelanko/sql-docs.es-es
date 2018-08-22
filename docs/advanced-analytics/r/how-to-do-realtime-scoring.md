---
title: Cómo realizar la puntuación en tiempo real o la puntuación nativa en SQL Server Machine Learning | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: dfea308f268d666ce070c21a7dd9afa513f95406
ms.sourcegitcommit: 9cd01df88a8ceff9f514c112342950e03892b12c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/20/2018
ms.locfileid: "40393966"
---
# <a name="how-to-perform-real-time-scoring-or-native-scoring-in-sql-server"></a>Cómo realizar la puntuación en tiempo real o la puntuación nativa en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo se muestran dos enfoques en SQL Server para predecir los resultados en casi en tiempo real con modelos previamente entrenados escritos en R. Puntuación en tiempo real tanto puntuación nativa están diseñados para permitir el uso de un modelo de machine learning sin tener que instalar R. Proporciona un modelo previamente entrenado en un formato compatible con - guardado en una base de datos de SQL Server: puede usar técnicas de acceso a datos estándar para generar rápidamente las puntuaciones de predicción en nuevas entradas.

## <a name="choose-a-scoring-method"></a>Elija un método de puntuación

Se admiten las siguientes opciones para la predicción por lotes rápidamente:

+ **Puntuación nativa**: la función PREDICT de Transact-SQL en Azure SQL Database, SQL Server 2017 para Linux y Windows de SQL Server 2017.
+ **Puntuación en tiempo real**: con el sp\_rxPredict el procedimiento almacenado en SQL Server 2016 o SQL Server 2017 (solo Windows).

> [!NOTE]
> Se recomienda usar la función PREDICT en SQL Server 2017.
> Para usar sp\_rxPredict requiere que habilite la integración de SQLCLR. Antes de habilitar esta opción, tenga en cuenta las implicaciones de seguridad.

El proceso general de preparar el modelo y, a continuación, generar puntuaciones es similar:

1. Crear un modelo usando un algoritmo compatible.
2. Serializa el modelo utilizando un formato binario especial.
3. Realice el modelo disponible en SQL Server. Normalmente, esto significa que almacenar el modelo serializado en una tabla de SQL Server.
4. Llame a la función o procedimiento almacenado y pasar el modelo y datos de entrada.

### <a name="requirements"></a>Requisitos

+ La función PREDICT está disponible en todas las ediciones de SQL Server 2017 y está habilitada de forma predeterminada. No es necesario instalar R o habilitar características adicionales.

+ Si usa sp\_rxPredict, son necesarios algunos pasos adicionales. Consulte [habilitar puntuar en tiempo real](#bkmk_enableRtScoring).

+ En este momento, sólo RevoScaleR y MicrosoftML pueden crear modelos compatibles. Tipos de modelo adicionales están disponibles en el futuro. Para obtener la lista de algoritmos admitidos actualmente, consulte [puntuar en tiempo real](../real-time-scoring.md).

### <a name="serialization-and-storage"></a>Almacenamiento y serialización

Para usar un modelo con cualquiera de las opciones rápidas de puntuación, guarde el modelo con un formato serializado especial, que se ha optimizado para el tamaño y la eficacia de puntuación.

+ Llame a `rxSerializeModel` para escribir un modelo compatible para la **raw** formato.
+ Llame a `rxUnserializeModel` para reconstituir el modelo para su uso en otro código de R, o para ver el modelo.

Para obtener más información, consulte [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel).

**Uso de SQL**

Desde el código SQL, puede entrenar el modelo mediante `sp_execute_external_script`e insertar directamente los modelos entrenados en una tabla, en una columna de tipo **varbinary (max)**.

Para obtener un ejemplo simple, vea [en este tutorial](../tutorials/rtsql-create-a-predictive-model-r.md)

**Uso de R**

Desde el código de R, hay dos maneras de guardar el modelo en una tabla:

+ Llame a la `rxWriteObject` función desde el paquete RevoScaleR, para escribir el modelo directamente en la base de datos.

  El `rxWriteObject()` función puede recuperar objetos de R desde un origen de datos ODBC, como SQL Server, o escribir objetos en SQL Server. La API se modela después de un almacén de pares clave-valor simple.
  
  Si usa esta función, asegúrese de serializar el modelo mediante la nueva función de serialización en primer lugar. A continuación, establezca el *serializar* argumento en `rxWriteObject` en FALSE para evitar repetir el paso de serialización.

+ Puede también guardar el modelo en formato sin procesar en un archivo y, a continuación, se leen desde el archivo en SQL Server. Esta opción puede ser útil si va a mover o copiar modelos entre entornos.

## <a name="native-scoring-with-predict"></a>Puntuación con PREDICT nativa

En este ejemplo, crear un modelo y, a continuación, llame a la función de predicción en tiempo real desde T-SQL.

### <a name="step-1-prepare-and-save-the-model"></a>Paso 1. Preparar y guardar el modelo

Ejecute el código siguiente para crear la base de datos de ejemplo y las tablas necesarias.

```SQL
CREATE DATABASE NativeScoringTest;
GO
USE NativeScoringTest;
GO
DROP TABLE IF EXISTS iris_rx_data;
GO
CREATE TABLE iris_rx_data (
  "Sepal.Length" float not null, "Sepal.Width" float not null
  , "Petal.Length" float not null, "Petal.Width" float not null
  , "Species" varchar(100) null
);
GO
```

Use la siguiente instrucción para rellenar la tabla de datos con los datos de la **iris** conjunto de datos.

```SQL
INSERT INTO iris_rx_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width" , "Species")
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

Ahora, cree una tabla para almacenar los modelos.

```SQL
DROP TABLE IF EXISTS ml_models;
GO
CREATE TABLE ml_models ( model_name nvarchar(100) not null primary key
  , model_version nvarchar(100) not null
  , native_model_object varbinary(max) not null);
GO
```

El código siguiente crea un modelo basado en el **iris** conjunto de datos y lo guarda en la tabla denominada **modelos**.

```SQL
DECLARE @model varbinary(max);
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'
    iris.sub <- c(sample(1:50, 25), sample(51:100, 25), sample(101:150, 25))
    iris.dtree <- rxDTree(Species ~ Sepal.Length + Sepal.Width + Petal.Length + Petal.Width, data = iris[iris.sub, ])
    model <- rxSerializeModel(iris.dtree, realtimeScoringOnly = TRUE)
    '
  , @params = N'@model varbinary(max) OUTPUT'
  , @model = @model OUTPUT
  INSERT [dbo].[ml_models]([model_name], [model_version], [native_model_object])
  VALUES('iris.dtree','v1', @model) ;
```

> [!NOTE] 
> Asegúrese de usar el [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) función de RevoScaleR para guardar el modelo. El estándar de R `serialize` función no puede generar el formato requerido.

Puede ejecutar una instrucción como la siguiente para ver el modelo almacenado en formato binario:

```SQL
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>Paso 2. Ejecutar PREDICT en el modelo

La siguiente instrucción de PREDICCIÓN simple Obtiene una clasificación desde el modelo de árbol de decisión mediante el **puntuación nativa** función. Predice la especie de iris en función de los atributos proporcionados, la longitud del pétalo y ancho.

```SQL
DECLARE @model varbinary(max) = (
  SELECT native_model_object
  FROM ml_models
  WHERE model_name = 'iris.dtree'
  AND model_version = 'v1');
SELECT d.*, p.*
  FROM PREDICT(MODEL = @model, DATA = dbo.iris_rx_data as d)
  WITH(setosa_Pred float, versicolor_Pred float, virginica_Pred float) as p;
go
```

Si se produce un error, "Error durante la ejecución de la función PREDICT. Modelo está dañado o no válido", normalmente significa que la consulta no devolvió un modelo. Compruebe si ha escrito el nombre del modelo correctamente, o si la tabla de modelos está vacía.

> [!NOTE]
> Dado que las columnas y valores devuelven por **PREDICT** puede variar por tipo de modelo, debe definir el esquema de los datos devueltos mediante el uso de un **WITH** cláusula.

## <a name="real-time-scoring-with-sprxpredict"></a>Puntuación con sp_rxPredict en tiempo real

En esta sección se describe los pasos necesarios para configurar **en tiempo real** predicción y proporciona un ejemplo de cómo llamar a la función desde T-SQL.

### <a name ="bkmk_enableRtScoring"></a> Paso 1. Habilitar el procedimiento de puntuación en tiempo real

Debe habilitar esta característica para cada base de datos que desea usar para la puntuación. El administrador del servidor debe ejecutar la utilidad de línea de comandos, RegisterRExt.exe, que se incluye con el paquete RevoScaleR.

> [!NOTE]
> Para puntuar en tiempo real para que funcione, la funcionalidad de CLR de SQL debe habilitarse en la instancia; Además, la base de datos debe estar marcado como de confianza. Al ejecutar el script, estas acciones se realizan automáticamente. Sin embargo, tenga en cuenta las implicaciones de seguridad adicional antes de hacer esto!

1. Abra un símbolo del sistema con privilegios elevados y vaya a la carpeta donde se encuentra RegisterRExt.exe. La siguiente ruta de acceso puede usarse en una instalación predeterminada:
    
    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. Ejecute el siguiente comando, sustituyendo el nombre de la instancia y la base de datos de destino donde desea habilitar los procedimientos almacenados extendidos:

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    Por ejemplo, para agregar el procedimiento almacenado extendido a la base de datos CLRPredict en la instancia predeterminada, escriba:

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    El nombre de instancia es opcional si se encuentra la base de datos en la instancia predeterminada. Si usa una instancia con nombre, debe especificar el nombre de instancia.

3. RegisterRExt.exe crea los siguientes objetos:

    + Ensamblados de confianza
    + El procedimiento almacenado `sp_rxPredict`
    + Un nuevo rol de base de datos, `rxpredict_users`. El Administrador de base de datos puede usar esta función para conceder permiso a los usuarios que utilizan la funcionalidad de puntuación en tiempo real.

4. Agregar los usuarios que necesitan para ejecutar `sp_rxPredict` al nuevo rol.

> [!NOTE]
> 
> En SQL Server 2017, las medidas de seguridad adicionales están en vigor para evitar problemas con la integración CLR. Estas medidas imponen restricciones adicionales sobre el uso de este procedimiento almacenado también. 

### <a name="step-2-prepare-and-save-the-model"></a>Paso 2. Preparar y guardar el modelo

El formato binario requerido por el sp\_rxPredict es el mismo que el formato necesario para usar la función PREDICT. Por lo tanto, en el código de R, incluya una llamada a [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)y no olvide especificar `realtimeScoringOnly = TRUE`, como en este ejemplo:

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-3-call-sprxpredict"></a>Paso 3. Llamada sp_rxPredict

Llamar a sp\_rxPredict como haría con cualquier otro procedimiento almacenado. En la versión actual, el procedimiento almacenado solo acepta dos parámetros:  _\@modelo_ para el modelo en formato binario, y  _\@inputData_ para que los datos que se va a usar para determinar la puntuación, se definen como una consulta SQL válida.

Dado que el formato binario es el mismo que se usa la función de PREDICCIÓN, puede usar la tabla de datos y modelos del ejemplo anterior.

```SQL
DECLARE @irismodel varbinary(max)
SELECT @irismodel = [native_model_object] from [ml_models]
WHERE model_name = 'iris.dtree' 
AND model_version = 'v1''

EXEC sp_rxPredict
@model = @irismodel,
@inputData = N'SELECT * FROM iris_rx_data'
```

> [!NOTE]
> 
> La llamada a sp\_rxPredict se produce un error si los datos de entrada para la puntuación no incluyen columnas que coinciden con los requisitos del modelo. Actualmente, se admiten solo los siguientes tipos de datos. NET: double, float, short, ushort, long, ulong y cadena.
> 
> Por lo tanto, es posible que deba filtrar los tipos no compatibles en los datos de entrada antes de usarlo para puntuar en tiempo real.
> 
> Para obtener información acerca de los correspondientes tipos SQL, vea [asignación de tipos de CLR de SQL](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping) o [asignación de datos de parámetros CLR](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data).

## <a name="disable-real-time-scoring"></a>Deshabilitar la puntuación en tiempo real

Para deshabilitar la funcionalidad de puntuación en tiempo real, abra un símbolo del sistema con privilegios elevados y ejecute el siguiente comando: `RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

## <a name="real-time-scoring-in-other-microsoft-product"></a>Puntuación en tiempo real en otro producto de Microsoft

Si usa el servidor independiente o un servidor de Microsoft Machine Learning en lugar de análisis en bases de datos de SQL Server, tiene otras opciones además de procedimientos almacenados y funciones de Transact-SQL para generar predicciones.

El servidor independiente y el servidor de Machine Learning admiten el concepto de un *servicio web* para la implementación de código. Puede agrupar un R o Python modelo previamente entrenado como un servicio web, que se llama en tiempo de ejecución para evaluar las nuevas entradas de datos. Para más información, vea estos artículos:

+ [¿Cuáles son los servicios web en Machine Learning Server?](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [¿Qué es la puesta en marcha?](https://docs.microsoft.com/machine-learning-server/operationalize/concept-operationalize-deploy-consume)
+ [Implementar un modelo de Python como un servicio web con Azure ml-model-management-sdk](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [Publicar un modelo en tiempo real o un bloque de código de R como un servicio web nuevo](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [paquete de mrsdeploy para R](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)
