---
title: 'Actualizado: Advanced Analytics para documentos de SQL Server | Documentos de Microsoft'
description: Mostrar fragmentos de contenido actualizado para recientemente modificadas en documentación, Advanced Analytics para Microsoft SQL Server.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: advanced-analytics
ms.date: 04/28/2018
ms.openlocfilehash: bbce32579b54647e167c25d2708a80027ae0e678
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-advanced-analytics-for-sql-server"></a>Nuevos y actualizados recientemente: análisis avanzados para SQL Server



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su [Docs.Microsoft.com](http://docs.microsoft.com/) sitio Web de documentación. Este artículo muestra extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

En este artículo es generado por un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto, o como marcado del artículo de origen. Nunca las imágenes se muestran aquí.

Actualizaciones recientes se notifican para el siguiente intervalo de fechas y el asunto:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **2018-02-03** &nbsp; - a - &nbsp; **2018-04-28**
- *Área de asunto:* &nbsp; **Advanced Analytics para SQL Server**.

<!-- Repo = 'MicrosoftDocs/sql-docs'.   Branch = 'live'. -->



&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


1. [Instalar equipo con SQL Server de 2017 aprendizaje Services (en bases de datos) en Windows](install/sql-machine-learning-services-windows-install.md)
2. [Instalar Server (independiente) en Windows de aprendizaje de máquina SQL Server de 2017](install/sql-machine-learning-standalone-windows-install.md)
3. [Instalar componentes de aprendizaje de máquina de SQL Server desde la línea de comandos](install/sql-ml-component-commandline-install.md)
4. [Instalar componentes sin acceso a internet de aprendizaje de automático de SQL Server](install/sql-ml-component-install-without-internet-access.md)
5. [Instalar SQL Server 2016 R Services (en bases de datos)](install/sql-r-services-windows-install.md)
6. [Instalar a SQL Server 2016 R Server (independiente)](install/sql-r-standalone-windows-install.md)
7. [Configurar Python herramientas de cliente para su uso con aprendizaje automático de SQL Server](python/setup-python-client-tools-sql.md)
8. [Utilizar el modelo de Python en SQL para el entrenamiento y de puntuación](tutorials/train-score-using-python-in-tsql.md)
9. [Incluir código Python en un procedimiento almacenado](tutorials/wrap-python-in-tsql-stored-procedure.md)
10. [¿Qué es SQL Server Machine Learning Services?](what-is-sql-server-machine-learning.md)
11. [Eventos extendidos para la supervisión de instrucciones PREDICT](xe-event-predict-tsql.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

En esta sección se muestran extractos de actualizaciones recopiladas de artículos que han sufrido una actualización importante recientemente.

Los extractos que se muestran aquí aparecen separados de su contexto semántica correcta. Además, en ocasiones, un extracto se separa de la sintaxis de markdown importante que rodea en el artículo real. Por lo tanto, estos extractos son para obtener instrucciones generales solo. Los extractos de sólo le permiten saber si sus intereses garantizan dedicar tiempo a haga clic en y visite el artículo real.

Por estas y otras razones, no se copie el código de estos fragmentos y no toma como verdaderos exacta cualquier fragmento de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact lista de artículos que se actualizó recientemente

En esta lista compacta se proporcionan vínculos a todos los artículos actualizados que aparecen en la sección de extractos.

1. [Visualización de R o paquetes de Python instalados en SQL Server](#TitleNum_1)
2. [Instalar previamente entrenado máquina aprendizaje de los modelos en SQL Server](#TitleNum_2)
3. [Configurar un cliente de ciencia de datos para el desarrollo de R en SQL Server](#TitleNum_3)
4. [SQL Server del equipo aprendizaje y R Services (en bases de datos)](#TitleNum_4)
5. [Ejecución de Python mediante T-SQL](#TitleNum_5)
6. [Usar Python con revoscalepy para crear un modelo](#TitleNum_6)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-viewing-r-or-python-packages-installed-on-sql-serverrdetermine-which-packages-are-installed-on-sql-servermd"></a>1. &nbsp; [Visualización de R o paquetes de Python instalados en SQL Server](r/determine-which-packages-are-installed-on-sql-server.md)

*Actualizado: 2018-04-19* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([siguiente](#TitleNum_2))

<!-- Source markdown line 208.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 7a1df11f57e7bbf0abc37d3aa240dedd2b88c45f ec6859ac91b27539dc36f21aec82c99937c0187a  (PR=5610  ,  Filename=determine-which-packages-are-installed-on-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f1f96a990644c0d6cfa5a1d88ccee959cab6c2b2) -->



**Python**


Este ejemplo devuelve la lista de carpetas incluidas en la versión de Python `sys.path` variable. La lista incluye el directorio actual y la ruta de acceso de la biblioteca estándar.

```
EXEC sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

**Resultado**

```
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\python35.zip
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\DLLs
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Sphinx-1.5.4-py3.5.egg
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Pythonwin
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\setuptools-27.2.0-py3.5.egg
```

Para obtener más información acerca de la variable `sys.path` y cómo se utiliza para establecer la ruta de búsqueda del intérprete de módulos, vea el [documentación de Python](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-install-pre-trained-machine-learning-models-on-sql-serverrinstall-pretrained-models-sql-servermd"></a>2. &nbsp; [Instalar previamente entrenado máquina aprendizaje de los modelos en SQL Server](r/install-pretrained-models-sql-server.md)

*Actualizado: 2018-04-12* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_1) | [siguiente](#TitleNum_3))

<!-- Source markdown line 140.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 aa03623d819750d4919feb7910b07ec1875bb509 7382228fa68b04b500a5fde73c29995e12aa20ac  (PR=5504  ,  Filename=install-pretrained-models-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f34765240b79a44167ca2af90f97a0fdd47c41d2) -->



1. Inicie el instalador independiente basado en Windows para cada uno [R Server](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server) o [servidor de aprendizaje de máquina](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).

2. Seleccione los idiomas que desea actualizar y seleccione el **Pre-trained modelos** opción.

    > [!TIP]
    > Si ya ha ejecutado el programa de instalación para actualizar el servidor de R (independiente) y sólo desea agregar los modelos previamente entrenados, deje todas las selecciones anteriores **sea**y seleccione solo la anterior **-entrenar modelos** opción . **No** anule la selección de las opciones seleccionadas previamente; si lo hace, el programa de instalación quita los componentes.

    Se recomienda que acepte la configuración predeterminada para las ubicaciones de modelo.

3. Haga clic en **Continuar**.

4. Acepte todos los demás mensajes, incluidos los contratos de licencia.

Una vez completada la instalación, debe realizar algunos pasos adicionales para registrar los modelos entrenados previamente.

1. Abra un símbolo del sistema de Windows **como administrador**.

2. Navegue hasta la carpeta de instalación de arranque para R Server (independiente), que también contiene el programa de instalación de Microsoft R.

3. Ejecutar `RSetup.exe` e indicar el componente para instalar, la versión y la carpeta que contiene los archivos de origen del modelo, con esta sintaxis:

    `RSetup.exe /install /component MLM /version <version> /language 1033 /destdir "~\R_SERVER\library\MicrosoftML\mxLibs\x64"`

    Se admiten los siguientes valores para el parámetro de versión:



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-set-up-a-data-science-client-for-r-development-on-sql-serverrset-up-a-data-science-clientmd"></a>3. &nbsp; [Configurar un cliente de ciencia de datos para el desarrollo de R en SQL Server](r/set-up-a-data-science-client.md)

*Actualizado: 2018-04-12* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_2) | [siguiente](#TitleNum_4))

<!-- Source markdown line 39.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0583f8febcedc5dc2e14ca1a8073ca204ca37987 3d50ad8f35f2985944741a9b2211a461df2c13e4  (PR=5504  ,  Filename=set-up-a-data-science-client.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f34765240b79a44167ca2af90f97a0fdd47c41d2) -->



**Herramientas de R**


Cuando se instala R con SQL Server, obtendrá las mismas herramientas de R que se instalan con cualquier **base** instalación de R, como RGui, Rterm y así sucesivamente. Por lo tanto, técnicamente, tiene todas las herramientas que necesarias para desarrollar y probar código R.

Se incluyen las siguientes herramientas estándares de R en un *base instalación* de R y por lo tanto, se instalan de forma predeterminada.

+ **RTerm**: un terminal de línea de comandos para ejecutar scripts de R

+ **RGui.exe**: sencillo editor interactivo de R. Los argumentos de la línea de comandos son los mismos en RGui.exe y en RTerm.

+ **RScript**: herramienta de línea de comandos para ejecutar scripts de R en el modo por lotes.

Para encontrar estas herramientas, determine la biblioteca de R que se instala al configurar SQL Server o la característica de aprendizaje de automático de independiente. Por ejemplo, en una instalación predeterminada, las herramientas de R se encuentran en estas carpetas:

+ SQL Server 2016 R Services: `~\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64`
+ Microsoft R Server independiente: `~\Program Files\Microsoft R\R_SERVER\bin\x64`
+ Equipo con SQL Server de 2017 servicios de aprendizaje: `~\Program Files\Microsoft SQL Server\MSSQL14.<instancename>\R_SERVICES\bin\x64`
+ Server (independiente) de aprendizaje automático: `~\Program Files\Microsoft\ML Server\R_SERVER\bin\x64`

Si necesita ayuda con las herramientas de R, simplemente abra **RGui**, haga clic en **ayuda**y seleccione una de las opciones

**Cliente de Microsoft R**


Cliente de Microsoft R es una descarga gratuita que proporciona acceso a los paquetes de RevoScaleR para fines de desarrollo. Al instalar el cliente de R, puede crear soluciones de R que se pueden ejecutar en todos los contextos de proceso admitidos, incluidos el análisis de en bases de datos de SQL Server y computación distribuida R en Hadoop, Spark o Linux con el servidor de aprendizaje de máquina.

Si ya ha instalado un entorno de desarrollo de R diferente, como RStudio, asegúrese de volver a configurar el entorno para usar las bibliotecas y ejecutables proporcionados por Microsoft R cliente. Por lo que puede usar todas las características del paquete RevoScaleR, aunque el rendimiento será limitada.



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-sql-server-machine-learning-and-r-services-in-databasersql-server-r-servicesmd"></a>4. &nbsp; [SQL Server del equipo aprendizaje y R Services (en bases de datos)](r/sql-server-r-services.md)

*Actualizado: 2018-04-12* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_3) | [siguiente](#TitleNum_5))

<!-- Source markdown line 83.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b1a95a7f6d391a518762eb271e8ea7e0d684d403 7fbfabf62917e03e2bcb99d297e1c9d0f0604440  (PR=5504  ,  Filename=sql-server-r-services.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f34765240b79a44167ca2af90f97a0fdd47c41d2) -->



Elegir el mejor lenguaje para la tarea. R es más adecuado para realizar cálculos estadísticos que son difíciles de implementar mediante SQL. Para las operaciones basadas en conjunto sobre datos, aprovechan la eficacia del *{incluidos contenido-va aquí}* para lograr un rendimiento máximo. Usar el motor de base de datos en memoria para realizar cálculos muy rápidos a través de las columnas.

**Paso 4: Optimizar la solución**


Cuando el modelo está listo para escalar de datos empresariales, los científicos de datos a menudo funciona con el programador de DBA o SQL para optimizar los procesos, como:

+ Ingeniería de características
+ Recopilación de datos y transformación de datos
+ Puntuaciones

Tradicionalmente científicos de datos con R han tenido problemas con el rendimiento y la escalabilidad, especialmente cuando se usa el conjunto de datos grande. Eso es porque la implementación en tiempo de ejecución común es de subproceso único y puede dar cabida a los conjuntos de datos que caben en la memoria disponible en el equipo local. Integración con servicios de aprendizaje de máquina de SQl Server proporciona varias características para mejorar el rendimiento, con más datos:

+ **RevoScaleR**: paquete de R esta contiene implementaciones de algunas de las funciones de R más populares, rediseñadas para ofrecer paralelismo y escalabilidad. El paquete también incluye funciones que aumentan aún más el rendimiento y la escalabilidad mediante la inserción de cálculos a la *{incluidos contenido-va aquí}* equipo, que normalmente tiene mayor memoria y potencia de cálculo.

+ **revoscalepy**. Esta biblioteca de Python, disponible en SQL Server 2017, implementa las funciones más populares en RevoScaleR, por ejemplo, los contextos de proceso remoto y el procesamiento distribuyen de muchos algoritmos que admiten.

**Recursos**

+ [Caso práctico de rendimiento]
+ [R y la optimización de datos]

**Paso 5: Implementar y consumir**




&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-run-python-using-t-sqltutorialsrun-python-using-t-sqlmd"></a>5. &nbsp; [Ejecución de Python mediante T-SQL](tutorials/run-python-using-t-sql.md)

*Actualizado: 2018-04-11* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_4) | [siguiente](#TitleNum_6))

<!-- Source markdown line 306.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 bde8c6476df259d225847c08224cefd02f3529d5 cad56997abe7928b588ac4a0302384c5edc1ede5  (PR=5497  ,  Filename=run-python-using-t-sql.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=86c4e1879c5914676b9da384ab101b50b4a63bf1) -->



2. Tenga en cuenta que los valores de índice no son de salida, incluso si utiliza el índice para obtener valores específicos de la data.frame.

    **Resultado**

    |ResultValue|
    |------|
    |0.5|
    |2|

**Valores de salida en data.frame mediante un índice**


Veamos cómo funciona la conversión a un data.frame con nuestras dos series que contiene los resultados de las operaciones matemáticas simple. La primera tiene un índice de valores secuenciales generados por Python. El segundo usa un índice arbitrario de valores de cadena.

1. En este ejemplo se obtiene un valor de la serie que utiliza un índice de entero.

```
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

```
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



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-use-python-with-revoscalepy-to-create-a-modeltutorialsuse-python-revoscalepy-to-create-modelmd"></a>6. &nbsp; [Usar Python con revoscalepy para crear un modelo](tutorials/use-python-revoscalepy-to-create-model.md)

*Actualizado: 2018-04-11* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_5))

<!-- Source markdown line 22.  ms.author= heidist.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5b642b391ca571412c30c8470875d3d4d3c57246 bd83387eb8a1076a1396bbd48dca12872843aa2f  (PR=5497  ,  Filename=use-python-revoscalepy-to-create-model.md  ,  Dirpath=docs\advanced-analytics\tutorials\  ,  MergeCommitSha40=86c4e1879c5914676b9da384ab101b50b4a63bf1) -->



Si instaló una versión preliminar de SQL Server 2017, debe actualizar al menos la versión RTM. Las versiones posteriores de servicio han continuado expandir y mejorar la funcionalidad de Python. Algunas características de este tutorial podrían no funcionar en las primeras versiones preliminares.

+ Este ejemplo usa un entorno de Python predefinido, denominado `PYTEST_SQL_SERVER`. Se ha configurado el entorno para contener **revoscalepy** y otras bibliotecas necesarias.

    Si no tiene un entorno configurado para ejecutarse Python, debe hacerlo por separado. La explicación de cómo crear o modificar entornos de Python queda fuera del ámbito de este tutorial. Para obtener más información acerca de cómo configurar un cliente de Python que contenga las bibliotecas correctas, consulte [cliente instalar Python](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) y [vínculo Python herramientas](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools).

**Revoscalepy y contextos de proceso remoto**


En este ejemplo se muestra el proceso de creación de un modelo de Python en un equipo remoto _contexto de proceso_, que permite trabajar desde un cliente, pero elija un entorno remoto, como SQL Server, Spark o servidor de aprendizaje de máquina, donde el las operaciones se realizan en realidad. Uso contextos de proceso hace que sea más fácil escribir el código una vez e implementarla en cualquier entorno compatible con.

Para ejecutar el código de Python en SQL Server requiere la **revoscalepy** paquete. Se trata de un paquete de Python especial suministrado por Microsoft, similar a la **RevoScaleR** paquete para el lenguaje R. El **revoscalepy** paquete es compatible con la creación de contextos de proceso y proporciona la infraestructura para pasar los datos y modelos entre una estación de trabajo local y un servidor remoto. El **revoscalepy** función compatible con la ejecución de código de base de datos está [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver).







## <a name="similar-articles-about-new-or-updated-articles"></a>Artículos similares sobre artículos nuevos o actualizados

En esta sección se enumeran artículos muy similares a los artículos actualizados recientemente en otras áreas temáticas, dentro de nuestro repositorio público de GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Áreas temáticas *con* artículos nuevos o actualizados recientemente

- [Nuevos y actualizados (11 + 6): &nbsp; &nbsp; **Advanced Analytics para SQL** documentos](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos y actualizados (18 + 0): &nbsp; &nbsp; **Analysis Services para SQL** documentos](../analysis-services/new-updated-analysis-services.md)
- [Nuevos y actualizados (218 + 14): **conectar con SQL Server** documentos](../connect/new-updated-connect.md)
- [Nuevos y actualizados (14 + 0): &nbsp; &nbsp; **motor de base de datos de SQL** documentos](../database-engine/new-updated-database-engine.md)
- [Nuevos y actualizados (3 + 2): &nbsp; &nbsp; **Integration Services para SQL** documentos](../integration-services/new-updated-integration-services.md)
- [Nuevos y actualizados (3 + 3): &nbsp; &nbsp; **Linux para SQL** documentos](../linux/new-updated-linux.md)
- [Nuevos y actualizados (10 + 7): &nbsp; &nbsp; **bases de datos relacionales de SQL** documentos](../relational-databases/new-updated-relational-databases.md)
- [Nuevos y actualizados (0 + 2): &nbsp; &nbsp; **Reporting Services para SQL** documentos](../reporting-services/new-updated-reporting-services.md)
- [Nuevos y actualizados (1 + 3): &nbsp; &nbsp; **Studio de operaciones SQL** documentos](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Nuevos y actualizados (2 + 3): &nbsp; &nbsp; **Microsoft SQL Server** documentos](../sql-server/new-updated-sql-server.md)
- [Nuevos y actualizados (1 + 1): &nbsp; &nbsp; **SQL Server Data Tools (SSDT)** documentos](../ssdt/new-updated-ssdt.md)
- [Nuevos y actualizados (5 + 2): &nbsp; &nbsp; **SQL Server Management Studio (SSMS)** documentos](../ssms/new-updated-ssms.md)
- [Nuevos y actualizados (0 + 2): &nbsp; &nbsp; **Transact-SQL** documentos](../t-sql/new-updated-t-sql.md)
- [Nuevos y actualizados (1 + 1): &nbsp; &nbsp; **Tools para SQL** documentos](../tools/new-updated-tools.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Áreas temáticas que *no* tienen artículos nuevos o actualizados recientemente

- [Nuevos y actualizados (0 + 0): **Analytics Platform System para SQL** documentos](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Nuevos y actualizados (0 + 0): **Data Quality Services para SQL** documentos](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos y actualizados (0 + 0): **extensiones de minería de datos (DMX) para SQL** documentos](../dmx/new-updated-dmx.md)
- [Nuevos + actualizados (0+0): documentos de **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Nuevos y actualizados (0 + 0): **expresiones multidimensionales (MDX) para SQL** documentos](../mdx/new-updated-mdx.md)
- [Nuevos y actualizados (0 + 0): **ODBC (conectividad abierta de base de datos) para SQL** documentos](../odbc/new-updated-odbc.md)
- [Nuevos y actualizados (0 + 0): **PowerShell para SQL** documentos](../powershell/new-updated-powershell.md)
- [Nuevos y actualizados (0 + 0): **ejemplos para SQL** documentos](../samples/new-updated-samples.md)
- [Nuevos y actualizados (0 + 0): **SQL Server Migration Assistant (SSMA)** documentos](../ssma/new-updated-ssma.md)
- [Nuevos y actualizados (0 + 0): **XQuery para SQL** documentos](../xquery/new-updated-xquery.md)

