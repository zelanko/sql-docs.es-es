---
title: sp_execute_external_script (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 10/20/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_execute_external_script_TSQL
- sys.sp_execute_external_script
- sys.sp_execute_external_script_TSQL
- sp_execute_external_script
dev_langs: TSQL
helpviewer_keywords: sp_execute_external_script
ms.assetid: de4e1fcd-0e1a-4af3-97ee-d1becc7f04df
caps.latest.revision: "34"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: d437e6e8d86aa648d9c6ef11a8ca04297cafbaf3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="spexecuteexternalscript-transact-sql"></a>sp_execute_external_script (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Ejecuta la secuencia de comandos que se proporciona como argumento en una ubicación externa. El script debe escribirse en un lenguaje admitido y registrado. El árbol de consulta se controla mediante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los usuarios no pueden realizar operaciones arbitrarias en la consulta. Para ejecutar **sp_execute_external_script**, primero debe habilitar los scripts externos mediante el uso de la `sp_configure 'external scripts enabled', 1;` instrucción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sp_execute_external_script   
    @language = N'language,   
    @script = N'script'  
    [ , @input_data_1 = N'input_data_1' ]   
    [ , @input_data_1_name = N'input_data_1_name' ]   
    [ , @output_data_1_name = N'output_data_1_name' ]  
    [ , @parallel = 0 | 1 ]  
    [ , @params = N'@parameter_name data_type [ OUT | OUTPUT ] [ ,...n ]' ] 
    [ , @parameter1 = 'value1' [ OUT | OUTPUT ] [ ,...n ] ]
```  
  
## <a name="arguments"></a>Argumentos  
 @language= N'*lenguaje*'  
 Indica el lenguaje de script. *idioma* es **sysname**.  

 Los valores válidos son `Python` o `R`. 
  
 @script= N'*script*'  
 Secuencia de comandos de idiomas externos especificada como una entrada literal o una variable. *secuencia de comandos* es **nvarchar (max)**.  
  
 [ @input_data_1_name = N'*input_data_1_name*']  
 Especifica el nombre de la variable utilizada para representar la consulta definida por @input_data_1. El tipo de datos de la variable en el script externo depende del idioma. En el caso de R, la variable de entrada es una trama de datos. En el caso de Python, la entrada debe ser tabular. *input_data_1_name* es **sysname**.  
  
 Valor predeterminado es "InputDataSet".  
  
 [ @input_data_1 = N'*input_data_1*']  
 Especifica los datos de entrada utilizados por la secuencia de comandos externo en forma de un [!INCLUDE[tsql](../../includes/tsql-md.md)] consulta. *input_data_1* es **nvarchar (max)**.  
  
 [ @output_data_1_name = N'*output_data_1_name*']  
 Especifica el nombre de la variable en el script externo que contiene los datos que se devuelven a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tras la finalización de la llamada de procedimiento almacenado. El tipo de datos de la variable en el script externo depende del idioma. En el caso de R, el resultado debe ser una trama de datos. En el caso de Python, el resultado debe ser una trama de datos de pandas. *output_data_1_name* es **sysname**.  
  
 Valor predeterminado es "OutputDataSet".  
  
 [ @parallel = 0 | 1 ]  
 Habilitar la ejecución en paralelo de scripts de R estableciendo la `@parallel` parámetro en 1. El valor predeterminado para este parámetro es 0 (ningún paralelismo).  
  
 Para los scripts de R que no se usan funciones de RevoScaleR, mediante el `@parallel` parámetro puede ser beneficioso para el procesamiento de grandes conjuntos de datos, suponiendo que el script se puede paralelizar trivial. Por ejemplo, cuando se usa el objeto R `predict` función con un modelo para generar nuevas predicciones, establezca `@parallel = 1` como una sugerencia para el motor de consultas. Si la consulta se puede ejecutar en paralelo, las filas se distribuyen según la **MAXDOP** configuración.  
  
 Si `@parallel = 1` y el resultado es que se transmite directamente en el equipo cliente, la `WITH RESULTS SETS` cláusula es obligatoria y debe especificarse un esquema de salida.  
  
 Para los scripts de R que usan funciones de RevoScaleR, procesamiento en paralelo se controla automáticamente y no se debe especificar `@parallel = 1` a la **sp_execute_external_script** llamar.  
  
 [ @params = N' *@parameter_name data_type* [OUT | OUTPUT] [,.. .n]']  
 Una lista de declaraciones de parámetro de entrada que se utilizan en el script externo.  
  
 [ @parameter1 = '*value1*' [OUT | OUTPUT] [,.. .n]]  
 Una lista de valores para los parámetros de entrada utilizados por la secuencia de comandos externo.  


## <a name="remarks"></a>Comentarios  
 Use **sp_execute_external_script** para ejecutar scripts escritos en un lenguaje compatible, como R. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] consta de un componente de servidor instalado con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], y un conjunto de herramientas de estación de trabajo y bibliotecas de conectividad que conectan a los científicos de datos al entorno de alto rendimiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Instalar R Services (In-Database) durante la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el programa de instalación para habilitar la ejecución de scripts de R. Para obtener más información, consulte [configuración de SQL Server R Services &#40; en bases de datos &#41;](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).  
  
 Puede controlar los recursos utilizados por un script externo mediante la configuración de un grupo de recursos externos. Para obtener más información, vea [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md). Puede obtenerse información sobre la carga de trabajo de las vistas de catálogo del regulador de recursos, vistas de administración dinámica y contadores. Para obtener más información, vea [vistas de catálogo del regulador de recursos &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md), [Regulador de recursos relacionados con vistas de administración dinámica &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md), y [objeto las secuencias de comandos de SQL Server, externo](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md).  

Ejecución del script Monitor con [sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md) y [sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md). 

 De forma predeterminada, los conjuntos de resultados devueltos por este procedimiento almacenado son salida con columnas sin nombre. Nombres de columna utilizados dentro de una secuencia de comandos son locales en el entorno de scripting y no se reflejan en el conjunto de resultados de archivos. Para denominar columnas del conjunto de resultados, use la `WITH RESULTS SET` cláusula de [ `EXECUTE` ](../../t-sql/language-elements/execute-transact-sql.md).
  
 Además de devolver un conjunto de resultados, puede devolver valores escalares desde un script de R a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante parámetros de salida. En el ejemplo siguiente se muestra el uso de parámetros de salida:  
  
```  
DECLARE @model varbinary(max);  
EXEC sp_execute_external_script  
        @language = N'R'  
        , @script = N'  
    # build classification model to predict tipped or not  
    logitObj <- glm(tipped ~ passenger_count + trip_distance + trip_time_in_secs + direct_distance, data = featureDataSource, family = binomial(link=logit));  
  
    # First, serialize a model and put it into a database table  
    modelbin <- serialize(logitObj, NULL);  
    '  
        , @input_data_1 = N'  
SELECT tipped, passenger_count, trip_time_in_secs, trip_distance, d.direct_distance  
  FROM dbo.nyctaxi_sample TABLESAMPLE (1 PERCENT) REPEATABLE (98074)  
  CROSS APPLY [CalculateDistance](pickup_latitude, pickup_longitude,  dropoff_latitude, dropoff_longitude) as d  
'  
        , @input_data_1_name = N'featureDataSource'  
        , @params = N'@modelbin varbinary(max) OUTPUT'  
        , @modelbin = @model OUTPUT;  
```  


## <a name="streaming-execution-for-r-script"></a>Ejecución de script de R de transmisión por secuencias  
 Ejecución de scripts de R de transmisión por secuencias se admite mediante la especificación de `@r_rowsPerRead int parameter` en `@params` colección.  Transmisión por secuencias permite a los scripts de R trabajar con datos que no caben en la memoria. Por ejemplo, si hay miles de millones de filas para puntuar usando predict, función nuevo `@r_rowsPerRead` parámetro puede usarse para dividir la ejecución en un flujo a la vez. Dado que este parámetro controla el número de filas que se envían a los procesos de R, también se puede utilizar para limitar al número de filas que se va a leer al mismo tiempo. Esto podría ser útil para mitigar los problemas de rendimiento de servidor si, por ejemplo, un modelo grande se esté entrenando. Tenga en cuenta que este parámetro solo puede usarse en casos donde la salida de la secuencia de comandos de R no depende de lectura o buscar en todo el conjunto de filas.  
  
 Tanto el `@r_rowsPerRead` parámetro para la transmisión por secuencias y `@parallel` argumento debe tenerse en cuenta las sugerencias. Para que la sugerencia que se aplicará, debe ser posible generar un plan de consulta SQL que incluye el procesamiento paralelo. Si esto no es posible, no se puede habilitar el procesamiento en paralelo.  
  
> [!NOTE]  
>  Transmisión por secuencias y procesamiento en paralelo solo se admiten en Enterprise Edition. Puede incluir los parámetros en las consultas en Standard Edition sin que se produzca un error, pero los parámetros no tienen ningún efecto y scripts de R que se ejecutan en un único proceso.  
  
## <a name="restrictions"></a>Restricciones  
 **Tipos de datos:** no se admiten los siguientes tipos de datos cuando se utiliza en la consulta de entrada o los parámetros de `sp_execute_external_script` procedimiento y devolver un error de tipo no admitido.  
  
 Como alternativa, **conversión** la columna o el valor a un tipo compatible en [!INCLUDE[tsql](../../includes/tsql-md.md)] y envíelo a R.  
  
-   **cursor**  
  
-   **timestamp**  
  
-   **datetime2**, **datetimeoffset**, **tiempo**  
  
-   **sql_variant**  
  
-   **texto**, **imagen**  
  
-   **xml**  
  
-   **hierarchyid**, **geometry**, **geography**  
  
-   Tipos definidos por el usuario CLR  
  
 **fecha y hora** valores en la entrada se convierten en NA en el lado de R para los valores que no caben en R. Esto es necesario porque el intervalo válido de valores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite un mayor intervalo de valores que se admite en el lenguaje R.  
  
 Valores flotantes (por ejemplo, + Inf, -Inf, NaN) no se admiten en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aunque ambos lenguajes utilizan conforme a IEEE 754. Comportamiento actual solo envía los valores para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] directamente y como un resultado sqlclient en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] produce error. Estos valores se convierten en **NULL**.  
  
 Cualquier conjunto de resultados de R que no puede asignarse a un [!INCLUDE[tsql](../../includes/tsql-md.md)] es de tipo de datos, se muestran como NULL.  
  
## <a name="permissions"></a>Permissions  
 Requiere **EXECUTE ANY EXTERNAL SCRIPT** permiso de base de datos.  
  
## <a name="examples"></a>Ejemplos  
 Esta sección contiene ejemplos de cómo se puede usar este procedimiento almacenado para ejecutar scripts de R con [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
### <a name="a-return-a-data-set-from-r-to-sql-server"></a>A. Devolver un conjunto de datos de R para SQL Server  
 En el ejemplo siguiente se crea un procedimiento almacenado que utiliza **sp_execute_external_script** para devolver un conjunto de datos de iris de R a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
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
go  
```  
  
### <a name="b-generate-a-model-based-on-data-from-sql-server"></a>B. Generar un modelo basado en datos de SQL Server  
 En el ejemplo siguiente se crea un procedimiento almacenado que utiliza **sp_execute_external_script** para generar un modelo de iris y devolver el modelo a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Este ejemplo requiere que se instale el paquete e1071. Para obtener más información, consulte [instalar paquetes de R adicionales en SQL Server](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md).  
  
```  
DROP PROC IF EXISTS generate_iris_model;  
go  
  
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
go  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Tipos de datos y las bibliotecas de Python](../../advanced-analytics/python/python-libraries-and-data-types.md)  
 [Bibliotecas de R y tipos de datos de R](../../advanced-analytics/r/r-libraries-and-data-types.md)  
 [SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services.md)   
 [Problemas conocidos de SQL Server R Services](../../advanced-analytics/r-services/known-issues-for-sql-server-r-services.md)   
 [Crear biblioteca externa &#40; Transact-SQL &#41;](../../t-sql/statements/create-external-library-transact-sql.md)  
 [sp_prepare &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-prepare-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Opción de configuración de servidor scripts externos habilitados](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md)   
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)   
 [External Scripts (objeto de SQL Server)](../../relational-databases/performance-monitor/sql-server-external-scripts-object.md)  
[sys.dm_external_script_requests](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-requests.md)  
[sys.dm_external_script_execution_stats](../../relational-databases/system-dynamic-management-views/sys-dm-external-script-execution-stats.md) 
  
