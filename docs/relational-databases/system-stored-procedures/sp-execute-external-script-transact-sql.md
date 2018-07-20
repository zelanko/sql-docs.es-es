---
title: sp_execute_external_script (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2018
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: f106a4ed11658856412e3e874f1f57af87e22211
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086177"
---
# <a name="spexecuteexternalscript-transact-sql"></a>sp_execute_external_script (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Ejecuta la secuencia de comandos proporcionada como argumento en una ubicación externa. El script debe escribirse en un lenguaje admitido y registrado (R o Python). Para ejecutar **sp_execute_external_script**, primero debe habilitar scripts externos mediante la instrucción, `sp_configure 'external scripts enabled', 1;`.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis

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

## <a name="arguments"></a>Argumentos
 \@Language = N'*lenguaje*'  
 Indica el lenguaje de script. *lenguaje* es **sysname**.  

 Los valores válidos son `Python` o `R`. 
  
 \@secuencia de comandos = N'*script*'  
 Script de lenguaje externo especificado como entrada de una literal o una variable. *secuencia de comandos* es **nvarchar (max)**.  
  
 [ \@input_data_1_name = N'*input_data_1_name*']  
 Especifica el nombre de la variable utilizada para representar la consulta definida por \@input_data_1. El tipo de datos de la variable en el script externo depende del idioma. En el caso de R, la variable de entrada es una trama de datos. En el caso de Python, la entrada debe ser tabular. *input_data_1_name* es **sysname**.  
  
 Valor predeterminado es `InputDataSet`.  
  
 [ \@input_data_1 = N'*input_data_1*']  
 Especifica los datos de entrada usados por el script externo en forma de un [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta. Tipo de datos de *input_data_1* es **nvarchar (max)**.
  
 [ \@output_data_1_name = N'*output_data_1_name*']  
 Especifica el nombre de la variable en el script externo que contiene los datos que debe devolverse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tras la finalización de la llamada al procedimiento almacenado. El tipo de datos de la variable en el script externo depende del idioma. Para R, el resultado debe ser una trama de datos. Para Python, la salida debe ser una trama de datos de pandas. *output_data_1_name* es **sysname**.  
  
 Valor predeterminado es "OutputDataSet".  
  
 [ \@paralelo = 0 | 1]

 Habilitar la ejecución de scripts de R en paralelo estableciendo el `@parallel` parámetro en 1. El valor predeterminado para este parámetro es 0 (sin paralelismo).  
  
 Para los scripts de R que no usan las funciones de RevoScaleR, con el `@parallel` parámetro puede ser beneficioso para el procesamiento de grandes conjuntos de datos, suponiendo que el script se puede paralelizar de forma trivial. Por ejemplo, cuando se usa el R `predict` función con un modelo para generar nuevas predicciones, establezca `@parallel = 1` como una sugerencia para el motor de consultas. Si se puede paralelizar la consulta, las filas se distribuyen según la **MAXDOP** configuración.  
  
 Si `@parallel = 1` y la salida se transmiten directamente en el equipo cliente, el `WITH RESULTS SETS` cláusula es obligatoria y debe especificarse un esquema de salida.  
  
 Para los scripts de R que usan funciones de RevoScaleR, procesamiento en paralelo se controla automáticamente y no debe especificar `@parallel = 1` a la **sp_execute_external_script** llamar.  
  
 [ \@params = N'*\@parameter_name data_type* [horizontal | SALIDA] [,.. .n] "]  
 Una lista de declaraciones de parámetro de entrada que se utilizan en el script externo.  
  
 [ \@parameter1 = '*value1*' [horizontal | SALIDA] [,.. .n]]  

 Una lista de valores para los parámetros de entrada usados por el script externo.  

## <a name="remarks"></a>Notas

Use **sp_execute_external_script** para ejecutar scripts escritos en un lenguaje compatible. Actualmente, los lenguajes admitidos son R para SQL Server 2016 y Python y R para SQL Server 2017. 

> [!IMPORTANT]
> El árbol de consulta se controla mediante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y usuarios no pueden realizar operaciones arbitrarias en la consulta. 

De forma predeterminada, los conjuntos de resultados devueltos por este procedimiento almacenado son salida con columnas sin nombre. Nombres de columna de una secuencia de comandos son locales en el entorno de scripting y no se reflejan en el conjunto de resultados de salida. Para denominar columnas del conjunto de resultados, utilice el `WITH RESULTS SET` cláusula de [ `EXECUTE` ](../../t-sql/language-elements/execute-transact-sql.md).
  
 Además de devolver un conjunto de resultados, puede devolver valores escalares a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante el uso de parámetros de salida. El ejemplo siguiente muestra el uso del parámetro de salida para devolver el modelo serializado de R que se usó como entrada para la secuencia de comandos:  

En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] está formado por un componente de servidor instalado con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y un conjunto de herramientas de estación de trabajo y bibliotecas de conectividad que conectan a los científicos de datos en el entorno de alto rendimiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Debe instalar los componentes durante de aprendizaje automático [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el programa de instalación para habilitar la ejecución de scripts externos. Para obtener más información, consulte [configurar SQL Server Machine Learning Services](../../advanced-analytics/r/set-up-sql-server-r-services-in-database.md).  
  
Puede controlar los recursos utilizados por los scripts externos mediante la configuración de un grupo de recursos externos. Para obtener más información, vea [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md). Puede obtenerse información sobre la carga de trabajo desde las vistas de catálogo del regulador de recursos y DMV de contadores. Para obtener más información, consulte [vistas de catálogo del regulador de recursos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md), [Resource Governor relacionados vistas de administración dinámica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)y [ SQL Server, objeto External Scripts](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md).  

Ejecución de secuencia de comandos de monitor mediante [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) y [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). 

## <a name="streaming-execution-for-r-and-python-scripts"></a>La ejecución de scripts de R y Python de transmisión por secuencias  

Streaming permite que el script de R o Python trabajar con más datos que pueden caber en memoria. Para controlar el número de filas que se pasan durante la transmisión por secuencias, especifique un valor entero para el parámetro, `@r_rowsPerRead` en el `@params` colección.  Por ejemplo, si está enseñando a un modelo que usa datos muy amplias, podría ajustar el valor para leer menos filas, para asegurarse de que todas las filas se pueden enviar en un solo fragmento de datos. También puede usar este parámetro para administrar el número de filas que se va a leer y procesar al mismo tiempo, para mitigar los problemas de rendimiento del servidor. 
  
Tanto el `@r_rowsPerRead` parámetro para el streaming y el `@parallel` argumento debe tenerse en cuenta las sugerencias. Para que la sugerencia se aplique, debe ser posible generar un plan de consulta SQL que incluye el procesamiento paralelo. Si esto no es posible, no se puede habilitar procesamiento en paralelo.  
  
> [!NOTE]  
>  Procesamiento paralelo y Streaming solo se admiten en Enterprise Edition. Puede incluir los parámetros en las consultas en Standard Edition sin provocar un error, pero los parámetros no tienen ningún efecto y scripts de R que se ejecutan en un único proceso.  
  
## <a name="restrictions"></a>Restrictions  


### <a name="data-types"></a>Tipos de datos

No se admiten los siguientes tipos de datos cuando se utiliza en la consulta de entrada o parámetros de **sp_execute_external_script** procedimiento y devolver un error de tipo no admitido.  

Como alternativa, **CAST** la columna o el valor a un tipo compatible en [!INCLUDE[tsql](../../includes/tsql-md.md)] antes de enviarlo a la secuencia de comandos externo.  
  
-   **cursor**  
  
-   **timestamp**  
  
-   **datetime2**, **datetimeoffset**, **tiempo**  
  
-   **sql_variant**  
  
-   **texto**, **imagen**  
  
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

### <a name="b-generate-an-r-model-based-on-data-from-sql-server"></a>B. Generar un modelo de R basado en datos de SQL Server  

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

Los encabezados de columna usados en el código Python no se envían como resultados a SQL Server, así que use la instrucción WITH RESULTS para especificar los nombres de columna y los tipos de datos para SQL.

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
