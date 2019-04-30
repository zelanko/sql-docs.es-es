---
title: 'Cómo llamar a Java desde SQL: SQL Server Machine Learning Services'
description: Obtenga información sobre cómo llamar a las clases de Java desde procedimientos almacenados de SQL Server mediante la extensión del lenguaje en SQL Server 2019 de programación Java.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a75878ccc4f14d03f84102dd48bfd43a6e04daea
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473556"
---
# <a name="how-to-call-java-from-sql-server-2019-preview"></a>Cómo llamar a Java de la versión preliminar de SQL Server 2019

Cuando se usa el [extensión del lenguaje Java](extension-java.md), [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) sistema al procedimiento almacenado es la interfaz utilizada para llamar a la ejecución de Java. Permisos en la base de datos se aplican a la ejecución de código de Java.

En este artículo se explica los detalles de implementación para las clases de Java y los métodos que se ejecutan en SQL Server. Cuando se haya familiarizado con estos detalles, revise el [ejemplo de Java](java-first-sample.md) en el paso siguiente.

Hay dos métodos para llamar a las clases de Java en SQL Server:

1. Colocar archivos .class o .jar en su [classpath de Java](#classpath). Esto está disponible para Windows y Linux.

2. Cargar clases compiladas en un archivo .jar y otras dependencias en la base de datos mediante el [biblioteca externa](#external-library) DDL. Esta opción está disponible para Windows y Linux desde CTP 2.4.

> [!NOTE]
> Como recomendación general, utilice archivos .jar y archivos .class no individual. Esto es una práctica común en Java y facilitará la experiencia general. Vea también: [Cómo crear un archivo jar desde archivos de clase](extension-java.md#create-jar).

<a name="classpath"></a>

## <a name="classpath"></a>Classpath

### <a name="basic-principles"></a>Principios básicos

* Clases de Java personalizadas compiladas deben existir en archivos .class o archivos .jar en la classpath de Java. El [parámetro CLASSPATH](#set-classpath) proporciona la ruta de acceso a los archivos de Java compilados. 

* El método de Java que llama debe proporcionarse en el parámetro "script" en el procedimiento almacenado.

* Si la clase pertenece a un paquete, debe proporcionarse el nombre del "paquete".

* "params" se usa para pasar parámetros a una clase de Java. Llamar a un método que requiere argumentos no se admite, lo que hace que los parámetros de la única manera de pasar los valores de argumento al método. 

> [!Note]
> Esta nota redefine admitidas y operaciones específicas de Java en CTP 2.x.
> * En el procedimiento almacenado, se admiten parámetros de entrada. No son parámetros de salida.
> * Streaming con el parámetro sp_execute_external_script @r_rowsPerRead no se admite.
> * Creación de particiones con @input_data_1_partition_by_columns no se admite.
> * Uso de procesamiento paralelo @parallel= 1 se admite.

### <a name="call-java-class"></a>Llamar a la clase de Java

Se aplica a Windows y Linux, el [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) sistema al procedimiento almacenado es la interfaz utilizada para llamar a la ejecución de Java. El ejemplo siguiente muestra un uso de la extensión de Java y los parámetros para especificar la ruta de acceso, el script y el código personalizado de sp_execute_external_script.

> [!NOTE]
> Tenga en cuenta que no es necesario definir qué método va a llamar. De forma predeterminada, un método llamado **ejecutar** se llama. Esto significa que debe seguir el SDK e implementar un método execute en la clase de Java.

```sql
DECLARE @param1 int
SET @param1 = 3

EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'<packageName>.<ClassName>'
, @input_data_1 = N'<Input Query>'
, @param1 = @param1
```

<a name="set-classpath"></a>

### <a name="set-classpath"></a>Establecer ruta de clase

Una vez se han compilado la clase de Java o clases y crea un archivo jar en la classpath de Java, tiene dos opciones para proporcionar la ruta de clase a la extensión de Java de SQL Server:

**Opción 1: Usar bibliotecas externas** la opción más sencilla es hacer que SQL Server busque automáticamente las clases para crear bibliotecas externas y elige la biblioteca de un archivo jar. [Uso de bibliotecas externas para Java](howto-call-java-from-sql.md#external-library)

**Opción 2: Registrar una variable de entorno del sistema**

Como ha creado una variable de entorno del sistema para el tiempo de ejecución de Java, puede crear una variable de entorno del sistema y proporcionar las rutas de acceso al archivo jar que contiene las clases. Para ello, deberá crear una variable de entorno del sistema denominada "CLASSPATH".

<a name="external-library"></a>

## <a name="external-library"></a>Biblioteca externa

En SQL Server 2019 CTP 2.4, puede usar las bibliotecas externas para Java en Windows y Linux. Puede compilar las clases en un archivo .jar y cargar el archivo .jar y otras dependencias en la base de datos mediante el [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) DDL.

Ejemplo de cómo cargar un archivo .jar con biblioteca externa:

```sql 
CREATE EXTERNAL LIBRARY myJar
FROM (CONTENT = '<local path to .jar file>') 
WITH (LANGUAGE = 'Java'); 
GO
```

Mediante la creación de una biblioteca externa, SQL Server automáticamente tendrán acceso a las clases de Java y no es necesario establecer los permisos especiales en la ruta de clase.

Ejemplo de una llamada a un método en una clase desde un paquete cargado como una biblioteca externa:

```sql
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'MyPackage.MyCLass'
, @input_data_1 = N'SELECT * FROM MYTABLE'
with result sets ((column1 int))
```

Para obtener más información, consulte [crear biblioteca externa](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

## <a name="next-steps"></a>Pasos siguientes

+ [Ejemplo de Java en SQL Server](java-first-sample.md)
+ [Tipos de datos de SQL Server y Java](java-sql-datatypes.md)
+ [Extensión del lenguaje Java en SQL Server](extension-java.md)
