---
title: Componentes de SQL Server para admitir R | Documentos de Microsoft
ms.custom: 
ms.date: 04/05/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 54e9ef3f-1136-471e-865a-7cf013673186
caps.latest.revision: 9
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e2bff53d3e324999c7cdca743d6e7b2ff9f85780
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="components-in-sql-server-to-support-r"></a>Componentes de SQL Server al soporte técnico de R

En SQL Server 2016 y de 2017, el motor de base de datos incluye los componentes opcionales que admiten la extensibilidad para los lenguajes de script externo, como R y Python. Se agregó compatibilidad con el lenguaje R en SQL Server 2016; compatibilidad con Python se agregó en servicios de aprendizaje de máquina de SQL Server de 2017.

En este tema se describe los nuevos componentes que funcionan específicamente con el lenguaje R. Para obtener una explicación de cómo funcionan estos componentes con R de código abierto, consulte [interoperabilidad de R](r-interoperability-in-sql-server.md)

## <a name="components-and-providers"></a>Componentes y proveedores

Además del shell que carga R y ejecuta código R tal como se describe en la información general sobre la arquitectura, [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] incluye estos componentes adicionales.

### <a name="launchpad"></a>Launchpad 

El [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] es un servicio proporcionado por [!INCLUDE[ssCurrent_md](../../includes/sscurrent-md.md)] para admitir la ejecución de scripts externos, similares a la manera en que el servicio de indización y consulta de texto completo inicia un host independiente para procesar las consultas de texto completo.

El servicio Launchpad solo iniciará selectores de confianza publicados por Microsoft o que, según Microsoft, cumplan los requisitos de rendimiento y administración de recursos. La denominación de los iniciadores específicos del idioma es sencilla:

  + R - RLauncher.dll
  + Python - PythonLauncher.dll

El servicio [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] se ejecuta en su propia cuenta de usuario. Cada proceso satélite de un tiempo de ejecución de un lenguaje específico heredará la cuenta de usuario de Launchpad. Para obtener más información sobre la configuración y el contexto de seguridad de Launchpad, consulte [información general sobre seguridad](../../advanced-analytics/r/security-overview-sql-server-r.md).

### <a name="bxlserver-and-sql-satellite"></a>BxlServer y satélite SQL

BxlServer es un archivo ejecutable proporcionado por Microsoft que administra la comunicación entre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y el runtime de R y también implementa las funciones de RevoScaleR. Crea los objetos de trabajo de Windows que se usan para contener sesiones de R, aprovisiona carpetas de trabajo seguras para cada trabajo de R y usa SQL Satellite para administrar la transferencia de datos entre R y [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].

De hecho, BxlServer es un complemento de R que funciona con [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] para admitir la integración de R con SQL Server. BXL hace referencia al lenguaje de intercambio binario y hace referencia a los formatos de datos utilizados para mover datos eficazmente entre SQL Server y procesos externos, como R. BxlServer.dll también se instala al instalar Microsoft R Client o Microsoft R Server.

SQL Satellite es una nueva API de extensibilidad de SQL Server 2016 proporcionada por el motor de base de datos para admitir código externo o tiempos de ejecución externos implementados mediante C o C++. BxlServer usa SQL Satellite para la comunicación con [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].

SQL Satellite usa un formato de datos personalizado que está optimizado para transferir datos entre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y lenguajes de script externos. Realiza conversiones de tipos y define los esquemas de los conjuntos de datos de entrada y salida durante las comunicaciones entre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y R.

BxlServer usa SQL Satellite para las tareas siguientes:

  + Leer datos de entrada
  + Escribir datos de salida
  + Obtener argumentos de entrada
  + Escribir argumentos de salida
  + Control de errores
  + Errores al cliente y salida estándar de escritura

SQL Satellite puede supervisarse mediante eventos extendidos. Para obtener más información, vea [Extended Events for SQL Server R Services](extended-events-for-sql-server-r-services.md) (Eventos extendidos para SQL Server R Services).

## <a name="communication-channels-between-components"></a>Canales de comunicación entre componentes

+ **TCP/IP**

    De forma predeterminada, la comunicación interna entre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y la licencia de satélite SQL utilizan TCP/IP.

+ **Canalizaciones con nombre**

    Transporte de datos interna entre el BxlServer y [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] vía satélite de SQL utiliza un formato de datos propietario, comprimida para mejorar el rendimiento. Los datos que van de la memoria de R a BxlServer se intercambian a través de canalizaciones con nombre en formato BXL.

+ **ODBC**

    Las comunicaciones entre los clientes de ciencia de datos externos y el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instancia utilizar ODBC. La cuenta que envía los trabajos de R a [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] debe tener permisos para conectarse a la instancia y para ejecutar scripts externos. Además, la cuenta debe tener permiso para obtener acceso a los datos que use el trabajo, para escribir datos (por ejemplo, si se guardan resultados en una tabla) o para crear objetos de base de datos (por ejemplo, si se guardan funciones de R como parte de un nuevo procedimiento almacenado).

    Cuando se usa [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] como contexto de cálculo para un trabajo de R enviado desde un cliente remoto y el comando de R debe recuperar datos de un origen externo, se usa ODBC para la escritura diferida. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] asignará la identidad del usuario mediante la emisión del comando de R remoto a la identidad del usuario en la instancia actual y ejecutará el comando ODBC con las credenciales del usuario. La cadena de conexión necesaria para realizar esta llamada ODBC se obtiene del código de cliente.

    Se pueden realizar llamadas ODBC adicionales dentro del script mediante **RODBC**. RODBC es un popular paquete de R que se usa para obtener acceso a datos de bases de datos relacionales, pero su rendimiento suele ser más lento que el de proveedores equiparables usados por [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Muchos scripts de R usan llamadas insertadas a RODBC como una manera de recuperar conjuntos de datos "secundarios" para su uso en el análisis. Por ejemplo, el procedimiento almacenado que entrena un modelo podría definir una consulta SQL para obtener datos para entrenar un modelo, pero podría usar una llamada RODBC insertada para obtener factores adicionales, realizar búsquedas u obtener nuevos datos de orígenes externos, como archivos de texto o Excel.

    El código siguiente muestra una llamada RODBC insertada en un script de R:

    ```R
    library(RODBC);
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    dbhandle <- odbcDriverConnect(connStr)
    OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
    ```

+ **Otros protocolos**

    También pueden usar los procesos que pueden necesitar trabajar en "fragmentos" o transferir datos a un cliente remoto el. Formato de xdf. compatible con la transferencia de datos de Microsoft R. real es a través de blobs codificados.

## <a name="interaction-of-components"></a>Interacción de componentes

La arquitectura de componentes descrita anteriormente se ha proporcionado para garantizar que el código fuente abierto de R puede funcionar "tal cual", a la vez que proporciona un rendimiento considerablemente mejorado para el código que se ejecuta en un equipo con [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. La forma en que interactúan los componentes con el tiempo de ejecución de R y el motor de base de datos de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] difiere ligeramente, en función de cómo se inicie el código de R. En esta sección se resumen los escenarios clave.

### <a name="r-scripts-executed-from-sql-server-in-database"></a>Scripts de R ejecutados desde SQL Server en bases de datos

El código de R que se ejecuta desde "dentro" de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] se ejecuta mediante una llamada a un procedimiento almacenado. Por lo tanto, cualquier aplicación que pueda llamar a un procedimiento almacenado podrá iniciar la ejecución de código de R.  A partir de entonces, [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] administra la ejecución del código de R, como se resume en el diagrama siguiente.

![rsql_indb780-01](media/script_in-db-r.png)

1. Mediante el parámetro _@language='R'_ pasado al procedimiento almacenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), se indica una solicitud para el tiempo de ejecución de R. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] envía esta solicitud al servicio Launchpad.
2. El servicio Launchpad inicia el selector adecuado, en este caso, RLauncher.
3. RLauncher inicia el proceso externo de R.
4. BxlServer coordina con el tiempo de ejecución de R la administración de los intercambios de datos con [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y el almacenamiento de los resultados del trabajo.
5. SQL satélite administra las comunicaciones acerca de las tareas relacionadas y procesa con [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
6. BxlServer usa SQL Satellite para comunicarle el estado y los resultados a [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
7. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] obtiene los resultados y cierra las tareas y los procesos relacionados.

### <a name="r-scripts-executed-from-a-remote-client"></a>Scripts de R ejecutados desde un cliente remoto

Cuando se conecta desde un cliente de ciencia de datos remotos que admita Microsoft R, puede ejecutar las funciones de R en el contexto de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mediante el uso de las funciones de RevoScaleR. Este es un flujo de trabajo diferente del anterior y se resume en el diagrama siguiente.

![rsql_fromR2db-01](media/remote-sqlcc-from-r2.png)

1. Para las funciones de RevoScaleR, el runtime de R llama a una función de vinculación que a su vez llama BxlServer.
2. BxlServer se proporciona con Microsoft R y se ejecuta en un proceso independiente del tiempo de ejecución de R.
3. BxlServer determina el destino de la conexión e inicia una conexión mediante ODBC. Para ello, pasa las credenciales proporcionadas como parte de la cadena de conexión en el objeto de origen de datos de R.
4. BxlServer abre una conexión con la instancia de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
5. Para una llamada de R, Launchpad se invoca el servicio, que es a su vez, inicia el selector adecuado, RLauncher. Posteriormente, el procesamiento del código de R es similar al proceso para ejecutar código de R desde T-SQL.
6. RLauncher realiza una llamada a la instancia del tiempo de ejecución de R que está instalada en el equipo con [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
7. Los resultados se devuelven a BxlServer.
8. SQL Satellite administra la comunicación con [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y la limpieza de los objetos de trabajo relacionados.
9. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] pasa los resultados de vuelta al cliente.

## <a name="next-steps"></a>Pasos siguientes

[Introducción a la arquitectura](architecture-overview-sql-server-r.md)

[Información general sobre seguridad](security-overview-sql-server-r.md)

[Consideraciones de seguridad](security-considerations-for-the-r-runtime-in-sql-server.md)

