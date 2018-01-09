---
title: Uso de R en la base de datos SQL Azure | Documentos de Microsoft
ms.custom: 
ms.date: 12/08/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: e6376a5b03a272633e876b993c3a67467d7b4637
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="using-r-in-azure-sql-database"></a>Uso de R en la base de datos SQL Azure

En octubre de 2017, el equipo de desarrollo de SQL Server anunciado planes para admitir la ejecución de R código de bases de datos mediante procedimientos almacenados, similares a los servicios de R en SQL Server 2016. 

Para mantener al día en la programación de publicación y próximos eventos, vea el [blog de SQL Server](https://blogs.technet.microsoft.com/dataplatforminsider/) o [blog de Microsoft R Server](https://blogs.msdn.microsoft.com/rserver/).

> [!IMPORTANT]
> Actualmente, la vista previa de soporte técnico de R solo está disponible en la base de datos de SQL de Azure en el oeste Ee.uu. Central y características están limitadas en comparación con las características de R y ejecución en SQL Server 2016 o 2017 del código Python.

## <a name="whats-included"></a>Qué se incluye

La funcionalidad de R en bases de datos puede utilizarse en los siguientes niveles de servicio de base de datos y los niveles de rendimiento:
 
- Nivel de servicio Premium: P1, P2, P4, P6, P11, P15
- Premium servicio RS nivel: PRS1, PRS2, PRS4, PRS6
- Grupo elástico Premium: 125 Edtu o superior
- Grupo de RS elástica Premium: 125 Edtu o superior

La versión de vista previa incluye estos paquetes:

+   Microsoft R Open con R versión 3.3.3
+   Funciones y paquetes de R de base se instalaron previamente
+   Microsoft R Server 9.2, incluido el paquete RevoScaleR

En la versión de vista previa actual, puede realizar las siguientes tareas:

+ Entrenamiento de modelos mediante cualquier dato que cabe en la memoria
+   La puntuación de modelos mediante cualquier dato que cabe en la memoria
+   Paralelismo trivial para la ejecución del Script de R (mediante el @parallel parámetro en sp_execute_external_script)
+   Transmisión por secuencias de ejecución para la ejecución del Script de R (mediante @r_RowsPerRead parámetro en sp_execute_external_script)
+   Ejecutar un script de R único al mismo tiempo


No se admiten las siguientes tareas en la versión preliminar de R en la base de datos de SQL Azure:

+ No se puede habilitar la ejecución de script de R en bases de datos específicas.
+ DMV proporcionan al monitor de CPU y uso de memoria de scripts de R no están disponibles.
+ No se puede instalar ningún paquete de aplicaciones de terceros. No se admite la instrucción crear biblioteca externa.

## <a name="example"></a>Ejemplo

En la base de datos de SQL Azure, se ejecutan todos los comandos de R de T-SQL, utilizando el procedimiento almacenado [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql). 

En el ejemplo siguiente se muestra cómo probar la característica de vista previa, con el conjunto de datos de iris incluido con base R.

### <a name="step-1-create-the-data-tables"></a>Paso 1. Crear las tablas de datos

Empiece por crear dos tablas: uno para almacenar los datos de origen extraídos de R y otro para almacenar el modelo entrenado.

```sql
DROP TABLE IF EXISTS iris_data, iris_models;
GO
CREATE TABLE iris_data (
        id INT NOT NULL IDENTITY PRIMARY KEY
        , "Sepal.Length" FLOAT NOT NULL, "Sepal.Width" FLOAT NOT NULL
        , "Petal.Length" FLOAT NOT NULL, "Petal.Width" FLOAT NOT NULL
        , "Species" VARCHAR(100) NULL
);
CREATE TABLE iris_models (
    model_name VARCHAR(30) NOT NULL PRIMARY KEY,
    model VARBINARY(max) NOT NULL,
    native_model VARBINARY(MAX) NOT NULL
);
GO
```

### <a name="step-2-populate-table-with-data-from-the-iris-dataset"></a>Paso 2. Rellenar la tabla con datos procedentes del conjunto de datos de iris

Después de las tablas se han creado, ejecute el siguiente código para insertar datos de entrenamiento en la tabla. El procedimiento almacenado sp_execute_external_script llama R y devuelve el conjunto de datos de iris como una trama de datos, utilizando el esquema especificado en la instrucción INSERT INTO.

```sql
INSERT INTO iris_data
("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
EXEC sp_execute_external_script @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

### <a name="step-3-create-the-stored-procedure-that-generates-the-model"></a>Paso 3. Crear el procedimiento almacenado que genera el modelo

El siguiente procedimiento almacenado realiza el trabajo de crear y entrenar el modelo, que puede guardarse en cualquiera de los dos formatos binarios de realmente.

```sql
CREATE PROCEDURE generate_iris_model
    @trained_model VARBINARY(MAX) OUTPUT, 
    @native_trained_model VARBINARY(MAX) OUTPUT
AS
BEGIN
  EXEC sp_execute_external_script @language = N'R'
  , @script = N'
    iris_model <- rxDTree(Species ~ Sepal.Length + Sepal.Width + Petal.Length + Petal.Width, data = iris_rx_data);
    trained_model <- as.raw(serialize(iris_model, connection=NULL));
    native_trained_model <- rxSerializeModel(iris_model, realtimeScoringOnly = TRUE)
    '
  , @input_data_1 = N'SELECT "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" FROM iris_data'
  , @input_data_1_name = N'iris_rx_data'
  , @params = N'@trained_model VARBINARY(MAX) OUTPUT, @native_trained_model VARBINARY(MAX) OUTPUT
    , @trained_model = @trained_model OUTPUT
    , @native_trained_model = @native_trained_model OUTPUT;
End
```

+ El **salida** palabra clave en los parámetros de entrada indica que los valores deben pasarse y se usa para la salida también.
+ La línea que comienza con `iris_model` define un modelo de árbol de decisión para predecir especies basadas en atributos de flores.
+ La llamada a `serialize` guarda el modelo en un formato binario adecuado para su almacenamiento en SQL Server. 
+ O bien, con los modelos basados en algoritmos de RevoScaleR, puede usar el [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel) función, que guarda el modelo en un nuevo formato binario nativo. Modelos se guarden en este formato se pueden cargar para puntuar con la función de PREDICCIÓN en SQL Server.

### <a name="step-4-train-and-save-the-model"></a>Paso 4. Entrenar y guardar el modelo

Después de haber creado el procedimiento almacenado, llámelo para procesar datos de entrada y crear un modelo. El código siguiente también guarda el modelo en la tabla **iris_models**, de modo que puede usar más adelante para predecir la especie de flores.

```sql
DECLARE @model VARBINARY(MAX), @native_modelVARBINARY(MAX);
EXEC generate_iris_model @model OUTPUT, @native_model OUTPUT;
DELETE FROM iris_models WHERE model_name = 'iris.dtree';
INSERT INTO iris_models (model_name, model, native_model) VALUES('iris.dtree', @model, @native_model);
SELECT model_name, datalength(model)/1024. AS model_size_kb, datalength(native_model)/1024. AS native_model_size_kb FROM iris_models;
GO
```

### <a name="step-5-create-a-stored-procedure-for-scoring"></a>Paso 5. Crear un procedimiento almacenado para puntuar

A continuación, cree un procedimiento almacenado para puntuar. Este procedimiento almacenado carga un modelo especificado de la tabla y crea puntuaciones en función de los datos de entrada.

```sql
CREATE PROCEDURE predict_iris_species (@model varchar(100))
AS
BEGIN
  DECLARE @rx_model VARBINARY(MAX) = (SELECT model FROM iris_models WHERE model_name = @model);
  EXEC sp_execute_external_script @language = N'R'
  , @script = N'
    irismodel<-unserialize(rx_model);
    OutputDataSet <-rxPredict(irismodel, iris_rx_data, extraVarsToWrite = c("Species", "id"));
      '
  , @input_data_1 = N'SELECT "id", "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" FROM iris_data'
  , @input_data_1_name = N'iris_rx_data'
  , @params = N'@rx_model varbinary(max)'
  , @rx_model = @rx_model
  WITH RESULT SETS ( ("setosa_Pred" FLOAT, "versicolor_Pred" FLOAT, "virginica_Pred" FLOAT, "Species.Actual" VARCHAR(100), "id" INT));
END;
GO
```

Este procedimiento almacenado se usa el [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) función, pero se podría usar la función de PREDICCIÓN nativa en T-SQL tal como se muestra [aquí](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/09/25/announcing-general-availability-of-native-scoring-using-predict-function-in-azure-sql-database/). Uso de la función de PREDICCIÓN requiere el uso de un [ **rx** modelo](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-revoscaler) y guarde el modelo con [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel).

### <a name="step-6-use-the-stored-procedure-to-generate-predictions"></a>Paso 6. Use el procedimiento almacenado para generar predicciones

Para generar puntuaciones a partir del modelo, ejecute el procedimiento almacenado. Puede insertar los valores en una tabla o devolver las predicciones a una aplicación que realiza la llamada.

```sql
EXEC predict_iris_species 'iris.dtree';
GO
```

## <a name="related-resources"></a>Recursos relacionados

Azure Marketplace también proporciona varias máquinas virtuales que incluyen SQL Server 2017:

+ [Aprovisionar una máquina virtual para el aprendizaje automático de Azure](provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)

Consulte también estas máquinas virtuales, que vienen preconfiguradas con una variedad de herramientas de aprendizaje de automático popular:

+ [Data Science Virtual Machine](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/overview)
+ [Máquina Virtual de aprendizaje profundo](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/deep-learning-dsvm-overview)

