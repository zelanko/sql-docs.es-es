---
title: Ejecutar Python mediante T-SQL | Documentos de Microsoft
ms.custom: 
ms.date: 02/28/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2017
dev_langs:
- Python
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 5c6145d3af6918a5f3daa954aae5522ffffebb89
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2018
---
# <a name="run-python-using-t-sql"></a>Ejecución de Python mediante T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este tutorial le explica cómo ejecutar código de Python en SQL Server 2017. Se le guía a través del proceso de mover datos entre SQL Server y Python y se explica cómo ajustar el código Python correcto en un procedimiento almacenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para crear, entrenar y usar modelos de aprendizaje automático de SQL Servidor.

## <a name="prerequisites"></a>Requisitos previos

Para completar este tutorial, primero debe instalar SQL Server 2017 y habilitar los servicios de aprendizaje de máquina en la instancia, tal y como se describe en [este artículo](../python/setup-python-machine-learning-services.md). 

También debe instalar [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms). Como alternativa, puede utilizar otra base de datos herramienta de administración o la consulta, siempre que se pueda conectar a un servidor y base de datos y ejecutar una consulta de T-SQL o un procedimiento almacenado.

Después de haber completado el programa de instalación, vuelva a este tutorial, para obtener información sobre cómo ejecutar el código de Python en el contexto de un procedimiento almacenado. 

## <a name="overview"></a>Información general

Este tutorial incluye cuatro lecciones:

+ Los conceptos básicos de mover datos entre SQL Server y Python: Obtenga información acerca de los requisitos básicos, las estructuras de datos, entradas y salidas.
+ Practicar el uso de procedimientos almacenados para tareas sencillas, Python, como cargar datos de ejemplo.
+ Usar procedimientos almacenados para crear un modelo de aprendizaje automático de Python y generar puntuaciones a partir del modelo.
+ Una lección opcional para los usuarios que se va a ejecutar Python desde un cliente remoto, con SQL Server como el _cálculo_. Incluye código para generar un modelo; Sin embargo, requiere que ya está un poco familiarizado con entornos de Python y las herramientas de Python.

Aquí se ofrecen ejemplos de Python adicionales específicas de SQL Server 2017: [tutoriales de SQL Server Python](../tutorials/sql-server-python-tutorials.md)

## <a name="verify-that-python-is-enabled-and-the-launchpad-is-running"></a>Compruebe que está habilitado Python y Launchpad está ejecutando

1. En Management Studio, ejecute esta instrucción para asegurarse de que se ha habilitado el servicio.

    ```sql
    sp_configure 'external scripts enabled'
    ```

    Si **run_value** es 1, la característica de aprendizaje de máquina está instalado y listo para usar.

    Una causa común de errores es que el Launchpad, que administra la comunicación entre SQL Server y Python, se ha detenido. Puede ver el estado de Launchpad, mediante las ventanas de **servicios** panel, o abrir el Administrador de configuración de SQL Server. Si el servicio se ha detenido, reinícielo.

2. A continuación, compruebe que el tiempo de ejecución de Python es funciona y se comunica con SQL Server. Para ello, abra una nueva **consulta** ventana en SQL Server Management Studio y conéctese a la instancia donde se instaló Python.

    ```sql
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'print(3+4)'
    ```

    Si todo es correcto, verá un mensaje de resultado como este

    ```text
    STDOUT message(s) from external script: 
    7
    ```

3. Si se producen errores, hay una variedad de cosas que puede hacer para asegurarse de que puede comunicarse el servidor y Python. 

    Debe agregar el grupo de usuarios de Windows `SQLRUserGroup` como un inicio de sesión en la instancia, para asegurarse de que Launchpad puede permitir la comunicación entre Python y SQL Server. (El mismo grupo se usa para ambos R y la ejecución de código Python.) Para obtener más información, consulte [autenticación implícita habilitado](../r/add-sqlrusergroup-to-database.md).
    
    Además, deberá habilitar los protocolos de red que se han deshabilitado, o abra el firewall para que SQL Server pueda comunicarse con clientes externos. Para obtener más información, consulte [solucionar problemas de instalación](../common-issues-external-script-execution.md).

## <a name="basic-python-interaction"></a>Interacción básica de Python

Hay dos maneras de ejecutar código Python en SQL Server:

+ Agregar un script de Python como un argumento de procedimiento almacenado del sistema, **sp_execute_external_script**
+ Desde un cliente remoto de Python, conectarse a SQL Server y ejecutar código que usa el servidor SQL Server como el contexto de proceso. Para ello, [revoscalepy](../python/what-is-revoscalepy.md).

El objetivo principal de este tutorial consiste en asegurarse de que puede utilizar Python en un procedimiento almacenado.

1. Ejecutar un código sencillo para ver cómo se pasan los datos y hacia atrás entre SQL Server y Python.

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

2. Suponiendo que todo lo configurado correctamente tiene y Python y SQL Server se comunican entre sí, se calcula el resultado correcto y la versión de Python `print` función devuelve el resultado a la **mensajes** windows.

    **Resultado**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```
    
    Al obtener **stdout** mensajes es útil cuando se prueba el código, más a menudo es necesario devolver los resultados en formato tabular, por lo que puede usar en una aplicación o escribir en una tabla. 

Por ahora, recuerde estas reglas:

+ Todos los datos la `@script` el argumento debe ser válido código Python. 
+ El código debe seguir todas las reglas Pythonic relacionadas con sangría, los nombres de variable y así sucesivamente. Cuando se recibe un error, compruebe el espacio en blanco y mayúsculas y minúsculas.
+ Si está utilizando las bibliotecas que no se cargan de forma predeterminada, debe usar una instrucción import al principio de la secuencia de comandos para cargarlos. 
+ Si la biblioteca no está ya instalada, detener e instale el paquete de Python fuera de SQL Server, como se describe aquí: [instalar nuevos paquetes de Python en SQL Server](../python/install-additional-python-packages-on-sql-server.md)

## <a name="inputs-and-outputs"></a>Entradas y salidas

De forma predeterminada, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) acepta un único conjunto de entrada, que normalmente se proporciona en forma de una consulta SQL válida. Otros tipos de entrada pueden pasarse como variables de SQL: por ejemplo, puede pasar un modelo entrenado como una variable, con una función de serialización como [pickle](https://docs.python.org/3.0/library/pickle.html) o [rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) para escribir el modelo un formato binario.

El procedimiento almacenado devuelve un único Python [pandas](http://pandas.pydata.org/pandas-docs/stable/index.html) trama de datos como salida. Sin embargo puede generar modelos y valores escalares como variables. Por ejemplo, puede generar un modelo entrenado como una variable binario y pasarlo a una instrucción INSERT de T-SQL para escribir ese modelo en una tabla. También puede generar gráficos (en formato binario) o valores escalares (valores individuales, como la fecha y hora, transcurrido el tiempo para entrenar el modelo y así sucesivamente).

Por ahora, echemos un vistazo a simplemente el valor predeterminado variables de entrada y salidas, `InputDataSet` y `OutputDataSet`. 

1. Ejecute el siguiente código para realizar algunos cálculos y generará los resultados.

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

2. Debe obtener un error, porque el código Python genera un valor escalar, no una trama de datos.

        **Results**

        ```text
        line 43, in transform
            raise TypeError('OutputDataSet should be of type pandas.DataFrame')
        ```

3. Ahora vea lo que ocurre cuando se pasa un conjunto de datos tabular a Python, mediante la variable de entrada predeterminado `InputDataSet`. 

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    OutputDataSet = InputDataSet
    ',
    @input_data_1 = N'SELECT 1 as Col1'
    ```

    El procedimiento almacenado devuelve un data.frame automáticamente, sin tener que hacer nada más en el código Python.

    **Resultado**

    | No hay columnname|
    |------|
    | 1|

    De forma predeterminada, el único conjunto de datos de entrada tabular tiene el nombre, `InputDataSet`. Sin embargo, puede cambiar ese nombre agregando una línea como esta: `@input_data_1_name = N'myResultName'`.

    Nombres de columna utilizados por Python nunca se conservan en la salida. Aunque la consulta de entrada especifica el nombre de columna `Col1`, no se devuelve ese nombre, ni tendría los encabezados de columna utilizados por el script de Python. Para especificar un tipo de datos y el nombre de columna cuando se devuelven los datos a SQL Server, utilice el código T-SQL `WITH RESULT SETS` cláusula.

4. Este ejemplo proporciona nuevos nombres de las variables de entrada y salidas.

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

    La cláusula con conjunto de resultados define el esquema para la salida, ya que nunca se devuelven los nombres de columna de Python con el data.frame.

    **Resultado**

    | ResultValue|
    |------|
    | 1|

5. Ahora Echemos un vistazo a un error típico de Python. Cambie la línea en el ejemplo anterior de `@input_data_1_name = N'MyInput'` a `@input_data_1_name = N'myinput'`.

    Errores de Python se pasan a usted como mensajes, por el servicio de satélite utilizado por SQL Server. Los mensajes pueden ser largos e incluir errores de SQL Server o errores de Launchpad además de errores de Python, por lo que debe paciente en profundizando a través del texto. El mensaje clave está en esta línea:

    ```text
    MyOutput = MyInput
    NameError: name 'MyInput' is not defined
    ```

    Recuerde que Python, como R, distingue mayúsculas de minúsculas. Por lo tanto, cuando se obtiene ningún tipo de error, asegúrese de comprobar los nombres de variable y buscar los problemas con los tipos de datos, sangría y espaciado.

## <a name="python-data-structures"></a>Estructuras de datos de Python

SQL Server se basa en la versión de Python **pandas** paquete, que es muy útil para trabajar con datos tabulares. No obstante, ya ha detectado que no se puede pasar un valor escalar de Python para SQL Server y esperan que "simplemente funcione". En esta sección, analizaremos algunas definiciones de tipo de datos básicos para prepararse para problemas adicionales que puede ejecutar a través de cuando se pasan datos tabulares entre Python y SQL Server.

+ Una trama de datos es una tabla con _varios_ columnas.
+ Una sola columna de una trama de datos, es un objeto de lista llamado a una serie.
+ Un valor único es una celda de una trama de datos y es necesario llamar por su índice.

Entonces, ¿cómo se expondría el único resultado de un cálculo como una trama de datos, si un data.frame requiere una estructura tabular? Una respuesta que se va a representar el único valor escalar como una serie, que se puede convertir fácilmente a una trama de datos. 

1. En este ejemplo se hace un simple cálculo matemático y se convierte un valor escalar en una serie. Una serie requiere un índice, lo que puede asignar manualmente, como se muestra aquí, o mediante programación.

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

2. Dado que la serie no se ha convertido en un data.frame, los valores se devuelven en la ventana de mensajes, pero puede ver que los resultados están en un formato más tabular.

    **Resultado**

    ```text
    STDOUT message(s) from external script: 
    0.5
    simple math example 1    0.5
    dtype: float64
    ```

3. Para aumentar la longitud de la serie, puede agregar nuevos valores, utilizando una matriz. 

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

    Si no especifica un índice, se genera un índice que tenga valores empezando por 0 y terminando con la longitud de la matriz.

    **Resultado**

    ```text
    STDOUT message(s) from external script: 
    0    0.5
    1    2.0
    dtype: float64
    ```

4. Si se aumenta el número de **índice** valores, pero no agregue nuevos **datos** valores, los valores de datos se repiten para rellenar la serie.

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

### <a name="convert-series-to-data-frame"></a>Convertir serie en la trama de datos.

Tener, nuestros resultados escalares matemáticas se convierte en una estructura tabular, necesitamos convertirlos a un formato que puede administrar SQL Server. 

1. Para convertir una serie en un data.frame, llame a la pandas [trama de datos](http://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe) método.

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

2. Tenga en cuenta que los valores de índice no son de salida, incluso si utiliza el índice para obtener valores específicos de la data.frame.

    **Resultado**

    |ResultValue|
    |------|
    |0.5|
    |2|

### <a name="output-values-into-dataframe-using-an-index"></a>Valores de salida en data.frame mediante un índice

Veamos cómo funciona la conversión a un data.frame con nuestras dos series que contiene los resultados de las operaciones matemáticas simple. La primera tiene un índice de valores secuenciales generados por Python. El segundo usa un índice arbitrario de valores de cadena.

1. En este ejemplo se obtiene un valor de la serie que utiliza un índice de entero.

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

2. Ahora vamos a obtener un valor único de la trama de datos que tiene un índice de cadena. 

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

Este ejercicio se ha diseñado para proporcionarle una idea de cómo trabajar con distintas estructuras de datos de Python y asegúrese de que obtener el resultado correcto como una trama de datos. Posible que haya finalizado esa salida de un solo valor como una trama de datos es más problemas para que su valor. Afortunadamente, puede pasar fácilmente todos los tipos de valores dentro y fuera del procedimiento almacenado como variables. Que se trata en la siguiente lección.

## <a name="tips"></a>Sugerencias

+ Entre los lenguajes de programación Python es uno de los más flexible con respecto a las comillas simples y comillas dobles; se trata prácticamente intercambiables. 

    Sin embargo, T-SQL usa comillas simples para sólo determinadas tareas y el `@script` argumento utiliza comillas simples para delimitar el código Python como una cadena Unicode. Por lo tanto, necesitará revisar el código Python y cambiar algunos comillas simples a las comillas dobles.

+ ¿No se puede encontrar el procedimiento almacenado, `sp_execute_external_script`? Significa que probablemente no ha terminado de configurar la instancia para admitir la ejecución de scripts externos. Después de ejecutar el programa de instalación de SQL Server 2017 y seleccionar Python como el lenguaje de aprendizaje automático, debe habilitar explícitamente la característica mediante `sp_configure`y, a continuación, reinicie la instancia. 

    Para obtener más información, consulte [programa de instalación de servicios de aprendizaje de máquina con Python](../python/setup-python-machine-learning-services.md).

## <a name="next-steps"></a>Pasos siguientes

[Incluir código Python en un procedimiento almacenado de SQL](wrap-python-in-tsql-stored-procedure.md)