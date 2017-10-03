---
title: "Trabajar con entradas y salidas (R en Inicio rápido de SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
- SQL
ms.assetid: 75480e5c-f37f-45b9-a176-67e08e9a9daf
caps.latest.revision: 7
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: a5ffcfafc29f0b741d8e6ada0d50ef6f94fecc7f
ms.contentlocale: es-es
ms.lasthandoff: 09/27/2017

---
# <a name="working-with-inputs-and-outputs-r-in-sql-quickstart"></a>Trabajar con entradas y salidas (R en Inicio rápido de SQL)

Cuando desea ejecutar código R en SQL Server, debe ajustar el script de R en un procedimiento almacenado del sistema, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). Este procedimiento almacenado sirve para iniciar el tiempo de ejecución de R en el contexto de SQL Server, que pasa datos a R, administra las sesiones de usuario de R de forma segura y devuelve los resultados al cliente.

## <a name="bkmk_SSMSBasics"></a>Crear algunos datos de prueba sencillos

Crear una tabla pequeña de datos de prueba mediante la ejecución de la siguiente instrucción T-SQL:

```sql
CREATE TABLE RTestData ([col1] int not null) ON [PRIMARY]
INSERT INTO RTestData   VALUES (1);
INSERT INTO RTestData   VALUES (10);
INSERT INTO RTestData   VALUES (100) ;
GO
```

Después de crear la tabla, use la siguiente instrucción para consultar la tabla:
  
```sql
SELECT * FROM RTestData
```

**Resultado**

|col1|
|------|
|*1*|
|*10*|
|*100*|

## <a name="get-the-same-data-using-r-script"></a>Obtener los mismos datos con el script de R

Una vez creada la tabla, ejecute la siguiente instrucción:

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N' OutputDataSet <- InputDataSet;'
    , @input_data_1 = N' SELECT *  FROM RTestData;'
    WITH RESULT SETS (([NewColName] int NOT NULL));
```

Obtiene los datos de la tabla, hace un recorrido de ida y durante el tiempo de ejecución de R y devuelve los valores con el nombre de columna, *NewColName*.

**Resultado**

![rsql_basictut_getsamedataR](media/rsql-basictut-getsamedatar.PNG)


**Comentarios**

+ In Management Studio, los resultados tabulares se devuelven en el panel **Valores**. Los mensajes devueltos por el tiempo de ejecución de R se proporcionan en el panel **Mensajes**.
+ El parámetro *@language* define la extensión del lenguaje para llamar (en este caso, R).
+ En el parámetro *@script* se definen los comandos que se van a pasar al tiempo de ejecución de R. El script de R debe estar todo incluido en este argumento en texto Unicode. También puede agregar texto a una variable de tipo **nvarchar** y, después, llamar a la variable.
+ Los datos devueltos por la consulta se pasan al tiempo de ejecución de R, que los devuelve a su vez a SQL Server como una trama de datos.
+ La cláusula WITH RESULT SETS define el esquema de la tabla de datos devueltos en SQL Server.

## <a name="change-input-or-output-variables"></a>Cambiar las variables de entrada o de salida

En el ejemplo anterior se usaban los nombres predeterminados de las variables de entrada y de salida, _InputDataSet_ y _OutputDataSet_. Para definir los datos de entrada asociados a _InputDatSet_, se usa la variable *@input_data_1*.

En este ejemplo, los nombres de las variables de entrada y salida del procedimiento almacenado se han cambiado a *SQL_Out* y *SQL_In*:

```sql
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N' SQL_out <- SQL_in;'
  , @input_data_1 = N' SELECT 12 as Col;'
  , @input_data_1_name  = N'SQL_In'
  , @output_data_1_name =  N'SQL_Out'
  WITH RESULT SETS (([NewColName] int NOT NULL));
```

¿Se produce un error "objeto SQL\_en no encontrado"? Esto sucede porque R distingue entre mayúsculas y minúsculas. En el ejemplo, el script de R usa las variables *SQL_in* y *SQL_out*, mientras que los parámetros del procedimiento almacenado usan las variables *SQL_In* y *SQL_Out*.

Eso es porque R distingue mayúsculas de minúsculas. En el ejemplo, el script de R usa las variables *SQL_in* y *SQL_out*, mientras que los parámetros del procedimiento almacenado usan las variables *SQL_In* y *SQL_Out*.
Intente corregir **sólo** el *SQL_In* variable y vuelva a ejecutar el procedimiento almacenado.

Ahora obtendrá una **diferentes** error:

```Error
EXECUTE statement failed because its WITH RESULT SETS clause specified 1 result set(s), but the statement only sent 0 result set(s) at run time.
```

Nos estamos muestran la este error porque se pueden esperar verlo con frecuencia al probar el nuevo código de R. Significa que el script de R se ejecutó correctamente, pero SQL Server no recibió ningún dato ni ha recibido datos incorrectos o inesperados.

En tal caso, el esquema de salida (la línea que comienza por **WITH**) especifica que se debe devolver una columna de datos enteros, pero como R pone los datos en otra variable, no se devuelve nada a SQL Server, de ahí el error. Para corregir el error, corrija el segundo nombre de variable.

**Recuerde que estos requisitos.**

- Los nombres de las variables deben seguir las reglas de los identificadores de SQL válidos.
- El orden de los parámetros es importante. Debe especificar los parámetros obligatorios *@input_data_1* y *@output_data_1* en primer lugar para poder usar los parámetros opcionales *@input_data_1_name* y *@output_data_1_name*.
- Solo se puede pasar un conjunto de datos de entrada como parámetro y solo puede devolver un conjunto de datos. Pero puede llamar a otros conjuntos de datos desde dentro de su código de R y devolver resultados de otros tipos además del conjunto de datos. También puede agregar la palabra clave OUTPUT a cualquier parámetro para que se devuelva con los resultados. Más adelante en este tutorial encontrará un ejemplo sencillo.
- La instrucción `WITH RESULT SETS` define el esquema de los datos para beneficio de SQL Server. Debe proporcionar tipos de datos compatibles con SQL en cada columna que se obtenga de R. También puede usar la definición de esquema para dar nuevos nombres de columna, no es necesario usar los nombres de columna de data.frame de R. En algunos casos, esta cláusula es opcional; Intente omitiéndola y vea Qué sucede.

## <a name="generate-results-using-r"></a>Generar resultados con R

También puede generar valores con el script de R y dejando la cadena de consulta de entrada _@input_data_1_ en blanco. O, si quiere, puede usar una instrucción SQL SELECT válida como marcador de posición y no usar los resultados de SQL en el script de R.

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
   , @script = N' mytextvariable <- c("hello", " ", "world");
       OutputDataSet <- as.data.frame(mytextvariable);'
   , @input_data_1 = N' SELECT 1 as Temp1'
   WITH RESULT SETS (([Col1] char(20) NOT NULL));
```

**Resultado**

*Col1*
*Hola*
<code>   </code>
*world*

## <a name="next-lesson"></a>Lección siguiente

Nos detendremos en algunos de los problemas que pueden surgir cuando se pasan datos entre R y SQL Server, como las conversiones implícitas y las diferencias en los datos tabulares entre R y SQL.

[Tipos de datos y objetos de datos de R y SQL](../tutorials/rtsql-r-and-sql-data-types-and-data-objects.md)

