---
title: "Modelo de seguridad del Agente de replicación | Microsoft Docs"
ms.custom: 
ms.date: 10/07/2015
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 07b24a4d11b0bb95417d3808afb8d9d4e5c1b849
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/08/2018
---
# <a name="replication-agent-security-model"></a>Modelo de seguridad del Agente de replicación
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El modelo de seguridad del agente de replicación permite un control concreto sobre las cuentas con las que los agentes de replicación se ejecutan y realizan conexiones: se puede especificar una cuenta diferente para cada agente. Para obtener más información sobre cómo especificar cuentas, vea [Administrar inicios de sesión y contraseñas en la replicación](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md).  
  
> [!IMPORTANT]  
>  Cuando un miembro de rol fijo de servidor **sysadmin** configura la replicación, los agentes de replicación se pueden configurar para suplantar la cuenta del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Esto se consigue no especificando ningún inicio de sesión ni contraseña para el agente de replicación; no obstante, no se recomienda este enfoque. En su lugar, por seguridad, se recomienda especificar una cuenta para cada agente con los permisos mínimos descritos en la sección "Permisos requeridos por los agentes", más adelante en este tema.  
  
 Los agentes de replicación, como todos los ejecutables, se ejecutan en el contexto de una cuenta de Windows. Los agentes establecen conexiones de seguridad integrada de Windows usando esta cuenta. La cuenta con la que se ejecuta el agente depende de la forma en que se inicie el agente:  
  
-   Inicio del agente desde un trabajo del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (valor predeterminado): cuando se utiliza un trabajo del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para iniciar un agente de replicación, el agente se ejecuta en el contexto de la cuenta que se especifica al configurar la replicación. Para obtener más información acerca del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y la replicación, vea la sección "Seguridad de agentes con el Agente SQL Server", más adelante en este tema. Para obtener información sobre los permisos necesarios para la cuenta con la que se ejecuta el Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vea [Configurar el Agente SQL Server](http://msdn.microsoft.com/library/2e361a62-9e92-4fcd-80d7-d6960f127900).  
  
-   Inicio del agente desde una línea de comandos de MS-DOS (directamente o mediante un script): el agente se ejecuta en el contexto de la cuenta del usuario que ejecuta el agente en la línea de comandos.  
  
-   Inicio del agente desde una aplicación que utiliza Replication Management Objects (RMO) o un control ActiveX: el agente se ejecuta en el contexto de la aplicación que llama a RMO o al control ActiveX.  
  
    > [!NOTE]  
    >  Los controles ActiveX han quedado desusados.  
  
 Se recomienda que las conexiones se realicen en el contexto de la seguridad integrada de Windows. Para mantener la compatibilidad con versiones anteriores, también se puede utilizar la seguridad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obtener más información acerca de las prácticas recomendadas, consulte [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md).  
  
## <a name="permissions-that-are-required-by-agents"></a>Permisos requeridos por los agentes  
 Las cuentas con las que los agentes se ejecutan y realizan conexiones requieren diversos permisos. Estos permisos se describen en la siguiente tabla. Se recomienda que cada agente se ejecute con una cuenta de Windows diferente y que solo se concedan los permisos requeridos a la cuenta. Para obtener información sobre la lista de acceso a la publicación (PAL), que es importante para varios agentes, vea [Proteger el publicador](../../../relational-databases/replication/security/secure-the-publisher.md).  
  
> [!NOTE]  
>  Control de cuentas de usuario (UAC) de algunos sistemas operativos Windows puede impedir el acceso administrativo al recurso compartido de instantáneas. Por lo tanto, debe conceder de forma explícita permisos del recurso compartido de instantáneas a las cuentas de Windows usadas por el Agente de instantáneas, el Agente de distribución y el Agente de mezcla. Debe hacerlo incluso si las cuentas de Windows pertenecen al grupo Administradores. Para obtener más información, vea [Proteger la carpeta de instantáneas](../../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
|Agente|Permisos|  
|-----------|-----------------|  
|Agente de instantáneas|La cuenta de Windows con la que se ejecuta el agente se utiliza al realizar conexiones al distribuidor. Esta cuenta debe:<br /><br /> − Ser como mínimo miembro del rol fijo de base de datos **db_owner** en la base de datos de distribución.<br /><br /> − Tener permisos de lectura, escritura y modificación en el recurso compartido de instantáneas.<br /><br /> <br /><br /> Observe que la cuenta utilizada para *conectarse* al publicador debe ser miembro, como mínimo, del rol fijo de base de datos **db_owner** en la base de datos de publicaciones.|  
|Agente de registro del LOG|La cuenta de Windows con la que se ejecuta el agente se utiliza al realizar conexiones al distribuidor. Esta cuenta debe ser, como mínimo, miembro del rol fijo de base de datos **db_owner** en la base de datos de distribución.<br /><br /> La cuenta utilizada para conectarse al publicador debe ser miembro, como mínimo, del rol fijo de base de datos **db_owner** en la base de datos de publicaciones.<br /><br /> Al seleccionar las opciones **replication support only** , *initialize with backup*o *initialize from lsn*de *sync_type*, el agente de registro del LOG se debe ejecutar después de ejecutar **sp_addsubscription**, de modo que los scripts de instalación se escriban en la base de datos de distribución. El agente de registro del LOG se debe ejecutar con una cuenta que sea miembro del rol fijo de servidor **sysadmin** . Cuando la opción **sync_type** se establece en *Automatic*, no se requiere ninguna acción especial del agente de registro del LOG.|  
|Agente de distribución para una suscripción de inserción|La cuenta de Windows con la que se ejecuta el agente se utiliza al realizar conexiones al distribuidor. Esta cuenta debe:<br /><br /> − Ser como mínimo miembro del rol fijo de base de datos **db_owner** en la base de datos de distribución.<br /><br /> − Ser miembro de la PAL.<br /><br /> − Tener permisos de lectura en el recurso compartido de instantáneas.<br /><br /> − Tener permisos de lectura en el directorio de instalación del proveedor OLE DB para el suscriptor si la suscripción es para un suscriptor que no sea de SQL Server.<br /><br /> − Cuando se replican datos de LOB, el agente de distribución debe tener permisos de escritura en la replicación **C:\Archivos de programa\Microsoft SQL Server\XX\COMfolder** , donde XX representa el instanceID.<br /><br /> <br /><br /> Observe que la cuenta usada para *conectarse* al suscriptor debe ser, como mínimo, miembro del rol fijo de base de datos **db_owner** en la base de datos de suscripciones, o tener permisos equivalentes si la suscripción es para un suscriptor que no sea de SQL Server.<br /><br /> Tenga en cuenta también que, cuando se usa `-subscriptionstreams >= 2` en el agente de distribución, también se debe conceder el permiso **View Server State** en los suscriptores para detectar interbloqueos.|  
|Agente de distribución para una suscripción de extracción|La cuenta de Windows con la que se ejecuta el agente se utiliza al realizar conexiones al suscriptor. Esta cuenta debe ser, como mínimo, miembro del rol fijo de base de datos **db_owner** en la base de datos de suscripciones. La cuenta utilizada para conectarse al distribuidor debe:<br /><br /> − Ser miembro de la PAL.<br /><br /> − Tener permisos de lectura en el recurso compartido de instantáneas.<br /><br /> − Cuando se replican datos de LOB, el agente de distribución debe tener permisos de escritura en la replicación **C:\Archivos de programa\Microsoft SQL Server\XX\COMfolder** , donde XX representa el instanceID.<br /><br /> <br /><br /> Tenga en cuenta que, cuando se usa `-subscriptionstreams >= 2` en el agente de distribución, también se debe conceder el permiso **View Server State** en los suscriptores para detectar interbloqueos.|  
|Agente de mezcla para una suscripción de inserción|La cuenta de Windows con la que se ejecuta el agente se utiliza al realizar conexiones al publicador y al distribuidor. Esta cuenta debe:<br /><br /> − Ser como mínimo miembro del rol fijo de base de datos **db_owner** en la base de datos de distribución.<br /><br /> − Ser miembro de la PAL.<br /><br /> − Ser un inicio de sesión asociado a un usuario en la base de datos de publicaciones.<br /><br /> − Tener permisos de lectura en el recurso compartido de instantáneas.<br /><br /> <br /><br /> Observe que la cuenta utilizada para *conectarse* al suscriptor debe ser miembro, como mínimo, del rol fijo de base de datos **db_owner** en la base de datos de suscripciones.|  
|Agente de mezcla para una suscripción de extracción|La cuenta de Windows con la que se ejecuta el agente se utiliza al realizar conexiones al suscriptor. Esta cuenta debe ser, como mínimo, miembro del rol fijo de base de datos **db_owner** en la base de datos de suscripciones. La cuenta utilizada para conectarse al publicador y al distribuidor debe:<br /><br /> − Ser miembro de la PAL.<br /><br /> − Ser un inicio de sesión asociado a un usuario en la base de datos de publicaciones.<br /><br /> − Ser un inicio de sesión asociado a un usuario en la base de datos de distribución. El usuario puede ser el usuario **Guest** .<br /><br /> − Tener permisos de lectura en el recurso compartido de instantáneas.|  
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
|Agente de distribución para suscripciones de inserción|**\<publicador>-\<baseDeDatosDePublicación>-\<publicación>-\<suscriptor>-\<entero>***|  
|Agente de distribución para suscripciones de extracción|**\<Publicador>-\<BaseDeDatosDePublicación>-\<Publicación>-\<Suscriptor>-\<BaseDeDatosDeSuscripción>-\<GUID>***\*|  
|Agente de distribución para suscripciones de inserción en suscriptores que no sean de SQL Server|**\<publicador>-\<baseDeDatosDePublicación>-\<publicación>-\<suscriptor>-\<entero>**|  
|Agente de lectura de cola|**[\<distribuidor>].\<entero>**|  
  
 \*Para suscripciones de inserción a publicaciones de Oracle, el nombre del trabajo es **\<publicador>-\<publicador**> en lugar de **\<publicador>-\<baseDeDatosDePublicación>**.  
  
 \*\*Para suscripciones de extracción a publicaciones de Oracle, el nombre del trabajo es **\<publicador>-\<baseDeDatosDeDistribución**> en lugar de **\<publicador>-\<baseDeDatosDePublicación>**.  
  
 Al configurar la replicación se especifican las cuentas en las que se ejecutarán los agentes. No obstante, todos los pasos del trabajo se ejecutan en el contexto de seguridad de un *proxy*, por lo que la replicación lleva a cabo internamente las siguientes asignaciones para las cuentas de agente que especifique:  
  
-   La cuenta se asigna primero a una credencial utilizando la instrucción [!INCLUDE[tsql](../../../includes/tsql-md.md)] [CREATE CREDENTIAL](../../../t-sql/statements/create-credential-transact-sql.md) statement. Las cuentas de proxy del Agente[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizan credenciales para almacenar información acerca de las cuentas de usuario de Windows.  
  
-   Se llama al procedimiento almacenado [sp_add_proxy](../../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md) y, a continuación, se utiliza la credencial para crear un proxy.  
  
> [!NOTE]  
>  Esta información se facilita para ayudarle a entender las implicaciones de ejecutar agentes con el contexto de seguridad adecuado. No debería ser necesario interactuar directamente con las credenciales o los proxy que se hayan creado.  
  
## <a name="see-also"></a>Ver también  
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Seguridad y protección &#40;replicación&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md)   
 [Proteger la carpeta de instantáneas](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)  
  
  
