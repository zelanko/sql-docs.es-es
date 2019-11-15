---
title: Extensión del lenguaje R
description: Obtenga información sobre la ejecución de código de R y las bibliotecas de R integradas en SQL Server R Services o en SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/04/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 98ef57702b01a3f32babd6b0ac9b64fb3c22e9ea
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727658"
---
# <a name="r-language-extension-in-sql-server"></a>Extensión del lenguaje R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La extensión de R forma parte del complemento de SQL Server Machine Learning Services al motor de base de datos relacional. Agrega un entorno de ejecución de R, una distribución de R base con herramientas y bibliotecas estándar, y las bibliotecas de Microsoft R: [RevoScaleR](../r/ref-r-revoscaler.md) para análisis a escala, [MicrosoftML](../r/ref-r-microsoftml.md) para algoritmos de aprendizaje automático y otras bibliotecas para acceder a datos o a código de R en SQL Server.

La integración de R está disponible en [SQL Server R Services](../r/sql-server-r-services.md) y [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md).

## <a name="r-components"></a>Componentes de R

SQL Server incluye los paquetes de código abierto y de propietario. Las bibliotecas de R base se instalan a través de la distribución de R de código abierto de Microsoft: Microsoft R Open (MRO). Los usuarios actuales de R deben poder portar su código de R y ejecutarlo como un proceso externo en SQL Server con pocas modificaciones o ninguna. MRO se instala independientemente de las herramientas de SQL y se ejecuta fuera de los procesos principales del motor, en el marco de extensibilidad. Durante la instalación, debe dar su consentimiento a los términos de la licencia de código abierto. Cuando lo haga, podrá ejecutar paquetes de R estándar sin necesidad de realizar ninguna modificación más, tal y como sucede con cualquier otra distribución de código abierto de R. 

SQL Server no modifica los ejecutables base de R, pero se debe usar la versión de R que instala el programa de instalación, ya que esa versión es en la que se compilan y prueban los paquetes de propietario. Para obtener más información sobre las diferencias entre MRO y una distribución base de R que podría obtener de CRAN, vea [Interoperabilidad con el lenguaje R y los productos y características de Microsoft R](https://docs.microsoft.com/r-server/what-is-r-server-interoperability).

La distribución de paquetes base de R que instala el programa de instalación se puede encontrar en la carpeta asociada a la instancia. Por ejemplo, si se ha instalado R Services en la instancia predeterminada de SQL Server, las bibliotecas de R estarán en esta carpeta `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library` de forma predeterminada. De forma similar, las herramientas de R asociadas a la instancia predeterminada se encontrarían en la carpeta `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin` por defecto.

Los paquetes de R que agrega Microsoft para cargas de trabajo paralelas y distribuidas incluyen las bibliotecas siguientes.

| Biblioteca | Descripción |
|---------|-------------|
| [**RevoScaleR**](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | Admite objetos de origen de datos y exploración, manipulación, transformación y visualización de datos. Admite la creación de contextos de proceso remotos, así como varios modelos de aprendizaje automático escalables, como **rxLinMod**. Estas API se han optimizado para analizar los conjuntos de datos que son demasiado grandes para caber en la memoria, así como para realizar cálculos que se distribuyen a través de varios núcleos o procesadores. El paquete RevoScaleR también admite el formato de archivo XDF, lo que permite mover y almacenar más rápidamente los datos empleados en los análisis. El formato XDF usa el almacenamiento en columnas, es portátil y se puede usar para cargar y manipular datos procedentes de distintos orígenes, como texto, SPSS o una conexión ODBC. |
| [**MicrosoftML**](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package) | Contiene algoritmos de aprendizaje automático que se han optimizado para la velocidad y precisión, así como las transformaciones en línea para trabajar con texto e imágenes. Para obtener más información, vea [MicrosoftML en SQL Server](../r/ref-r-microsoftml.md). | 

## <a name="using-r-in-sql-server"></a>Uso de R en SQL Server

Puede generar scripts de R mediante funciones base, pero para beneficiarse del procesamiento múltiple, debe importar los módulos **RevoScaleR** y **MicrosoftML** en el código R y, después, llamar a sus funciones para crear modelos que se ejecuten en paralelo. 
 
Entre los orígenes de datos admitidos se incluyen las bases de datos ODBC, SQL Server y el formato de archivo XDF para intercambiar datos con otros orígenes o con soluciones de R. Los datos de entrada deben ser tabulares. Todos los resultados de R se deben devolver en formato de trama de datos.

Entre los contextos de proceso admitidos se incluyen el contexto de proceso local o remoto de SQL Server. Un contexto de proceso remoto hace referencia a la ejecución de código que se inicia en un equipo como, por ejemplo, una estación de trabajo, pero que luego cambia la ejecución del script a un equipo remoto. Cambiar el contexto de proceso requiere que ambos sistemas tengan la misma biblioteca RevoScaleR.

El contexto de proceso local, como cabría esperar, incluye la ejecución de código de R en el mismo servidor que la instancia del motor de base de datos, con código dentro de T-SQL o incrustado en un procedimiento almacenado. También se puede ejecutar el código desde un IDE de R local y hacer que el script se ejecute en el equipo de SQL Server mediante la definición de un contexto de proceso remoto.

## <a name="execution-architecture"></a>Arquitectura de la ejecución

En los diagramas siguientes se describe la interacción de los componentes de SQL Server con el entorno de ejecución de R en cada uno de los escenarios admitidos: ejecutar un script en la base de datos y ejecutarlo de forma remota desde una línea de comandos de R, utilizando un contexto de proceso de SQL Server.

### <a name="r-scripts-executed-from-sql-server-in-database"></a>Scripts de R ejecutados desde SQL Server en una base de datos

El código de R que se ejecuta desde "dentro" de SQL Server se ejecuta mediante una llamada a un procedimiento almacenado. Por lo tanto, cualquier aplicación que pueda llamar a un procedimiento almacenado podrá iniciar la ejecución de código de R.  A partir de entonces, SQL Server administra la ejecución del código de R, como se resume en el diagrama siguiente.

![rsql_indb780-01](../r/media/script_in-db-r.png)

1. Mediante el parámetro _@language='R'_ pasado al procedimiento almacenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), se indica una solicitud para el tiempo de ejecución de R. SQL Server envía esta solicitud al servicio Launchpad.
En Linux, SQL usa un servicio **Launchpad** a fin de comunicarse con un proceso de Launchpad independiente para cada usuario. Consulte el [Diagrama de la arquitectura de extensibilidad](extensibility-framework.md#architecture-diagram) para obtener más información.
2. El servicio Launchpad inicia el selector adecuado, en este caso, RLauncher.
3. RLauncher inicia el proceso externo de R.
4. BxlServer coordina con el entorno de ejecución de R la administración de los intercambios de datos con SQL Server y el almacenamiento de los resultados del trabajo.
5. SQL Satellite administra las comunicaciones sobre las tareas y los procesos relacionados con SQL Server.
6. BxlServer usa SQL Satellite para comunicar el estado y los resultados a SQL Server.
7. SQL Server obtiene los resultados y cierra las tareas y los procesos relacionados.

### <a name="r-scripts-executed-from-a-remote-client"></a>Scripts de R ejecutados desde un cliente remoto

Al conectarse desde un cliente de ciencia de datos remoto que admite Microsoft R, puede ejecutar funciones de R en el contexto de SQL Server mediante funciones de RevoScaleR. Este es un flujo de trabajo diferente del anterior y se resume en el diagrama siguiente.

![rsql_fromR2db-01](../r/media/remote-sqlcc-from-r2.png)

1. Para las funciones de RevoScaleR, el entorno de ejecución de R llama a una función de enlace que a su vez llama a BxlServer.
2. BxlServer se proporciona con Microsoft R y se ejecuta en un proceso independiente del tiempo de ejecución de R.
3. BxlServer determina el destino de la conexión e inicia una conexión mediante ODBC. Para ello, pasa las credenciales proporcionadas como parte de la cadena de conexión en el objeto de origen de datos de R.
4. BxlServer abre una conexión con la instancia de SQL Server.
5. Para una llamada de R, se invoca el servicio LaunchPad, que a su vez inicia el selector adecuado, RLauncher. Posteriormente, el procesamiento del código de R es similar al proceso para ejecutar código de R desde T-SQL.
6. RLauncher realiza una llamada a la instancia del entorno de ejecución de R que está instalada en el equipo con SQL Server.
7. Los resultados se devuelven a BxlServer.
8. SQL Satellite administra la comunicación con SQL Server y la limpieza de los objetos de trabajo relacionados.
9. SQL Server devuelve los resultados al cliente.

## <a name="see-also"></a>Vea también

+ [Marco de extensibilidad en SQL Server](extensibility-framework.md)
+ [Extensiones de Python y aprendizaje automático en SQL Server](extension-python.md)