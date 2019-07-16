---
title: 'Conversiones: SQL Server Machine Learning Services tipos de datos de R para SQL'
description: Revise el tipo de datos implícitas y explícitas converstions entre R y SQL Server en soluciones de aprendizaje automático y ciencia de datos.
ms.prod: sql
ms.technology: machine-learning
ms.date: 12/10/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 93a0e15d8fdca31971cd16d187ae88a180fb481f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962531"
---
# <a name="data-type-mappings-between-r-and-sql-server"></a>Asignaciones de tipos de datos entre R y SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Para las soluciones de R que se ejecutan en la característica de integración de R en SQL Server Machine Learning Services, revise la lista de tipos de datos no admitidos y conversiones de tipos de datos que pueden realizarse de forma implícita cuando se pasan datos entre las bibliotecas de R y SQL Server.

## <a name="base-r-version"></a>Versión de la base de R

SQL Server 2016 R Services y SQL Server 2017 Machine Learning Services con R, se alinean con las versiones específicas de Microsoft R Open. Por ejemplo, la última versión de SQL Server 2017 Machine Learning Services se integra en Microsoft R Open 3.3.3.

Para ver la versión de R asociada a una determinada instancia de SQL Server, abra **RGui**. Para la instancia predeterminada, la ruta de acceso sería como sigue: `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64\`

La herramienta de carga base R y otras bibliotecas. Se proporciona información de versión de paquete en una notificación para cada paquete que se carga durante el inicio de sesión. 

## <a name="r-and-sql-data-types"></a>Tipos de datos SQL y R

Mientras que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite varios tipos de datos de las primeras, R tiene un número limitado de tipos de datos escalares (numérico, entero, complejo, lógico, carácter, fecha y hora y sin formato). Como resultado, siempre que use datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en scripts de R, datos pueden convertirse implícitamente a un tipo de datos compatible. Sin embargo, a menudo una conversión exacta no puede realizarse automáticamente y se devuelve un error, como "Tipo de datos SQL no controlado".

Esta sección enumeran las conversiones implícitas que se proporcionan y se enumeran los tipos de datos no admitido. Se proporciona orientación para asignar los tipos de datos entre R y SQL Server.

## <a name="implicit-data-type-conversions-between-r-and-sql-server"></a>Conversiones implícitas de tipos de datos entre R y SQL Server

En la tabla siguiente se muestran los cambios que se producen en los tipos de datos y los valores cuando los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se usan en un script de R y después se devuelven a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

|Tipo SQL|Clase de R|Tipo de conjunto de resultados|Comentarios|
|-|-|-|-|
|**bigint**|`numeric`|**float**||
|**binary(n)**<br /><br /> n <= 8000|`raw`|**varbinary(max)**|Solo se permite como parámetro de entrada y salida.|
|**bit**|`logical`|**bit**||
|**char(n)**<br /><br /> n <= 8000|`character`|**ntext**||
|**datetime**|`POSIXct`|**datetime**|Se representa como GMT.|
|**date**|`POSIXct`|**datetime**|Se representa como GMT.|
|**decimal(p,s)**|`numeric`|**float**||
|**float**|`numeric`|**float**||
|**int**|`integer`|**int**||
|**money**|`numeric`|**float**||
|**numeric(p,s)**|`numeric`|**float**||
|**real**|`numeric`|**float**||
|**smalldatetime**|`POSIXct`|**datetime**|Se representa como GMT.|
|**smallint**|`integer`|**int**||
|**smallmoney**|`numeric`|**float**||
|**tinyint**|`integer`|**int**||
|**uniqueidentifier**|`character`|**ntext**||
|**varbinary(n)**<br /><br /> n <= 8000|`raw`|**varbinary(max)**|Solo se permite como parámetro de entrada y salida.|
|**varbinary(max)**|`raw`|**varbinary(max)**|Solo se permite como parámetro de entrada y salida.|
|**varchar(n)**<br /><br /> n <= 8000|`character`|**ntext**||


## <a name="data-types-not-supported-by-r"></a>Tipos de datos no compatibles con R

De las categorías de tipos de datos compatibles con el [sistema de tipos de SQL Server](../../t-sql/data-types/data-types-transact-sql.md), es probable que los siguientes tipos planteen problemas al pasarlos a código de R:

+ Tipos de datos que aparecen en la **otros** sección del artículo de sistema de tipo SQL: **cursor**, **timestamp**, **hierarchyid**,  **uniqueidentifier**, **sql_variant**, **xml**, **tabla**
+ Todos los tipos espaciales
+ **image**

## <a name="data-types-that-might-convert-poorly"></a>Tipos de datos cuya conversión puede ser deficiente

+ La mayoría de los tipos de fecha y hora deberían funcionar, salvo **datetimeoffset** 
+ Se admite la mayoría de los tipos de datos numéricos, pero es posible que las conversiones de **money** y **smallmoney** no se realicen
+ Se admite **varchar**, pero dado que SQL Server usa Unicode por norma, se recomienda usar **nvarchar** y otros tipos de datos de texto Unicode siempre que sea posible.
+ Las funciones de la biblioteca RevoScaleR que usan el prefijo rx pueden tratar los tipos de datos binarios de SQL (**binary** y **varbinary**), pero en la mayoría de los escenarios se necesitará un tratamiento especial de estos tipos. La mayor parte del código de R no puede trabajar con columnas binarias.

  
 Para obtener más información sobre los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Data Types &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md) [Tipos de datos (Transact-SQL)].

## <a name="changes-in-data-types-between-sql-server-2016-and-earlier-versions"></a>Cambios en los tipos de datos entre SQL Server 2016 y versiones anteriores

Microsoft SQL Server 2016 y Microsoft Azure SQL Database incluyen mejoras en las conversiones de tipos de datos y en otras operaciones. La mayoría de estas mejoras ofrecen mayor precisión en lo que respecta al uso de tipos de datos de punto flotante, así como cambios menores en operaciones en tipos de datos **datetime** clásicos.

Estas mejoras están todas disponibles de manera predeterminada cuando se usa un nivel de compatibilidad de la base de datos de 130 o posterior. Pero si usa otro nivel de compatibilidad de la base de datos o se conecta a la base de datos con una versión anterior, puede que observe diferencias en la precisión de números u otros resultados. 

Para obtener más información, vea [Mejoras de SQL Server 2016 en el control de algunos tipos de datos y operaciones infrecuentes](https://support.microsoft.com/help/4010261/sql-server-2016-improvements-in-handling-some-data-types-and-uncommon-).
 

## <a name="verify-r-and-sql-data-schemas-in-advance"></a>Comprobar esquemas de datos de SQL y R de antemano 

En general, siempre que tenga alguna duda sobre cómo se usa en R un tipo o una estructura de datos en concreto, use la función  `str()` para obtener la estructura interna y el tipo del objeto de R. El resultado de la función se imprime en la consola de R y también está disponible en los resultados de la consulta, en la pestaña **Mensajes** de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. 

Al recuperar datos de una base de datos para su uso en código de R, siempre debe eliminar las columnas que no pueden usarse en R, así como las columnas que no son útiles para análisis, como GUID (uniqueidentifier), marcas de tiempo y otras columnas que se utiliza para la auditoría, o linaje información creada por los procesos ETL. 

Tenga en cuenta que la inclusión de columnas innecesarias puede reducir considerablemente el rendimiento del código de R, especialmente si se usan columnas de alta cardinalidad como factores. Por consiguiente, se recomienda usar vistas de información y procedimientos almacenados del sistema de SQL Server para obtener de antemano los tipos de datos de una tabla determinada y eliminar o convertir las columnas incompatibles. Para obtener más información, vea [Vistas de esquema de información del sistema (Transact-SQL)](../../relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)

Si R no admite un tipo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en concreto, pero hay que usar las columnas de datos en el script de R, se recomienda que use las funciones [CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md) para garantizar que las conversiones de los tipos de datos se realicen como se espera antes de usar los datos en el script de R.  

> [!WARNING]
> Si usa el **rxDataStep** para quitar columnas incompatibles al mover los datos, tenga en cuenta que los argumentos _varsToKeep_ y _varsToDrop_ no son compatibles con el tipo de origen de datos **RxSqlServerData**.


## <a name="examples"></a>Ejemplos

### <a name="example-1-implicit-conversion"></a>Ejemplo 1: Conversión implícita

En el ejemplo siguiente se muestra cómo se transforman los datos al hacer el recorrido de ida y vuelta entre SQL Server y R.

La consulta obtiene una serie de valores de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de tabla y utiliza el procedimiento almacenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para generar los valores con el tiempo de ejecución de R.

```sql
CREATE TABLE MyTable (    
 c1 int,    
 c2 varchar(10),    
 c3 uniqueidentifier    
);    
go    
INSERT MyTable VALUES(1, 'Hello', newid());    
INSERT MyTable VALUES(-11, 'world', newid());    
SELECT * FROM MyTable;    
  
EXECUTE sp_execute_external_script    
 @language = N'R'    
 , @script = N'    
inputDataSet["cR"] <- c(4, 2)    
str(inputDataSet)    
outputDataSet <- inputDataSet'    
 , @input_data_1 = N'SELECT c1, c2, c3 FROM MyTable'    
 , @input_data_1_name = N'inputDataSet'    
 , @output_data_1_name = N'outputDataSet'    
 WITH RESULT SETS((C1 int, C2 varchar(max), C3 varchar(max), C4 float));  
```

**Resultado**

||||||
|-|-|-|-|-|
||C1|C2|C3|C4|
|1|1|Hello|6e225611-4b58-4995-a0a5-554d19012ef1|4|
|1|-11|world|6732ea46-2d5d-430b-8ao1-86e7f3351c3e|2|

Observe el uso de la función `str` en R para obtener el esquema de los datos de salida. Esta función devuelve la siguiente información:

<code>'data.frame':2 obs. of  4 variables:</code>
<code> $ c1: int  1 -11</code>
<code> $ c2: Factor w/ 2 levels "Hello","world": 1 2</code>
<code> $ c3: Factor w/ 2 levels "6732EA46-2D5D-430B-8A01-86E7F3351C3E",..: 2 1</code>
<code> $ cR: num  4 2</code>

Aquí puede ver que las siguientes conversiones de tipos de datos se han realizado implícitamente como parte de esta consulta:

-   **Columna C1**. La columna se representa como **int** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `integer` en R y **int** en el conjunto de resultados de salida.  
  
     No se ha realizado ninguna conversión de tipo.  
  
-   **Columna C2**. La columna se representa como **varchar(10)** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `factor` en R y **varchar(max)** en la salida.  
  
     Observe los cambios que se han producido en la salida: todas las cadenas de R (tanto si son un factor como una cadena normal) se representarán como **varchar(max)** , independientemente de la longitud de las cadenas.  
  
-   **Columna C3**.  La columna se representa como **uniqueidentifier** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `character` en R y **varchar(max)** en la salida.
  
     Observe la conversión de tipo de datos que se ha producido. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite **uniqueidentifier** , pero R no. Por eso, los identificadores se representan como cadenas.
  
-   **Columna C4**. La columna contiene valores generados por el script de R que no están presentes en los datos originales.


## <a name="example-2-dynamic-column-selection-using-r"></a>Ejemplo 2: Selección de columnas dinámicas con R

En el ejemplo siguiente se muestra cómo puede usar código de R para buscar tipos de columnas no válidos. Luego se obtiene el esquema de una tabla especificada mediante vistas del sistema de SQL Server y se quitan las columnas que tengan un tipo no válido especificado.

```R
connStr <- "Server=.;Database=TestDB;Trusted_Connection=Yes"
data <- RxSqlServerData(connectionString = connStr, sqlQuery = "SELECT COLUMN_NAME FROM TestDB.INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME = N'testdata' AND DATA_TYPE <> 'image';")
columns <- rxImport(data)
columnList <- do.call(paste, c(as.list(columns$COLUMN_NAME), sep = ","))
sqlQuery <- paste("SELECT", columnList, "FROM testdata")
```

## <a name="see-also"></a>Vea también

