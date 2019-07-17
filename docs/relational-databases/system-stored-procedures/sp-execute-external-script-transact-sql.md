---
title: sp_execute_external_script (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions||=azuresqldb-mi-current'
ms.openlocfilehash: 7ce26cd3d4e42d6d94e32a3454318a0ee841c486
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124488"
---
# <a name="spexecuteexternalscript-transact-sql"></a>sp_execute_external_script (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

Ejecuta un script que se proporciona como un argumento de entrada al procedimiento. Secuencia de comandos se ejecuta en el [marco de extensibilidad](../../advanced-analytics/concepts/extensibility-framework.md). Secuencia de comandos debe escribirse en un lenguaje admitido y registrado, en un motor de base de datos que tenga al menos una extensión: [**R**](../../advanced-analytics/concepts/extension-r.md), [ **Python**](../../advanced-analytics/concepts/extension-python.md), o [ **Java** (en SQL Server 2019 solo en versión preliminar)](../../advanced-analytics/java/extension-java.md). 

Para ejecutar **sp_execute_external_script**, primero debe habilitar scripts externos mediante la instrucción, `sp_configure 'external scripts enabled', 1;`.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

> [!Note]
> Aprendizaje automático (R y Python) y las extensiones de programación se instala como un complemento de la instancia del motor de base de datos. Compatibilidad con extensiones específicas varían según la versión de SQL Server.

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
::: moniker range=">=sql-server-2016 <=sql-server-2017||=sqlallproducts-allversions"
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
 **@language** = N'*lenguaje*'  
 Indica el lenguaje de script. *lenguaje* es **sysname**.  Según la versión de SQL Server, los valores válidos son R (SQL Server 2016 y versiones posterior), (SQL Server 2017 y versiones posterior) de Python y Java (versión preliminar de SQL Server 2019). 
  
 **@script** = N'*script*' especificado como entrada de una literal o una variable de secuencia de comandos de lenguaje externo. *secuencia de comandos* es **nvarchar (max)** .  

`[ @input_data_1 =  N'input_data_1' ]` Especifica los datos de entrada usados por el script externo en forma de un [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta. Tipo de datos de *input_data_1* es **nvarchar (max)** .

`[ @input_data_1_name = N'input_data_1_name' ]` Especifica el nombre de la variable utilizada para representar la consulta definida por @input_data_1. El tipo de datos de la variable en el script externo depende del idioma. En el caso de R, la variable de entrada es una trama de datos. En el caso de Python, la entrada debe ser tabular. *input_data_1_name* es **sysname**.  Valor predeterminado es *InputDataSet*.  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
`[ @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]` Solo se aplica a SQL Server 2019 y se usa para generar modelos por partición. Especifica el nombre de la columna utilizada para ordenar el conjunto de resultados, por ejemplo por el nombre de producto. El tipo de datos de la variable en el script externo depende del idioma. En el caso de R, la variable de entrada es una trama de datos. En el caso de Python, la entrada debe ser tabular.

`[ @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]` Solo se aplica a SQL Server 2019 y se usa para generar modelos por partición. Especifica el nombre de la columna utilizada para segmentar los datos, como la fecha o la región geográfica. El tipo de datos de la variable en el script externo depende del idioma. En el caso de R, la variable de entrada es una trama de datos. En el caso de Python, la entrada debe ser tabular. 
::: moniker-end

`[ @output_data_1_name =  N'output_data_1_name' ]` Especifica el nombre de la variable en el script externo que contiene los datos que debe devolverse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tras la finalización de la llamada al procedimiento almacenado. El tipo de datos de la variable en el script externo depende del idioma. Para R, el resultado debe ser una trama de datos. Para Python, la salida debe ser una trama de datos de pandas. *output_data_1_name* es **sysname**.  Valor predeterminado es *OutputDataSet*.  

`[ @parallel = 0 | 1 ]` Habilitar la ejecución de scripts de R en paralelo estableciendo el `@parallel` parámetro en 1. El valor predeterminado para este parámetro es 0 (sin paralelismo). Si `@parallel = 1` y la salida se transmiten directamente en el equipo cliente, el `WITH RESULT SETS` cláusula es obligatoria y debe especificarse un esquema de salida.  

 + Para los scripts de R que no usan las funciones de RevoScaleR, con el `@parallel` parámetro puede ser beneficioso para el procesamiento de grandes conjuntos de datos, suponiendo que el script se puede paralelizar de forma trivial. Por ejemplo, cuando se usa el R `predict` función con un modelo para generar nuevas predicciones, establezca `@parallel = 1` como una sugerencia para el motor de consultas. Si se puede paralelizar la consulta, las filas se distribuyen según la **MAXDOP** configuración.  
  
 + Para los scripts de R que usan funciones de RevoScaleR, procesamiento en paralelo se controla automáticamente y no debe especificar `@parallel = 1` a la **sp_execute_external_script** llamar.  
  
`[ @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ]` Una lista de declaraciones de parámetro de entrada que se utilizan en el script externo.  
  
`[ @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]` Una lista de valores para los parámetros de entrada usados por el script externo.  

## <a name="remarks"></a>Comentarios

> [!IMPORTANT]
> El árbol de consulta se controla mediante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y usuarios no pueden realizar operaciones arbitrarias en la consulta. 

Use **sp_execute_external_script** para ejecutar scripts escritos en un lenguaje compatible. Actualmente, los lenguajes admitidos son R para SQL Server 2016 R Services y Python y R para Machine Learning Services de SQL Server 2017. 

De forma predeterminada, los conjuntos de resultados devueltos por este procedimiento almacenado son salida con columnas sin nombre. Nombres de columna de una secuencia de comandos son locales en el entorno de scripting y no se reflejan en el conjunto de resultados de salida. Para denominar columnas del conjunto de resultados, utilice el `WITH RESULT SET` cláusula de [ `EXECUTE` ](../../t-sql/language-elements/execute-transact-sql.md).
  
 Además de devolver un conjunto de resultados, puede devolver valores escalares a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante el uso de parámetros de salida. El ejemplo siguiente muestra el uso del parámetro de salida para devolver el modelo serializado de R que se usó como entrada para la secuencia de comandos:  
  
Puede controlar los recursos utilizados por los scripts externos mediante la configuración de un grupo de recursos externos. Para obtener más información, vea [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md). Puede obtenerse información sobre la carga de trabajo desde las vistas de catálogo del regulador de recursos y DMV de contadores. Para obtener más información, consulte [vistas de catálogo del regulador de recursos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md), [Resource Governor relacionados vistas de administración dinámica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)y [ SQL Server, objeto External Scripts](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md).  

### <a name="monitor-script-execution"></a>Supervisar la ejecución de secuencia de comandos

Ejecución de secuencia de comandos de monitor mediante [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) y [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="parameters-for-partition-modeling"></a>Parámetros para el modelado de partición

 En SQL Server 2019, actualmente en versión preliminar pública, puede establecer dos parámetros adicionales que permiten el modelo de datos con particiones, donde las particiones se basan en uno o más columnas que proporcione que naturalmente segmentación un conjunto de datos en particiones lógicas, crean y usa durante la ejecución del script. Las columnas que contienen valores que se repiten para edad, sexo, región geográfica, fecha u hora, son algunos ejemplos que se prestan a los conjuntos de datos con particiones.
 
 Los dos parámetros son **input_data_1_partition_by_columns** y **input_data_1_order_by_columns**, donde el segundo parámetro se utiliza para ordenar el conjunto de resultados. Los parámetros se pasan como entradas para `sp_execute_external_script` con el script externo ejecuta una vez para cada partición. Para obtener más información y ejemplos, vea [Tutorial: Crear modelos basados en la partición](https://docs.microsoft.com/sql/advanced-analytics/tutorials/r-tutorial-create-models-per-partition).

 Puede ejecutar la secuencia de comandos en paralelo mediante la especificación de `@parallel=1`. Si se puede paralelizar la consulta de entrada, debe establecer `@parallel=1` como parte de los argumentos de `sp_execute_external_script`. De forma predeterminada, el optimizador de consultas funciona bajo `@parallel=1` en las tablas que tienen más de 256 filas, pero si desea controlar esto de forma explícita, este script incluye el parámetro como una demostración.

 > [!Tip]
> Para entrenamiento workoads, puede usar `@parallel` con los scripts de entrenamiento arbitrario, incluso aquellas que usan algoritmos de rx que no sean de Microsoft. Normalmente, solo los algoritmos RevoScaleR (con el prefijo rx) ofrecen paralelismo en escenarios de formación en SQL Server. Pero con los nuevos parámetros de SQL Server vNext, puede paralelizar una secuencia de comandos que llama a funciones no específicamente diseñadas con esa capacidad.
::: moniker-end

### <a name="streaming-execution-for-r-and-python-scripts"></a>La ejecución de scripts de R y Python de transmisión por secuencias  

Streaming permite que el script de R o Python trabajar con más datos que pueden caber en memoria. Para controlar el número de filas que se pasan durante la transmisión por secuencias, especifique un valor entero para el parámetro, `@r_rowsPerRead` en el `@params` colección.  Por ejemplo, si está enseñando a un modelo que usa datos muy amplias, podría ajustar el valor para leer menos filas, para asegurarse de que todas las filas se pueden enviar en un solo fragmento de datos. También puede usar este parámetro para administrar el número de filas que se va a leer y procesar al mismo tiempo, para mitigar los problemas de rendimiento del servidor. 
  
Tanto el `@r_rowsPerRead` parámetro para el streaming y el `@parallel` argumento debe tenerse en cuenta las sugerencias. Para que la sugerencia se aplique, debe ser posible generar un plan de consulta SQL que incluye el procesamiento paralelo. Si esto no es posible, no se puede habilitar procesamiento en paralelo.  
  
> [!NOTE]  
>  Procesamiento paralelo y Streaming solo se admiten en Enterprise Edition. Puede incluir los parámetros en las consultas en Standard Edition sin provocar un error, pero los parámetros no tienen ningún efecto y scripts de R que se ejecutan en un único proceso.  
  
## <a name="restrictions"></a>Restricciones  


### <a name="data-types"></a>Tipos de datos

No se admiten los siguientes tipos de datos cuando se utiliza en la consulta de entrada o parámetros de **sp_execute_external_script** procedimiento y devolver un error de tipo no admitido.  

Como alternativa, **CAST** la columna o el valor a un tipo compatible en [!INCLUDE[tsql](../../includes/tsql-md.md)] antes de enviarlo a la secuencia de comandos externo.  
  
-   **cursor**  
  
-   **timestamp**  
  
-   **datetime2**, **datetimeoffset**, **time**  
  
-   **sql_variant**  
  
-   **text**, **image**  
  
-   **xml**  
  
-   **hierarchyid**, **geometría**, **geography**  
  
-   Tipos definidos por el usuario CLR

En general, cualquier conjunto de resultados que no puede asignarse a un [!INCLUDE[tsql](../../includes/tsql-md.md)] es de tipo de datos, la salida como NULL.  

### <a name="restrictions-specific-to-r"></a>Restricciones específicas de R

Si la entrada incluye **datetime** valores que no se ajustan el intervalo de valores permitido en R, los valores se convierten en **NA**. Esto es necesario porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite un mayor intervalo de valores que se admite en el lenguaje R.

Valores flotantes (por ejemplo, `+Inf`, `-Inf`, `NaN`) no se admiten en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , aunque ambos lenguajes utilizan IEEE 754. Comportamiento actual solo envía los valores para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] directamente; como resultado, el cliente SQL en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] produce un error. Por lo tanto, estos valores se convierten en **NULL**.

## <a name="permissions"></a>Permisos

Requiere **EXECUTE ANY EXTERNAL SCRIPT** permiso de base de datos.  

## <a name="examples"></a>Ejemplos

Esta sección contiene ejemplos de cómo se puede usar este procedimiento almacenado para ejecutar scripts de R o Python mediante [!INCLUDE[tsql](../../includes/tsql-md.md)].

### <a name="a-return-an-r-data-set-to-sql-server"></a>A. Devolver un conjunto de datos de R a SQL Server  

En el ejemplo siguiente se crea un procedimiento almacenado que utiliza **sp_execute_external_script** para devolver el conjunto de datos de Iris incluido en R a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

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

### <a name="b-generate-an-r-model-based-on-data-from-sql-server"></a>b. Generar un modelo de R basado en datos de SQL Server  

En el ejemplo siguiente se crea un procedimiento almacenado que utiliza **sp_execute_external_script** para generar un modelo iris y devolver el modelo a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

> [!NOTE]
>  En este ejemplo requiere la instalación de avance del paquete e1071. Para obtener más información, consulte [instalar más paquetes de R en SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md).

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

### <a name="c-create-a-python-model-and-generate-scores-from-it"></a>C. Crear un modelo de Python y generar puntuaciones a partir de él

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

Encabezados de columna utilizados en el código de Python no son la salida a SQL Server; por lo tanto, use la instrucción con resultados para especificar los nombres de columna y tipos de datos para SQL.

Para puntuar, también puede usar la función nativa [PREDICT](../../t-sql/queries/predict-transact-sql.md), que es normalmente más rápida porque evita llamar al runtime de Python o R.

## <a name="see-also"></a>Vea también

 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Bibliotecas de Python y tipos de datos](../../advanced-analytics/python/python-libraries-and-data-types.md)  
 [Bibliotecas de R y tipos de datos de R](../../advanced-analytics/r/r-libraries-and-data-types.md)  
 [SQL Server R Services](../../advanced-analytics/r/sql-server-r-services.md)   
 [Problemas conocidos de SQL Server Machine Learning Services](../../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)   
 [CREAR una biblioteca externa &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
 [sp_prepare &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Opción de configuración del servidor external scripts enabled](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [External Scripts (objeto de SQL Server)](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
