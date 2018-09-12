---
title: Extensión de Python en SQL Server Machine Learning Services | Microsoft Docs
description: Obtenga información sobre la ejecución de código de Python y las bibliotecas de Python integradas en SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/05/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 24d34ee2ca9220ca1569ea83bcb092030d1ef692
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43892914"
---
# <a name="python-extension-in-sql-server"></a>Extensión de Python en SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

La extensión de Python es parte del complemento SQL Server Machine Learning Services para el motor de base de datos relacional. Agrega un entorno de ejecución de Python, distribución de Anaconda con el tiempo de ejecución de Python 3.5 e intérprete, bibliotecas estándar y las herramientas y las bibliotecas de producto de Microsoft para Python: [revoscalepy](../python/what-is-revoscalepy.md) para el análisis a escala y [microsoftml](../using-the-microsoftml-package.md) algoritmos de aprendizaje para la máquina. 

Integración de Python se instala como [SQL Server Machine Learning Services](../what-is-sql-server-machine-learning.md).

Instalación del tiempo de ejecución de Python 3.5 y el intérprete garantiza compatibilidad casi completa con las soluciones de Python estándar. Python se ejecuta en un proceso independiente de SQL Server, para garantizar que las operaciones de base de datos no están en peligro.

## <a name="python-components"></a>Componentes de Python

SQL Server incluye paquetes de código abierto y propietarios. Programa de instalación instalado el runtime de Python es 4.2 Anaconda Python 3.5. El runtime de Python se instala independientemente de las herramientas de SQL y se ejecuta fuera de los procesos de motor de core, en el marco de extensibilidad. Como parte de la instalación de servicios de Machine Learning con Python, debe dar su consentimiento a los términos de la licencia pública de GNU. 

SQL Server no modifica los archivos ejecutables de Python, pero debe usar la versión de Python instalado el programa de instalación porque esa versión es la que los paquetes de propiedad se crearon y probaron. Para obtener una lista de paquetes admitidos por la distribución de Anaconda, consulte el sitio de Continuum analytics: [lista de paquetes de Anaconda](https://docs.continuum.io/anaconda/pkg-docs).

La distribución de Anaconda asociada con una instancia del motor de base de datos específica puede encontrarse en la carpeta asociada con la instancia. Por ejemplo, si instaló el motor de base de datos de SQL Server 2017 con servicios de Machine Learning y Python en la instancia predeterminada, mire en `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`.

Los paquetes de Python agregados por Microsoft para cargas de trabajo paralelas y distribuidas incluyen las siguientes bibliotecas.

| Biblioteca | Descripción |
|---------|-------------|
| [**revoscalepy**](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | Admite la visualización y exploración de datos, manipulación, transformación y objetos de origen de datos. Admite la creación de contextos de cálculo remoto, así como un diversos modelos de aprendizaje automático escalables, tales como **rxLinMod**. Es equivalente a la de la [ **RevoScaleR** ](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) paquete para Microsoft R. |
| [**microsoftml**](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | Contiene los algoritmos de aprendizaje automático que se han optimizado para la velocidad y la precisión, así como las transformaciones para trabajar con texto e imágenes en línea. Para obtener más información, consulte [mediante el paquete MicrosoftML con SQL Server](https://docs.microsoft.com/sql/advanced-analytics/using-the-microsoftml-package). |

Microsoftml y revoscalepy están estrechamente relacionados; orígenes de datos utilizados en microsoftml se definen como objetos revoscalepy. Calcular las limitaciones de contexto de transferencia de revoscalepy a microsoftml. Es decir, toda la funcionalidad está disponible para operaciones locales, pero al cambiar a un contexto de cálculo remoto necesita RxInSqlServer.

## <a name="using-python-in-sql-server"></a>Uso de Python en SQL Server

Importar el **revoscalepy** módulo en su código de Python y, a continuación, llaman a funciones del módulo, al igual que cualquier otra función de Python.

Orígenes de datos admitidos incluyen las bases de datos ODBC, SQL Server y formato de archivo XDF para intercambiar datos con otros orígenes, o con soluciones de R. Datos de entrada para Python deben ser tabulares. Se deben devolver todos los resultados de Python en el formulario de un **pandas** trama de datos.

Contextos de cálculo admitidos incluyen el contexto de proceso de SQL Server local o remoto. Un contexto de proceso remoto se refiere a la ejecución de código que se inicia en un equipo como una estación de trabajo, pero, a continuación, modificadores de la secuencia de comandos a un equipo remoto. Cambiar el contexto de proceso requiere que ambos sistemas tengan la misma biblioteca de revoscalepy.

Contexto de proceso local, como cabría esperar, incluye la ejecución de código de Python en el mismo servidor que la instancia del motor de base de datos, con el código de T-SQL o incrustado en un procedimiento almacenado. También puede ejecutar el código de un IDE de Python local y tiene el script se ejecute en el equipo de SQL Server, contexto de proceso mediante la definición de un control remoto.

## <a name="execution-architecture"></a>Arquitectura de ejecución

Los diagramas siguientes describe la interacción de componentes de SQL Server con el tiempo de ejecución de Python en cada uno de los escenarios admitidos: ejecuta la ejecución del script de base de datos y remota desde un terminal de Python, con un contexto de proceso de SQL Server.

### <a name="python-scripts-executed-in-database"></a>Scripts de Python ejecutan en bases de datos

Al ejecutar Python "en" SQL Server, debe encapsular el script de Python dentro de un procedimiento almacenado especial, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Después de la secuencia de comandos se ha incrustado en el procedimiento almacenado, cualquier aplicación que se puede llamar a un procedimiento almacenado podrá iniciar la ejecución del código Python.  A partir de entonces, SQL Server administra la ejecución de código como se resume en el diagrama siguiente.

![script de python de base de datos](../../advanced-analytics/python/media/script-in-db-python2.png)

1. Una solicitud para el runtime de Python se indica mediante el parámetro `@language='Python'` pasa al procedimiento almacenado. SQL Server envía esta solicitud al servicio Launchpad.
2. El servicio Launchpad inicia el selector adecuado; en este caso, PythonLauncher.
3. PythonLauncher inicia el proceso de Python35 externo.
4. BxlServer coordina con el tiempo de ejecución de Python para administrar los intercambios de datos y almacenamiento de los resultados del trabajo.
5. SQL Satellite administra las comunicaciones sobre las tareas relacionadas y los procesos con SQL Server.
6. BxlServer usa SQL Satellite para comunicar el estado y los resultados a SQL Server.
7. SQL Server obtiene los resultados y cierra los procesos y tareas relacionadas.

### <a name="python-scripts-executed-from-a-remote-client"></a>Scripts de Python que se ejecuta desde un cliente remoto

Puede ejecutar scripts de Python desde un equipo remoto, como un equipo portátil y hacer que se ejecuten en el contexto del equipo de SQl Server, si se cumplen estas condiciones:

+ Diseñar adecuadamente las secuencias de comandos
+ El equipo remoto ha instalado las bibliotecas de extensibilidad utilizados por servicios Machine Learning. El [revoscalepy](../python/what-is-revoscalepy.md) paquete es necesario usar contextos de cálculo remoto.

El diagrama siguiente resume el flujo de trabajo global cuando las secuencias de comandos se envían desde un equipo remoto.

![sqlcc remoto desde python](../../advanced-analytics/python/media/remote-sqlcc-from-python3.png)

1. Para las funciones que se admiten en **revoscalepy**, el runtime de Python llama a una función de enlace, que a su vez llama a BxlServer.
2. BxlServer se incluye con Machine Learning Services (In-Database) y se ejecuta en un proceso independiente desde el tiempo de ejecución de Python.
3. BxlServer determina el destino de la conexión e inicia una conexión mediante ODBC, pasa las credenciales proporcionadas como parte de la cadena de conexión en el script de Python.
4. BxlServer abre una conexión a la instancia de SQL Server.
5. Cuando se llama a un tiempo de ejecución de scripts externos, se invoca el servicio Launchpad, que a su vez inicia el selector adecuado: en este caso, PythonLauncher.dll. A partir de entonces, el procesamiento de código Python se controla en un flujo de trabajo similar a la que cuando se invoca código de Python desde un procedimiento almacenado de T-SQL.
6. PythonLauncher realiza una llamada a la instancia de la versión de Python que se instala en el equipo de SQL Server.
7. Los resultados se devuelven a BxlServer.
8. SQL Satellite administra la comunicación con SQL Server y la limpieza de objetos de trabajo relacionados.
9. SQL Server pasa los resultados al cliente.

## <a name="see-also"></a>Vea también

+ [¿Qué es revoscalepy](../python/what-is-revoscalepy.md) 
+ [Marco de extensibilidad en SQL Server](extensibility-framework.md)
+ [R y machine learning extensiones en SQL Server](extension-r.md)