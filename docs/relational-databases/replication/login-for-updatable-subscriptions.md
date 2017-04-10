---
title: "Inicio de sesi&#243;n para suscripciones actualizables | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newsubwizard.updatablesubscriptionslogin.f1"
ms.assetid: 301ea227-0455-40ba-9009-d38f8676b325
caps.latest.revision: 18
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 18
---
# Inicio de sesi&#243;n para suscripciones actualizables
  Para actualización inmediata, si seleccionó **replicar** en el **suscripciones actualizables** página de este asistente, debe especificar una cuenta con el suscriptor en la que se realizan las conexiones al publicador. 
  
 Las conexiones se utilizan los desencadenadores que activan en el suscriptor y propagar los cambios al publicador. Esta cuenta es necesaria incluso si ha seleccionado **poner en cola cambios y confirmar cuando sea posible** en la **suscripciones actualizables** página. El Asistente para nueva suscripción predeterminada se configura la actualización en cola con la capacidad de cambiar a actualización inmediata si es necesario.  
  
> **IMPORTANTE:** La cuenta especificada para la conexión debe ser de sólo permiso Insertar, actualizar y eliminar datos en las vistas que la replicación se crea en la base de datos de publicación. No debe tener permisos adicionales. Conceder permisos en las vistas en la base de datos de publicación con el nombre en el formulario **syncobj_***\< númerohexadecimal>* a la cuenta configurada en cada suscriptor.  
  
 Hay tres opciones disponibles para el tipo de conexión:  
  
-   Un servidor vinculado o un servidor remoto previamente definido.  
  
-   Un servidor vinculado que crea la replicación; la conexión se establece con las credenciales especificadas en este asistente.  
  
-   Un servidor vinculado que crea la replicación; la conexión se establece con las credenciales del usuario que realiza el cambio en el suscriptor.  
  
 Las dos primeras opciones se pueden especificar en este asistente. La última opción solo puede especificarse mediante [sp_link_publication &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md); Especifique un valor de **1** para el parámetro **@security_mode**.  
  
## Opciones  
 **Crear un servidor vinculado que se conecte mediante el siguiente inicio de sesión para la Autenticación de SQL Server:**  
 La replicación crea un servidor vinculado mediante las credenciales especificadas en la **Inicio de sesión** y **contraseña** campos.  
  
 **Inicio de sesión**  
 Escriba un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Inicio de sesión que sólo tiene los permisos descritos en este tema.  
  
 **Contraseña**  
 Escriba una contraseña segura para el inicio de sesión especificado en **Inicio de sesión**.  
    
 **Utilizar un servidor vinculado o un servidor remoto que ya está definido.**  
 Esta opción requiere un servidor vinculado o un servidor remoto que ya se ha definido. Para obtener más información, consulte [servidores vinculados &#40; el motor de base de datos &#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md) y [servidores remotos](../../database-engine/configure-windows/remote-servers.md). Asegúrese de que el inicio de sesión utilizado para el servidor vinculado o el servidor remoto tiene una contraseña segura y solo tiene los permisos descritos en este tema.  
  
## Vea también  
 [Crear una suscripción actualizable en una publicación transaccional](https://msdn.microsoft.com/library/ms152769.aspx)   
 [Ver y modificar la configuración de seguridad de la replicación](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [Suscripciones actualizables para replicación transaccional](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)  
  
  