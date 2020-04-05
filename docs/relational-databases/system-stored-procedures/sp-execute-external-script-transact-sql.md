---
title: sp_execute_external_script (Transact-SQL) Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: machine-learning
ms.topic: language-reference
f1_keywords:
- sp_execute_external_script_TSQL
- sys.sp_execute_external_script
- sys.sp_execute_external_script_TSQL
- sp_execute_external_script
dev_langs:
- TSQL
helpviewer_keywords:
- sp_execute_external_script
ms.assetid: de4e1fcd-0e1a-4af3-97ee-d1becc7f04df
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 8800df26e505f1fffe25e6f65218481e7a8158f0
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2020
ms.locfileid: "80663010"
---
# <a name="sp_execute_external_script-transact-sql"></a>sp_execute_external_script (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
El procedimiento almacenado **sp_execute_external_script** ejecuta un script proporcionado como argumento de entrada para el procedimiento y se usa con Machine [Learning Services](../../machine-learning/index.yml) y extensiones de [lenguaje.](../../language-extensions/language-extensions-overview.md) 

Para Machine Learning Services, [Python](../../machine-learning/concepts/extension-python.md) y [R](../../machine-learning/concepts/extension-r.md) son idiomas compatibles. Para extensiones de lenguaje, Java es compatible, pero debe definirse con [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md).

Para ejecutar **sp_execute_external_script**, primero debe instalar Machine Learning Services o Extensiones de idioma. Para obtener más información, vea [Instalar SQL Server Machine Learning Services (Python y R) en Windows](../../machine-learning/install/sql-machine-learning-services-windows-install.md) y [Linux](../../linux/sql-server-linux-setup-machine-learning.md)o Instalar [extensiones](../../language-extensions/install/install-sql-server-language-extensions-on-windows.md) de lenguaje de SQL Server en Windows y [Linux.](../../linux/sql-server-linux-setup-language-extensions.md)
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
El procedimiento almacenado **sp_execute_external_script** ejecuta un script proporcionado como argumento de entrada para el procedimiento y se usa con Machine [Learning Services](../../machine-learning/index.yml) en SQL Server 2017. 

Para Machine Learning Services, [Python](../../machine-learning/concepts/extension-python.md) y [R](../../machine-learning/concepts/extension-r.md) son idiomas compatibles. 

Para ejecutar **sp_execute_external_script**, primero debe instalar Machine Learning Services. Para obtener más información, vea [Instalar SQL Server Machine Learning Services (Python y R) en Windows.](../../machine-learning/install/sql-machine-learning-services-windows-install.md)
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
El procedimiento almacenado **sp_execute_external_script** ejecuta un script proporcionado como argumento de entrada para el procedimiento y se usa con [R Services](../../machine-learning/r/sql-server-r-services.md) en SQL Server 2016.

Para R Services, [R](../../machine-learning/concepts/extension-r.md) es el idioma admitido.

Para ejecutar **sp_execute_external_script**, primero debe instalar R Services. Para obtener más información, vea [Instalar SQL Server Machine Learning Services (Python y R) en Windows.](../../machine-learning/install/sql-r-services-windows-install.md)
::: moniker-end

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
## <a name="syntax"></a>Sintaxis

```
sp_execute_external_script   
    @language = N'language',   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]  
    [ , @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]    
    [ , @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]  
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
## <a name="syntax-for-2017-and-earlier"></a>Sintaxis para 2017 y versiones anteriores

```
sp_execute_external_script   
    @language = N'language',   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]  
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```
::: moniker-end

## <a name="arguments"></a>Argumentos
 Idioma n'*idioma*' ** \@**  
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
 Indica el idioma del script. *idioma* es **sysname**. Los valores válidos son **R**, **Python**y cualquier lenguaje definido con [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) (por ejemplo, Java).
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
 Indica el idioma del script. *idioma* es **sysname**. En SQL Server 2017, los valores válidos son **R** y **Python.**
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
 Indica el idioma del script. *idioma* es **sysname**. En SQL Server 2016, el único valor válido es **R**.
::: moniker-end

 Script á N'*script*' Script de lenguaje externo especificado como una entrada literal o variable. ** \@** *script* es **nvarchar(max)**.  

`[ @input_data_1 =  N'input_data_1' ]`Especifica los datos de entrada utilizados por el [!INCLUDE[tsql](../../includes/tsql-md.md)] script externo en forma de consulta. El tipo de datos de *input_data_1* es **nvarchar(max)**.

`[ @input_data_1_name = N'input_data_1_name' ]`Especifica el nombre de la variable utilizada @input_data_1para representar la consulta definida por . El tipo de datos de la variable en el script externo depende del idioma. En el caso de R, la variable de entrada es un marco de datos. En el caso de Python, la entrada debe ser tabular. *input_data_1_name* es **sysname**.  El valor predeterminado es *InputDataSet*.  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
`[ @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]`Se utiliza para crear modelos por partición. Especifica el nombre de la columna utilizada para ordenar el conjunto de resultados, por ejemplo, por nombre de producto. El tipo de datos de la variable en el script externo depende del idioma. En el caso de R, la variable de entrada es un marco de datos. En el caso de Python, la entrada debe ser tabular.

`[ @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]`Se utiliza para crear modelos por partición. Especifica el nombre de la columna utilizada para segmentar datos, como la región geográfica o la fecha. El tipo de datos de la variable en el script externo depende del idioma. En el caso de R, la variable de entrada es un marco de datos. En el caso de Python, la entrada debe ser tabular. 
::: moniker-end

`[ @output_data_1_name =  N'output_data_1_name' ]`Especifica el nombre de la variable en el script externo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contiene los datos que se devolverán al finalizar la llamada al procedimiento almacenado. El tipo de datos de la variable en el script externo depende del idioma. Para R, la salida debe ser una trama de datos. Para Python, la salida debe ser un marco de datos pandas. *output_data_1_name* es **sysname**.  El valor predeterminado es *OutputDataSet*.  

`[ @parallel = 0 | 1 ]`Habilite la ejecución paralela de `@parallel` scripts de R estableciendo el parámetro en 1. El valor predeterminado para este parámetro es 0 (sin paralelismo). Si `@parallel = 1` y la salida se transmite directamente al `WITH RESULT SETS` equipo cliente, se requiere la cláusula y se debe especificar un esquema de salida.  

 + Para los scripts de R que no `@parallel` utilizan funciones RevoScaleR, el uso del parámetro puede ser beneficioso para procesar conjuntos de datos grandes, suponiendo que el script se pueda paralelizar trivialmente. Por ejemplo, cuando `predict` se utiliza la función R `@parallel = 1` con un modelo para generar nuevas predicciones, establezca como sugerencia para el motor de consultas. Si la consulta se puede paralelizar, las filas se distribuyen según la configuración **MAXDOP.**  
  
 + Para los scripts de R que utilizan funciones RevoScaleR, `@parallel = 1` el procesamiento paralelo se controla automáticamente y no debe especificar la **llamada sp_execute_external_script.**  
  
`[ @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ]`Una lista de declaraciones de parámetros de entrada que se utilizan en el script externo.  
  
`[ @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]`Una lista de valores para los parámetros de entrada utilizados por el script externo.  

## <a name="remarks"></a>Observaciones

> [!IMPORTANT]
> El árbol de consultas está controlado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los usuarios no pueden realizar operaciones arbitrarias en la consulta. 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Utilice **sp_execute_external_script** para ejecutar scripts escritos en un idioma admitido. Los lenguajes admitidos son **Python** y **R** que se utilizan con Machine Learning Services, y cualquier lenguaje definido con [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) (por ejemplo, Java) utilizado con extensiones de lenguaje.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Utilice **sp_execute_external_script** para ejecutar scripts escritos en un idioma admitido. Los lenguajes admitidos son **Python** y **R** en SQL Server 2017 Machine Learning Services.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Utilice **sp_execute_external_script** para ejecutar scripts escritos en un idioma admitido. El único idioma admitido es **R** en SQL Server 2016 R Services.
::: moniker-end

De forma predeterminada, los conjuntos de resultados devueltos por este procedimiento almacenado se generan con columnas sin nombre. Los nombres de columna utilizados dentro de un script son locales para el entorno de scripting y no se reflejan en el conjunto de resultados outputted. Para asignar un nombre `WITH RESULT SET` a [`EXECUTE`](../../t-sql/language-elements/execute-transact-sql.md)las columnas del conjunto de resultados, utilice la cláusula de .

Además de devolver un conjunto de resultados, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede devolver valores escalares mediante parámetros OUTPUT. 
  
Puede controlar los recursos utilizados por scripts externos configurando un grupo de recursos externo. Para obtener más información, vea [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQLTransact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md). La información sobre la carga de trabajo se puede obtener de las vistas de catálogo del regulador de recursos, DMV y contadores. Para obtener más información, vea Vistas de catálogo del regulador de recursos [&#40;&#41;Transact-SQLTransact-SQL ](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md), Vistas de administración dinámica relacionadas con el regulador de recursos [&#40;&#41;Transact-SQLTransact-SQL ](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)y Objeto de scripts externos de [SQL Server.](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  

### <a name="monitor-script-execution"></a>Supervisar la ejecución del script

Supervise la ejecución del script mediante [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) y [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="parameters-for-partition-modeling"></a>Parámetros para el modelado de particiones

Puede establecer dos parámetros adicionales que habilitan el modelado en datos particionados, donde las particiones se basan en una o varias columnas que proporciona que segmentan naturalmente un conjunto de datos en particiones lógicas creadas y utilizadas solo durante la ejecución del script. Las columnas que contienen valores repetidos para la edad, el sexo, la región geográfica, la fecha u hora, son algunos ejemplos que se prestan a conjuntos de datos particionados.
 
Los dos parámetros son **input_data_1_partition_by_columns** y **input_data_1_order_by_columns**, donde se utiliza el segundo parámetro para ordenar el conjunto de resultados. Los parámetros se `sp_execute_external_script` pasan como entradas con el script externo ejecutándose una vez para cada partición. Para obtener más información y ejemplos, vea [Tutorial: Crear modelos basados en particiones.](https://docs.microsoft.com/sql/machine-learning/tutorials/r-tutorial-create-models-per-partition)

Puede ejecutar script en paralelo `@parallel=1`especificando . Si la consulta de entrada se `@parallel=1` puede paralelizar, `sp_execute_external_script`debe establecer como parte de los argumentos en . De forma predeterminada, el `@parallel=1` optimizador de consultas funciona en tablas que tienen más de 256 filas, pero si desea controlar esto explícitamente, este script incluye el parámetro como una demostración.

> [!Tip]
> En las cargas de trabajo de entrenamiento, puede usar `@parallel` con cualquier script de entrenamiento arbitrario, incluso aquellos que usan algoritmos rx que no son de Microsoft. Normalmente, solo los algoritmos de RevoScaleR (con el prefijo rx) ofrecen paralelismo en escenarios de entrenamiento de SQL Server. Pero con los nuevos parámetros de SQL Server vNext, puede paralelizar un script que llame a funciones que no están diseñadas específicamente con esa capacidad.
::: moniker-end

### <a name="streaming-execution-for-python-and-r-scripts"></a>Ejecución de streaming para scripts de Python y R  

La transmisión por secuencias permite que el script de Python o R funcione con más datos de los que caben en la memoria. Para controlar el número de filas pasadas durante la `@r_rowsPerRead` transmisión por secuencias, especifique un valor entero para el parámetro, en la `@params` colección.  Por ejemplo, si está entrenando un modelo que utiliza datos muy amplios, podría ajustar el valor para leer menos filas, para asegurarse de que todas las filas se pueden enviar en un fragmento de datos. También puede usar este parámetro para administrar el número de filas que se leen y procesan a la vez, para mitigar los problemas de rendimiento del servidor. 
  
Tanto `@r_rowsPerRead` el parámetro para `@parallel` la transmisión por secuencias como el argumento deben considerarse sugerencias. Para que se aplique la sugerencia, debe ser posible generar un plan de consulta SQL que incluya el procesamiento paralelo. Si esto no es posible, no se puede habilitar el procesamiento paralelo.  
  
> [!NOTE]  
> El streaming y el procesamiento paralelo solo se admiten en Enterprise Edition. Puede incluir los parámetros en las consultas en Standard Edition sin generar un error, pero los parámetros no tienen ningún efecto y los scripts de R se ejecutan en un solo proceso.  
  
## <a name="restrictions"></a>Restricciones  

### <a name="data-types"></a>Tipos de datos

Los siguientes tipos de datos no se admiten cuando se usan en la consulta de entrada o parámetros de **sp_execute_external_script** procedimiento y devuelven un error de tipo no admitido.  

Como solución alternativa, **CAST** la columna [!INCLUDE[tsql](../../includes/tsql-md.md)] o el valor a un tipo admitido antes de enviarlo al script externo.  
  
-   **Cursor**  
  
-   **Timestamp**  
  
-   **datetime2**, **datetimeoffset**, **time**  
  
-   **sql_variant**  
  
-   **texto**, **imagen**  
  
-   **xml**  
  
-   **hierarchyid**, **geometría**, **geografía**  
  
-   Tipos definidos por el usuario CLR

En general, cualquier conjunto de resultados [!INCLUDE[tsql](../../includes/tsql-md.md)] que no se puede asignar a un tipo de datos, se genera como NULL.  

### <a name="restrictions-specific-to-r"></a>Restricciones específicas de R

Si la entrada incluye valores **datetime** que no se ajustan al rango de valores permitido en R, los valores se convierten a **NA**. Esto es [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] necesario porque permite un rango de valores mayor que el que se admite en el lenguaje R.

Los valores flotantes `+Inf` `-Inf`(por ejemplo, , , `NaN`) no se admiten en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aunque ambos idiomas utilicen IEEE 754. Comportamiento actual solo envía [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los valores directamente; como resultado, el cliente [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] SQL en produce un error. Por lo tanto, estos valores se convierten en **NULL**.

## <a name="permissions"></a>Permisos

Requiere permiso de base de datos **EXECUTE ANY EXTERNAL SCRIPT.**  

## <a name="examples"></a>Ejemplos

Esta sección contiene ejemplos de cómo se puede utilizar este [!INCLUDE[tsql](../../includes/tsql-md.md)]procedimiento almacenado para ejecutar scripts de R o Python mediante .

### <a name="a-return-an-r-data-set-to-sql-server"></a>A. Devolver un conjunto de datos de R a SQL Server  

En el ejemplo siguiente se **sp_execute_external_script** crea un procedimiento almacenado que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]usa sp_execute_external_script para devolver el conjunto de datos Iris incluido con R a .  

```sql
DROP PROC IF EXISTS get_iris_dataset;  
go  
CREATE PROC get_iris_dataset
AS  
BEGIN  
 EXEC   sp_execute_external_script  
       @language = N'R'  
     , @script = N'iris_data <- iris;'
     , @input_data_1 = N''  
     , @output_data_1_name = N'iris_data'
     WITH RESULT SETS (("Sepal.Length" float not null,   
           "Sepal.Width" float not null,  
        "Petal.Length" float not null,   
        "Petal.Width" float not null, "Species" varchar(100)));  
END;
GO
```

### <a name="b-generate-an-r-model-based-on-data-from-sql-server"></a>B. Generar un modelo de R basado en datos de SQL Server  

En el ejemplo siguiente se **sp_execute_external_script** crea un procedimiento almacenado que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]usa sp_execute_external_script para generar un modelo de iris y devolver el modelo a .  

> [!NOTE]
>  Este ejemplo requiere la instalación anticipada del paquete e1071. Para obtener más información, vea [Instalar paquetes r adicionales en SQL Server](../../machine-learning/package-management/install-additional-r-packages-on-sql-server.md).

```sql
DROP PROC IF EXISTS generate_iris_model;
GO
CREATE PROC generate_iris_model
AS
BEGIN
 EXEC sp_execute_external_script  
      @language = N'R'  
     , @script = N'  
          library(e1071);  
          irismodel <-naiveBayes(iris_data[,1:4], iris_data[,5]);  
          trained_model <- data.frame(payload = as.raw(serialize(irismodel, connection=NULL)));  
'  
     , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" from iris_data'  
     , @input_data_1_name = N'iris_data'  
     , @output_data_1_name = N'trained_model'  
    WITH RESULT SETS ((model varbinary(max)));  
END;
GO
```

Para generar un modelo similar mediante Python, tendría que cambiar el identificador de idioma de `@language=N'R'` a `@language = N'Python'`y realizar las modificaciones necesarias para el argumento `@script`. En caso contrario, todos los parámetros funcionan del mismo modo que para R.

### <a name="c-create-a-python-model-and-generate-scores-from-it"></a>C. Creación de un modelo de Python y generar puntuaciones a partir de él

En este ejemplo se muestra cómo usar sp\_execute\_external\_script para generar puntuaciones en un modelo simple de Python. 

```sql
CREATE PROCEDURE [dbo].[py_generate_customer_scores]
AS
BEGIN

-- Input query to generate the customer data
DECLARE @input_query NVARCHAR(MAX) = N'SELECT customer, orders, items, cost FROM dbo.Sales.Orders'

EXEC sp_execute_external_script @language = N'Python', @script = N'
import pandas as pd
from sklearn.cluster import KMeans

# Get data from input query
customer_data = my_input_data

# Define the model
n_clusters = 4
est = KMeans(n_clusters=n_clusters, random_state=111).fit(customer_data[["orders","items","cost"]])
clusters = est.labels_
customer_data["cluster"] = clusters

OutputDataSet = customer_data
'
, @input_data_1 = @input_query
, @input_data_1_name = N'my_input_data'
WITH RESULT SETS (("CustomerID" int, "Orders" float,"Items" float,"Cost" float,"ClusterResult" float));
END;
GO
```

Los encabezados de columna utilizados en el código de Python no se envían a SQL Server; por lo tanto, utilice la instrucción WITH RESULT para especificar los nombres de columna y los tipos de datos que se va a usar en SQL.

Para puntuar, también puede usar la función nativa [PREDICT](../../t-sql/queries/predict-transact-sql.md), que es normalmente más rápida porque evita llamar al runtime de Python o R.

## <a name="see-also"></a>Vea también

+ [SQL Server Machine Learning Services](../../machine-learning/index.yml)
+ [Extensiones de idioma de SQL Server](../../language-extensions/language-extensions-overview.md). 
+ [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
+ [Bibliotecas y tipos de datos de Python](../../machine-learning/python/python-libraries-and-data-types.md)  
+ [Bibliotecas R y tipos de datos R](../../machine-learning/r/r-libraries-and-data-types.md)  
+ [Servicios de SQL Server R](../../machine-learning/r/sql-server-r-services.md)   
+ [Problemas conocidos de SQL Server Machine Learning Services](../../machine-learning/known-issues-for-sql-server-machine-learning-services.md)   
+ [CREATE EXTERNAL LIBRARY &#40;Transact-SQLTransact-SQL&#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [sp_prepare &#40;&#41;Transact SQL](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
+ [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
+ [Opción de configuración del servidor external scripts enabled](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
+ [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
+ [SQL Server, objeto External Scripts](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
+ [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
