---
title: "Uso de c&#243;digo de R en Transact-SQL (SQL Server R Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 4e6fe30d-a105-4d5b-bc05-5e5204753847
caps.latest.revision: 36
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 28
---
# Uso de c&#243;digo de R en Transact-SQL (SQL Server R Services)
En este tutorial se proporcionan ejemplos muy breves de la sintaxis para trabajar con R en SQL Server R Services.    
    
    
Es un buen punto de partida si no está familiarizado con SQL Server R Services y quiere conocer los conceptos básicos de cómo definir un script de R en un procedimiento almacenado de T-SQL, el uso de datos como entrada y cómo definir las salidas.    
    
**Requisitos previos:** para ejecutar el código de R en SQL Server R Services, debe estar conectado a una instancia de SQL Server donde R ya esté instalado.     
    
## Parte 1: operaciones básicas  

En las secciones siguientes, aprenderá cómo extender el procedimiento almacenado mediante la adición de parámetros y cómo configurar las entradas y salidas.   
  
### 1.1. Comprobar si funciona R en SQL Server  

Esta consulta usa el procedimiento almacenado del sistema [sp_execute_external_script](https://msdn.microsoft.com/library/mt604368.aspx), que es la forma de llamar a R en el contexto de SQL Server. Este ejemplo pasa una consulta SQL como entrada para R y R devuelve esa trama de datos a SQL Server.     
    
1. En el menú Inicio de Windows, busque Microsoft SQL Server Management Studio.     
2. Si no lo encuentra, es posible que tenga que instalarlo: [Descargar SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).    
3. En el cuadro de diálogo **Conectar al servidor**, escriba el nombre de un servidor o de una instancia que tenga habilitado SQL Server R Services. Para estos ejemplos, asegúrese de iniciar sesión con una cuenta que tenga la capacidad para crear una nueva base de datos, ejecutar instrucciones SELECT y ver tablas.  Abra una nueva ventana **Consulta** y pegue esta instrucción, solo para comprobar que todo es operativo:    
    
    ```sql   
    exec sp_execute_external_script  
      @language =N'R',    
      @script=N'OutputDataSet<-InputDataSet',      
      @input_data_1 =N'select 1 as hello'    
      with result sets (([hello] int not null));    
    go    
    ```   
       
       
  
### <a name="bkmk_SSMSBasics"></a>1.2. Crear algunos datos de prueba sencillos  
    
Antes de desarrollar una solución de ciencia de datos complejos, es importante comprender las diferencias entre SQL Server y R.    
  
1. Cree una tabla de datos temporal ejecutando la siguiente instrucción T-SQL.     
   
    ```sql    
    CREATE TABLE #MyData ([Col1] int not null) ON [PRIMARY]    
    INSERT INTO #MyData   VALUES (1);    
    INSERT INTO #MyData   Values (10);    
    INSERT INTO #MyData   Values (100) ;    
    GO    
    ```    
5. Después de crear la tabla, use la siguiente instrucción para consultar la tabla:  
    ```sql  
    SELECT * from #MyData  
    ```  

**Resultado**  
  
|Col1 |   
|----|   
|1|   
|10|   
|100|   
  
    
### 1.3. Obtener los datos de prueba mediante el script de R    
  
Una vez creada la tabla, ejecute la siguiente instrucción:  
  
  ```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' OutputDataSet <- InputDataSet;'    
    , @input_data_1 = N' SELECT *  FROM #MyData;'    
    WITH RESULT SETS (([NewColName] int NOT NULL));
  ```    
    
Debe devolver los mismos valores, pero con un nuevo nombre de columna.  
  
**Notas**    
- El parámetro *@language* define la extensión del lenguaje para llamar, en este caso, R.    
- En el parámetro *@script* se definen los comandos para pasar al tiempo de ejecución de R como texto Unicode. También puede agregar texto a una variable de tipo **nvarchar** y, después, llamar a la variable.    
- La línea `N'OutputDataSet <- InputDataSet;'` pasa los datos de entrada, incluidos en el nombre de variable predeterminado **InputDataSet** a R y, después, vuelve a los resultados sin realizar más operaciones. Tenga en cuenta que R distingue mayúsculas de minúsculas; por lo tanto, los nombres de variable de entrada y salida deben usar la grafía correcta o se generará un error.    
   
    
Para especificar una variable de entrada o salida distinta, use el parámetro *@input_data_1_name* y escriba un identificador SQL válido. Por ejemplo, en este caso, los nombres de las variables de entrada y salida han cambiado a *SQLOut* y *SQLIn* respectivamente:    
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' SQLOut <- SQLIn;'    
    , @input_data_1 = N' SELECT 12 as Col;'    
    , @input_data_1_name  = N'SQLIn'    
    , @output_data_1_name =  N'SQLOut'    
    WITH RESULT SETS (([NewColName] int NOT NULL));    
```    
    
**Notas**    
- Los parámetros obligatorios *@input_data_1* y *@output_data_1* deben especificarse en primer lugar, para poder usar los parámetros opcionales *@input_data_1_name* y *@output_data_1_name*.    
- SQL y R no admiten los mismos tipos de datos; por lo tanto, es muy común que se produzcan conversiones de tipos cuando se envían datos de SQL Server a R y viceversa. Para obtener más información, consulte [Working with R Data Types (Trabajar con tipos de datos de R)](../../advanced-analytics/r-services/working-with-r-data-types.md).    
- Solo se puede pasar un conjunto de datos de entrada como parámetro y solo puede devolver un conjunto de datos. Pero puede llamar a otros conjuntos de datos desde dentro de su código de R y devolver resultados de otros tipos además del conjunto de datos. También puede agregar la palabra clave OUTPUT a cualquier parámetro para que se devuelva con los resultados.      
- El esquema del conjunto de datos devuelto (R data.frame) está definido por la instrucción `WITH RESULT SETS`. Intente omitir esto y vea qué sucede.    
- Se devuelven resultados tabulares en el panel **Valores**. Los mensajes devueltos por el tiempo de ejecución de R se proporcionan en **Mensajes**     
  
### 1.4. Generar resultados con R    
    
También puede generar valores mediante el script de R y dejando la cadena de consulta de entrada _@input_data_1_ en blanco. También puede usar una instrucción SQL SELECT válida como marcador de posición pero no usar los resultados de SQL en el script de R.    
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' mytextvariable <- c("hello", " ", "world");    
                         OutputDataSet <- as.data.frame(mytextvariable);'    
    , @input_data_1 = N' SELECT 1 as Temp1'    
    WITH RESULT SETS (([col] char(20) NOT NULL));    
```    
    
**Resultado**    
    
    
 |*col* |    
 |-----|    
 |*hello*|    
 |     |    
 |*world*|    
    

Ahora, pruebe una versión diferente del ejemplo Hello World que se ha proporcionado anteriormente.     
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' OutputDataSet<- data.frame(c("hello"), " ", c("world"));'    
    , @input_data_1 = N'  '    
    WITH RESULT SETS (([col1] varchar(20) , [col2] char(1), [col3] varchar(20) ));    
```    
    
    
**Resultado**    
    
    
 |*col1* | *col2* | *col3*|    
 |-------|-------|-------    
 |*hello*|  |*world*|    
    
Tenga en cuenta que ambas instrucciones crean un vector con tres valores, pero en el segundo ejemplo se devuelven tres columnas con una única fila, y el primero devuelve una única columna con tres filas. ¿Por qué?
    
La razón es que R proporciona muchas formas de trabajar con columnas de valores: vectores, matrices y listas. Estas operaciones aunque son eficaces y flexibles, no siempre cumplen las expectativas de los desarrolladores de SQL.  Algunas funciones de R realizarán conversiones de objetos de datos implícitos en listas y matrices.

> [!TIP] 
> 
> Compruebe siempre los resultados y determine el número de columnas de datos que devolverá el código de R y cuáles serán los tipos de datos.    
>     
> Independientemente de si el código de R usa matrices, vectores u otro tipo de estructura de datos, recuerde que el resultado que se obtiene del script de R para el procedimiento almacenado debe ser un **data.frame**.      
  
  
## Parte 2: conversión de datos y otros problemas  
  
En esta sección se proporciona información general rápida de algunos problemas que debe tener en cuenta al ejecutar el código de R en SQL Server.  
  
+ Tipos de datos: descripción de las opciones de transmisión y conversión, así como las conversiones implícitas  
+ Conjuntos de resultados tabulares: prever las formas en que R puede cambiar las columnas y filas de datos    
  
### 2.1 Conversión implícita de tipos de datos  
    
R y SQL Server no usan los mismos tipos de datos, por lo que debe ser consciente de las restricciones al mover datos entre R y la base de datos. En los siguientes ejemplos se ilustran algunos problemas comunes.   
    
    
1. Ejecute la siguiente instrucción para realizar la multiplicación de matrices mediante R. En este script, la columna única de tres valores se convierte en una matriz de una sola columna.  Después, R convierte implícitamente la segunda variable, `y`, en una matriz de una sola columna para ajustar los dos argumentos.  
    
    ```sql    
    execute sp_execute_external_script    
      @language = N'R'    
      , @script = N'    
        x <- as.matrix(InputDataSet);    
        y <- array(12:15);    
      OutputDataSet <- as.data.frame(x %*% y);'    
     , @input_data_1 = N' SELECT [Col1]  from #MyData;'    
      WITH RESULT SETS (([Col1] int, [Col2] int, [Col3] int, Col4 int));    
    ```    
**Resultado**

|Col1|Col2|Col3|Col4|
|---|---|---|---|
|12|13|14|15|
|120|130|140|150|
|1200|1300|1400|1500|
 
  
      
2. Ahora ejecute el siguiente script, que es similar, y vea qué ocurre cuando cambia la longitud de la matriz. 
   
    ```sql    
    execute sp_execute_external_script    
      @language = N'R'    
      , @script = N'    
        x <- as.matrix(InputDataSet);    
        y <- array(12:14);    
      OutputDataSet <- as.data.frame(y %*% x);'    
      , @input_data_1 = N' SELECT [Col1]  from #MyData;'    
      WITH RESULT SETS (([Col1] int ));    
    ```    

**Resultado**    
    
|Col1|
|---|    
|1542|    
  
  Esta vez R devuelve un solo valor como resultado. Este resultado es válido porque los dos argumentos son vectores de la misma longitud; por lo tanto, R devolverá el producto interior como una matriz.    
    
   
  
### 2.2 Combinar o multiplicar columnas de longitud diferente    
    
  
En el siguiente script se ilustran algunos comportamientos de R que pueden no cumplir las expectativas de un desarrollador de bases de datos.   
  
El script define una nueva matriz numérica de longitud 6 y la almacena en la variable `df1` de R. Después, la matriz numérica se combina con los enteros de la tabla #MyData, que contiene 3 valores para crear una nueva trama de datos, `df2`.   
    
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N'    
               df1 <- as.data.frame( array(1:6) );    
               df2 <- as.data.frame( c( InputDataSet , df1 ));    
               OutputDataSet <- df2'    
    , @input_data_1 = N' SELECT [Col1]  from #MyData;'    
    WITH RESULT SETS (( [Col2] int not null, [Col3] int not null ));    
```    
    
**Resultado**    
    
|*Col2*|*Col3*|    
|----|----|    
|1|1|    
|10|2|    
|100|3|    
|1|4|    
|10|5|    
|100|6|    
    
Hay muchas funciones de R que crean salida tabular pero realizan operaciones muy diferentes en los valores según el objeto de datos de R. Como este procedimiento almacenado de [!INCLUDE[tsql](../../includes/tsql-md.md)] requiere que tanto las entradas como las salidas se pasen como un data.frame, usará con frecuencia funciones para convertir columnas y filas en tramas de datos y viceversa.    
    
Si alguna vez tiene dudas sobre qué objeto de datos de R se está usando, agregue la función `str()` de R o una de las funciones de identificación (`is.matrix`, `is.vector`, etc.) para inspeccionar los resultados y obtener el esquema y los tipos de valores reales.    
  
  
Para obtener más información, consulte este artículo de Hadley Wickham sobre [Estructuras de datos de R](http://adv-r.had.co.nz/Data-structures.html).    
    
### 2.3 Identificar tipos de datos y comprobar los esquemas   
Verá que es importante saber exactamente cuántas columnas se devolverán desde el código R y cuál será el tipo de datos de cada columna.     
    
  
Puede usar la función `str()` en el script de R para que el esquema de datos del objeto de R se devuelva como un mensaje informativo en . 

Por ejemplo, la siguiente instrucción devuelve el esquema de la tabla #MyData.    
        
```sql    
    execute sp_execute_external_script    
      @language = N'R'    
    , @script = N' str(InputDataSet);'    
    , @input_data_1 = N' SELECT *  FROM #MyData;'    
      WITH RESULT SETS undefined;    
```    
    
    
**Resultado**    
    
*Mensaje(s) STDOUT del script externo:*    
*'data.frame': 3 obs. de 1 variable:*    
*Mensaje(s) STDOUT del script externo:*    
*$ Col1: int 1   10   100*    
    
  
  
### 2.4 Convertir columnas   
  
Al enviar datos desde SQL Server a R, con frecuencia necesitará convertir tipos de datos para asegurarse de que se pueden controlar adecuadamente.    
  
Cuando se usa una consulta SQL como entrada al código de R, tienen lugar varias transformaciones de datos:    
- SQL Server inserta los datos de la consulta en el proceso de R administrado por el servicio Launchpad y los convierte en una representación interna.    
- El tiempo de ejecución de R carga los datos en una variable data.frame y realiza sus propias operaciones en los datos.    
- El motor de base de datos devuelve los datos a Management Studio u otro cliente usando tipos de datos de SQL Server.  
    
1. Ejecute la siguiente consulta en el almacenamiento de datos AdventureWorksDW. La consulta de datos de entrada define una tabla de datos de ventas que se usan para crear un pronóstico.   
  
    ```sql    
    execute sp_execute_external_script    
       @language = N'R'    
      , @script = N' str(InputDataSet);'    
      , @input_data_1 = N'
           SELECT ReportingDate    
         , CAST(ModelRegion as varchar(50)) as ProductSeries    
         , Amount    
           FROM [AdventureworksDW2016CTP3].[dbo].[vTimeSeries]     
           WHERE [ModelRegion] = ''M200 Europe''    
           ORDER BY ReportingDate ASC ;'    
        WITH RESULT SETS undefined;    
    ```    
  
2. Ahora revise los resultados de la función `str` para ver cómo R controla los datos de entrada.
      
**Resultado**    
    
  *STDOUT message(s) from external script: 'data.frame':    37 obs. de  3 variables:*    
  *STDOUT message(s) from external script: $ ReportingDate: POSIXct, format: "2010-12-24 23:00:00" "2010-12-24 23:00:00"*    
  *STDOUT message(s) from external script: $ ProductSeries: Factor w/ 1 levels "M200 Europe",..: 1 1 1 1 1 1 1 1 1 1 ...*    
  *STDOUT message(s) from external script: $ Amount       : num  3400 16925 20350 16950 16950*    
    
    
**Notas**    
    
- R no admite algunos tipos de datos de SQL Server. Por lo tanto, para evitar errores, debe especificar las columnas individualmente y convertir algunas de ellas.    
- El predicado de cadena en la cláusula WHERE debe estar delimitado por dos conjuntos de comillas simples.    
- La columna de fecha y hora se ha devuelto como el tipo de datos R, **POSIXct**.    
- La columna [ProductSeries] se ha identificado (correctamente) como un **factor**.    
     
  
### 2.5 Usar varias entradas   
Solo se puede pasar un conjunto de datos de entrada como parámetro. Pero puede llamar a otros conjuntos de datos desde dentro de su código de R con RODBC.     
  
Por ejemplo, en el ejemplo siguiente se realiza una llamada al paquete RODBC, especificando los datos en una instrucción SELECT.    
    
```sql    
    @script = N' 
       <other R code here>;    
       library(RODBC);    
       connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");        dbhandle <- odbcDriverConnect(connStr)    
       OutputDataSet <- sqlQuery(dbhandle, "SELECT * from <table_name>");    
       <more R code combining the data>'    
```

Le recomendamos que use RODBC para obtener conjuntos de datos más pequeños, como búsquedas o listas de factores, y use el parámetro @input_data para obtener conjuntos de datos más grandes, como los que se usan para el entrenamiento de un modelo de SQL Server. 


### 2.6 Generar varias salidas

En SQL Server 2016, el resultado de R del procedimiento almacenado sp_execute_external_script se limita a un único data.frame o un conjunto de datos. (Es posible que esta limitación desaparezca en el futuro.)   
Pero puede devolver resultados de otros tipos además del conjunto de datos. Por ejemplo, podría entrenar un modelo con un único conjunto de datos como entrada, pero devolver una tabla de estadísticas como salida, además del modelo entrenado como un objeto.    
    
También puede agregar la palabra clave `OUTPUT` a cualquier parámetro para que se devuelva con los resultados.   
    
### 2.7 Procesamiento paralelo    
    
Si trabaja con un gran conjunto de datos y la consulta SQL que obtiene los datos puede generar un plan de consulta paralelo, puede ejecutar el script de R en paralelo estableciendo el parámetro *@parallel* en 1. Esto es generalmente útil si está puntuando un conjunto de resultados de gran tamaño. Si usa esta opción, debe especificar el esquema de resultados de salida de antemano CON CONJUNTOS DE RESULTADOS.    
    
Pero este parámetro no tiene ningún efecto si necesita entrenar un modelo que usa todas las filas. En esos casos, se recomienda usar los paquetes **ScaleR**. Estos paquetes pueden distribuir el procesamiento automáticamente sin necesidad de especificar *@parallel =1* en la llamada a sp_execute_external_script.    
    
      
  
## Parte 3. Ajustar funciones de R en procedimientos almacenados  
  
R puede realizar muchas funciones estadísticas avanzadas que pueden requerir código complicado de reproducir mediante T-SQL.  En cambio, con R Services, puede ejecutar scripts de utilidad de R en un procedimiento almacenado para admitir tareas como estas:   
    
- Aplicar las funciones matemáticas y estadísticas de R en datos de SQL Server    
    
- Crear funciones con valores de tabla o funciones escalares que usan código de R    
     

 Normalmente, encapsularía las llamadas a estas funciones de R en procedimientos almacenados, para pasar los parámetros más fácilmente. Para ilustrar este proceso, se proporciona la misma función en código R, en una llamada del procedimiento almacenado ad hoc a sp_execute_external_script, y en un procedimiento almacenado que puede usar para parametrizar la función de R.
 
      
### 3.1. Generar números aleatorios  
  
En la instrucción siguiente se usa una de las funciones de R del paquete `stats`, que se carga de manera predeterminada cuando está instalado R Services. La función `rnorm` que se muestra aquí genera 20 números aleatorios con una distribución normal, dada una media de 100.    

Este es el código R que realiza el trabajo.

```r
as.data.frame(rnorm(20, mean = 100));
```

Esta instrucción llama a la función desde T-SQL y devuelve los resultados a SQL Server.  
   
```sql    
EXEC sp_execute_external_script    
      @language = N'R'    
    , @script = N' 
         OutputDataSet <- as.data.frame(rnorm(20, mean = 100));'    
    , @input_data_1 = N'   ;'    
      WITH RESULT SETS (([Density] float NOT NULL));    
```    

Después, encapsule el procedimiento almacenado en otro procedimiento almacenado para pasar los parámetros más fácilmente. Debe definir cada uno de los parámetros de entrada en el argumento _@params_, y asignar cada parámetro a su parámetro de R correspondiente por el nombre.

```sql
CREATE PROCEDURE MyRNorm (@mynorm int, @mymean int)
AS
    EXEC sp_execute_external_script    
      @language = N'R'    
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynorm, mymean));'    
    , @input_data_1 = N'   ;' 
    , @params = N' @mynorm int, @mymean int'  
    , @mynorm = @mynorm
    , @mymean = @mymean
    WITH RESULT SETS (([Density] float NOT NULL));    
```

Llame al nuevo procedimiento almacenado y pase los valores.

```sql
exec MyRNorm @mynorm = 20,@mymean = 100
```  
    
### 3.2 Más usos para las funciones de utilidad de R  
  
Este ejemplo llama a uno de los paquetes de utilidad de R y usa su función `memory.limit()` para obtener memoria para el entorno actual. El paquete `utils` está instalado pero no se carga de forma predeterminada.    
    
```sql    
execute sp_execute_external_script    
      @language = N'R'    
    , @script = N'    
        library(utils);    
        mymemory <- memory.limit();    
        OutputDataSet <- as.data.frame(mymemory);'    
    , @input_data_1 = N' ;'    
     WITH RESULT SETS (([Col1] int not null));    
```    

En el siguiente ejemplo se obtiene la longitud máxima de enteros que se admiten en el equipo actual, mediante la función R .Machine, y se envía a la consola.

```R
localmax <- .Machine$integer.max;
localmax;
```

```sql
execute sp_execute_external_script
  @language = N'R'
  , @script = N'
      localmax <- .Machine$integer.max;
      OutputDataSet <- as.data.frame(localmax);'
  , @input_data_1 = N'select [Col1]  from #MyData;'
  WITH RESULT SETS (([MaxIntValue] int not null));
```     
    
En cambio, no siempre R realiza mejor el trabajo. Las operaciones basadas en conjuntos en SQL Server pueden ser mucho más eficaces para algunas operaciones que lo que los científicos de datos realizarían normalmente en R. Para obtener un ejemplo de una comparación de rendimiento de funciones de R y funciones personalizadas de T-SQL, vea el [Tutorial integral de ciencia de datos](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md). 

Se recomienda evaluar según cada caso si tiene más sentido realizar una operación determinada mediante R, mediante T-SQL o con alguna otra herramienta.    
    
    
    
### Recursos adicionales    
    
[Análisis detallado de ciencia de datos: Uso de los paquetes RevoScaleR](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md): este tutorial proporciona una experiencia práctica con las tareas comunes de ciencia de datos    
[Solución integral de ciencia datos](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md): este tutorial ilustra el proceso de desarrollo e implementación que equilibra enfoques de SQL y R       
[Análisis avanzado para desarrolladores de SQL](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md): muestra la operatividad de modelos completa el programador de SQL     
    
    
    
    
