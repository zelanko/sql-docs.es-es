---
title: "Cómo realizar la puntuación en tiempo real o puntuación nativo de SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 11/09/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 9287a85017df7b05b3b354a855811ea528a3ad79
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2018
---
# <a name="how-to-perform-realtime-scoring-or-native-scoring-in-sql-server"></a>Cómo realizar la puntuación en tiempo real o puntuación nativo de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este tema proporciona instrucciones y código de ejemplo de cómo ejecutar el en tiempo real de la puntuación y las características nativas de puntuación de 2017 de SQL Server y SQL Server 2016. El objetivo de puntuación en tiempo real y de puntuación nativo es mejorar el rendimiento de las operaciones de puntuación de lotes pequeños.

Tanto en tiempo real de puntuación y de puntuación nativo están diseñados para permitir el uso de un modelo de aprendizaje sin tener que instalar R. automático Todo lo que necesita hacer es obtener un modelo previamente entrenado en un formato compatible y lo guarda en una base de datos de SQL Server.

## <a name="choosing-a-scoring-method"></a>Elegir un método de puntuación

Se admiten las siguientes opciones para la predicción por lotes rápidamente:

+ **Puntuación nativo**: función PREDECIR de T-SQL en SQL Server 2017
+ **En tiempo real de puntuación**: con sp\_rxPredict el procedimiento almacenado en SQL Server 2016 o 2017 de SQL Server.

> [!NOTE]
> Se recomienda el uso de la función de PREDICCIÓN en SQL Server 2017.
> Usar sp\_rxPredict requiere que habilite la integración de SQLCLR. Antes de habilitar esta opción, tenga en cuenta las implicaciones de seguridad.

El proceso general de preparar el modelo y, a continuación, generar puntuaciones es similar:

1. Crear un modelo usando un algoritmo compatible.
2. Serializa el modelo utilizando un formato binario especial.
3. Hacer que el modelo esté disponible para SQL Server. Normalmente, esto significa almacenar el modelo serializado en una tabla de SQL Server.
4. Llame a la función o procedimiento almacenado y pasar el modelo y datos de entrada.

### <a name="requirements"></a>Requisitos

+ La función de PREDICCIÓN está disponible en todas las ediciones de SQL Server 2017 y está habilitada de forma predeterminada. No es necesario instalar R o habilitar características adicionales.

+ Si usa sp\_rxPredict, son necesarios algunos pasos adicionales. Vea [habilitar en tiempo real de puntuación](#bkmk_enableRtScoring).

+ En este momento, solo RevoScaleR y MicrosoftML pueden crear modelos compatibles. Tipos de modelo adicionales están disponibles en el futuro. Para obtener la lista de algoritmos actualmente compatibles, consulte [en tiempo real de puntuación](../real-time-scoring.md).

### <a name="serialization-and-storage"></a>Serialización y almacenamiento

Para usar un modelo con cualquiera de las opciones de puntuación rápidas, guarde el modelo utilizando un formato serializado especial, que se ha optimizado para el tamaño y la eficacia de puntuación.

+ Llame a `rxSerializeModel` para escribir un modelo admitidos para la **sin formato** formato.
+ Llame a `rxUnserializeModel` para reconstituir el modelo para su uso en otro código de R, o para ver el modelo.

Para obtener más información, consulte [rxSerializeModel](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel).

**Usar SQL**

Desde el código SQL, puede entrenar el modelo con `sp_execute_external_script`e insertar directamente los modelos entrenados en una tabla, en una columna de tipo **varbinary (max)**.

Para obtener un ejemplo, vea [este tutorial](../tutorials/rtsql-create-a-predictive-model-r.md)

**Uso de R**

Desde el código de R, hay dos maneras de guardar el modelo en una tabla:

+ Llame a la `rxWriteObject` función del paquete RevoScaleR, para escribir el modelo directamente en la base de datos.

  El `rxWriteObject()` función puede recuperar objetos de R de un origen de datos ODBC como SQL Server, o escribir objetos en SQL Server. La API se basa en un almacén de clave y valor simple.
  
  Si usa esta función, asegúrese de serializar el modelo utilizando la nueva función de serialización en primer lugar. A continuación, establezca el *serializar* argumento en `rxWriteObject` en Falso, para evitar repetir el paso de serialización.

+ Puede guardar el modelo en formato sin procesar en un archivo y, a continuación, se leen desde el archivo en SQL Server. Esta opción puede ser útil si va a mover o copiar modelos entre entornos.

## <a name="native-scoring-with-predict"></a>Nativo de puntuación con PREDICT

En este ejemplo, crear un modelo y, a continuación, llame a la función de predicción en tiempo real de T-SQL.

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

Utilice la siguiente instrucción para rellenar la tabla de datos con los datos de la **iris** conjunto de datos.

```SQL
INSERT INTO iris_rx_data ("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width" , "Species")
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

Ahora, cree una tabla para almacenar modelos.

```SQL
DROP TABLE IF EXISTS ml_models;
GO
CREATE TABLE ml_models ( model_name nvarchar(100) not null primary key
  , model_version nvarchar(100) not null
  , native_model_object varbinary(max) not null);
GO
```

El siguiente código crea un modelo basado en la **iris** conjunto de datos y lo guarda en la tabla denominada **modelos**.

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
> Asegúrese de utilizar el [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) función de RevoScaleR para guardar el modelo. El estándar R `serialize` función no puede generar el formato requerido.

Puede ejecutar una instrucción como la siguiente para ver el modelo almacenado en formato binario:

```SQL
SELECT *, datalength(native_model_object)/1024. as model_size_kb
FROM ml_models;
```

### <a name="step-2-run-predict-on-the-model"></a>Paso 2. Ejecutar PREDICT en el modelo

La siguiente instrucción de PREDICCIÓN simple Obtiene una clasificación desde el modelo de árbol de decisión con la **puntuación nativo** función. Predice la especie iris en función de los atributos proporcionados, longitud pétalo y ancho.

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

Si se produce un error, "Error durante la ejecución de la función de PREDICCIÓN. Modelo está dañado o no válido", normalmente significa que la consulta no devolvió un modelo. Compruebe si se ha escrito el nombre del modelo correctamente, o si la tabla de modelos está vacía.

> [!NOTE]
> Dado que las columnas y valores devuelven por **PREDICT** puede variar según el tipo de modelo, debe definir el esquema de los datos devueltos mediante un **WITH** cláusula.

## <a name="realtime-scoring-with-sprxpredict"></a>En tiempo real con sp_rxPredict de puntuación

Esta sección describen los pasos necesarios para configurar **en tiempo real** predicción y proporciona un ejemplo de cómo llamar a la función desde código T-SQL.

### <a name ="bkmk_enableRtScoring"></a>Paso 1. Habilitar el procedimiento de puntuación de en tiempo real

Debe habilitar esta característica para cada base de datos que desea usar para puntuar. El administrador del servidor debe ejecutar la utilidad de línea de comandos, RegisterRExt.exe, que se incluye con el paquete RevoScaleR.

> [!NOTE]
> En tiempo real de puntuación para trabajar, funcionalidad de CLR de SQL debe estar habilitado en la instancia; Además, la base de datos debe estar marcado como de confianza. Cuando se ejecuta la secuencia de comandos, estas acciones se realizan automáticamente. Sin embargo, tenga en cuenta las implicaciones de seguridad adicional antes de hacerlo.

1. Abra un símbolo del sistema con privilegios elevados y vaya a la carpeta donde se encuentra RegisterRExt.exe. La ruta de acceso siguiente puede utilizarse en una instalación predeterminada:
    
    `<SQLInstancePath>\R_SERVICES\library\RevoScaleR\rxLibs\x64\`

2. Ejecute el siguiente comando, sustituyendo el nombre de la instancia y la base de datos de destino en la que desea habilitar los procedimientos almacenados extendidos:

    `RegisterRExt.exe /installRts [/instance:name] /database:databasename`

    Por ejemplo, para agregar el procedimiento almacenado extendido a la base de datos CLRPredict en la instancia predeterminada, escriba:

    `RegisterRExt.exe /installRts /database:CLRPRedict`

    El nombre de instancia es opcional si la base de datos se encuentra en la instancia predeterminada. Si está utilizando una instancia con nombre, debe especificar el nombre de instancia.

3. RegisterRExt.exe crea los siguientes objetos:

    + Ensamblados de confianza
    + El procedimiento almacenado`sp_rxPredict`
    + Un nuevo rol de base de datos, `rxpredict_users`. El Administrador de base de datos puede utilizar esta función para conceder permiso a los usuarios que utilizan la funcionalidad de puntuación en tiempo real.

4. Agregue los usuarios que necesitan ejecutar `sp_rxPredict` a la nueva función.

> [!NOTE]
> 
> En SQL Server de 2017 medidas de seguridad adicionales son para evitar problemas con la integración CLR. Estas medidas imponen restricciones adicionales sobre el uso de este procedimiento almacenado también. 

### <a name="step-2-prepare-and-save-the-model"></a>Paso 2. Preparar y guardar el modelo

El formato binario requerido por sp\_rxPredict es el mismo que el formato necesario para usar la función de PREDICCIÓN. Por lo tanto, en el código de R, incluya una llamada a [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)y no olvide especificar `realtimeScoringOnly = TRUE`, como en este ejemplo:

```R
model <- rxSerializeModel(model.name, realtimeScoringOnly = TRUE)
```

### <a name="step-3-call-sprxpredict"></a>Paso 3. Llamar a sp_rxPredict

Se llama a sp\_rxPredict como haría con cualquier otro procedimiento almacenado. En la versión actual, el procedimiento almacenado toma dos parámetros:  _@model_  para el modelo en formato binario, y  _@inputData_  para que los datos que se va a usar para determinar la puntuación, definen como una consulta SQL válida .

Dado que el formato binario es el mismo que se utiliza la función de PREDICCIÓN, puede usar la tabla de datos y modelos del ejemplo anterior.

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
> La llamada a sp\_rxPredict se produce un error si los datos de entrada para puntuar no incluyen columnas que coinciden con los requisitos del modelo. Actualmente, se admiten sólo los siguientes tipos de datos. NET: double, float, short, ushort, long, ulong y cadena.
> 
> Por lo tanto, deberá filtrar los tipos no compatibles en los datos de entrada antes de usarlo para puntuar en tiempo real.
> 
> Para obtener información acerca de los tipos correspondientes de SQL, consulte [asignación de tipo de CLR de SQL](https://msdn.microsoft.com/library/bb386947.aspx) o [asignación de datos de parámetro de CLR](https://docs.microsoft.com/sql/relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data).

## <a name="disable-realtime-scoring"></a>Deshabilitar la puntuación en tiempo real

Para deshabilitar la funcionalidad de puntuación en tiempo real, abra un símbolo del sistema con privilegios elevados y ejecute el siguiente comando:`RegisterRExt.exe /uninstallrts /database:<database_name> [/instance:name]`

## <a name="realtime-scoring-in-microsoft-r-server-or-machine-learning-server"></a>En tiempo real de puntuación en Microsoft R Server o servidor de aprendizaje de máquina

Servidor de aprendizaje de máquina admite distribuida en tiempo real de puntuación de modelos publicados como un servicio web. Para más información, vea estos artículos:

+ [¿Cuáles son los servicios web en el servidor de aprendizaje de máquina?](https://docs.microsoft.com/machine-learning-server/operationalize/concept-what-are-web-services)
+ [¿Qué es la puesta en marcha?](https://docs.microsoft.com/machine-learning-server/operationalize/concept-operationalize-deploy-consume)
+ [Implementar un modelo de Python como un servicio web con el aprendizaje automático de Azure-modelo-sdk de administración](https://docs.microsoft.com/machine-learning-server/operationalize/python/quickstart-deploy-python-web-service)
+ [Publicar un modelo en tiempo real o un bloque de código de R como un servicio web nuevo](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/publishservice)
+ [paquete de mrsdeploy para R](https://docs.microsoft.com/machine-learning-server/r-reference/mrsdeploy/mrsdeploy-package)
