---
title: 'Ejemplo de Java y el tutorial de SQL Server 2019: SQL Server Machine Learning Services'
description: Ejecutar código de ejemplo de Java en SQL Server de 2019 para conocer los pasos para usar la extensión del lenguaje Java con datos de SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 02/28/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 86a379191033f49ab6a5d06ceda2d1ed7a747c12
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018041"
---
# <a name="sql-server-java-sample-walkthrough"></a>Tutorial de ejemplo de Java de SQL Server

En este ejemplo se muestra una clase de Java que recibe dos columnas (ID y text) de SQL Server y devuelve dos columnas a SQL Server (Id. y ngram). Para un identificador dado y la combinación de cadena, el código genera las permutaciones de ngrams (subcadenas), devolver estas permutaciones junto con el identificador original. La longitud de la ngram se define mediante un parámetro enviado a la clase de Java.

## <a name="prerequisites"></a>Requisitos previos

+ Instancia del motor de base de datos de SQL Server 2019 con el marco de extensibilidad y la extensión de programación Java [en Windows](../install/sql-machine-learning-services-windows-install.md) o [en Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-setup). Para obtener más información sobre la configuración del sistema, consulte [extensión del lenguaje Java en SQL Server 2019](extension-java.md). Para obtener más información sobre los requisitos de codificación, vea [cómo llamar a Java en SQL Server](howto-call-java-from-sql.md).

+ SQL Server Management Studio u otra herramienta para ejecutar T-SQL.

+ Java SE Development Kit (JDK) 8 en Windows o Linux.

Compilación de línea de comandos utilizando **javac** es suficiente para este tutorial. 

## <a name="1---load-sample-data"></a>1 - carga de datos de ejemplo

En primer lugar, crear y rellenar un *revisa* tabla con **ID** y **texto** columnas. Conectarse a SQL Server y ejecute el siguiente script para crear una tabla:

```sql
DROP TABLE IF exists reviews;
GO
CREATE TABLE reviews(
    id int NOT NULL,
    "text" nvarchar(30) NOT NULL)

INSERT INTO reviews(id, "text") VALUES (1, 'AAA BBB CCC DDD EEE FFF')
INSERT INTO reviews(id, "text") VALUES (2, 'GGG HHH III JJJ KKK LLL')
INSERT INTO reviews(id, "text") VALUES (3, 'MMM NNN OOO PPP QQQ RRR')
GO
```

## <a name="2---class-ngramjava"></a>2 - clase Ngram.java

Empiece por crear la clase principal. Éste es el primero de tres clases.

En este paso, creará una clase denominada **Ngram.java** y copie el código Java siguiente en ese archivo. 


```java
//We will package our classes in a package called pkg
//Packages are option in Java-SQL, but required for this sample.
package pkg;

import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.IntStream;

public class Ngram {

    //Required: This is only required if you are passing data in @input_data_1
    //from SQL Server in sp_execute_external_script
    public static int[] inputDataCol1 = new int[1];
    public static String[] inputDataCol2 = new String[1];

    //Required: Input null map. Size just needs to be set to "1"
    public static boolean[][] inputNullMap = new boolean[1][1];

    //Required: Output data columns returned back to SQL Server
    public static int[] outputDataCol1;
    public static String[] outputDataCol2;

    //Required: Output null map. Is populated with true or false values 
    //to indicate nulls
    public static boolean[][] outputNullMap;

    //Optional: This is only required if parameters are passed with @params
    // from SQL Server in sp_execute_external_script
    // n is giving us the size of ngram substrings
    public static int param1;

    //Optional: The number of rows we will be returning
    public static int numberOfRows;

    //Required: Number of output columns returned
    public static short numberOfOutputCols;

    /*Java main method - Only for testing purposes outside of SQL Server
    public static void main(String... args) {
        //getNGrams();
    }*/

    //This is the method we will be calling from SQL Server
    public static void getNGrams() {

        System.out.println("inputDataCol1.length= "+ inputDataCol1.length);
        if (inputDataCol1.length == 0 ) {
            // TODO: Set empty return
            return;
        }
        //Using a stream to "loop" over the input data inputDataCol1.length. You can also use a for loop for this.
        final List<InputRow> inputDataSet = IntStream.range(0, inputDataCol1.length)
                .mapToObj(i -> new InputRow(inputDataCol1[i], inputDataCol2[i]))
                .collect(Collectors.toList());


        //Again, we are using a stream to loop over data
        final List<OutputRow> outputDataSet = inputDataSet.stream()
                // Generate ngrams of size n for each incoming string
                // Each invocation of ngrams returns a list. flatMap flattens
                // the resulting list-of-lists to a flat list.
                .flatMap(inputRow -> ngrams(param1, inputRow.text).stream().map(s -> new OutputRow(inputRow.id, s)))
                .collect(Collectors.toList());

        //Print the outputDataSet
        System.out.println(outputDataSet);

        //Set the number of rows and columns we will be returning
        numberOfOutputCols = 2;
        numberOfRows = outputDataSet.size();
        outputDataCol1 = new int[numberOfRows]; // ID column
        outputDataCol2 = new String[numberOfRows]; //The ngram column
        outputNullMap = new boolean[2][numberOfRows];// output null map

        //Since we don't have any null values, we will populate all values in the outputNullMap to false
        IntStream.range(0, numberOfRows).forEach(i -> {
            final OutputRow outputRow = outputDataSet.get(i);
            outputDataCol1[i] = outputRow.id;
            outputDataCol2[i] = outputRow.ngram;
            outputNullMap[0][i] = false;
            outputNullMap[1][i] = false;
        });
    }

    // Example: ngrams(3, "abcde") = ["abc", "bcd", "cde"].
    private static List<String> ngrams(int n, String text) {
        return IntStream.range(0, text.length() - n + 1)
                .mapToObj(i -> text.substring(i, i + n))
                .collect(Collectors.toList());
    }
}
```

## <a name="3---class-inputrowjava"></a>3 - clase InputRow.java

Cree una segunda clase denominada **InputRow.java**, formado por el código siguiente y guardado en la misma ubicación que **Ngram.java**.

```java
package pkg;

//This object represents one input row
public class InputRow {
    public final int id;
    public final String text;

    public InputRow(final int id, final String text) {
        this.id = id;
        this.text = text;
    }
}
```

## <a name="4---class-outputrowjava"></a>4 - clase OutputRow.java

Se llama a la tercera y última clase **OutputRow.java**. Copie el código y guardar como OutputRow.java en la misma ubicación que los demás.

```java
package pkg;

//This object represents one output row
public class OutputRow {
    public final int id;
    public final String ngram;

    public OutputRow(final int id, final String ngram) {
        this.id = id;
        this.ngram = ngram;
    }

    @Override
    public String toString() { return id + ":" + ngram; }
}
```

## <a name="5---compile"></a>5 - compilación

Una vez que tenga las clases que esté listas, ejecute javac para compilarlos en archivos "class" (`javac Ngram.java InputRow.java OutputRow.java`). Debe obtener tres archivos .class para este ejemplo (Ngram.class, InputRow.class y OutputRow.class).

Coloque el código compilado en una subcarpeta denominada "paquete" en la ubicación de la ruta de clase. Si está trabajando en una estación de trabajo de desarrollo, este paso es donde copiar los archivos en el equipo de SQL Server.

La ruta de clase es la ubicación del código compilado. Por ejemplo, en Linux, si es la ruta de clase '/ home/myclasspath /', a continuación, los archivos .class deben estar en '/ home/myclasspath/pkg'. En el script de ejemplo en el paso 7, la ruta de clase proporcionado en el sp_execute_external_script es ' / home/myclasspath /' (suponiendo que Linux). 

En Windows, se recomienda usar una carpeta relativamente superficial estructura, uno o dos niveles de profundidad, para simplificar los permisos. Por ejemplo, la ruta de clase podría parecer 'C:\myJavaCode' con una subcarpeta denominada '\pkg' que contiene las clases compiladas. 

Para obtener más información acerca de la ruta de clase, vea [establecer CLASSPATH](howto-call-java-from-sql.md#set-classpath). 

### <a name="using-jar-files"></a>Uso de archivos .jar

Si tiene previsto empaquetar las clases y las dependencias en los archivos .jar, proporcione la ruta de acceso completa al archivo .jar en el parámetro CLASSPATH de sp_execute_external_script. Por ejemplo, si el archivo jar se denomina 'ngram.jar', la ruta de clase será ' / home/myclasspath/ngram.jar' en Linux.

## <a name="6---set-permissions"></a>6: establecer permisos

Ejecución del script solo se realiza correctamente si las identidades de proceso tienen acceso a su código. 

### <a name="on-linux"></a>En Linux

Conceder permisos de lectura y ejecución en la ruta de clase para el **mssql_satellite** usuario.

### <a name="on-windows"></a>En Windows

Conceder permisos de 'Lectura y ejecución' a **SQLRUserGroup** y **todos los paquetes de aplicación** SID en la carpeta que contiene el código compilado de Java. 

Todo el árbol debe tener los permisos, desde la raíz primaria a la última subcarpeta. 
 
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

## <a name="7---call-getngrams"></a>7 - Call *getNgrams()*

Para llamar al código de SQL Server, especifique el método Java **getNgrams()** en el parámetro "script" de sp_execute_external_script. Este método pertenece a un paquete denominado "paquete" y un archivo de clase denominado **Ngram.java**.

En este ejemplo pasa el parámetro de ruta de clase para proporcionar la ruta de acceso a los archivos de Java. También se usa "params" para pasar un parámetro a la clase de Java. Asegúrese de que esa ruta de clase no superar los 30 caracteres. Si es así, aumente el valor en el siguiente script.

+ En Linux, ejecute el siguiente código en SQL Server Management Studio u otra herramienta que puede usada para ejecutar Transact-SQL. 

+ En Windows, cambie @myClassPath a N'C:\myJavaCode\' (suponiendo que es la carpeta principal de \pkg) antes de ejecutar la consulta en SQL Server Management Studio u otra herramienta.

```sql
DECLARE @myClassPath nvarchar(50)
DECLARE @n int 
--This is where you store your classes or jars.
--Update this to your own classpath
SET @myClassPath = N'/home/myclasspath/'
--This is the size of the ngram
SET @n = 3
EXEC sp_execute_external_script
  @language = N'Java'
, @script = N'pkg.Ngram.getNGrams'
, @input_data_1 = N'SELECT id, text FROM reviews'
, @parallel = 0
, @params = N'@CLASSPATH nvarchar(30), @param1 INT'
, @CLASSPATH = @myClassPath
, @param1 = @n
with result sets ((ID int, ngram varchar(20)))
GO
```

### <a name="results"></a>Resultado

Después de ejecutar la llamada, debería obtener un conjunto que muestra las dos columnas de resultados:

![Resultado de ejemplo de Java](../media/java/java-sample-results.png "resultados de ejemplo")

### <a name="if-you-get-an-error"></a>Si se produce un error

Descartar cualquier problema relacionado con la ruta de clase. 

+ Classpath debe constar de la carpeta primaria y todas las subcarpetas, pero no en la subcarpeta "pkg". Si bien debe existir la subcarpeta del paquete, no se supone que esté en el valor de ruta de clase especificado en el procedimiento almacenado.

+ La subcarpeta "pkg" debe contener el código compilado para las tres clases.

+ La longitud de ruta de clase no puede superar el valor declarado (`DECLARE @myClassPath nvarchar(50)`). Si es así, se trunca la ruta de acceso a los 50 primeros caracteres y no se cargará el código compilado. Puede hacer un `SELECT @myClassPath` para comprobar el valor. Aumente la longitud, si no es suficiente 50 caracteres. 

+ Por último, compruebe los permisos en *cada* carpeta desde la raíz hasta la subcarpeta "pkg", para asegurarse de que las identidades de seguridad que ejecuta el proceso externo tienen permiso para leer y ejecutar el código.

## <a name="see-also"></a>Vea también

+ [Cómo llamar a Java en SQL Server](howto-call-java-from-sql.md)
+ [Extensiones de Java en SQL Server](extension-java.md)
+ [Tipos de datos de SQL Server y Java](java-sql-datatypes.md)
