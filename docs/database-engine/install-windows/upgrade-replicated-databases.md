---
title: "Actualizar bases de datos replicadas | Microsoft Docs"
ms.custom: ""
ms.date: "02/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "actualizaciones de bases de datos de la replicación de mezcla [replicación de SQL Server]"
  - "replicación [SQL Server], actualizar"
  - "replicación transaccional, actualizar bases de datos"
  - "replicación de instantáneas [SQL Server], actualizar bases de datos"
  - "actualizar bases de datos replicadas"
ms.assetid: 9926a4f7-bcd8-4b9b-9dcf-5426a5857116
caps.latest.revision: 74
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 73
---
# Actualizar bases de datos replicadas
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] admite la actualización de bases de datos replicadas desde versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; no es necesario detener la actividad en otros nodos mientras se actualiza un nodo. Asegúrese de cumplir las reglas relativas a la versión admitida en una topología:  
  
-   Un distribuidor puede ser de cualquier versión siempre que ésta sea mayor o igual que la versión del publicador (en muchos casos el distribuidor es la misma instancia que el publicador).  
  
-   Un publicador puede ser de cualquier versión siempre que ésta sea menor o igual que la versión del distribuidor.  
  
-   La versión del suscriptor depende del tipo de publicación:  
  
    -   Un suscriptor de una publicación transaccional puede ser de cualquiera de las dos versiones del publicador. Por ejemplo, un publicador de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] puede tener suscriptores de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] , y un publicador de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] puede tener suscriptores de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] .  
  
    -   Un suscriptor de una publicación de combinación puede ser de cualquier versión menor o igual que la versión del publicador.  
  
> [!NOTE]  
>  Este tema se encuentra disponible en la documentación de la Ayuda del programa de instalación y en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Los vínculos con temas que aparecen en negrita en la documentación de la Ayuda del programa de instalación hacen referencia a temas que solo se encuentran disponibles en los Libros en pantalla.  
  
## Ejecutar el Agente de registro del LOG para la replicación transaccional antes de la actualización  
 Antes de actualizar a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], debe asegurarse de que el Agente de registro del LOG ha procesado todas las transacciones confirmadas en las tablas publicadas. Para asegurarse de que se han procesado todas las transacciones, siga estos pasos para cada base de datos que contenga publicaciones transaccionales:  
  
1.  Asegurarse de que el Agente de registro del LOG se está ejecutando para la base de datos. De forma predeterminada, el agente se ejecuta sin interrupción.  
  
2.  Detenga la actividad de usuario en las tablas publicadas.  
  
3.  Deje tiempo para que el Agente de registro del LOG copie las transacciones en la base de datos de distribución y, a continuación, detenga el agente.  
  
4.  Ejecute [sp_replcmds](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) para comprobar que se han procesado todas las transacciones. El conjunto de resultados de este procedimiento debe estar vacío.  
  
5.  Ejecute [sp_replflush](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md) para cerrar la conexión de sp_replcmds.  
  
6.  Realice la actualización del servidor a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
7.  Reinicie el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el Agente de registro del LOG si no se inician automáticamente después de la actualización.  
  
## Ejecutar agentes para la replicación de mezcla después de la actualización  
 Después de la actualización, ejecute el Agente de instantáneas de cada publicación de combinación y el Agente de mezcla de cada suscripción para actualizar los metadatos de la replicación. No tiene que aplicar la nueva instantánea porque no es necesaria para reinicializar las suscripciones. Los metadatos de suscripción se actualizan la primera vez que el Agente de mezcla se ejecuta tras la actualización. Esto significa que la base de datos de suscripciones puede permanecer en línea y activa durante la actualización del publicador.  
  
 La replicación de mezcla almacena metadatos de publicación y suscripción en un determinado número de tablas del sistema en las bases de datos de publicaciones y suscripciones. La ejecución del Agente de instantáneas actualiza los metadatos de publicación y la ejecución del Agente de mezcla actualiza los metadatos de suscripción. Solo es necesaria para generar una instantánea de publicación. Si una publicación de combinación utiliza filtros con parámetros, cada partición también tendrá una instantánea. No es necesario actualizar estas instantáneas con particiones.  
  
 Ejecute los agentes desde [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], el Monitor de replicación o la línea de comandos. Para obtener más información sobre la ejecución del Agente de instantáneas, vea los siguientes temas:  
  
-   [Crear y aplicar la instantánea inicial](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)  
  
-   [Iniciar y detener un agente de replicación &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)  
  
-   [Crear y aplicar la instantánea inicial](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)  
  
-   [Conceptos de los ejecutables del Agente de replicación](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
 Para obtener más información sobre la ejecución del Agente de mezcla, vea los siguientes temas:  
  
-   [Sincronizar una suscripción de extracción](../../relational-databases/replication/synchronize-a-pull-subscription.md)  
  
-   [Sincronizar una suscripción de inserción](../../relational-databases/replication/synchronize-a-push-subscription.md)  
  
 Después de actualizar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una topología que utiliza la replicación de mezcla, cambie el nivel de compatibilidad de publicación de todas las publicaciones si desea utilizar nuevas características.  
  
## Actualizar a Standard Edition, Workgroup Edition o Express Edition  
 Antes de actualizar de una edición de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] a otra, compruebe que las funciones que actualmente utiliza son compatibles con la edición a la que desea actualizar. Para obtener más información, vea la sección sobre replicación de [Características compatibles con las ediciones de SQL Server 2016](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md).  
  
## Sincronización web para la replicación de mezcla  
 La opción de sincronización web para replicación de mezcla requiere que se copie el archivo Escucha de replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (replisapi.dll) en el directorio virtual del servidor de Internet Information Services (IIS) que se usa para la sincronización. Cuando se configura la sincronización web, se copia el archivo en el directorio virtual mediante el Asistente para configurar la sincronización web. Si se actualizan los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalados en el servidor IIS, debe copiarse manualmente el archivo replisapi.dll del directorio COM en el directorio virtual del servidor IIS. Para obtener más información sobre cómo configurar la sincronización web, vea [Configurar la sincronización web](../../relational-databases/replication/configure-web-synchronization.md).  
  
## Restaurar una base de datos replicada a partir de una versión anterior  
 Para asegurarse de que la configuración de replicación se conserva al restaurar una copia de seguridad de una base de datos replicada a partir de una versión anterior, restaure en un servidor y una base de datos con los mismos nombres que el servidor y la base de datos donde se realizó la copia de seguridad.  
  
## Vea también  
 [Administración &#40;replicación&#41;](../../relational-databases/replication/administration/administration-replication.md)   
 [Compatibilidad con versiones anteriores de replicación](../../relational-databases/replication/replication-backward-compatibility.md)   
 [Novedades &#40;Replicación&#41;](../../relational-databases/replication/what-s-new-replication.md)   
 [Actualizaciones de ediciones y versiones admitidas](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [Actualizar a SQL Server 2016](../../database-engine/install-windows/upgrade-to-sql-server-2016.md)  
  
  