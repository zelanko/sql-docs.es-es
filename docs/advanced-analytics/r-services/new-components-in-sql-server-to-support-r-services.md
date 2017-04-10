---
title: "Los nuevos componentes de SQL Server para admitir servicios de R | Microsoft Docs"
ms.custom: ""
ms.date: "06/03/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 54e9ef3f-1136-471e-865a-7cf013673186
caps.latest.revision: 9
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 9
---
# Los nuevos componentes de SQL Server para admitir servicios de R

[!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)] incluye nuevos componentes, proporcionados por el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] motor de base de datos, que admiten la extensibilidad para el lenguaje R. Administra la seguridad para estos componentes [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y se describen en detalle más adelante.

## Los proveedores y los nuevos componentes de SQL Server

Además el shell que carga R y ejecuta código R tal como se describe en la información general de arquitectura, [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] incluye estos componentes adicionales.

### **LaunchPad** 
  El [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] es un nuevo servicio suministrado por [!INCLUDE[ssCurrent_md](../../includes/sscurrent-md.md)] para admitir la ejecución de scripts externos, similares a la forma en que el servicio de indización y consulta de texto completo inicia un host independiente para procesar las consultas de texto completo. 
  
  El servicio Launchpad iniciará sólo confianza iniciadores que se publican por Microsoft, o certificadas por Microsoft como cumplen los requisitos de rendimiento y administración de recursos. En [!INCLUDE[ssCurrent_md](../../includes/sscurrent-md.md)], R es actualmente el lenguaje externo solo admitido la [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)].
  
  El [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] service se ejecuta en su propia cuenta de usuario. Cada proceso de satélite en tiempo de ejecución de un idioma específico heredará la cuenta de usuario de Launchpad. Para obtener más información sobre la configuración y el contexto de seguridad del Launchpad, consulte [Introducción a la seguridad](../../advanced-analytics/r-services/security-overview-sql-server-r-services.md).

### **BxlServer y satélite SQL**
  BxlServer es un archivo ejecutable proporcionado por Microsoft que administra la comunicación entre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y el tiempo de ejecución de R y también implementa funciones de utilizar otros equipos. Crea los objetos de trabajo de Windows que se utilizan para contener las sesiones de R, carpetas de trabajo seguro disposiciones para cada trabajo de R y utiliza SQL satélite para administrar la transferencia de datos entre R y [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].  

  De hecho, BxlServer es un complemento de R que funciona con [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] para admitir la integración de R con SQL Server. BXL significa lenguaje de intercambio binario y hace referencia al formato de datos que se utiliza para mover datos de manera eficaz entre SQL Server y procesos externos como R. 

 Satélite de SQL es una nueva API de extensibilidad en SQL Server 2016 proporcionado por el motor de base de datos para admitir código externo o tiempos de ejecución externo de implementada mediante C o C++. Actualmente, R es el único runtime compatible. BxlServer usa SQL satélite para la comunicación con [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
 
  Satélite SQL utiliza un formato de datos personalizado que se optimiza para transferir datos entre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y lenguajes de secuencias de comandos externos. Realiza conversiones de tipos y define los esquemas de los conjuntos de datos de entrada y salida durante las comunicaciones entre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y r.

  BxlServer usa SQL satélite para estas tareas: 
  - Leer datos de entrada
  - Escribir datos de salida
  - Obtener argumentos de entrada
  - Argumentos de salida de escritura
  - Control de errores
  - Escritura de STDOUT y STDERR en el cliente

  Satélite SQL puede supervisarse con eventos extendidos. Para obtener más información, consulte [Extended Events para los servicios de SQL Server R](../../advanced-analytics/r-services/extended-events-for-sql-server-r-services.md).


## Canales de comunicación entre componentes

+ **TCP/IP** de forma predeterminada, la comunicación interna entre [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y satélite SQL utilizan TCP/IP.

+ **Canalizaciones con nombre**

  Transporte de datos internas entre el BxlServer y [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] a través de satélite de SQL utiliza un formato de datos comprimidos, propietario para mejorar el rendimiento. Datos de memoria de R a BxlServer se intercambian a través de canalizaciones con nombre en formato BXL. 
  
+ **ODBC** las comunicaciones entre los clientes de ciencia de datos externos y el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instancia utilizar ODBC. La cuenta que envía la R trabajos a [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] debe tener ambos permisos para conectarse a la instancia y ejecutar scripts externos. Además, la cuenta debe tener permiso de acceso a los datos usados por el trabajo, al escribir los datos (por ejemplo, si guardar los resultados en una tabla) o para crear objetos de base de datos (por ejemplo, si guarda las funciones de R como parte de un nuevo procedimiento almacenado).

  Cuando [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] es usar como el contexto de cálculo para un trabajo de R se envía desde un cliente remoto y el comando R debe recuperar datos desde un origen externo, se utiliza ODBC para la escritura diferida. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] se asignan la identidad del usuario que emite el comando R remoto a la identidad del usuario en la instancia actual y ejecute el comando ODBC con las credenciales del usuario. La cadena de conexión necesaria para realizar esta llamada ODBC se obtiene del código de cliente.
  
  Se pueden realizar llamadas ODBC adicionales dentro de la secuencia de comandos utilizando **RODBC**. RODBC es un paquete de R popular utilizado para obtener acceso a datos en bases de datos relacionales; Sin embargo, su rendimiento es generalmente más lento que los proveedores comparables de usar [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]. Muchas secuencias de comandos de R utilizan embedded llamadas a RODBC como una manera de recuperar los conjuntos de datos "secundaria" para su uso en el análisis. Por ejemplo, el procedimiento almacenado que entrena un modelo podría definir una consulta SQL para obtener los datos de entrenamiento de un modelo, pero usar una llamada RODBC incrustada para obtener factores adicionales, para realizar búsquedas o para obtener nuevos datos de orígenes externos, como archivos de texto o Excel.

  El código siguiente muestra una llamada RODBC incrustada en un script de R:
   ~~~~
  library(RODBC);
  connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
  dbhandle <- odbcDriverConnect(connStr)
  OutputDataSet <- sqlQuery(dbhandle, "select * from table_name");
  ~~~~

+ **Otros protocolos** procesos que quizás necesite trabajar en "fragmentos" o transferir datos a un cliente remoto también pueden usar el. Formato XDF compatible con la transferencia de datos real de R. de Microsoft es a través de blobs codificados.

## Interacción de componentes

La arquitectura de componentes descrito anteriormente se ha proporcionado para garantizar que el código fuente abierto R puede trabajar "tal cual", mientras que, en gran medida la proporciona mejor rendimiento para el código que se ejecuta en un [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] equipo. El mecanismo de cómo interactúan los componentes con el tiempo de ejecución de R y el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] motor de base de datos difiere ligeramente, dependiendo de cómo se inicia el código R. En esta sección se resumen los escenarios clave. 
 
### Scripts de R que se ejecutan desde SQL Server (en bases de datos)

Código de R que se ejecuta desde "interior" [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] se ejecuta mediante una llamada a un procedimiento almacenado. Por lo tanto, cualquier aplicación que se puede llamar a un procedimiento almacenado puede iniciar la ejecución de código R.  A partir de entonces [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] administra la ejecución de código R, como se resume en el diagrama siguiente.

![rsql_indb780-01](../../advanced-analytics/r-services/media/rsql-indb780-01.png)

1. Una solicitud para el tiempo de ejecución de R se indica mediante el parámetro _@language = 'R'_ pasa al procedimiento almacenado, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Esta solicitud se envía al servicio Launchpad.
2. El servicio Launchpad inicia el selector adecuado; en este caso, RLauncher.
3. RLauncher inicia el proceso externo de R.
4. Coordenadas BxlServer con el tiempo de ejecución de R para administrar los intercambios de datos con [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y el almacenamiento de los resultados del trabajo.
5. En resumen, SQL satélite administra las comunicaciones acerca de tareas relacionadas y procesa con [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
6. BxlServer SQL satélite se utiliza para comunicar el estado y los resultados a [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
7. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Obtiene los resultados y cierra los procesos y tareas relacionadas. 


### Scripts de R que se ejecuta desde un cliente remoto

Al conectarse desde un cliente de ciencia de datos remota que admita Microsoft R, puede ejecutar funciones de R en el contexto de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] mediante las funciones de utilizar otros equipos. Esto es un flujo de trabajo diferente de la anterior y se resume en el diagrama siguiente.


![rsql_fromR2db-01](../../advanced-analytics/r-services/media/rsql-fromr2db-01.png)

1. Para las funciones de utilizar otros equipos, el tiempo de ejecución de R llama a una función de enlace que a su vez llama a BxlServer. 
2. BxlServer se proporciona con Microsoft R y se ejecuta en un proceso independiente del tiempo de ejecución de R.
3. BxlServer determina el destino de la conexión y se inicia una conexión mediante ODBC, pasando las credenciales proporcionadas como parte de la cadena de conexión en el objeto de origen de datos de R.
4. BxlServer abre una conexión con el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] instancia.
5. En una llamada de R, LaunchPad, se invoca el servicio, que es el turno inicia el selector adecuado, RLauncher. Posteriormente, el procesamiento del código R es similar al proceso para ejecutar código R de T-SQL.
6. RLauncher realiza una llamada a la instancia de ejecución R que se instala en el [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] equipo. 
7. Se devuelven resultados a BxlServer.
8. Administra la comunicación con SQL satélite [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] y limpieza de los objetos de trabajo relacionados.
9. [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] pasa los resultados al cliente.

## Vea también
[Información general sobre la arquitectura](../../advanced-analytics/r-services/architecture-overview-sql-server-r-services.md)
