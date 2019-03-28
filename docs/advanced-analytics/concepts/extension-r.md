---
title: SQL Server Machine Learning - extensión del lenguaje de programación R
description: Obtenga información sobre la ejecución de código de R y las bibliotecas integradas de R en SQL Server 2016 R Services o SQL Server 2017 Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: c3f72a755d0ca75ca699465f7eb7a62ea48ff81f
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58511372"
---
# <a name="r-language-extension-in-sql-server"></a>Extensión del lenguaje R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

La extensión de R es parte del complemento SQL Server Machine Learning Services para el motor de base de datos relacional. Agrega un entorno de ejecución de R, la distribución básica de R con herramientas y las bibliotecas estándar y las bibliotecas de R de Microsoft: [RevoScaleR](../r/ref-r-revoscaler.md) para el análisis a escala, [MicrosoftML](../r/ref-r-microsoftml.md) para algoritmos de aprendizaje automático y otras bibliotecas para tener acceso a datos o código de R en SQL Server.

Integración de R está disponible en SQL Server a partir de SQL Server 2016, [R Services](../r/sql-server-r-services.md)y continuando hacia delante como parte de [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md).

## <a name="r-components"></a>Componentes de R

SQL Server incluye paquetes de código abierto y propietarios. Las bibliotecas de R bases se instalan a través de la distribución de Microsoft de código abierto R: Microsoft R Open (MRO). Los usuarios actuales de R deben ser capaz de portar su código de R y ejecutarlo como un proceso externo en SQL Server con pocas o ninguna modificación. MRO se instala independientemente de las herramientas de SQL y se ejecuta fuera de los procesos de motor de core, en el marco de extensibilidad. Durante la instalación, debe dar su consentimiento a los términos de la licencia de código abierto. A partir de entonces, puede ejecutar paquetes de R estándares sin modificaciones adicionales como haría en cualquier otra distribución de código abierto de R. 

SQL Server no modifica los archivos ejecutables de R bases, pero debe usar la versión de R instalado el programa de instalación porque esa versión es la que los paquetes de propiedad se crearon y probaron. Para obtener más información acerca de cómo MRO difiere de una distribución de base de R que puede obtener desde CRAN, consulte [interoperabilidad con el lenguaje R y productos de Microsoft R y funciones](https://docs.microsoft.com/r-server/what-is-r-server-interoperability).

La distribución de paquetes base de R instalada por el programa de instalación puede encontrarse en la carpeta asociada con la instancia. Por ejemplo, si instaló R Services en una instancia predeterminada de SQL Server 2016, las bibliotecas de R se encuentran en esta carpeta de forma predeterminada: `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`. De forma similar, las herramientas de R asociadas con la instancia predeterminada podrían estar ubicadas en esta carpeta de forma predeterminada: `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin`.

Paquetes de R agregados por Microsoft para cargas de trabajo paralelas y distribuidas incluyen las siguientes bibliotecas.

| Biblioteca | Descripción |
|---------|-------------|
| [**RevoScaleR**](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | Admite la visualización y exploración de datos, manipulación, transformación y objetos de origen de datos. Admite la creación de contextos de cálculo remoto, así como un diversos modelos de aprendizaje automático escalables, tales como **rxLinMod**. Estas API se han optimizado para analizar los conjuntos de datos que son demasiado grandes para caber en la memoria, así como para realizar cálculos que se distribuyen a través de varios núcleos o procesadores. El paquete RevoScaleR también admite el formato de archivo XDF para más rápido movimiento y el almacenamiento de datos que se usan para el análisis. El formato XDF usa el almacenamiento en columnas, es portátil y se puede usar para cargar y manipular datos procedentes de distintos orígenes, como texto, SPSS o una conexión ODBC. |
| [**MicrosoftML**](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package) | Contiene los algoritmos de aprendizaje automático que se han optimizado para la velocidad y la precisión, así como las transformaciones para trabajar con texto e imágenes en línea. Para obtener más información, consulte [MicrosoftML en SQL Server](../r/ref-r-microsoftml.md). | 

## <a name="using-r-in-sql-server"></a>Uso de R en SQL Server

Puede crear scripts de R mediante las funciones de bases, pero para sacar partido del procesamiento de varios, debe importar el **RevoScaleR** y **MicrosoftML** módulos en su código de R y, a continuación, llame a sus funciones para crear modelos que ejecutar en paralelo. 
 
Orígenes de datos admitidos incluyen las bases de datos ODBC, SQL Server y formato de archivo XDF para intercambiar datos con otros orígenes, o con soluciones de R. Datos de entrada deben ser tabulares. Todos los resultados de R se deben devolver en forma de una trama de datos.

Contextos de cálculo admitidos incluyen el contexto de proceso de SQL Server local o remoto. Un contexto de proceso remoto se refiere a la ejecución de código que se inicia en un equipo como una estación de trabajo, pero, a continuación, modificadores de la secuencia de comandos a un equipo remoto. Cambiar el contexto de proceso requiere que ambos sistemas tengan la misma biblioteca de RevoScaleR.

Contexto de proceso local, como cabría esperar, incluye la ejecución del código de R en el mismo servidor que la instancia del motor de base de datos, con el código de T-SQL o incrustado en un procedimiento almacenado. También puede ejecutar el código de un IDE de R local y tiene el script se ejecute en el equipo de SQL Server, contexto de proceso mediante la definición de un control remoto.

## <a name="execution-architecture"></a>Arquitectura de ejecución

Los diagramas siguientes describe la interacción de componentes de SQL Server con el tiempo de ejecución de R en cada uno de los escenarios admitidos: ejecuta la ejecución del script de base de datos y remota desde una línea de comandos de R, mediante un contexto de proceso de SQL Server.

### <a name="r-scripts-executed-from-sql-server-in-database"></a>Scripts de R ejecutados desde SQL Server en bases de datos

Código de R que se ejecuta desde "dentro" SQL Server se ejecuta mediante una llamada a un procedimiento almacenado. Por lo tanto, cualquier aplicación que pueda llamar a un procedimiento almacenado podrá iniciar la ejecución de código de R.  A partir de entonces, SQL Server administra la ejecución de código de R, como se resume en el diagrama siguiente.

![rsql_indb780-01](../r/media/script_in-db-r.png)

1. Mediante el parámetro _@language='R'_ pasado al procedimiento almacenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), se indica una solicitud para el tiempo de ejecución de R. SQL Server envía esta solicitud al servicio Launchpad.
2. El servicio Launchpad inicia el selector adecuado, en este caso, RLauncher.
3. RLauncher inicia el proceso externo de R.
4. BxlServer coordina con el tiempo de ejecución de R para administrar los intercambios de datos con SQL Server y el almacenamiento de los resultados del trabajo.
5. SQL Satellite administra las comunicaciones sobre las tareas relacionadas y los procesos con SQL Server.
6. BxlServer usa SQL Satellite para comunicar el estado y los resultados a SQL Server.
7. SQL Server obtiene los resultados y cierra los procesos y tareas relacionadas.

### <a name="r-scripts-executed-from-a-remote-client"></a>Scripts de R ejecutados desde un cliente remoto

Al conectarse desde un cliente de ciencia de datos remoto que admita Microsoft R, puede ejecutar funciones de R en el contexto de SQL Server mediante el uso de las funciones de RevoScaleR. Este es un flujo de trabajo diferente del anterior y se resume en el diagrama siguiente.

![rsql_fromR2db-01](../r/media/remote-sqlcc-from-r2.png)

1. Para las funciones de RevoScaleR, el runtime de R llama a una función de vinculación que a su vez llama a BxlServer.
2. BxlServer se proporciona con Microsoft R y se ejecuta en un proceso independiente del tiempo de ejecución de R.
3. BxlServer determina el destino de la conexión e inicia una conexión mediante ODBC. Para ello, pasa las credenciales proporcionadas como parte de la cadena de conexión en el objeto de origen de datos de R.
4. BxlServer abre una conexión a la instancia de SQL Server.
5. Para una llamada de R, Launchpad se invoca al servicio, que a su vez inicia el selector adecuado, RLauncher. Posteriormente, el procesamiento del código de R es similar al proceso para ejecutar código de R desde T-SQL.
6. RLauncher realiza una llamada a la instancia del runtime de R que se instala en el equipo de SQL Server.
7. Los resultados se devuelven a BxlServer.
8. SQL Satellite administra la comunicación con SQL Server y la limpieza de objetos de trabajo relacionados.
9. SQL Server pasa los resultados al cliente.

## <a name="see-also"></a>Vea también

+ [Marco de extensibilidad en SQL Server](extensibility-framework.md)
+ [Python y las extensiones de SQL Server de aprendizaje automático](extension-python.md)