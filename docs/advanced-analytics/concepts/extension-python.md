---
title: Extensión del lenguaje de programación de Python
description: Obtenga información sobre la ejecución de código de Python y las bibliotecas de Python integradas en SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f3825a2b5085bf5a6e144a602c36cb20ccaca430
ms.sourcegitcommit: 36c3ead6f2a3628f58040acf47f049f0b0957b8a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/30/2019
ms.locfileid: "71688280"
---
# <a name="python-language-extension-in-sql-server"></a>Extensión del lenguaje Python en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La extensión de Python forma parte del complemento de SQL Server Machine Learning Services al motor de base de datos relacional. Agrega un entorno de ejecución de Python, distribución de Anaconda con el tiempo de ejecución y el intérprete de Python 3,5, bibliotecas y herramientas estándar y las bibliotecas de productos de Microsoft para Python: [revoscalepy](../python/ref-py-revoscalepy.md) para análisis a escala y [microsoftml](../python/ref-py-microsoftml.md) para algoritmos de aprendizaje automático. 

La integración de Python se instala como [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md).

La instalación del tiempo de ejecución de Python 3,5 y el intérprete garantiza la compatibilidad casi completa con las soluciones estándar de Python. Python se ejecuta en un proceso independiente de SQL Server, para garantizar que las operaciones de base de datos no se vean comprometidas.

## <a name="python-components"></a>Componentes de Python

SQL Server incluye los paquetes de código abierto y propietario. El tiempo de ejecución de Python instalado por el programa de instalación es Anaconda 4,2 con Python 3,5. El tiempo de ejecución de Python se instala independientemente de las herramientas de SQL y se ejecuta fuera de los procesos del motor principal, en el marco de extensibilidad. Como parte de la instalación de Machine Learning Services con Python, debe dar su consentimiento a los términos de la licencia pública GNU. 

SQL Server no modifica los ejecutables de Python, pero debe usar la versión de Python instalada por el programa de instalación de, ya que esa versión es aquella en la que se compilan y prueban los paquetes de propiedad. Para obtener una lista de los paquetes admitidos por la distribución de Anaconda, consulte el sitio de continuum Analytics: [Lista de paquetes de Anaconda](https://docs.continuum.io/anaconda/packages/pkg-docs).

La distribución Anaconda asociada a una instancia específica del motor de base de datos se puede encontrar en la carpeta asociada a la instancia. Por ejemplo, si ha instalado SQL Server motor de base de datos 2017 con Machine Learning Services y Python en la instancia predeterminada `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`, busque en.

Los paquetes de Python agregados por Microsoft para cargas de trabajo paralelas y distribuidas incluyen las siguientes bibliotecas.

| Biblioteca | Descripción |
|---------|-------------|
| [**revoscalepy**](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | Admite objetos de origen de datos y exploración de datos, manipulación, transformación y visualización. Admite la creación de contextos de cálculo remotos, así como varios modelos de aprendizaje automático escalables, como **rxLinMod**. Para obtener más información, vea [módulo revoscalepy con SQL Server](../python/ref-py-revoscalepy.md).  |
| [**microsoftml**](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | Contiene algoritmos de aprendizaje automático que se han optimizado para la velocidad y la precisión, así como las transformaciones en línea para trabajar con texto e imágenes. Para obtener más información, vea [módulo microsoftml con SQL Server](../python/ref-py-microsoftml.md). |

Microsoftml y revoscalepy están estrechamente acoplados; los orígenes de datos usados en microsoftml se definen como objetos revoscalepy. Limitaciones del contexto de proceso en la transferencia de revoscalepy a microsoftml. Es decir, todas las funciones están disponibles para las operaciones locales, pero el cambio a un contexto de cálculo remoto requiere RxInSqlServer.

## <a name="using-python-in-sql-server"></a>Usar Python en SQL Server

Importe el módulo **revoscalepy** en el código de Python y, a continuación, llame a las funciones desde el módulo, como cualquier otra función de Python.

Entre los orígenes de datos admitidos se incluyen las bases de datos ODBC, SQL Server y el formato de archivo XDF para intercambiar datos con otros orígenes o con soluciones de R. Los datos de entrada de Python deben ser tabulares. Todos los resultados de Python se deben devolver en forma de trama de datos **pandas** .

Entre los contextos de cálculo admitidos se incluyen el contexto de proceso local o remoto SQL Server. Un contexto de cálculo remoto hace referencia a la ejecución de código que se inicia en un equipo como, por ejemplo, una estación de trabajo, pero, a continuación, cambia la ejecución del script a un equipo remoto. Cambiar el contexto de cálculo requiere que ambos sistemas tengan la misma biblioteca revoscalepy.

El contexto de proceso local, como cabría esperar, incluye la ejecución de código de Python en el mismo servidor que la instancia del motor de base de datos, con código dentro de T-SQL o incrustado en un procedimiento almacenado. También puede ejecutar el código desde un IDE de Python local y hacer que el script se ejecute en el SQL Server equipo, mediante la definición de un contexto de cálculo remoto.

## <a name="execution-architecture"></a>Arquitectura de ejecución

En los diagramas siguientes se describe la interacción de los componentes de SQL Server con el tiempo de ejecución de Python en cada uno de los escenarios admitidos: ejecutar script en la base de datos y ejecutarlo de forma remota desde un terminal de Python, utilizando un contexto de cálculo de SQL Server.

### <a name="python-scripts-executed-in-database"></a>Scripts de Python ejecutados en la base de datos

Cuando ejecute Python "Inside" SQL Server, debe encapsular el script de Python dentro de un procedimiento almacenado especial, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Una vez que el script se ha incrustado en el procedimiento almacenado, cualquier aplicación que pueda realizar una llamada a un procedimiento almacenado puede iniciar la ejecución del código de Python.  Después SQL Server administra la ejecución del código tal y como se resume en el diagrama siguiente.

![script-in-db-python](../../advanced-analytics/python/media/script-in-db-python2.png)

1. El parámetro `@language='Python'` pasado al procedimiento almacenado indica una solicitud para el tiempo de ejecución de Python. SQL Server envía esta solicitud al servicio Launchpad.
2. El servicio Launchpad inicia el iniciador adecuado. en este caso, PythonLauncher.
3. PythonLauncher inicia el proceso de Python35 externo.
4. BxlServer coordina con el tiempo de ejecución de Python para administrar los intercambios de datos y el almacenamiento de los resultados de trabajo.
5. SQL Satellite administra las comunicaciones de las tareas y los procesos relacionados con SQL Server.
6. BxlServer usa SQL Satellite para comunicar el estado y los resultados a SQL Server.
7. SQL Server obtiene los resultados y cierra las tareas y los procesos relacionados.

### <a name="python-scripts-executed-from-a-remote-client"></a>Scripts de Python ejecutados desde un cliente remoto

Puede ejecutar scripts de Python desde un equipo remoto, como un equipo portátil, y hacer que se ejecuten en el contexto del equipo de SQl Server, si se cumplen estas condiciones:

+ Diseña los scripts correctamente
+ El equipo remoto ha instalado las bibliotecas de extensibilidad que se usan en Machine Learning Services. El paquete [revoscalepy](../python/ref-py-revoscalepy.md) es necesario para usar contextos de cálculo remotos.

En el diagrama siguiente se resume el flujo de trabajo general cuando se envían scripts desde un equipo remoto.

![remote-sqlcc-from-python](../../advanced-analytics/python/media/remote-sqlcc-from-python3.png)

1. En el caso de las funciones que se admiten en **revoscalepy**, el tiempo de ejecución de Python llama a una función de vinculación que, a su vez, llama a BxlServer.
2. BxlServer se incluye con Machine Learning Services (en la base de datos) y se ejecuta en un proceso independiente del tiempo de ejecución de Python.
3. BxlServer determina el destino de la conexión e inicia una conexión mediante ODBC, pasando las credenciales proporcionadas como parte de la cadena de conexión en el script de Python.
4. BxlServer abre una conexión a la instancia de SQL Server.
5. Cuando se llama a un tiempo de ejecución de script externo, se invoca al servicio Launchpad, que a su vez inicia el iniciador adecuado: en este caso, PythonLauncher. dll. A partir de ese momento, el procesamiento de código de Python se controla en un flujo de trabajo similar al de un procedimiento almacenado en T-SQL.
6. PythonLauncher realiza una llamada a la instancia de Python instalada en el equipo SQL Server.
7. Los resultados se devuelven a BxlServer.
8. SQL Satellite administra la comunicación con SQL Server y la limpieza de objetos de trabajo relacionados.
9. SQL Server devuelve los resultados al cliente.

## <a name="next-steps"></a>Pasos siguientes

+ [módulo revoscalepy en SQL Server](../python/ref-py-revoscalepy.md)
+ [referencia de la función revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 
+ [Marco de extensibilidad en SQL Server](extensibility-framework.md)
+ [Extensiones de R y machine learning en SQL Server](extension-r.md)
+ [Obtener información de paquete de Python](../package-management/python-package-information.md)
+ [Instalación de paquetes de Python con sqlmlutils](../package-management/install-additional-python-packages-on-sql-server.md)
