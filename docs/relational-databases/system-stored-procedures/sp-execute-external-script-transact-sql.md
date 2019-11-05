---
title: sp_execute_external_script (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: ab3bf4f98abaf5f164a3b38f4e09b10acf28b2f4
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/04/2019
ms.locfileid: "73532833"
---
# <a name="sp_execute_external_script-transact-sql"></a>sp_execute_external_script (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
El procedimiento almacenado **sp_execute_external_script** ejecuta un script proporcionado como argumento de entrada para el procedimiento y se usa con [las extensiones](../../language-extensions/language-extensions-overview.md)de [Machine Learning Services](../../advanced-analytics/index.yml) y de lenguaje. 

Por Machine Learning Services, [Python](../../advanced-analytics/concepts/extension-python.md) y [R](../../advanced-analytics/concepts/extension-r.md) son lenguajes admitidos. En el caso de las extensiones de lenguaje, se admite Java pero debe definirse con [Create external Language](../../t-sql/statements/create-external-language-transact-sql.md).

Para ejecutar **sp_execute_external_script**, primero debe instalar Machine Learning Services o extensiones de lenguaje. Para obtener más información, consulte [instalación de SQL Server Machine Learning Services (Python y R) en Windows](../../advanced-analytics/install/sql-machine-learning-services-windows-install.md) y [Linux](../../linux/sql-server-linux-setup-machine-learning.md), o [instalación de extensiones de lenguaje de SQL Server en Windows](../../language-extensions/install/install-sql-server-language-extensions-on-windows.md) y [Linux](../../linux/sql-server-linux-setup-language-extensions.md).
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
El procedimiento almacenado **sp_execute_external_script** ejecuta un script proporcionado como argumento de entrada para el procedimiento y se utiliza con [Machine Learning Services](../../advanced-analytics/index.yml) en SQL Server 2017. 

Por Machine Learning Services, [Python](../../advanced-analytics/concepts/extension-python.md) y [R](../../advanced-analytics/concepts/extension-r.md) son lenguajes admitidos. 

Para ejecutar **sp_execute_external_script**, primero debe instalar Machine Learning Services. Para obtener más información, consulte [instalación de SQL Server Machine Learning Services (Python y R) en Windows](../../advanced-analytics/install/sql-machine-learning-services-windows-install.md).
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
El procedimiento almacenado **sp_execute_external_script** ejecuta un script proporcionado como argumento de entrada para el procedimiento y se usa con [R Services](../../advanced-analytics/r/sql-server-r-services.md) en SQL Server 2016.

Para R Services, [r](../../advanced-analytics/concepts/extension-r.md) es el idioma admitido.

Para ejecutar **sp_execute_external_script**, primero debe instalar R Services. Para obtener más información, consulte [instalación de SQL Server Machine Learning Services (Python y R) en Windows](../../advanced-analytics/install/sql-r-services-windows-install.md).
::: moniker-end

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo a temas") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

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
## <a name="syntax-for-2017-and-earlier"></a>Sintaxis de 2017 y versiones anteriores

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
 **\@Language** = N '*Language*'  
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
 Indica el lenguaje del script. *Language* es de **tipo sysname**. Los valores válidos son **R**, **Python**y cualquier lenguaje definido con [Create external Language](../../t-sql/statements/create-external-language-transact-sql.md) (por ejemplo, Java).
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
 Indica el lenguaje del script. *Language* es de **tipo sysname**. En SQL Server 2017, los valores válidos son **R** y **Python**.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
 Indica el lenguaje del script. *Language* es de **tipo sysname**. En SQL Server 2016, el único valor válido es **R**.
::: moniker-end

 **\@script** = N script de lenguaje externo de '*script*' especificado como una entrada literal o de variable. el *script* es de tipo **nvarchar (Max)** .  

`[ @input_data_1 =  N'input_data_1' ]` especifica los datos de entrada utilizados por el script externo en forma de una consulta [!INCLUDE[tsql](../../includes/tsql-md.md)]. El tipo de datos de *input_data_1* es **nvarchar (Max)** .

`[ @input_data_1_name = N'input_data_1_name' ]` especifica el nombre de la variable utilizada para representar la consulta definida por @input_data_1. El tipo de datos de la variable en el script externo depende del lenguaje. En el caso de R, la variable de entrada es una trama de datos. En el caso de Python, la entrada debe ser tabular. *input_data_1_name* es de **tipo sysname**.  El valor predeterminado es *InputDataSet*.  

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
`[ @input_data_1_order_by_columns = N'input_data_1_order_by_columns' ]` usa para compilar modelos por partición. Especifica el nombre de la columna utilizada para ordenar el conjunto de resultados, por ejemplo por nombre de producto. El tipo de datos de la variable en el script externo depende del lenguaje. En el caso de R, la variable de entrada es una trama de datos. En el caso de Python, la entrada debe ser tabular.

`[ @input_data_1_partition_by_columns = N'input_data_1_partition_by_columns' ]` usa para compilar modelos por partición. Especifica el nombre de la columna utilizada para segmentar los datos, como la región geográfica o la fecha. El tipo de datos de la variable en el script externo depende del lenguaje. En el caso de R, la variable de entrada es una trama de datos. En el caso de Python, la entrada debe ser tabular. 
::: moniker-end

`[ @output_data_1_name =  N'output_data_1_name' ]` especifica el nombre de la variable en el script externo que contiene los datos que se van a devolver a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tras la finalización de la llamada al procedimiento almacenado. El tipo de datos de la variable en el script externo depende del lenguaje. Para R, la salida debe ser una trama de datos. En el caso de Python, la salida debe ser una trama de datos pandas. *output_data_1_name* es de **tipo sysname**.  El valor predeterminado es *OutputDataSet*.  

`[ @parallel = 0 | 1 ]` habilita la ejecución en paralelo de scripts de R estableciendo el parámetro de `@parallel` en 1. El valor predeterminado para este parámetro es 0 (sin paralelismo). Si `@parallel = 1` y la salida se transmite directamente al equipo cliente, se requiere la cláusula `WITH RESULT SETS` y se debe especificar un esquema de salida.  

 + En el caso de los scripts de R que no usan funciones de RevoScaleR, el uso del parámetro `@parallel` puede ser beneficioso para el procesamiento de grandes conjuntos de archivos, suponiendo que el script se puede paralelizar de forma trivial. Por ejemplo, al usar la función R `predict` con un modelo para generar nuevas predicciones, establezca `@parallel = 1` como una sugerencia para el motor de consultas. Si la consulta se puede ejecutar en paralelo, las filas se distribuyen según el valor de **MAXDOP** .  
  
 + En el caso de los scripts de R que usan funciones de RevoScaleR, el procesamiento en paralelo se administra automáticamente y no se debe especificar `@parallel = 1` a la llamada a **sp_execute_external_script** .  
  
`[ @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ]` lista de declaraciones de parámetros de entrada que se usan en el script externo.  
  
`[ @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]` lista de valores para los parámetros de entrada utilizados por el script externo.  

## <a name="remarks"></a>Comentarios

> [!IMPORTANT]
> El árbol de consultas se controla mediante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los usuarios no pueden realizar operaciones arbitrarias en la consulta. 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
Use **sp_execute_external_script** para ejecutar scripts escritos en un lenguaje compatible. Los idiomas admitidos son **Python** y **R** usados con Machine Learning Services y cualquier lenguaje definido con [Create external Language](../../t-sql/statements/create-external-language-transact-sql.md) (por ejemplo, Java) usado con extensiones de lenguaje.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Use **sp_execute_external_script** para ejecutar scripts escritos en un lenguaje compatible. Los idiomas admitidos son **Python** y **R** en SQL Server 2017 Machine Learning Services.
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
Use **sp_execute_external_script** para ejecutar scripts escritos en un lenguaje compatible. El único idioma admitido es **R** en SQL Server 2016 r Services.
::: moniker-end

De forma predeterminada, los conjuntos de resultados devueltos por este procedimiento almacenado se generan con columnas sin nombre. Los nombres de columna que se usan en un script son locales para el entorno de scripting y no se reflejan en el conjunto de resultados de salida. Para asignar un nombre a las columnas del conjunto de resultados, use la cláusula `WITH RESULT SET` de [`EXECUTE`](../../t-sql/language-elements/execute-transact-sql.md).

Además de devolver un conjunto de resultados, puede devolver valores escalares a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante parámetros de salida. 
  
Puede controlar los recursos utilizados por los scripts externos mediante la configuración de un grupo de recursos externos. Para obtener más información, vea [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md). La información sobre la carga de trabajo se puede obtener a partir de las vistas de catálogo del regulador de recursos, las DMV y los contadores. Para obtener más información, vea [Resource Governor Catalog &#40;views de&#41;Transact-SQL](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md), [Resource Governor vistas &#40;de administración dinámica&#41;relacionadas de Transact-SQL](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)y [SQL Server, y el objeto de scripts externos](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md).  

### <a name="monitor-script-execution"></a>Supervisión de la ejecución del script

Supervise la ejecución de scripts mediante [Sys. DM _ _external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) y [Sys. DM _ _external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). 

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
### <a name="parameters-for-partition-modeling"></a>Parámetros para el modelado de particiones

Puede establecer dos parámetros adicionales que permitan el modelado de datos con particiones, donde las particiones se basan en una o varias columnas que se proporcionan para segmentar lógicamente un conjunto de datos en particiones lógicas creadas y usadas únicamente durante la ejecución del script. Las columnas que contienen valores de repetición de edad, sexo, región geográfica, fecha u hora, son algunos ejemplos que se prestan a conjuntos de datos con particiones.
 
Los dos parámetros son **input_data_1_partition_by_columns** y **input_data_1_order_by_columns**, donde el segundo parámetro se utiliza para ordenar el conjunto de resultados. Los parámetros se pasan como entradas a `sp_execute_external_script` con el script externo que se ejecuta una vez para cada partición. Para obtener más información y ejemplos, vea [Tutorial: crear modelos basados en particiones](https://docs.microsoft.com/sql/advanced-analytics/tutorials/r-tutorial-create-models-per-partition).

Puede ejecutar un script en paralelo especificando `@parallel=1`. Si la consulta de entrada puede ejecutarse en paralelo, debe establecer `@parallel=1` como parte de los argumentos en `sp_execute_external_script`. De forma predeterminada, el optimizador de consultas funciona en `@parallel=1` en tablas que tienen más de 256 filas, pero si desea controlar esto explícitamente, este script incluye el parámetro como una demostración.

> [!Tip]
> Para entrenar workoads, puede usar `@parallel` con cualquier script de aprendizaje arbitrario, incluso aquellos que usan algoritmos que no son de Microsoft. Normalmente, solo los algoritmos RevoScaleR (con el prefijo RX) ofrecen paralelismo en los escenarios de aprendizaje de SQL Server. Sin embargo, con los nuevos parámetros de SQL Server vNext, puede paralelizar un script que llama a funciones que no se han diseñado específicamente con esa capacidad.
::: moniker-end

### <a name="streaming-execution-for-python-and-r-scripts"></a>Ejecución de streaming para Python y scripts de R  

Streaming permite que el script de Python o R funcione con más datos de los que caben en la memoria. Para controlar el número de filas que se pasan durante la transmisión por secuencias, especifique un valor entero para el parámetro `@r_rowsPerRead` en la colección `@params`.  Por ejemplo, si va a entrenar un modelo que utiliza datos muy anchos, puede ajustar el valor para que se lean menos filas, para asegurarse de que todas las filas se pueden enviar en un fragmento de datos. También puede usar este parámetro para administrar el número de filas que se leen y procesan al mismo tiempo, a fin de mitigar los problemas de rendimiento del servidor. 
  
El parámetro `@r_rowsPerRead` para el streaming y el argumento `@parallel` deben considerarse sugerencias. Para que se aplique la sugerencia, debe ser posible generar un plan de consulta SQL que incluya el procesamiento en paralelo. Si esto no es posible, no se puede habilitar el procesamiento en paralelo.  
  
> [!NOTE]  
> La transmisión por secuencias y el procesamiento paralelo solo se admiten en la edición Enterprise. Puede incluir los parámetros en las consultas en Standard Edition sin producir un error, pero los parámetros no tienen ningún efecto y los scripts de R se ejecutan en un único proceso.  
  
## <a name="restrictions"></a>Restricciones  

### <a name="data-types"></a>Tipos de datos

Los siguientes tipos de datos no se admiten cuando se usan en la consulta de entrada o los parámetros del procedimiento **sp_execute_external_script** y devuelven un error de tipo no compatible.  

Como alternativa, **convierta** la columna o el valor a un tipo compatible en [!INCLUDE[tsql](../../includes/tsql-md.md)] antes de enviarlo al script externo.  
  
-   **cursor**  
  
-   **timestamp**  
  
-   **datetime2**, **DateTimeOffset**, **Time**  
  
-   **sql_variant**  
  
-   **texto**, **imagen**  
  
-   **xml**  
  
-   **hierarchyid**, **Geometry**, **Geography**  
  
-   Tipos definidos por el usuario CLR

En general, los conjuntos de resultados que no se pueden asignar a un tipo de datos [!INCLUDE[tsql](../../includes/tsql-md.md)], se generan como NULL.  

### <a name="restrictions-specific-to-r"></a>Restricciones específicas de R

Si la entrada incluye valores de **fecha y hora** que no se ajustan al intervalo de valores permitido en R, los valores se convierten en **na**. Esto es necesario porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite un intervalo mayor de valores que se admite en el lenguaje R.

Los valores Float (por ejemplo, `+Inf`, `-Inf`, `NaN`) no se admiten en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], aunque ambos idiomas utilicen IEEE 754. El comportamiento actual solo envía los valores a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] directamente; como resultado, el cliente SQL de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] produce un error. Por lo tanto, estos valores se convierten en **null**.

## <a name="permissions"></a>Permisos

Requiere el permiso ejecutar cualquier base de datos de **script externa** .  

## <a name="examples"></a>Ejemplos

Esta sección contiene ejemplos de cómo se puede usar este procedimiento almacenado para ejecutar scripts de R o Python mediante [!INCLUDE[tsql](../../includes/tsql-md.md)].

### <a name="a-return-an-r-data-set-to-sql-server"></a>A. Devuelve un conjunto de datos de R a SQL Server  

En el ejemplo siguiente se crea un procedimiento almacenado que usa **sp_execute_external_script** para devolver el conjunto de resultados de iris incluido con R a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

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

En el ejemplo siguiente se crea un procedimiento almacenado que utiliza **sp_execute_external_script** para generar un modelo de iris y devolver el modelo a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

> [!NOTE]
>  Este ejemplo requiere la instalación anticipada del paquete e1071. Para obtener más información, consulte [instalación de paquetes de R adicionales en SQL Server](../../advanced-analytics/r/install-additional-r-packages-on-sql-server.md).

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

### <a name="c-create-a-python-model-and-generate-scores-from-it"></a>C. Creación de un modelo de Python y generación de puntuaciones a partir de él

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

Los encabezados de columna que se usan en el código de Python no se muestran en SQL Server; por lo tanto, use la instrucción WITH RESULT para especificar los nombres de columna y los tipos de datos que SQL va a utilizar.

Para puntuar, también puede usar la función nativa [PREDICT](../../t-sql/queries/predict-transact-sql.md), que es normalmente más rápida porque evita llamar al runtime de Python o R.

## <a name="see-also"></a>Vea también

+ [Servicios de aprendizaje de máquina SQL Server](../../advanced-analytics/index.yml)
+ [Extensiones de lenguaje de SQL Server](../../language-extensions/language-extensions-overview.md). 
+ [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
+ [Tipos de datos y bibliotecas de Python](../../advanced-analytics/python/python-libraries-and-data-types.md)  
+ [Bibliotecas de r y tipos de datos de R](../../advanced-analytics/r/r-libraries-and-data-types.md)  
+ [SQL Server R Services](../../advanced-analytics/r/sql-server-r-services.md)   
+ [Problemas conocidos de SQL Server Machine Learning Services](../../advanced-analytics/known-issues-for-sql-server-machine-learning-services.md)   
+ [CREAR una biblioteca &#40;externa TRANSACT-SQL&#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
+ [Transact &#40;-SQL de sp_prepare&#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
+ [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
+ [Opción de configuración de servidor Scripts externos habilitados](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
+ [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
+ [External Scripts (objeto de SQL Server)](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
+ [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
+ [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
