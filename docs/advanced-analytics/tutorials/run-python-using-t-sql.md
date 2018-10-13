---
title: Ejecución de Python mediante T-SQL | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7b4a6035996ce457cb2e58aef5d1c7498ad9f826
ms.sourcegitcommit: ce4b39bf88c9a423ff240a7e3ac840a532c6fcae
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2018
ms.locfileid: "48878028"
---
# <a name="run-python-using-t-sql"></a>Ejecutar Python mediante T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este tutorial explica cómo se puede ejecutar código de Python en SQL Server 2017. Se le guiará a través del proceso de mover datos entre SQL Server y Python y se explica cómo ajustar el código de Python correcto en un procedimiento almacenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para compilar, entrenar y usar modelos de aprendizaje automático en SQL Servidor.

## <a name="prerequisites"></a>Requisitos previos

Para completar este tutorial, primero debe instalar SQL Server 2017 y habilitar los servicios Machine Learning en la instancia, como se describe en [instalar SQL Server 2017 Machine Learning Services (In-Database)](../install/sql-machine-learning-services-windows-install.md). 

También debe instalar [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms). Como alternativa, puede usar otra base de datos herramienta de administración o una consulta, siempre se puede conectar a un servidor y base de datos y ejecutar una consulta de Transact-SQL o procedimiento almacenado.

Una vez completado el programa de instalación, vuelva a este tutorial, para obtener información sobre cómo ejecutar código de Python en el contexto de un procedimiento almacenado. 

## <a name="overview"></a>Información general

Este tutorial incluye cuatro lecciones:

+ Los conceptos básicos sobre cómo mover datos entre SQL Server y Python: Obtenga información sobre los requisitos básicos, las estructuras de datos, las entradas y salidas.
+ Practicar el uso de procedimientos almacenados para tareas sencillas de Python, como cargar datos de ejemplo.
+ Usar procedimientos almacenados para crear un modelo de aprendizaje automático de Python y generar puntuaciones a partir del modelo.
+ Una lección opcional para los usuarios que se va a ejecutar Python desde un cliente remoto, utilizando SQL Server como el _contexto de proceso_. Incluye código para generar un modelo; Sin embargo, requiere que ya están un poco familiarizado con las herramientas de Python y entornos de Python.

Aquí se ofrecen ejemplos de Python adicionales específicas de SQL Server 2017: [tutoriales de Python de SQL Server](../tutorials/sql-server-python-tutorials.md)

## <a name="verify-that-python-is-enabled-and-the-launchpad-is-running"></a>Comprobar que Python está habilitado y el Launchpad se está ejecutando

1. En Management Studio, ejecute esta instrucción para asegurarse de que se ha habilitado el servicio.

    ```sql
    sp_configure 'external scripts enabled'
    ```

    Si **run_value** es 1, la característica de aprendizaje de la máquina está instalada y lista para usarse.

    Una causa común de errores es que el Launchpad, que administra la comunicación entre SQL Server y Python, se ha detenido. Puede ver el estado de Launchpad mediante el uso de la Windows **servicios** panel o abrir el Administrador de configuración de SQL Server. Si el servicio se ha detenido, reinícielo.

2. A continuación, compruebe que el runtime de Python está trabajando y comunicarse con SQL Server. Para ello, abra una nueva **consulta** ventana en SQL Server Management Studio y conéctese a la instancia donde se ha instalado Python.

    ```sql
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'print(3+4)'
    ```

    Si todo es correcto, verá un mensaje de resultado como este

    ```text
    STDOUT message(s) from external script: 
    7
    ```

3. Si se producen errores, hay una variedad de cosas que puede hacer para asegurarse de que el servidor y Python puede comunicarse. 

    Debe agregar el grupo de usuarios de Windows `SQLRUserGroup` como inicio de sesión en la instancia, para asegurarse de que Launchpad puede proporcionar comunicación entre Python y SQL Server. (El mismo grupo se usa para ambos R y ejecución de código de Python). Para obtener más información, consulte [autenticación implícita habilitada](../security/add-sqlrusergroup-to-database.md).
    
    Además, deberá habilitar los protocolos de red que se han deshabilitado o abrir el firewall para que SQL Server puedan comunicarse con los clientes externos. Para obtener más información, consulte [solucionar problemas de instalación](../common-issues-external-script-execution.md).

## <a name="basic-python-interaction"></a>Interacción básica de Python

Hay dos maneras de ejecutar código de Python en SQL Server:

+ Agregar un script de Python como un argumento de procedimiento almacenado del sistema, **sp_execute_external_script**
+ Desde un cliente remoto como Python, conectarse a SQL Server y ejecutar código con el servidor SQL Server como el contexto de cálculo. Esto requiere [revoscalepy](../python/what-is-revoscalepy.md).

El objetivo principal de este tutorial es para asegurarse de que puede usar Python en un procedimiento almacenado.

1. Ejecutar cierto código simple para ver cómo se pasan los datos y hacia atrás entre SQL Server y Python.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    print(c, d)
    '
    ```

2. Suponiendo que tiene todo está configurado correctamente y Python y SQL Server se comunican entre sí, se calcula el resultado correcto y la versión de Python `print` función devuelve el resultado a la **mensajes** windows.

    **Resultado**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```
    
    Al obtener **stdout** mensajes es útil al probar el código, más a menudo es necesario devolver los resultados en formato tabular, para que pueda usarlo en una aplicación o escribirlo en una tabla. 

Por ahora, recuerde estas reglas:

+ Todos los elementos de la `@script` el argumento debe ser código Python válido. 
+ El código debe seguir todas las reglas de Python con respecto a la sangría, los nombres de variable y así sucesivamente. Cuando se produce un error, compruebe el espacio en blanco y mayúsculas y minúsculas.
+ Si usa las bibliotecas que no se cargan de forma predeterminada, debe usar una instrucción de importación al principio de la secuencia de comandos para cargarlas. 
+ Si la biblioteca no está ya instalada, detener e instale el paquete de Python fuera de SQL Server, como se describe aquí: [instalar nuevos paquetes de Python en SQL Server](../python/install-additional-python-packages-on-sql-server.md)

## <a name="inputs-and-outputs"></a>Entradas y salidas

De forma predeterminada, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) acepta un único conjunto de entrada, que normalmente proporciona en forma de una consulta SQL válida. Otros tipos de entrada pueden pasarse como variables de SQL: por ejemplo, puede pasar un modelo entrenado como una variable, con una función de serialización como [pickle](https://docs.python.org/3.0/library/pickle.html) o [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) para escribir el modelo un formato binario.

El procedimiento almacenado devuelve un único Python [pandas](http://pandas.pydata.org/pandas-docs/stable/index.html) trama de datos como salida. Sin embargo puede generar modelos y valores escalares como variables. Por ejemplo, puede de salida de un modelo entrenado como una variable binaria y pasarlo a una instrucción INSERT de T-SQL para escribir ese modelo en una tabla. También puede generar trazados (en formato binario) o valores escalares (valores individuales, como la fecha y hora, transcurrido el tiempo para entrenar el modelo y así sucesivamente).

Por ahora, echemos un vistazo a solo el valor predeterminado las variables de entrada y salidas, `InputDataSet` y `OutputDataSet`. 

1. Ejecute el siguiente código para realizar algunos cálculos matemáticos y los resultados.

        ```sql
        execute sp_execute_external_script 
        @language = N'Python', 
        @script = N'
        a = 1
        b = 2
        c = a/b
        print(c)
        OutputDataSet = c
        '
        WITH RESULT SETS ((ResultValue float))
        ```

2. Debe obtener un error, ya que el código de Python genera un valor escalar, no una trama de datos.

        **Results**

        ```text
        line 43, in transform
            raise TypeError('OutputDataSet should be of type pandas.DataFrame')
        ```

3. Ahora veamos qué sucede cuando se pasa un conjunto de datos tabular a Python, mediante la variable de entrada predeterminada `InputDataSet`. 

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    OutputDataSet = InputDataSet
    ',
    @input_data_1 = N'SELECT 1 as Col1'
    ```

    El procedimiento almacenado devuelve un data.frame automáticamente, sin tener que hacer nada más en el código de Python.

    **Resultado**

    | No hay columnname|
    |------|
    | 1|

    De forma predeterminada, el único conjunto de datos de entrada tabular tiene el nombre, `InputDataSet`. Sin embargo, puede cambiar ese nombre mediante la adición de una línea como esta: `@input_data_1_name = N'myResultName'`.

    Nombres de columna usados por Python nunca se conservan en la salida. Aunque la consulta de entrada especifica el nombre de columna `Col1`, no se devuelve ese nombre, ni tampoco sería los encabezados de columna utilizados por el script de Python. Para especificar un tipo de datos y el nombre de columna cuando se devuelven los datos a SQL Server, use T-SQL `WITH RESULT SETS` cláusula.

4. En este ejemplo proporciona nuevos nombres de las variables de entrada y salidas.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    MyOutput = MyInput
    ',
    @input_data_1_name = N'MyInput',
    @input_data_1 = N'SELECT 1 as Col1',
    @output_data_1_name = N'MyOutput'
    WITH RESULT SETS ((ResultValue int))
    ```

    La cláusula de conjunto de resultados con define el esquema para la salida, ya que nunca se devuelven los nombres de columna de Python con la trama de datos.

    **Resultado**

    | ResultValue|
    |------|
    | 1|

5. Ahora Echemos un vistazo a un error típico de Python. Cambie la línea en el ejemplo anterior de `@input_data_1_name = N'MyInput'` a `@input_data_1_name = N'myinput'`.

    Errores de Python se pasan a usted como mensajes, por el servicio de satélite utilizado por SQL Server. Los mensajes pueden ser largos y se incluyen errores de SQL Server o del Launchpad además de los errores de Python, así que los paciente de indagar en el texto. El mensaje clave es en esta línea:

    ```text
    MyOutput = MyInput
    NameError: name 'MyInput' is not defined
    ```

    Recuerde que Python, como R, distingue mayúsculas de minúsculas. Por lo tanto, cuando se produce cualquier tipo de error, asegúrese de comprobar los nombres de variables y buscar los problemas con los tipos de datos, sangría y espaciado.

## <a name="python-data-structures"></a>Estructuras de datos de Python

SQL Server se basa en la versión de Python **pandas** paquete, que resulta ideal para trabajar con datos tabulares. Sin embargo, ya hemos visto que no se puede pasar un valor escalar de Python para SQL Server y espera que "simplemente funcione". En esta sección, revisaremos algunas definiciones de tipo de datos básicos para prepararse para problemas adicionales que podrían surgir cuando se pasan datos tabulares entre Python y SQL Server.

+ Una trama de datos es una tabla con _varios_ columnas.
+ Una sola columna de una trama de datos es un objeto de lista como llama a una serie.
+ Un valor único es una celda de una trama de datos y tiene que llamarse por índice.

¿Cómo podría exponer el resultado de un cálculo como una trama de datos único si data.frame requiere una estructura tabular? Una respuesta que se va a representar el único valor escalar como una serie, que fácilmente se convierte en una trama de datos. 

1. En este ejemplo se hace un simple cálculo matemático y se convierte un valor escalar en una serie. Una serie requiere un índice, que puede asignar manualmente, tal como se muestra a continuación, o mediante programación.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    print(c)
    s = pandas.Series(c, index =["simple math example 1"])
    print(s)
    '
    ```

2. Dado que la serie no se ha convertido en un data.frame, se devuelven los valores en la ventana de mensajes, pero puede ver que los resultados están en formato tabular más.

    **Resultado**

    ```text
    STDOUT message(s) from external script: 
    0.5
    simple math example 1    0.5
    dtype: float64
    ```

3. Para aumentar la longitud de la serie, puede agregar nuevos valores utilizando una matriz. 

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    s = pandas.Series([c,d])
    print(s)
    '
    ```

    Si no especifica un índice, se genera un índice que tiene valores empezando por 0 y finalizando con la longitud de la matriz.

    **Resultado**

    ```text
    STDOUT message(s) from external script: 
    0    0.5
    1    2.0
    dtype: float64
    ```

4. Si aumenta el número de **índice** valores, pero no agregue nuevos **datos** valores, los valores de datos se repiten para rellenar la serie.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
    print(s)
    '
    ```

    **Resultado**

    ```text
    STDOUT message(s) from external script: 
    0.5
    simple math example 1    0.5
    simple math example 2    0.5
    dtype: float64
    ```

### <a name="convert-series-to-data-frame"></a>Convertir serie en la trama de datos

Tener convertido nuestros resultados escalares matemáticas a una estructura tabular, necesitamos convertirlos a un formato que puede administrar SQL Server. 

1. Para convertir una serie en un data.frame, llame a la pandas [DataFrame](http://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe) método.

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    d = a*b
    s = pandas.Series([c,d])
    print(s)
    df = pd.DataFrame(s)
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
    ```

2. Tenga en cuenta que los valores de índice no son de salida, incluso si utiliza el índice para obtener los valores específicos de la trama de datos.

    **Resultado**

    |ResultValue|
    |------|
    |0.5|
    |2|

### <a name="output-values-into-dataframe-using-an-index"></a>Valores de salida en data.frame mediante un índice

Veamos cómo funciona la conversión a un data.frame con nuestros dos series que contiene los resultados de operaciones matemáticas sencillas. La primera tiene un índice de valores secuenciales generados por Python. El segundo usa un índice de valores de cadena arbitrario.

1. En este ejemplo se obtiene un valor de la serie que utiliza un índice entero.

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    d = a*b
    s = pandas.Series([c,d])
    print(s)
    df = pd.DataFrame(s, index=[1])
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
    ```

    Recuerde que el índice generado automáticamente comienza en 0. Pruebe a usar un valor fuera del intervalo índice y vea Qué sucede.

2. Ahora vamos a obtener un único valor desde el marco de datos que tiene un índice de cadena. 

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
    print(s)
    df = pd.DataFrame(s, index=["simple math example 1"])
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
    ```

    **Resultado**

    |ResultValue|
    |------|
    |0.5|

    Si intenta usar un índice numérico para obtener un valor de esta serie, obtendrá un error.

Este ejercicio se diseñó para darle una idea de cómo trabajar con estructuras de datos diferentes de Python y asegúrese de que obtener el resultado como una trama de datos correcto. Es posible que haya finalizado que generar un valor único, como una trama de datos es más problemas que vale la pena! Afortunadamente, puede pasar fácilmente todos los tipos de valores dentro y fuera del procedimiento almacenado como variables. Que se trata en la lección siguiente.

## <a name="tips"></a>Sugerencias

+ Los lenguajes de programación, Python es uno de los más flexible con respecto a las comillas simples y comillas dobles; son prácticamente intercambiables. 

    Sin embargo, T-SQL usa comillas simples solo determinadas acciones y el `@script` argumento usa comillas simples para delimitar el código de Python como una cadena Unicode. Por lo tanto, deberá revisar el código de Python y cambie algunos comillas simples por comillas dobles.

+ ¿No se puede encontrar el procedimiento almacenado, `sp_execute_external_script`? Esto significa que probablemente no ha terminado de configurar la instancia para admitir la ejecución de scripts externos. Después de ejecutar el programa de instalación de SQL Server 2017 y seleccionar Python como el lenguaje de aprendizaje automático, debe habilitar explícitamente la característica mediante `sp_configure`y, a continuación, reinicie la instancia. 

    Para obtener más información, consulte [instalar SQL Server 2017 Machine Learning Services (In-Database)](../install/sql-machine-learning-services-windows-install.md).

## <a name="next-steps"></a>Pasos siguientes

[Encapsule el código de Python en un procedimiento almacenado de SQL](wrap-python-in-tsql-stored-procedure.md)