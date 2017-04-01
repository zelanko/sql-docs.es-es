---
title: "Requisitos del rol de seguridad para la replicaci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "seguridad [replicación de SQL Server], roles"
  - "roles [SQL Server], replicación"
ms.assetid: b324a80f-4319-4cb2-847b-1910c49d90e0
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# Requisitos del rol de seguridad para la replicaci&#243;n
  La replicación restringe las acciones específicas que puede llevar a cabo un usuario, basándose en los roles a los que está asignado el nombre de inicio de sesión del usuario. La replicación ha concedido ciertos permisos a la **sysadmin** rol fijo de servidor, el **db_owner** fija de base de datos y los inicios de sesión en la lista de acceso de la publicación (PAL).  
  
## Requisitos del rol de seguridad para la configuración de la replicación  
 En la tabla siguiente se resume el nivel de autenticación necesario para las tareas comunes de configuración de la replicación:  
  
|Tarea de configuración|Requisito de pertenencia|  
|----------------|----------------------------|  
|Habilitar un distribuidor, publicador o suscriptor.|Rol de servidor**sysadmin** en el publicador.|  
|Habilitar una base de datos para replicación.|Rol de servidor**sysadmin** en el publicador.|  
|Crear una publicación.|**db_owner** rol de base de datos en la base de datos de publicación en el publicador o **sysadmin** rol de servidor en el publicador.|  
|Ver propiedades de publicación.|Miembro de la PAL en el publicador, **db_owner** rol de base de datos en la base de datos de publicación en el publicador o **sysadmin** rol de servidor en el publicador.|  
|Crear una suscripción.|**db_owner** rol de base de datos en la base de datos de publicación en el publicador o **sysadmin** rol de servidor en el publicador.<br /><br /> **db_owner** rol de base de datos en la base de datos de suscripción en el suscriptor o **sysadmin** rol de servidor en el suscriptor.|  
|Configurar perfiles de agente.|Rol de servidor**sysadmin** en el distribuidor.|  
  
## Requisitos del rol de seguridad para el mantenimiento de la replicación  
 En la tabla siguiente se resume el nivel de autenticación necesario para las tareas comunes de mantenimiento de la replicación:  
  
|Tarea de mantenimiento|Requisito de pertenencia|  
|----------------------|----------------------------|  
|Modificar o quitar un distribuidor, publicador o suscriptor.|Rol de servidor**sysadmin** en el servidor apropiado.|  
|Modificar o quitar una publicación.|**db_owner** rol de base de datos en la base de datos de publicación en el publicador o **sysadmin** rol de servidor en el publicador.|  
|Modificar o quitar una suscripción en el publicador.|**db_owner** rol de base de datos en la base de datos de publicación en el publicador o **sysadmin** rol de servidor en el publicador.|  
|Modificar o quitar una suscripción en el suscriptor.|**db_owner** rol de base de datos en la base de datos de suscripción en el suscriptor o **sysadmin** rol de servidor en el suscriptor.|  
|Marcar una suscripción para reinicializarla.|Suscripción de inserción: **db_owner** rol de base de datos en la base de datos de publicación en el publicador o **sysadmin** rol de servidor en el publicador.<br /><br /> Suscripción de extracción: **db_owner** rol de base de datos en la base de datos de suscripción en el suscriptor o **sysadmin** rol de servidor en el suscriptor.|  
|Ver la actividad de replicación, los errores y el historial con el Monitor de replicación. Un usuario no puede modificar perfiles de agente, programaciones, etc., a menos que sea miembro del rol de servidor **sysadmin** .|Rol de base de datos**replmonitor** en la base de datos de distribución del distribuidor o rol de servidor **sysadmin** en el distribuidor.|  
|Mantener agentes de replicación.|**db_owner** rol de base de datos en la base de datos adecuada o **sysadmin** rol de servidor en el servidor apropiado.<br /><br /> Si un usuario creó el agente en el rol **sysadmin** y no especificó una cuenta de proxy para el agente, éste se ejecutará en el contexto de la cuenta del Agente [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . En este caso, un usuario en el **db_owner** rol no puede modificar el trabajo asociado con el agente.|  
|Iniciar o detener un agente de replicación.|Propietario del trabajo de agente o rol de servidor **sysadmin** en el servidor apropiado.|  
  
## Vea también  
 [Prácticas recomendadas de seguridad de replicación](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Seguridad y protección & #40; Replicación y nº 41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  