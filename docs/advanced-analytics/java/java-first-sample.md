---
title: 'Ejemplo de Java y el tutorial de SQL Server 2019: SQL Server Machine Learning Services'
description: Ejecutar código de ejemplo de Java en SQL Server de 2019 para conocer los pasos para usar la extensión del lenguaje Java con datos de SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/23/2019
ms.topic: conceptual
author: nelgson
ms.author: negust
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 000318716b07f58e94bd5c482d9c349e5d4e5481
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473772"
---
# <a name="sql-server-regex-java-sample"></a>Ejemplo de Regex Java SQL Server

En este ejemplo se muestra una clase de Java que recibe dos columnas (ID y text) de SQL Server y también toma una expresión regular como un parámetro de entrada. La clase devuelve dos columnas a SQL Server (Id. y texto).

Para obtener un texto determinado en la columna de texto enviado a la clase de Java, el código comprueba si se cumple la expresión regular especificada y devuelve ese texto junto con el identificador original. 

En este ejemplo concreto usa una expresión regular que comprueba si un texto contiene la palabra "Java" o "java".

## <a name="microsoft-extensibility-sdk-for-java-for-microsoft-sql-server"></a>Extensibilidad de Microsoft SDK para Java para Microsoft SQL Server

 En CTP 2.5, que estamos cambiando la forma de que implementar código de Java que usa la extensión del lenguaje Java para comunicarse con SQL Server. Esto proporcionará una mejor experiencia de desarrollador al interactuar con SQL Server desde Java.

Debe pensar sobre el SDK como una interfaz auxiliar, que le resultará más fácil de implementar el código de Java que se ejecuta en SQL Server.

> [!NOTE]
> La introducción del SDK es un importante cambio en las versiones de CTP anteriores. Los ejemplos anteriores tenían trabajo deberá actualizarse para usar el SDK.

Para obtener más información, consulte el [documentación del SDK](java-sdk.md).

## <a name="prerequisites"></a>Requisitos previos

+ Instancia del motor de base de datos de SQL Server 2019 con el marco de extensibilidad y la extensión de programación Java [en Windows](../install/sql-machine-learning-services-windows-install.md) o [en Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup). Para obtener más información sobre la configuración del sistema, consulte [extensión del lenguaje Java en SQL Server 2019](extension-java.md). Para obtener más información sobre los requisitos de codificación, vea [cómo llamar a Java en SQL Server](howto-call-java-from-sql.md).

+ SQL Server Management Studio o Azure Data Studio para ejecutar T-SQL.

+ Java SE Development Kit (JDK) 8 o JRE 8 Windows on o Linux.

+ [Extensibilidad de SDK de Java de Microsoft para Microsoft SQL Server](http://aka.ms/mssql-java-lang-extension) mssql-java-lang-extension.jar.

Compilación de línea de comandos utilizando **javac** es suficiente para este tutorial.

## <a name="1---create-sample-data-in-a-sql-server-table"></a>1 - crear datos de ejemplo en una tabla de SQL Server

En primer lugar, crear y rellenar un *testdata* tabla con **ID** y **texto** columnas. Conectarse a SQL Server y ejecute el siguiente script para crear una tabla:

```sql
CREATE DATABASE javatest
GO
USE javatest
GO

-- Create table for test data
DROP TABLE IF exists testdata;
GO

CREATE TABLE testdata(
id int NOT NULL,
"text" nvarchar(100) NOT NULL)
GO

TRUNCATE TABLE testdata
GO

-- Insert data into test table
INSERT INTO testdata(id, "text") VALUES (1, 'This sentence contains java')
INSERT INTO testdata(id, "text") VALUES (2, 'This sentence does not')
INSERT INTO testdata(id, "text") VALUES (3, 'I love Java!')
GO
Select * FROM testdata
```

## <a name="2---class-regexsamplejava"></a>2 - clase RegexSample.java

Empiece por crear la clase principal.

En este paso, creará una clase denominada **RegexSample.java** y copie el código Java siguiente en ese archivo.

Esta clase principal está importando el SDK, lo que significa que el archivo jar que descargó en el paso 1 debe ser reconocible de esta clase.

> [!NOTE]
> Tenga en cuenta que esta clase importa el paquete del SDK de extensión de Java.
Consulte el artículo sobre la [extensibilidad de Microsoft SDK para Java para Microsoft SQL Server](java-sdk.md) para obtener más detalles.

```java
package pkg;

import com.microsoft.sqlserver.javalangextension.PrimitiveDataset;
import com.microsoft.sqlserver.javalangextension.AbstractSqlServerExtensionExecutor;
import java.util.LinkedHashMap;
import java.util.LinkedList;
import java.util.ListIterator;
import java.util.regex.*;

public class RegexSample extends AbstractSqlServerExtensionExecutor {
    private Pattern expr;

    public RegexSample() {
        // Setup the expected extension version, and class to use for input and output dataset
        executorExtensionVersion = SQLSERVER_JAVA_LANG_EXTENSION_V1;
        executorInputDatasetClassName = PrimitiveDataset.class.getName();
        executorOutputDatasetClassName = PrimitiveDataset.class.getName();
    }
    
    public PrimitiveDataset execute(PrimitiveDataset input, LinkedHashMap<String, Object> params) {
        // Validate the input parameters and input column schema
        validateInput(input, params);

        int[] inIds = input.getIntColumn(0);
        String[] inValues = input.getStringColumn(1);
        int rowCount = inValues.length;

        String regexExpr = (String)params.get("regexExpr");
        expr = Pattern.compile(regexExpr);

        System.out.println("regex expression: " + regexExpr);

        // Lists to store the output data
        LinkedList<Integer> outIds = new LinkedList<Integer>();
        LinkedList<String> outValues = new LinkedList<String>();

        // Evaluate each row
        for(int i = 0; i < rowCount; i++) {
            if (check(inValues[i])) {
                outIds.add(inIds[i]);
                outValues.add(inValues[i]);
            }
        }

        int outputRowCount = outValues.size();

        int[] idOutputCol = new int[outputRowCount];
        String[] valueOutputCol = new String[outputRowCount];

        // Convert the list of output columns to arrays
        outValues.toArray(valueOutputCol);

        ListIterator<Integer> it = outIds.listIterator(0);
        int rowId = 0;

        System.out.println("Output data:");
        while (it.hasNext()) {
            idOutputCol[rowId] = it.next().intValue();

            System.out.println("ID: " + idOutputCol[rowId] + " Value: " + valueOutputCol[rowId]);
            rowId++;
        }

        // Construct the output dataset
        PrimitiveDataset output = new PrimitiveDataset();

        output.addColumnMetadata(0, "ID", java.sql.Types.INTEGER, 0, 0);
        output.addColumnMetadata(1, "Text", java.sql.Types.NVARCHAR, 0, 0);

        output.addIntColumn(0, idOutputCol, null);
        output.addStringColumn(1, valueOutputCol);

        return output;
    }

    private void validateInput(PrimitiveDataset input, LinkedHashMap<String, Object> params) {
        // Check for the regex expression input parameter
        if (params.get("regexExpr") == null) {
            throw new IllegalArgumentException("Input parameter 'regexExpr' is not found");
        }

        // The expected input schema should be at least 2 columns, (INTEGER, STRING)
        if (input.getColumnCount() < 2) {
            throw new IllegalArgumentException("Unexpected input schema, schema should be an (INTEGER, NVARCHAR or VARCHAR)");
        }

        // Check that the input column types are expected
        if (input.getColumnType(0) != java.sql.Types.INTEGER &&
                (input.getColumnType(1) != java.sql.Types.VARCHAR && input.getColumnType(1) == java.sql.Types.NVARCHAR )) {
            throw new IllegalArgumentException("Unexpected input schema, schema should be an (INTEGER, NVARCHAR or VARCHAR)");
        }
    }

    private boolean check(String text) {
        Matcher m = expr.matcher(text);

        return m.find();
    }
}
```

## <a name="3-compile-and-create-jar-file"></a>3 para compilar y crear el archivo .jar

Se recomienda que empaquetar las clases y las dependencias en los archivos .jar. Mayoría de los IDE Java como Eclipse o IntelliJ soporte generando archivos jar al que el proyecto de compilación o compilar. En este ejemplo, hemos llamado el archivo jar **regex.jar**.

Si va a crear manualmente un archivo .jar, puede seguir los pasos, consulte [cómo crear un archivo jar](extension-java.md#create-jar).

> [!NOTE]
> Este ejemplo usa los paquetes, lo que significa que el paquete "pkg" proporcionado en la parte superior de la clase garantiza que el código compilado se guarda en una subcarpeta denominada "pkg". Esto se realiza de forma automática si usa un IDE, pero si está compilando manualmente clases mediante **javac**, tendrá que colocar el código compilado en la subcarpeta pkg manualmente.

## <a name="4---create-external-libraries"></a>4 - Creación de bibliotecas externas

Mediante la creación de una biblioteca externa, SQL Server tendrán acceso automáticamente a los archivos jar y no es necesario establecer los permisos especiales en la ruta de clase.

En este ejemplo, deberá crear dos bibliotecas externas. Uno para el SDK y otro para el ejemplo de Regex Java.

1.  Descargar [extensibilidad de Microsoft SDK para Java para Microsoft SQL Server](http://aka.ms/mssql-java-lang-extension) mssql-java-lang-extension.jar.

1. Crear una biblioteca externa para el sdk

```sql
-- Create external library for the SDK
CREATE EXTERNAL LIBRARY sdk
FROM (CONTENT = '<path>/mssql-java-lang-extension.jar')
WITH (LANGUAGE = 'Java');
GO
```

3. Crear una biblioteca externa para el ejemplo de expresión regular

```sql
-- Create external library for the regex sample
CREATE EXTERNAL LIBRARY regex
FROM (CONTENT = '<path>/regex.jar')
WITH (LANGUAGE = 'Java');
GO
```

## <a name="5---set-permissions-skip-if-you-performed-step-4"></a>5: establecer permisos (saltar si ha realizado el paso 4)

Este paso no es necesario si usa las bibliotecas externas. Es la manera recomendada de trabajo crear una biblioteca externa de jar.

Si no desea usar bibliotecas externas, deberá establecer los permisos necesarios. Ejecución del script solo se realiza correctamente si las identidades de proceso tienen acceso a su código. Puede encontrar más información acerca de cómo establecer permisos [aquí](extension-java.md).

### <a name="on-linux"></a>En Linux

Conceder permisos de lectura y ejecución en la ruta de clase para el **mssql_satellite** usuario.

### <a name="on-windows"></a>En Windows

Conceder permisos de 'Lectura y ejecución' a **SQLRUserGroup** y **todos los paquetes de aplicación** SID en la carpeta que contiene el código compilado de Java. 

Todo el árbol debe tener los permisos, desde la raíz primaria a la última carpeta sub. 
 
1. Haga clic en la carpeta (por ejemplo, ' C:\myJavaCode'), elija **propiedades** > **seguridad**.
2. Haga clic en **Editar**.
3. Haga clic en **Agregar**.
4. En **Seleccionar usuarios, equipos, cuentas de servicio o grupos**:
   + Haga clic en **tipos de objeto** y asegúrese de que *los principios de seguridad integrados* y *grupos* están seleccionadas.
   + Haga clic en **ubicaciones** para seleccionar el nombre del equipo local en la parte superior de la lista.
5. Escriba **SQLRUserGroup**, compruebe el nombre y, a continuación, haga clic en Aceptar para agregar el grupo.
6. Escriba **todos los paquetes de aplicación**, compruebe el nombre y, a continuación, haga clic en Aceptar para agregar. Si no se resuelve el nombre, vuelva a consultar el paso de las ubicaciones. El SID es local en el equipo.

Asegúrese de que ambas identidades de seguridad tienen permisos de 'Lectura y ejecución' en la carpeta y la subcarpeta "pkg".

<a name="call-method"></a>

## <a name="2---call-the-java-class"></a>2 - llamar a la clase de Java

Para llamar al código de Java desde SQL Server, se creará un procedimiento almacenado que llama a sp_execute_external_script. En el parámetro "script", definimos qué [paquete]. [class] que queremos llamar. En este ejemplo, la clase pertenece a un paquete denominado **pkg** y un archivo de clase denominado **RegexSample.java**.

> [!NOTE]
>No se define qué método va a llamar. De forma predeterminada, el **ejecutar** se llamará al método. Esto significa que debe seguir la interfaz SDK e implementar un método execute en la clase de Java, si desea poder llamar a la clase de SQL Server.

```sql
/*
This stored procedure takes an input query (input dataset) and a regular expression and returns the rows that fulfilled the given regular expression. This sample uses a regular expression that checks if a text contains the word "Java" or "java" ([Jj]ava) 
*/

CREATE OR ALTER PROCEDURE [dbo].[java_regex] @expr nvarchar(200), @query nvarchar(400)
AS
BEGIN
--Call the Java program by giving the package.className in @script
--The method invoked in the Java code is always the "execute" method
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'pkg.RegexSample'
, @input_data_1 = @query
, @params = N'@regexExpr nvarchar(200)'
, @regexExpr = @expr
with result sets ((ID int, text nvarchar(100)));
END
GO

--Now execute the above stored procedure and provide the regular expression and an input query
EXECUTE [dbo].[java_regex] N'[Jj]ava', N'SELECT id, text FROM testdata'
GO
```

### <a name="results"></a>Resultado

Después de ejecutar la llamada, debe obtener un conjunto de resultados con dos de las filas.

![Resultado de ejemplo de Java](../media/java/java-sample-results.png "resultados de ejemplo")

### <a name="if-you-get-an-error"></a>Si se produce un error

+ Al compilar las clases, la subcarpeta "pkg" debe contener el código compilado para las tres clases.

+ Por último, si no usa bibliotecas externas, compruebe los permisos en *cada* carpeta desde la raíz hasta la subcarpeta "pkg", para asegurarse de que las identidades de seguridad que ejecuta el proceso externo tienen permiso para leer y ejecutar el código.

## <a name="next-steps"></a>Pasos siguientes

+ [Extensibilidad de Microsoft SDK para Java para Microsoft SQL Server](java-sdk.md)
+ [Cómo llamar a Java en SQL Server](howto-call-java-from-sql.md)
+ [Extensiones de Java en SQL Server](extension-java.md)
+ [Tipos de datos de SQL Server y Java](java-sql-datatypes.md)
