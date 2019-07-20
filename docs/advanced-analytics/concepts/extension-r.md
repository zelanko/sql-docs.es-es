---
title: Extensión del lenguaje de programación R
description: Obtenga información sobre la ejecución de código R y las bibliotecas de R integradas en SQL Server 2016 R Services o SQL Server 2017 Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3bf8e77cec92cde0e5a8adf4d3e1e36f1689b917
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343414"
---
# <a name="r-language-extension-in-sql-server"></a>Extensión de lenguaje R en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

La extensión de R forma parte del complemento de SQL Server Machine Learning Services al motor de base de datos relacional. Agrega un entorno de ejecución de R, una distribución de R base con herramientas y bibliotecas estándar, y las bibliotecas de Microsoft R: [RevoScaleR](../r/ref-r-revoscaler.md) para análisis a escala, [MicrosoftML](../r/ref-r-microsoftml.md) para algoritmos de aprendizaje automático y otras bibliotecas para el acceso a datos o código R en SQL Server.

La integración de r está disponible en SQL Server a partir de SQL Server 2016, con [R Services](../r/sql-server-r-services.md)y continuar adelante como parte del [Machine Learning Services de SQL Server](../what-is-sql-server-machine-learning.md).

## <a name="r-components"></a>Componentes de R

SQL Server incluye los paquetes de código abierto y propietario. Las bibliotecas de R base se instalan a través de la distribución de R de código abierto de Microsoft. Microsoft R Open (MRO). Los usuarios actuales de R deben poder migrar su código de R y ejecutarlo como un proceso externo en SQL Server con pocas modificaciones o ninguna modificación. MRO se instala independientemente de las herramientas de SQL y se ejecuta fuera de los procesos del motor principal, en el marco de extensibilidad. Durante la instalación, debe dar su consentimiento a los términos de la licencia de código abierto. A partir de ese momento, puede ejecutar paquetes de R estándar sin más modificaciones, tal como lo haría en cualquier otra distribución de código abierto de R. 

SQL Server no modifica los ejecutables de R base, pero debe usar la versión de R instalada por el programa de instalación de, ya que esa versión es aquella en la que se compilan y prueban los paquetes de propiedad. Para obtener más información sobre cómo MRO difiere de una distribución base de R que puede obtener de CRAN, consulte [interoperabilidad con el lenguaje r y productos y características de Microsoft r](https://docs.microsoft.com/r-server/what-is-r-server-interoperability).

La distribución de paquetes base de R instalada por el programa de instalación de se puede encontrar en la carpeta asociada a la instancia de. Por ejemplo, si instaló R Services en una instancia predeterminada de SQL Server 2016, las bibliotecas de R se encuentran en esta carpeta de forma `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`predeterminada:. De forma similar, las herramientas de R asociadas a la instancia predeterminada se ubicarían en esta carpeta `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin`de forma predeterminada:.

Los paquetes de R agregados por Microsoft para cargas de trabajo paralelas y distribuidas incluyen las siguientes bibliotecas.

| Biblioteca | Descripción |
|---------|-------------|
| [**RevoScaleR**](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) | Admite objetos de origen de datos y exploración de datos, manipulación, transformación y visualización. Admite la creación de contextos de cálculo remotos, así como varios modelos de aprendizaje automático escalables, como **rxLinMod**. Estas API se han optimizado para analizar los conjuntos de datos que son demasiado grandes para caber en la memoria, así como para realizar cálculos que se distribuyen a través de varios núcleos o procesadores. El paquete RevoScaleR también admite el formato de archivo XDF para un movimiento y almacenamiento más rápidos de los datos usados para el análisis. El formato XDF usa el almacenamiento en columnas, es portátil y se puede usar para cargar y manipular datos procedentes de distintos orígenes, como texto, SPSS o una conexión ODBC. |
| [**MicrosoftML**](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package) | Contiene algoritmos de aprendizaje automático que se han optimizado para la velocidad y la precisión, así como las transformaciones en línea para trabajar con texto e imágenes. Para obtener más información, consulte [MicrosoftML en SQL Server](../r/ref-r-microsoftml.md). | 

## <a name="using-r-in-sql-server"></a>Uso de R en SQL Server

Puede crear scripts de R mediante funciones base, pero para beneficiarse del procesamiento múltiple, debe importar los módulos **RevoScaleR** y **MicrosoftML** en el código de R y, a continuación, llamar a sus funciones para crear modelos que se ejecuten en paralelo. 
 
Entre los orígenes de datos admitidos se incluyen las bases de datos ODBC, SQL Server y el formato de archivo XDF para intercambiar datos con otros orígenes o con soluciones de R. Los datos de entrada deben ser tabulares. Todos los resultados de R se deben devolver en forma de trama de datos.

Entre los contextos de cálculo admitidos se incluyen el contexto de proceso local o remoto SQL Server. Un contexto de cálculo remoto hace referencia a la ejecución de código que se inicia en un equipo como, por ejemplo, una estación de trabajo, pero, a continuación, cambia la ejecución del script a un equipo remoto. Cambiar el contexto de cálculo requiere que ambos sistemas tengan la misma biblioteca RevoScaleR.

El contexto de proceso local, como cabría esperar, incluye la ejecución de código de R en el mismo servidor que la instancia del motor de base de datos, con código dentro de T-SQL o incrustado en un procedimiento almacenado. También puede ejecutar el código desde un IDE de R local y hacer que el script se ejecute en el SQL Server equipo, mediante la definición de un contexto de cálculo remoto.

## <a name="execution-architecture"></a>Arquitectura de ejecución

En los diagramas siguientes se describe la interacción de los componentes de SQL Server con el tiempo de ejecución de R en cada uno de los escenarios admitidos: ejecutar script en la base de datos y ejecutar de forma remota desde una línea de comandos de R, utilizando un contexto de cálculo de SQL Server.

### <a name="r-scripts-executed-from-sql-server-in-database"></a>Scripts de R ejecutados desde SQL Server en la base de datos

El código de R que se ejecuta desde el SQL Server "interior" se ejecuta llamando a un procedimiento almacenado. Por lo tanto, cualquier aplicación que pueda llamar a un procedimiento almacenado podrá iniciar la ejecución de código de R.  Después SQL Server administra la ejecución de código de R como se resume en el diagrama siguiente.

![rsql_indb780-01](../r/media/script_in-db-r.png)

1. Mediante el parámetro _@language='R'_ pasado al procedimiento almacenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), se indica una solicitud para el tiempo de ejecución de R. SQL Server envía esta solicitud al servicio Launchpad.
2. El servicio Launchpad inicia el selector adecuado, en este caso, RLauncher.
3. RLauncher inicia el proceso externo de R.
4. BxlServer coordina con el tiempo de ejecución de R para administrar los intercambios de datos con SQL Server y el almacenamiento de los resultados de trabajo.
5. SQL Satellite administra las comunicaciones de las tareas y los procesos relacionados con SQL Server.
6. BxlServer usa SQL Satellite para comunicar el estado y los resultados a SQL Server.
7. SQL Server obtiene los resultados y cierra las tareas y los procesos relacionados.

### <a name="r-scripts-executed-from-a-remote-client"></a>Scripts de R ejecutados desde un cliente remoto

Al conectarse desde un cliente de ciencia de datos remoto que admite Microsoft R, puede ejecutar funciones de R en el contexto de SQL Server mediante el uso de las funciones de RevoScaleR. Este es un flujo de trabajo diferente del anterior y se resume en el diagrama siguiente.

![rsql_fromR2db-01](../r/media/remote-sqlcc-from-r2.png)

1. En el caso de las funciones RevoScaleR, el tiempo de ejecución de R llama a una función de vinculación que a su vez llama a BxlServer.
2. BxlServer se proporciona con Microsoft R y se ejecuta en un proceso independiente del tiempo de ejecución de R.
3. BxlServer determina el destino de la conexión e inicia una conexión mediante ODBC. Para ello, pasa las credenciales proporcionadas como parte de la cadena de conexión en el objeto de origen de datos de R.
4. BxlServer abre una conexión a la instancia de SQL Server.
5. En el caso de una llamada de R, se invoca el servicio Launchpad, que inicia el iniciador adecuado, RLauncher. Posteriormente, el procesamiento del código de R es similar al proceso para ejecutar código de R desde T-SQL.
6. RLauncher realiza una llamada a la instancia del Runtime de R que está instalado en el equipo SQL Server.
7. Los resultados se devuelven a BxlServer.
8. SQL Satellite administra la comunicación con SQL Server y la limpieza de objetos de trabajo relacionados.
9. SQL Server devuelve los resultados al cliente.

## <a name="see-also"></a>Vea también

+ [Marco de extensibilidad en SQL Server](extensibility-framework.md)
+ [Extensiones de Python y machine learning en SQL Server](extension-python.md)