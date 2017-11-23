---
title: "Información general (SMO) | Documentos de Microsoft"
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: e988f9e8-6801-41d1-8069-726f487244d5
caps.latest.revision: "69"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 3a768d79345789dfbe9e33dc885e296928429e01
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="overview-smo"></a>Información general (SMO)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO) son objetos diseñados para la administración mediante programación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede usar SMO para crear aplicaciones de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] personalizadas. Aunque [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] es una aplicación eficaz y completa para administrar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], habrá ocasiones en las que resultará más conveniente usar una aplicación SMO.  
  
 Por ejemplo, es posible que haya que simplificar las aplicaciones de usuario que controlan las tareas de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para satisfacer las necesidades de nuevos usuarios y reducir los costes de aprendizaje. Quizá tenga que crear bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] personalizadas o crear una aplicación para crear y supervisar la eficacia de los índices. También podría utilizarse una aplicación SMO para incluir hardware o software de terceros sin ningún tipo de problema en la aplicación de administración de base de datos.  
  
 Dado que SMO es compatible con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores, puede administrar fácilmente un entorno multiversión.  
  
 Características de SMO son los siguientes:  
  
-   Modelo de objetos de caché y creación de instancias de objetos optimizada. Los objetos solo se cargan cuando se hace referencia a ellos de forma específica. Las propiedades de objeto solo se cargan parcialmente cuando se crea el objeto. Los objetos y propiedades restantes se cargan cuando se hace referencia a ellos directamente.  
  
-   Ejecución por lotes de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)]. Las instrucciones se ejecutan por lotes para mejorar el rendimiento de la red.  
  
-   Captura de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)]. Permite capturar cualquier operación en un script. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] usa esta capacidad para crear script de una operación en lugar de ejecutarla inmediatamente.  
  
-   Administración de servicios [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el proveedor WMI. Los servicios [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden iniciarse, detenerse y ponerse en pausa mediante programación.  
  
-   Generación de scripting avanzada. Es posible crear scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] para recrear objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que describen relaciones con otros objetos en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Uso de nombres de recurso únicos (URN). Un URN permite crear instancias y hacer referencia a objetos SMO.  
  
 SMO también representa como nuevos objetos o propiedades muchas características y componentes que se introdujeron en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Entre estas características y componentes nuevos se incluyen los siguientes:  
  
-   Partición de tablas e índices para el almacenamiento de datos en un esquema de partición. Para obtener más información, consulte [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
-   Extremos HTTP para administrar solicitudes SOAP. Para obtener más información, consulte [Implementing Endpoints](../../relational-databases/server-management-objects-smo/tasks/implementing-endpoints.md).  
  
-   Aislamiento de instantánea y control de versiones de nivel de fila de cara a una mayor simultaneidad. Para obtener más información, consulte [trabajar con aislamiento de instantánea](../../relational-databases/native-client/features/working-with-snapshot-isolation.md).  
  
-   Colección de esquemas XML, índices XML y tipos de datos XML que proporcionan validación y almacenamiento de datos XML. Para obtener más información, vea [colecciones de esquemas XML &#40; SQL Server &#41; ](../../relational-databases/xml/xml-schema-collections-sql-server.md) y [mediante esquemas XML](../../relational-databases/server-management-objects-smo/tasks/using-xml-schemas.md).  
  
-   Bases de datos de instantánea para crear copias de solo lectura de bases de datos.  
  
-   [!INCLUDE[ssSB](../../includes/sssb-md.md)] permite una comunicación basada en mensajes. Para obtener más información, consulte [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md).  
  
-   Compatibilidad con sinónimos para varios nombres de objetos de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [sinónimos &#40; motor de base de datos &#41;](../../relational-databases/synonyms/synonyms-database-engine.md).  
  
-   Administración del Correo electrónico de base de datos, que permite crear servidores de correo electrónico, perfiles del correo electrónico y cuentas de correo electrónico en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [Correo electrónico de base de datos](../../relational-databases/database-mail/database-mail.md).  
  
-   Servidores registrados que admiten el registro de información de conexión. Para obtener más información, consulte [registrar servidores](../../tools/sql-server-management-studio/register-servers.md).  
  
-   Seguimiento y reproducción de eventos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md), [SQL Trace](../../relational-databases/sql-trace/sql-trace.md), [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md), y [Extended Events](../../relational-databases/extended-events/extended-events.md).  
  
-   Compatibilidad con certificados y claves para el control de seguridad. Para obtener más información, consulte [jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md).  
  
-   Desencadenadores DDL para agregar funcionalidad cuando se producen eventos DDL. Para más información, consulte [DDL Triggers](../../relational-databases/triggers/ddl-triggers.md).  
  
 El espacio de nombres de SMO es <xref:Microsoft.SqlServer.Management.Smo>. SMO se implementa como un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] ensamblado. Esto significa que common language runtime desde la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] versión 2.0 debe estar instalada antes de usar los objetos SMO. Los ensamblados SMO se instalan de forma predeterminada en la memoria caché de ensamblados global (GAC) con la opción SDK de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los ensamblados se encuentran en C:\Program Files\Microsoft SQL Server\130\SDK\Assemblies\. Para obtener más información, consulte el [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] documentación.  
  
## <a name="smo-classes"></a>Clases SMO  
 Las clases SMO incluyen dos categorías: clases de instancia y clases de utilidad.  
  
 **Clases de instancia**  
  
 Las clases de instancia representan objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como servidores, bases de datos, tablas, desencadenadores y procedimientos almacenados. La clase <xref:Microsoft.SqlServer.Management.Common.ServerConnection> se usa para establecer una conexión con la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y controlar el modo de captura de los comandos que se envían.  
  
 Los objetos de instancia SMO forman una jerarquía que representa la jerarquía de un servidor de base de datos. En la parte superior se encuentran las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], bajo las cuales están las bases de datos, seguidas de las tablas, columnas, desencadenadores, etc. Si es lógico que haya una relación de un elemento primario a varios elementos secundarios, como en el caso de una tabla que tiene una o más columnas, el elemento secundario se representa mediante una colección de objetos. De lo contrario, el elemento secundario se representa simplemente mediante un objeto.  
  
 **Clases de utilidad**  
  
 Las clases de utilidad son grupos de objetos creados explícitamente para realizar tareas concretas. Se han dividido en distintas jerarquías de objetos basadas en su función:  
  
-   Clase de transferencia. Se usa para transferir esquemas y datos a otra base de datos.  
  
-   Clases de copia de seguridad y restauración Se usan para realizar copias de seguridad y restaurar bases de datos.  
  
-   Clase Scripter. Se usa para crear archivos de script para la regeneración de objetos y sus dependencias.  
  
## <a name="smo-features"></a>Características de SMO  
 **Rendimiento optimizado**  
  
 La arquitectura SMO es eficaces en cuanto a memoria porque solo parcialmente se crean instancias de objetos al principio y se solicita información de propiedad mínimo desde el servidor. La creación de instancias completas de los objetos se retrasa hasta que se hace referencia al objeto de forma explícita. Se crea una instancia completa de un objeto cuando se solicita una propiedad que no está en el conjunto de propiedades que se recuperan al principio o cuando se llama a un método que requiere dicha propiedad. La transición entre la creación de instancias parciales e instancias completas de los objetos es transparente para el usuario. Además, algunas propiedades que usan mucha memoria no se recuperan nunca, a menos que se haga referencia a ellas de forma explícita. Un ejemplo de esto último sería la propiedad <xref:Microsoft.SqlServer.Management.Smo.Database.Size%2A> de la propiedad de objeto <xref:Microsoft.SqlServer.Management.Smo.Database>. Sin embargo, la creación de instancias parciales requiere más ciclos de ida y vuelta en la red y no es la mejor opción de rendimiento para la aplicación.  
  
 Puede controlar la creación de instancias para que se ajuste al entorno del sistema. La dependencia de la creación de instancias retrasada minimiza la cantidad de memoria que requiere la aplicación, aunque puede desencadenar muchas solicitudes al servidor cuando se hace referencia a las propiedades.  
  
 Las clases de instancia, objetos que representan objetos de base de datos reales, pueden existir en tres niveles distintos de creación de instancias. El nivel de creación de instancias puede ser mínimo (solo se leen las propiedades mínimas necesarias en un bloque), parcial (todas las propiedades que usan una cantidad de memoria relativamente grande se leen en un bloque) y completo. Los estados tradicionales de creación de instancias son no creada o completamente creada. El estado de creación de instancias parcial aumenta la eficacia, puesto que un objeto del que se ha creado una instancia parcial no contiene valores para todo su conjunto completo de propiedades. La creación de instancias parciales es el estado predeterminado de un objeto al que no se hace referencia directamente. Cuando se hace referencia a una de estas propiedades, se genera un error que solicita la creación de una instancia completa del objeto.  
  
 **Ejecución de captura**  
  
 La ejecución directa es el método habitual de ejecución. Las instrucciones se envían directamente a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a medida que se generan. La ejecución de captura constituye una alternativa al método habitual de ejecución.  
  
 La ejecución de captura permite capturar lotes [!INCLUDE[tsql](../../includes/tsql-md.md)] que, en condiciones normales, se ejecutarían. Esto permite al programador de SMO aplazar el script, almacenarlo para ejecutarlo posteriormente o proporcionar una vista previa al usuario final. Por ejemplo, es posible enviar una instrucción **create database**, **create table**y **create index** en un lote y, a continuación, realizar la ejecución en tres pasos secuenciales. El usuario es quien controla esta funcionalidad utilizando el objeto <xref:Microsoft.SqlServer.Management.Smo.Server.%23ctor%2A>.  
  
 **Proveedor WMI**  
  
 SMO encapsula los objetos de proveedor WMI. Esto proporciona al programador de SMO un modelo de objetos simple muy similar a las clases SMO, sin necesidad de que entienda el modelo de programación representado por el espacio de nombres ni los detalles del proveedor WMI de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El proveedor WMI permite configurar servicios, alias y bibliotecas de red de cliente y de servidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Scripting**  
  
 En SMO, se han realizado mejoras en la creación de script, que se ha trasladado a la clase **Scripter** . La clase **Scripter** puede detectar dependencias, entender las relaciones entre objetos y habilitar la manipulación de la jerarquía de dependencias. El principal objeto de creación de script es el objeto **Scripter** . Hay también varios objetos de soporte que administran las dependencias y responden a eventos de progreso o error.  
  
 El objeto **Scripter** admite las siguientes opciones avanzadas de creación de script:  
  
-   Creación de script simple de 1 fase (crea el script en un solo paso)  
  
-   Avanzadas de scripting de 3 fases (crea el script en tres pasos: detección de dependencias, generación de lista, generación de script)  
  
-   Detección de dependencias bidireccional (permite detectar dependencias o dependientes)  
  
-   Respuesta a eventos de progreso  
  
-   Respuesta a eventos de error  
  
 **Nombres de recurso únicos**  
  
 Un concepto clave para utilizar la biblioteca de objetos SMO es el nombre de recurso único (URN). El URN usa una sintaxis similar a XPath. XPath es una ruta de acceso jerárquica que se usa para especificar un objeto en el que cada nivel tiene calificadores y funciones. En SMO, el URN tiene dos elementos, la ruta de acceso y la denominación de atributo, que tiene una funcionalidad limitada. La ruta de acceso se usa para especificar la ubicación del objeto, mientras que la denominación de atributo permite un grado de filtrado.  
  
 Un ejemplo de un URN para una base de datos sería  
  
```  
/Server/Database[@Name='Adventureworks2012']  
```  
  
 El URN de un objeto puede recuperarse haciendo referencia a su propiedad URN. El objeto Scripter también usa los URN como parámetros que pasan referencias de objeto al método del objeto **Scripter** . Además, puede especificarse un URN para el método **GetSmoObject** del objeto **Server** . Se utiliza para crear una instancia del objeto SMO.  
  
## <a name="sql-server-features-represented-in-smo"></a>Características de SQL Server representadas en SMO  
 **Tabla de particiones e índices**  
  
 Las particiones de tabla e índice permiten administrar la difusión de los datos de tablas e índices a través de grupos de archivos. Esta nueva característica se representa mediante objetos SMO.  
  
 **Puntos de conexión**  
  
 Los extremos administran las solicitudes SOAP y de creación de reflejo de base de datos utilizando el objeto <xref:Microsoft.SqlServer.Management.Smo.Endpoint>.  
  
 **Versiones de nivel de aislamiento/fila de instantánea**  
  
 El aislamiento de instantánea (control de versiones de nivel de fila) se representa mediante nuevas propiedades de objeto <xref:Microsoft.SqlServer.Management.Smo.Database>.  
  
 **Namespace de esquema XML, índices XML y tipos de datos XML**  
  
 Los espacios de nombres de esquema XML se representan en SMO mediante una colección de objetos. Los índices XML se representan en SMO mediante una propiedad de objeto **Index** .  
  
 **Mejoras en la búsqueda de texto completo**  
  
 En SMO, se proporcionan nuevos objetos que representan las mejoras en la búsqueda de texto completo.  
  
 **Comprobación de páginas**  
  
 El objeto <xref:Microsoft.SqlServer.Management.Smo.DatabaseOptions.PageVerify%2A> representa las opciones de comprobación de páginas de base de datos.  
  
 **Bases de datos de instantánea**  
  
 Una base de datos de instantánea es una copia de solo lectura de una base de datos especificada en un punto concreto del tiempo. Una base de datos de instantánea puede especificarse utilizando la propiedad <xref:Microsoft.SqlServer.Management.Smo.Database.IsDatabaseSnapshot%2A> del objeto <xref:Microsoft.SqlServer.Management.Smo.Database>.  
  
 **Service Broker**  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] y su funcionalidad se representan mediante un grupo de objetos  
  
 **Mejoras de índice**  
  
 Las mejoras de índice [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se representan mediante nuevas propiedades del objeto <xref:Microsoft.SqlServer.Management.Smo.Index>.  
  
## <a name="see-also"></a>Vea también  
 [Replication Management Objects Concepts (Conceptos de Replication Management Objects)](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)  
  
  
