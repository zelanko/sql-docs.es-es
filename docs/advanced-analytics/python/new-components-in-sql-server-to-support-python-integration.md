---
title: "Componentes de integración de Python con SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 11/03/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: a23acdc0c39e0325f31050b299b883616912be71
ms.sourcegitcommit: ec5f7a945b9fff390422d5c4c138ca82194c3a3b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/11/2017
---
# <a name="components-in-sql-server-to-support-python-integration"></a>Componentes de SQL Server para admitir la integración de Python

A partir de 2017 de SQL Server, servicios de aprendizaje de máquina admite Python como un lenguaje externo que se puede ejecutar desde el código T-SQL o ejecuta de forma remota con SQL Server como el contexto de proceso.

Este tema describe específicamente los componentes de SQL Server de 2017 que admiten la extensibilidad en general y el lenguaje de Python.

## <a name="sql-server-components-and-providers"></a>Proveedores y los componentes de SQL Server

Para configurar SQL Server 2017 para permitir la ejecución del script de Python es un proceso de varios pasos.

1. Instale la característica de extensibilidad.
2. Habilitar la característica de ejecución de script externo.
3. Reinicie el servicio de motor de base de datos.

Pueden requerir pasos adicionales para admitir la ejecución de scripts remotos.

Para obtener más información, vea [configurar los servicios de aprendizaje de máquina](setup-python-machine-learning-services.md)

### <a name="launchpad"></a>Launchpad

El Launchpad de confianza de SQL Server es un servicio que se introdujo en SQL Server 2016 que administra y ejecuta scripts externos, similares a la manera en que el servicio de indización y consulta de texto completo inicia un host independiente para procesar las consultas de texto completo.

El servicio Launchpad puede iniciar solo confianza iniciadores que están publicadas por Microsoft o que han sido certificados por Microsoft como cumplen los requisitos para la administración de recursos y rendimiento.

+ SQL Server 2017 admite R y 3.5 de Python
+ SQL Server 2016 es compatible con R

El servicio [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] se ejecuta en su propia cuenta de usuario.

> [!TIP]
> Si cambia la cuenta que ejecuta Launchpad, asegúrese de hacerlo mediante el Administrador de configuración de SQL Server, para asegurarse de que los cambios se escriben en archivos relacionados.

Para ejecutar tareas en un lenguaje compatible específico, Launchpad Obtiene una cuenta de trabajo protegidos del grupo e inicia un proceso de satélite para administrar el tiempo de ejecución externo:

+ RLauncher.dll para el lenguaje R
+ Pythonlauncher.dll para Python 3.5

Cada proceso satélite hereda la cuenta de usuario de Launchpad y usa esa cuenta de trabajo para la duración de ejecución del script. Si el script de Python utiliza procesos en paralelo, se crean bajo la cuenta del trabajador de la misma, una sola.

Para obtener más información sobre el contexto de seguridad de Launchpad, consulte [seguridad](security-overview-sql-server-python-services.md).

### <a name="bxlserver-and-sql-satellite"></a>BxlServer y satélite SQL

Si ejecuta [Process Explorer](https://technet.microsoft.com/sysinternals/processexplorer.aspx) mientras se ejecuta un trabajo de Python, verá una o varias instancias de BxlServer.

**BxlServer** es un archivo ejecutable proporcionado por Microsoft que administra la comunicación entre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y Python (o R). Crea los objetos de trabajo de Windows que se utilizan para contener las sesiones de script externo, disposiciones seguros las carpetas de trabajo para cada trabajo de script externo y utiliza SQL satélite para administrar la transferencia de datos entre el tiempo de ejecución externo y [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].

En efecto, BxlServer es un complemento de Python que funciona con [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] para transferir datos y administrar tareas. BXL hace referencia al lenguaje de intercambio binario y hace referencia a los formatos de datos utilizados para mover datos eficazmente entre SQL Server y procesos externos. BxlServer también es una parte importante de Microsoft R Client y Microsoft R Server.

**SQL satélite** es una API de extensibilidad, incluida en el motor de base de datos a partir de SQL Server 2016, que admite código externo o tiempos de ejecución externos implementada mediante C o C++.

BxlServer usa SQL Satellite para las tareas siguientes:

+ Leer datos de entrada
+ Escribir datos de salida
+ Obtener argumentos de entrada
+ Escribir argumentos de salida
+ Control de errores
+ Escribir STDOUT y STDERR de vuelta en el cliente

Satélite de SQL utiliza un formato de datos personalizado que se optimiza para la transferencia de datos rápidas entre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y lenguajes de script externo. Realiza las conversiones de tipos y define los esquemas de los conjuntos de datos de entrada y salida durante las comunicaciones entre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y el tiempo de ejecución de script externo.

La licencia satélite de SQL se puede supervisar mediante el uso de windows (xEvents) de eventos extendidos. Para obtener más información, consulte [Extended Events para R](../../advanced-analytics/r/extended-events-for-sql-server-r-services.md).

## <a name="communication-channels-between-components"></a>Canales de comunicación entre componentes

+ **TCP/IP**

  De forma predeterminada, la comunicación interna entre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y la licencia de satélite SQL utilizan TCP/IP.

+ **Canalizaciones con nombre**

  El transporte de datos internos entre BxlServer y [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mediante SQL Satellite usa un formato de datos comprimidos registrado para mejorar el rendimiento. Se intercambian datos entre Python y BxlServer en formato BXL, mediante canalizaciones con nombre.

+ **ODBC**

  Las comunicaciones entre los clientes de ciencia de datos externos y el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instancia utilizar ODBC. Trabajos de la cuenta que envía la secuencia de comandos para [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] debe tener los permisos para conectarse a la instancia y ejecutar scripts externos.

  Además, en función de la tarea, la cuenta que tenga estos permisos:

  + Leer datos utilizados por el trabajo
  + Escribir datos en tablas: por ejemplo, al guardar los resultados en una tabla
  + Crear objetos de base de datos: por ejemplo, si se guarda el script externo como parte de un nuevo procedimiento almacenado.

  Cuando [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] es utiliza como el contexto de proceso para ejecuta el script de Python desde un cliente remoto y el ejecutable de Python debe recuperar datos desde un origen externo, se usa para la reescritura de ODBC. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]asigna la identidad del usuario que emite el comando remoto a la identidad del usuario en la instancia actual y se ejecuta el comando ODBC con las credenciales del usuario. La cadena de conexión necesaria para realizar esta llamada ODBC se obtiene del código de cliente.

## <a name="interaction-of-components"></a>Interacción de componentes

Los siguientes diagramas indican la interacción de componentes de SQL Server con el tiempo de ejecución de Python en cada uno de los escenarios admitidos: ejecución de secuencia de comandos en bases de datos y remotos desde un terminal de Python, usando un contexto de proceso de SQL Server.

### <a name="python-scripts-executed-in-database"></a>Python scripts ejecutados en bases de datos

Al ejecutar Python "en" [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], se debe encapsular el script de Python dentro de un procedimiento almacenado especial, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Después de la secuencia de comandos se han incrustado en el procedimiento almacenado, cualquier aplicación que puede realizar un procedimiento almacenado llamada puede iniciar la ejecución del código Python.  A partir de ahí [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] administra la ejecución de código como se resume en el diagrama siguiente.

![script de python de base de datos](../../advanced-analytics/python/media/script-in-db-python2.png)

1. Una solicitud para el tiempo de ejecución de Python se indica mediante el parámetro `@language='Python'` pasa al procedimiento almacenado. SQL Server envía esta solicitud para el servicio Launchpad.
2. El servicio Launchpad inicia el selector adecuado; en este caso, PythonLauncher.
3. PythonLauncher inicia el proceso de Python35 externo.
4. BxlServer se coordina con el tiempo de ejecución de Python para administrar el intercambio de datos y el almacenamiento de resultados de trabajo.
5. SQL satélite administra las comunicaciones acerca de las tareas relacionadas y procesa con [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
6. BxlServer usa SQL Satellite para comunicarle el estado y los resultados a [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
7. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] obtiene los resultados y cierra las tareas y los procesos relacionados.

### <a name="python-scripts-executed-from-a-remote-client"></a>Scripts de Python que se ejecuta desde un cliente remoto

Puede ejecutar scripts de Python desde un equipo remoto, como un equipo portátil y hacer que se ejecutan en el contexto del equipo de SQl Server, si se cumplen estas condiciones:

+ Diseñar las secuencias de comandos correctamente
+ El equipo remoto ha instalado las bibliotecas de extensibilidad que usan servicios de aprendizaje de máquina. El [revoscalepy](what-is-revoscalepy.md) paquete es necesario para usar contextos de proceso remoto.

En el diagrama siguiente se resume el flujo de trabajo global cuando las secuencias de comandos se envían desde un equipo remoto.

![sqlcc remoto de python](../../advanced-analytics/python/media/remote-sqlcc-from-python3.png)

1. Para las funciones que se admiten en **revoscalepy**, el tiempo de ejecución de Python llama a una función de enlace, que a su vez llama BxlServer.
2. BxlServer se incluye con servicios de aprendizaje de máquina (en bases de datos) y se ejecuta en un proceso independiente del tiempo de ejecución de Python.
3. BxlServer determina el destino de la conexión e inicia una conexión mediante ODBC, pasar las credenciales proporcionadas como parte de la cadena de conexión en el script de Python.
4. BxlServer abre una conexión con la instancia de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
5. Cuando se llama a un tiempo de ejecución de script externo, se invoca el servicio Launchpad, que a su vez inicia el selector adecuado: en este caso, PythonLauncher.dll. A partir de ahí, procesamiento de código Python se trata de un flujo de trabajo similar a la que cuando se invoca el código Python de un procedimiento almacenado de T-SQL.
6. PythonLauncher realiza una llamada a la instancia de la versión de Python que está instalado en el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] equipo.
7. Los resultados se devuelven a BxlServer.
8. SQL Satellite administra la comunicación con [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y la limpieza de los objetos de trabajo relacionados.
9. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] pasa los resultados de vuelta al cliente.

## <a name="next-steps"></a>Pasos siguientes

[Introducción a la arquitectura de Python en SQL Server](architecture-overview-sql-server-python.md)
