---
title: "Modelo de seguridad del Agente de replicaci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "10/07/2015"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Agente de instantáneas, seguridad"
  - "agentes [replicación de SQL Server], seguridad"
  - "Agente de distribución, seguridad"
  - "inicios de sesión [replicación de SQL Server], permisos para agentes"
  - "seguridad [replicación de SQL Server], modelo de seguridad del agente"
  - "Agente de registro del LOG, seguridad"
  - "Agente de lectura de cola, seguridad"
  - "Agente de mezcla, seguridad"
  - "replicación [SQL Server], agentes y perfiles"
ms.assetid: 6d09fc8d-843a-4a7a-9812-f093d99d8192
caps.latest.revision: 72
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 72
---
# Modelo de seguridad del Agente de replicaci&#243;n
  El modelo de seguridad del agente de replicación permite un control concreto sobre las cuentas con las que los agentes de replicación se ejecutan y realizan conexiones: se puede especificar una cuenta diferente para cada agente. Para obtener más información acerca de cómo especificar cuentas, consulte [administrar inicios de sesión y contraseñas en la replicación](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md).  
  
> [!IMPORTANT]  
>  Cuando un miembro de rol fijo de servidor **sysadmin** configura la replicación, los agentes de replicación se pueden configurar para suplantar la cuenta del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Esto se consigue no especificando ningún inicio de sesión ni contraseña para el agente de replicación; no obstante, no se recomienda este enfoque. En su lugar, por seguridad, se recomienda especificar una cuenta para cada agente con los permisos mínimos descritos en la sección "Permisos requeridos por los agentes", más adelante en este tema.  
  
 Los agentes de replicación, como todos los ejecutables, se ejecutan en el contexto de una cuenta de Windows. Los agentes establecen conexiones de seguridad integrada de Windows usando esta cuenta. La cuenta con la que se ejecuta el agente depende de la forma en que se inicie el agente:  
  
-   Inicio del agente desde un trabajo del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (valor predeterminado): cuando se utiliza un trabajo del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para iniciar un agente de replicación, el agente se ejecuta en el contexto de la cuenta que se especifica al configurar la replicación. Para obtener más información acerca del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y la replicación, vea la sección "Seguridad de agentes con el Agente SQL Server", más adelante en este tema. Para obtener información acerca de los permisos que son necesarios para la cuenta en la que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se ejecuta el agente, consulte [Configurar el Agente SQL Server](../../../ssms/agent/configure-sql-server-agent.md).  
  
-   Inicio del agente desde una línea de comandos de MS-DOS (directamente o mediante un script): el agente se ejecuta en el contexto de la cuenta del usuario que ejecuta el agente en la línea de comandos.  
  
-   Inicio del agente desde una aplicación que utiliza Replication Management Objects (RMO) o un control ActiveX: el agente se ejecuta en el contexto de la aplicación que llama a RMO o al control ActiveX.  
  
    > [!NOTE]  
    >  Los controles ActiveX han quedado desusados.  
  
 Se recomienda que las conexiones se realicen en el contexto de la seguridad integrada de Windows. Para mantener la compatibilidad con versiones anteriores, también se puede utilizar la seguridad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obtener más información acerca de las prácticas recomendadas, consulte [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md).  
  
## Permisos requeridos por los agentes  
 Las cuentas con las que los agentes se ejecutan y realizan conexiones requieren diversos permisos. Estos permisos se describen en la siguiente tabla. Se recomienda que cada agente se ejecute con una cuenta de Windows diferente y que solo se concedan los permisos requeridos a la cuenta. Para obtener información acerca de la lista de acceso de publicación (PAL), que es relevante para un número de agentes, consulte [proteger el publicador](../../../relational-databases/replication/security/secure-the-publisher.md).  
  
> [!NOTE]  
>  Control de cuentas de usuario (UAC) de algunos sistemas operativos Windows puede impedir el acceso administrativo al recurso compartido de instantáneas. Por lo tanto, debe conceder de forma explícita permisos del recurso compartido de instantáneas a las cuentas de Windows usadas por el Agente de instantáneas, el Agente de distribución y el Agente de mezcla. Debe hacerlo incluso si las cuentas de Windows pertenecen al grupo Administradores. Para obtener más información, consulte [proteger la carpeta de instantáneas](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
|Agente|Permisos|  
|-----------|-----------------|  
|Agente de instantáneas|La cuenta de Windows con la que se ejecuta el agente se utiliza al realizar conexiones al distribuidor. Esta cuenta debe:<br /><br /> -Como mínimo, ser miembro de la **db_owner** rol fijo de base de datos en la base de datos de distribución.<br /><br /> − Tener permisos de lectura, escritura y modificación en el recurso compartido de instantáneas.<br /><br /> <br /><br /> Tenga en cuenta que la cuenta que se utiliza para *Conectar* al publicador debe ser como mínimo un miembro de la **db_owner** rol fijo de base de datos en la base de datos de publicación.|  
|Agente de registro del LOG|La cuenta de Windows con la que se ejecuta el agente se utiliza al realizar conexiones al distribuidor. Como mínimo, esta cuenta debe ser miembro de la **db_owner** rol fijo de base de datos en la base de datos de distribución.<br /><br /> Como mínimo, la cuenta que se usa para conectarse al publicador debe ser miembro de la **db_owner** rol fijo de base de datos en la base de datos de publicación.<br /><br /> Cuando se selecciona el **sync_type** opciones *sólo compatibilidad con réplica*, *inicializar con copia de seguridad*, o *inicializar desde lsn*, debe ejecutar el agente de lector del registro después de ejecutar **sp_addsubscription**, de modo que los scripts de instalación se escriben en la base de datos de distribución. El agente de registro del LOG se debe ejecutar con una cuenta que sea miembro del rol fijo de servidor **sysadmin** . Cuando el **sync_type** opción está establecida en *automática*, se requiere ninguna acción de agente de lector de registro especial.|  
|Agente de distribución para una suscripción de inserción|La cuenta de Windows con la que se ejecuta el agente se utiliza al realizar conexiones al distribuidor. Esta cuenta debe:<br /><br /> -Como mínimo pertenecer el **db_owner** rol fijo de base de datos en la base de datos de distribución.<br /><br /> − Ser miembro de la PAL.<br /><br /> − Tener permisos de lectura en el recurso compartido de instantáneas.<br /><br /> − Tener permisos de lectura en el directorio de instalación del proveedor OLE DB para el suscriptor si la suscripción es para un suscriptor que no sea de SQL Server.<br /><br /> -Cuando se replican datos LOB, el agente de distribución debe tener permisos de escritura en la replicación **C:\Program Files\Microsoft SQL Server\XX\COMfolder** donde XX representa el identificador de instancia.<br /><br /> <br /><br /> Tenga en cuenta que la cuenta que se utiliza para *Conectar* al suscriptor debe ser como mínimo un miembro de la **db_owner** fija de base de datos en la base de datos de suscripción, o tener permisos equivalentes si la suscripción es para un suscriptor no SQL Server.<br /><br /> Observe también que al usar `-subscriptionstreams >= 2` en el agente de distribución también debe conceder el **View Server State** permiso en los suscriptores para detectar interbloqueos.|  
|Agente de distribución para una suscripción de extracción|La cuenta de Windows con la que se ejecuta el agente se utiliza al realizar conexiones al suscriptor. Como mínimo, esta cuenta debe ser miembro de la **db_owner** rol fijo de base de datos en la base de datos de suscripción. La cuenta utilizada para conectarse al distribuidor debe:<br /><br /> − Ser miembro de la PAL.<br /><br /> − Tener permisos de lectura en el recurso compartido de instantáneas.<br /><br /> -Cuando se replican datos LOB, el agente de distribución debe tener permisos de escritura en la replicación **C:\Program Files\Microsoft SQL Server\XX\COMfolder** donde XX representa el identificador de instancia.<br /><br /> <br /><br /> Tenga en cuenta que al usar `-subscriptionstreams >= 2` en el agente de distribución también debe conceder el **View Server State** permiso en los suscriptores para detectar interbloqueos.|  
|Agente de mezcla para una suscripción de inserción|La cuenta de Windows con la que se ejecuta el agente se utiliza al realizar conexiones al publicador y al distribuidor. Esta cuenta debe:<br /><br /> -Como mínimo pertenecer el **db_owner** rol fijo de base de datos en la base de datos de distribución.<br /><br /> − Ser miembro de la PAL.<br /><br /> − Ser un inicio de sesión asociado a un usuario en la base de datos de publicaciones.<br /><br /> − Tener permisos de lectura en el recurso compartido de instantáneas.<br /><br /> <br /><br /> Tenga en cuenta que la cuenta utilizada para *Conectar* al suscriptor debe ser como mínimo un miembro de la **db_owner** rol fijo de base de datos en la base de datos de suscripción.|  
|Agente de mezcla para una suscripción de extracción|La cuenta de Windows con la que se ejecuta el agente se utiliza al realizar conexiones al suscriptor. Como mínimo, esta cuenta debe ser miembro de la **db_owner** rol fijo de base de datos en la base de datos de suscripción. La cuenta utilizada para conectarse al publicador y al distribuidor debe:<br /><br /> − Ser miembro de la PAL.<br /><br /> − Ser un inicio de sesión asociado a un usuario en la base de datos de publicaciones.<br /><br /> − Ser un inicio de sesión asociado a un usuario en la base de datos de distribución. El usuario puede ser el usuario **Guest** .<br /><br /> − Tener permisos de lectura en el recurso compartido de instantáneas.|  
|Agente de lectura de cola|La cuenta de Windows con la que se ejecuta el agente se utiliza al realizar conexiones al distribuidor. Como mínimo, esta cuenta debe ser miembro de la **db_owner** rol fijo de base de datos en la base de datos de distribución.<br /><br /> Como mínimo, la cuenta que se usa para conectarse al publicador debe ser miembro de la **db_owner** rol fijo de base de datos en la base de datos de publicación.<br /><br /> La cuenta que se usa para conectarse al suscriptor debe ser como mínimo un miembro de la **db_owner** rol fijo de base de datos en la base de datos de suscripción.|  
  
## Seguridad de agentes con el Agente SQL Server  
 Cuando se configura la replicación mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], procedimientos de [!INCLUDE[tsql](../../../includes/tsql-md.md)] o RMO, se crea de forma predeterminada un trabajo del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para cada agente. A continuación, los agentes se ejecutan en el contexto de un paso de trabajo, independientemente de si se ejecutan de forma continua, programada o a petición. Estos trabajos se pueden ver en la carpeta **Trabajos** de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. En la tabla siguiente se enumeran los nombres de los trabajos.  
  
|Agente|Nombre del trabajo|  
|-----------|--------------|  
|Agente de instantáneas|**\< publicador>-\< Basededatosdepublicaciones>-\< publicación>-\< entero>**|  
|Agente de replicación para una partición de publicación de combinación|**Dyn_ \< publicador>-\< Basededatosdepublicaciones>-\< publicación>-\< GUID>**|  
|Agente de registro del LOG|**\< publicador>-\< Basededatosdepublicaciones>-\< entero>**|  
|Agente de mezcla para suscripciones de extracción|**\< publicador>-\< Basededatosdepublicaciones>-\< publicación>-\< suscriptor>-\< Basededatosdesuscripciones>-\< entero>**|  
|Agente de mezcla para suscripciones de inserción|**\< publicador>-\< Basededatosdepublicaciones>-\< publicación>-\< suscriptor>-\< entero>**|  
|Agente de distribución para suscripciones de inserción|**\< publicador>-\< Basededatosdepublicaciones>-\< publicación>-\< suscriptor>-\< entero>***|  
|Agente de distribución para suscripciones de extracción|**\< publicador>-\< Basededatosdepublicaciones>-\< publicación>-\< suscriptor>-\< Basededatosdesuscripciones>-\< GUID>***\*|  
|Agente de distribución para suscripciones de inserción en suscriptores que no sean de SQL Server|**\< publicador>-\< Basededatosdepublicaciones>-\< publicación>-\< suscriptor>-\< entero>**|  
|Agente de lectura de cola|**[\< distribuidor>]. \< entero>**|  
  
 \*Para las suscripciones de inserción a publicaciones de Oracle, que es el nombre del trabajo **\< publicador>-\< publicador**> en lugar de **\< publicador>-\< Basededatosdepublicaciones>**.  
  
 \*\*Para las suscripciones de extracción a publicaciones de Oracle, que es el nombre del trabajo **\< publicador>-\< DistributionDatabase**> en lugar de **\< publicador>-\< Basededatosdepublicaciones>**.  
  
 Al configurar la replicación se especifican las cuentas en las que se ejecutarán los agentes. No obstante, todos los pasos del trabajo se ejecutan en el contexto de seguridad de un *proxy*, por lo que la replicación lleva a cabo internamente las siguientes asignaciones para las cuentas de agente que especifique:  
  
-   La cuenta se asigna primero a una credencial utilizando la instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] [de](../../../t-sql/statements/create-credential-transact-sql.md) . [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizan credenciales para almacenar información acerca de las cuentas de usuario de Windows.  
  
-   El [sp_add_proxy](../../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md) se llama al procedimiento almacenado y la credencial se utiliza para crear un proxy...  
  
> [!NOTE]  
>  Esta información se facilita para ayudarle a entender las implicaciones de ejecutar agentes con el contexto de seguridad adecuado. No debería ser necesario interactuar directamente con las credenciales o los proxy que se hayan creado.  
  
## Vea también  
 [Prácticas recomendadas de seguridad de replicación](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Seguridad y protección & #40; Replicación y nº 41;](../../../relational-databases/replication/security/security-and-protection-replication.md)   
 [Proteger la carpeta de instantáneas](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  