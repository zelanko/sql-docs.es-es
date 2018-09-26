---
title: Cómo llamar a Java desde SQL | Microsoft Docs
description: Obtenga información sobre cómo llamar a las clases de Java desde procedimientos almacenados de SQL Server mediante la extensión del lenguaje en SQL Server 2019 de programación Java.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/24/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 08af5a18b827c783515ecd3b4ba4a802c3472f93
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2018
ms.locfileid: "46715433"
---
# <a name="how-to-call-java-from-sql-server-2019"></a>Cómo llamar a Java desde SQL Server 2019

Cuando se usa el [extensión del lenguaje Java](extension-java.md), [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) sistema al procedimiento almacenado es la interfaz utilizada para llamar a la ejecución de Java. Permisos en la base de datos se aplican a la ejecución de código de Java.

En este artículo se explica los detalles de implementación para las clases de Java y los métodos que se ejecutan en SQL Server. Cuando se haya familiarizado con estos detalles, revise el [ejemplo de Java](java-first-sample.md) en el paso siguiente.

## <a name="basic-principles"></a>Principios básicos

* Clases de Java personalizadas compiladas deben existir en archivos .class o archivos .jar en la classpath de Java. El [parámetro CLASSPATH](#set-classpath) proporciona la ruta de acceso a los archivos de Java compilados. 

* El método de Java que llama debe proporcionarse en el parámetro "script" en el procedimiento almacenado.

* Si la clase pertenece a un paquete, debe proporcionarse el nombre del "paquete".

* "params" se usa para pasar parámetros a una clase de Java. Llamar a un método que requiere argumentos no se admite, lo que hace que los parámetros de la única manera de pasar los valores de argumento al método. 

> [!Note]
> Esta nota redefine admitidas y operaciones específicas de Java en CTP 2.0.
> * En el procedimiento almacenado, se admiten parámetros de entrada. No son parámetros de salida.
> * Streaming con el parámetro sp_execute_external_script **@r_rowsPerRead** no se admite.
> * Creación de particiones mediante **@input_data_1_partition_by_columns** no se admite.
> * Uso de procesamiento paralelo  **@parallel= 1** se admite.

## <a name="call-spexecuteexternalscript"></a>Llamada a sp_execute_external_script

El [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) sistema al procedimiento almacenado es la interfaz utilizada para llamar a la ejecución de Java. El ejemplo siguiente muestra un uso de la extensión de Java y los parámetros para especificar la ruta de acceso, el script y el código personalizado de sp_execute_external_script.

```sql
DECLARE @myClassPath nvarchar(30)
DECLARE @param1 int

SET @myClassPath = N'/<my path>/program.jar'
SET @param1 = 3

EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'<packageName>.<ClassName>.<methodName>'
, @input_data_1 = N'<Input Query>
, @params = N'@CLASSPATH nvarchar(30), @param1 INT'
, @CLASSPATH = @myClassPath
, @param1 = @param1
```

<a name="set-classpath"></a>

## <a name="set-classpath"></a>Establecer ruta de clase

Después de compilar la clase de Java o clases y coloca los archivos de .class o archivos .jar en la classpath de Java, tiene dos opciones para proporcionar la ruta de clase a la extensión de Java de SQL Server:

**Opción 1: Pasar como un parámetro**

Un enfoque para especificar una ruta de acceso al código compilado es estableciendo la ruta de clase como parámetro de entrada para el procedimiento de sp_execute_external_script. El [ejemplo de Java](java-first-sample.md#call-method) demuestra esta técnica. Si elige este enfoque y tiene varias rutas de acceso, asegúrese de utilizar el separador de ruta de acceso es válido para el sistema operativo subyacente:

* En Linux, separe las rutas de acceso en la ruta de clase con dos puntos ":".
* En Windows, separe las rutas de acceso en la ruta de clase con un punto y coma ";"

**Opción 2: Registrar una variable del sistema**

Como ha creado una variable del sistema para los archivos ejecutables JDK, puede crear una variable del sistema para las rutas de código. Para ello, crea una variable de entorno del sistema denominada "CLASSPATH"

## <a name="class-requirements"></a>Requisitos de la clase

En orden para SQL Server para comunicarse con el tiempo de ejecución de Java, deberá implementar variables estáticas específicas en la clase. SQL Server, a continuación, puede ejecutar un método en los datos de exchange y de clase de Java mediante la extensión del lenguaje Java.

> [!Note]
> Esperar a que los detalles de implementación para cambiar en las próximas versiones de CTP mientras seguimos trabajando para mejorar la experiencia para desarrolladores.

## <a name="method-requirements"></a>Requisitos del método
Para pasar argumentos, use el **@param** parámetro en sp_execute_external_script. El propio método no puede tener ningún argumento. El tipo de valor devuelto debe ser void.  

```java
public static void test()  {}
```

## <a name="data-inputs"></a>Entradas de datos 

En esta sección se explica cómo insertar datos en Java desde una consulta de SQL Server mediante **InputDataSet** en sp_execute_external_script.

Para cada columna de entrada que la consulta SQL se inserta en Java, debe declarar una matriz.

### <a name="inputdatacol"></a>inputDataCol

En la versión actual de la extensión de Java, el **inputDataColN** variable donde es necesaria, *N* es el número de columnas. 

```java
public static <type>[] inputDataColN = new <type>[1]
```

Estas matrices tienen que inicializarse (el tamaño de la matriz debe ser mayor que 0 y no tiene por qué reflejar la longitud real de la columna).

Ejemplo: `public static int[] inputDataCol1 = new int[1];`

Estas variables de matriz se rellenará con datos de entrada de una consulta de SQL server antes de la ejecución del programa de Java que está llamando.

### <a name="inputnullmap"></a>inputNullMap

Mapa de NULL se utiliza la extensión de saber qué valores son null. Esta variable se rellenará con información acerca de los valores null por SQL Server antes de la ejecución de la función de usuario.

El usuario solo necesita inicializar esta variable (y el tamaño de la matriz debe ser mayor que 0).

```java
public static boolean[][] inputNullMap = new boolean[1][1];
```

## <a name="data-outputs"></a>Salidas de datos 

Esta sección se describen **OutputDataSet**, los conjuntos de datos de salida devuelto desde Java, que puede enviar a y persisten en SQL Server.

> [!Note]
> Parámetros de salida [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) no se admiten en esta versión.

### <a name="outputdatacoln"></a>outputDataColN

Similar a **inputDataSet**, para cada columna de salida que el programa de Java envía a SQL Server, debe declarar una variable de matriz. Todos los **outputDataCol** matrices deben tener la misma longitud. Deberá asegurarse de que esto se inicializa en el momento en que finaliza la ejecución de la clase.

```java
public static <type>[] outputDataColN = new <type>[]
```

### <a name="numberofoutputcols"></a>numberofOutputCols

Establecer esta variable en el número de columnas de datos de salida que espera tener cuando finaliza la ejecución de la función de usuario.

```java
public static short numberofOutputCols = <expected number of output columns>;
```

### <a name="outputnullmap"></a>outputNullMap

Mapa de NULL se utiliza la extensión para indicar qué valores son null. Se requiere esto, ya que los tipos primitivos no son compatibles con null. Actualmente, también es necesario que la asignación de null para los tipos de cadena, aunque las cadenas pueden ser null. Los valores NULL se indican mediante "true".

Este NullMap debe rellenarse con el número esperado de columnas y filas que se va a devolver a SQL Server.

```java
public static boolean[][] outputNullMap
```

## <a name="next-steps"></a>Pasos siguientes

+ [Ejemplo de Java en SQL Server](java-first-sample.md)
+ [Tipos de datos de SQL Server y Java](java-sql-datatypes.md)
+ [Extensión del lenguaje Java en SQL Server](extension-java.md)
