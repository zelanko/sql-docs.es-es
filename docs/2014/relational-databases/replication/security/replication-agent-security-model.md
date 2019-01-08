---
title: Modelo de seguridad del Agente de replicación | Microsoft Docs
ms.custom: ''
ms.date: 10/07/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Snapshot Agent, security
- agents [SQL Server replication], security
- Distribution Agent, security
- logins [SQL Server replication], permissions for agents
- security [SQL Server replication], agent security model
- Log Reader Agent, security
- Queue Reader Agent, security
- Merge Agent, security
- replication [SQL Server], agents and profiles
ms.assetid: 6d09fc8d-843a-4a7a-9812-f093d99d8192
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f34b5accc278a55946546c149c00bffd3a02a693
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52812003"
---
# <a name="replication-agent-security-model"></a>Modelo de seguridad del Agente de replicación
  El modelo de seguridad del agente de replicación permite un mayor control sobre las cuentas en la que los agentes de replicación ejecutan y realizan conexiones: Se puede especificar una cuenta diferente para cada agente. Para obtener más información sobre cómo especificar cuentas, vea [Administrar inicios de sesión y contraseñas en la replicación](manage-logins-and-passwords-in-replication.md).  
  
> [!IMPORTANT]  
>  Cuando un miembro de rol fijo de servidor **sysadmin** configura la replicación, los agentes de replicación se pueden configurar para suplantar la cuenta del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Esto se consigue no especificando ningún inicio de sesión ni contraseña para el agente de replicación; no obstante, no se recomienda este enfoque. En su lugar, por seguridad, se recomienda especificar una cuenta para cada agente con los permisos mínimos descritos en la sección "Permisos requeridos por los agentes", más adelante en este tema.  
  
 Los agentes de replicación, como todos los ejecutables, se ejecutan en el contexto de una cuenta de Windows. Los agentes establecen conexiones de seguridad integrada de Windows usando esta cuenta. La cuenta con la que se ejecuta el agente depende de la forma en que se inicie el agente:  
  
-   Inicio del agente desde un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] trabajo del agente, el valor predeterminado: Cuando un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] trabajo del agente se usa para iniciar un agente de replicación, el agente se ejecuta en el contexto de una cuenta que especifique al configurar la replicación. Para obtener más información acerca del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y la replicación, vea la sección "Seguridad de agentes con el Agente SQL Server", más adelante en este tema. Para obtener información sobre los permisos necesarios para la cuenta con la que se ejecuta el Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vea [Configurar el Agente SQL Server](../../../ssms/agent/configure-sql-server-agent.md).  
  
-   Iniciar al agente desde una línea de comandos de MS-DOS, ya sea directamente o a través de una secuencia de comandos: El agente se ejecuta en el contexto de la cuenta del usuario que ejecuta al agente en la línea de comandos.  
  
-   Iniciar al agente desde una aplicación que utiliza Replication Management Objects (RMO) o un control ActiveX: El agente se ejecuta en el contexto de la aplicación que llama a RMO o el control ActiveX.  
  
    > [!NOTE]  
    >  Los controles ActiveX han quedado desusados.  
  
 Se recomienda que las conexiones se realicen en el contexto de la seguridad integrada de Windows. Para mantener la compatibilidad con versiones anteriores, también se puede utilizar la seguridad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obtener más información acerca de las prácticas recomendadas, consulte [Replication Security Best Practices](replication-security-best-practices.md).  
  
## <a name="permissions-that-are-required-by-agents"></a>Permisos requeridos por los agentes  
 Las cuentas con las que los agentes se ejecutan y realizan conexiones requieren diversos permisos. Estos permisos se describen en la siguiente tabla. Se recomienda que cada agente se ejecute con una cuenta de Windows diferente y que solo se concedan los permisos requeridos a la cuenta. Para obtener información sobre la lista de acceso a la publicación (PAL), que es importante para varios agentes, vea [Proteger el publicador](secure-the-publisher.md).  
  
> [!NOTE]  
>  Control de cuentas de usuario (UAC) de algunos sistemas operativos Windows puede impedir el acceso administrativo al recurso compartido de instantáneas. Por lo tanto, debe conceder de forma explícita permisos del recurso compartido de instantáneas a las cuentas de Windows usadas por el Agente de instantáneas, el Agente de distribución y el Agente de mezcla. Debe hacerlo incluso si las cuentas de Windows pertenecen al grupo Administradores. Para obtener más información, vea [Proteger la carpeta de instantáneas](secure-the-snapshot-folder.md).  
  
|Agente|Permisos|  
|-----------|-----------------|  
|Agente de instantáneas|La cuenta de Windows con la que se ejecuta el agente se utiliza al realizar conexiones al distribuidor. Esta cuenta debe:<br /><br /> − Ser como mínimo miembro del rol fijo de base de datos **db_owner** en la base de datos de distribución.<br /><br /> − Tener permisos de lectura, escritura y modificación en el recurso compartido de instantáneas.<br /><br /> <br /><br /> La cuenta utilizada para conectarse al publicador debe ser miembro, como mínimo, del rol fijo de base de datos **db_owner** en la base de datos de publicaciones.|  
|Agente de registro del LOG|La cuenta de Windows con la que se ejecuta el agente se utiliza al realizar conexiones al distribuidor. Esta cuenta debe ser, como mínimo, miembro del rol fijo de base de datos **db_owner** en la base de datos de distribución.<br /><br /> La cuenta utilizada para conectarse al publicador debe ser miembro, como mínimo, del rol fijo de base de datos **db_owner** en la base de datos de publicaciones.<br /><br /> Al seleccionar el `sync_type` opciones *solo compatibilidad con replicación*, *inicializar con copia de seguridad*, o *inicializar desde lsn*, debe ejecutar el agente de lector del registro después de ejecutar `sp_addsubscription`, de modo que los scripts de instalación se escriben en la base de datos de distribución. El agente de registro del LOG se debe ejecutar con una cuenta que sea miembro del rol fijo de servidor **sysadmin** . Cuando el `sync_type` opción está establecida en *automática*, no se requiere ninguna acción del agente de lector de registro especial.|  
|Agente de distribución para una suscripción de inserción|La cuenta de Windows con la que se ejecuta el agente se utiliza al realizar conexiones al distribuidor. Esta cuenta debe:<br /><br /> − Ser como mínimo miembro del rol fijo de base de datos **db_owner** en la base de datos de distribución.<br /><br /> − Ser miembro de la PAL.<br /><br /> − Tener permisos de lectura en el recurso compartido de instantáneas.<br /><br /> − Tener permisos de lectura en el directorio de instalación del proveedor OLE DB para el suscriptor si la suscripción es para un suscriptor que no sea de SQL Server.<br /><br /> − Cuando se replican datos de LOB, el agente de distribución debe tener permisos de escritura en la replicación **C:\Archivos de programa\Microsoft SQL Server\XX\COMfolder** , donde XX representa el instanceID.<br /><br /> <br /><br /> La cuenta usada para conectarse al suscriptor debe ser, como mínimo, miembro del rol fijo de base de datos **db_owner** en la base de datos de suscripciones, o tener permisos equivalentes si la suscripción es para un suscriptor que no sea de SQL Server.<br /><br /> Nota: Cuando se usa `-subscriptionstreams >= 2` en el agente de distribución, también debe conceder el `View Server State` permiso en los suscriptores para detectar interbloqueos.|  
|Agente de distribución para una suscripción de extracción|La cuenta de Windows con la que se ejecuta el agente se utiliza al realizar conexiones al suscriptor. Esta cuenta debe ser, como mínimo, miembro del rol fijo de base de datos **db_owner** en la base de datos de suscripciones. La cuenta utilizada para conectarse al distribuidor debe:<br /><br /> − Ser miembro de la PAL.<br /><br /> − Tener permisos de lectura en el recurso compartido de instantáneas.<br /><br /> − Cuando se replican datos de LOB, el agente de distribución debe tener permisos de escritura en la replicación **C:\Archivos de programa\Microsoft SQL Server\XX\COMfolder** , donde XX representa el instanceID.<br /><br /> <br /><br /> Nota: Cuando se usa `-subscriptionstreams >= 2` en el agente de distribución, también debe conceder el `View Server State` permiso en los suscriptores para detectar interbloqueos.|  
|Agente de mezcla para una suscripción de inserción|La cuenta de Windows con la que se ejecuta el agente se utiliza al realizar conexiones al publicador y al distribuidor. Esta cuenta debe:<br /><br /> − Ser como mínimo miembro del rol fijo de base de datos **db_owner** en la base de datos de distribución.<br /><br /> − Ser miembro de la PAL.<br /><br /> − Ser un inicio de sesión asociado a un usuario en la base de datos de publicaciones.<br /><br /> − Tener permisos de lectura en el recurso compartido de instantáneas.<br /><br /> <br /><br /> La cuenta utilizada para conectarse al suscriptor debe ser miembro, como mínimo, del rol fijo de base de datos **db_owner** en la base de datos de suscripciones.|  
|Agente de mezcla para una suscripción de extracción|La cuenta de Windows con la que se ejecuta el agente se utiliza al realizar conexiones al suscriptor. Esta cuenta debe ser, como mínimo, miembro del rol fijo de base de datos **db_owner** en la base de datos de suscripciones. La cuenta utilizada para conectarse al publicador y al distribuidor debe:<br /><br /> − Ser miembro de la PAL.<br /><br /> − Ser un inicio de sesión asociado a un usuario en la base de datos de publicaciones.<br /><br /> − Ser un inicio de sesión asociado a un usuario en la base de datos de distribución. El usuario puede ser el usuario `Guest`.<br /><br /> − Tener permisos de lectura en el recurso compartido de instantáneas.|  
|Agente de lectura de cola|La cuenta de Windows con la que se ejecuta el agente se utiliza al realizar conexiones al distribuidor. Esta cuenta debe ser, como mínimo, miembro del rol fijo de base de datos **db_owner** en la base de datos de distribución.<br /><br /> La cuenta utilizada para conectarse al publicador debe ser miembro, como mínimo, del rol fijo de base de datos **db_owner** en la base de datos de publicaciones.<br /><br /> La cuenta utilizada para conectarse al suscriptor debe ser miembro, como mínimo, del rol fijo de base de datos **db_owner** en la base de datos de suscripciones.|  
  
## <a name="agent-security-under-sql-server-agent"></a>Seguridad de agentes con el Agente SQL Server  
 Cuando se configura la replicación mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], procedimientos de [!INCLUDE[tsql](../../../includes/tsql-md.md)] o RMO, se crea de forma predeterminada un trabajo del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para cada agente. A continuación, los agentes se ejecutan en el contexto de un paso de trabajo, independientemente de si se ejecutan de forma continua, programada o a petición. Estos trabajos se pueden ver en la carpeta **Trabajos** de [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. En la tabla siguiente se enumeran los nombres de los trabajos.  
  
|Agente|Nombre del trabajo|  
|-----------|--------------|  
|Agente de instantáneas|**\<publicador>-\<baseDeDatosDePublicación>-\<publicación>-\<entero>**|  
|Agente de replicación para una partición de publicación de combinación|**Dyn_\<publicador>-\<baseDeDatosDePublicación>-\<publicación>-\<GUID>**|  
|Agente de registro del LOG|**\<publicador>-\<baseDeDatosDePublicación>-\<entero>**|  
|Agente de mezcla para suscripciones de extracción|**\<publicador>-\<baseDeDatosDePublicación>-\<publicación>-\<suscriptor>-\<baseDeDatosDeSuscripciones>-\<entero>**|  
|Agente de mezcla para suscripciones de inserción|**\<publicador>-\<baseDeDatosDePublicación>-\<publicación>-\<suscriptor>-\<entero>**|  
|Agente de distribución para suscripciones de inserción|**\<publicador>-\<baseDeDatosDePublicación>-\<publicación>-\<suscriptor>-\<entero>** <sup>1</sup>|  
|Agente de distribución para suscripciones de extracción|**\<publicador>-\<baseDeDatosDePublicación>-\<publicación>-\<suscriptor>-\<baseDeDatosDeSuscripción>-\<GUID>** <sup>2</sup>|  
|Agente de distribución para suscripciones de inserción en suscriptores que no sean de SQL Server|**\<publicador>-\<baseDeDatosDePublicación>-\<publicación>-\<suscriptor>-\<entero>**|  
|Agente de lectura de cola|**[\<distribuidor>].\<entero>**|  
  
 <sup>1</sup> para suscripciones de inserción a publicaciones de Oracle, es el nombre del trabajo  **\<Publisher >-\<Publisher**> en lugar de  **\<Publisher >-\< Basededatosdepublicación >**.  
  
 <sup>2</sup> para suscripciones de extracción a publicaciones de Oracle, es el nombre del trabajo  **\<Publisher >-\<Basededatosdedistribución**> en lugar de  **\<Publisher >-\< Basededatosdepublicación >**.  
  
 Al configurar la replicación se especifican las cuentas en las que se ejecutarán los agentes. No obstante, todos los pasos del trabajo se ejecutan en el contexto de seguridad de un *proxy*, por lo que la replicación lleva a cabo internamente las siguientes asignaciones para las cuentas de agente que especifique:  
  
-   La cuenta se asigna primero a una credencial utilizando la instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] [CREATE CREDENTIAL](/sql/t-sql/statements/create-credential-transact-sql) statement. Las cuentas de proxy del Agente[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizan credenciales para almacenar información acerca de las cuentas de usuario de Windows.  
  
-   Se llama al procedimiento almacenado [sp_add_proxy](/sql/relational-databases/system-stored-procedures/sp-add-proxy-transact-sql) y, a continuación, se utiliza la credencial para crear un proxy.  
  
> [!NOTE]  
>  Esta información se facilita para ayudarle a entender las implicaciones de ejecutar agentes con el contexto de seguridad adecuado. No debería ser necesario interactuar directamente con las credenciales o los proxy que se hayan creado.  
  
## <a name="see-also"></a>Vea también  
 [Replication Security Best Practices](replication-security-best-practices.md)   
 [Seguridad y protección &#40;replicación&#41;](security-and-protection-replication.md)   
 [Proteger la carpeta de instantáneas](secure-the-snapshot-folder.md)  
  
  
