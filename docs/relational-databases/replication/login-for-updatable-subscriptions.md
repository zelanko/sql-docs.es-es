---
title: Inicio de sesión para suscripciones actualizables | Microsoft Docs
ms.custom: ''
ms.date: 08/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.updatablesubscriptionslogin.f1
ms.assetid: 301ea227-0455-40ba-9009-d38f8676b325
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 223d1f8cab99a75d78bfa75b25a2092e4ba83865
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62760337"
---
# <a name="login-for-updatable-subscriptions"></a>Inicio de sesión para suscripciones actualizables
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Para una actualización inmediata, si seleccionó **Replicar** en la página **Suscripciones actualizables** de este asistente, debe especificar una cuenta con el suscriptor con el que se realizan las conexiones al publicador. 
  
 Las conexiones las usan los desencadenadores que se activan en el suscriptor y propagan los cambios al publicador. Se necesita esta cuenta incluso si se selecciona **Poner en cola cambios y confirmar cuando sea posible** en la página **Suscripciones actualizables**. De forma predeterminada, el Asistente para nueva suscripción configura la actualización en cola con la capacidad de cambiar a actualización inmediata si fuera necesario.  
  
> **IMPORTANTE:** La cuenta especificada para la conexión solo debería tener permiso para insertar, actualizar y eliminar datos en las vistas que crea la replicación en la base de datos de publicación. No debería tener ningún permiso adicional. Conceda permisos para las vistas de la base de datos de publicación designadas con el formato **syncobj_** _\<númeroHexadecimal>_ a la cuenta de configuró en cada suscriptor.  
  
 Hay tres opciones disponibles para el tipo de conexión:  
  
-   Un servidor vinculado o un servidor remoto previamente definido.  
  
-   Un servidor vinculado que crea la replicación; la conexión se establece con las credenciales especificadas en este asistente.  
  
-   Un servidor vinculado que crea la replicación; la conexión se establece con las credenciales del usuario que realiza el cambio en el suscriptor.  
  
 Las dos primeras opciones se pueden especificar en este asistente. La última opción solo se puede especificar con [sp_link_publication &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md); especifique un valor de **1** para el parámetro **@security_mode** .  
  
## <a name="options"></a>Opciones  
 **Crear un servidor vinculado que se conecte mediante el siguiente inicio de sesión para la Autenticación de SQL Server:**  
 La replicación crea un servidor vinculado utilizando las credenciales especificadas en los campos **Inicio de sesión** y **Contraseña** .  
  
 **Inicio de sesión**  
 Escriba un inicio de sesión de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que solo tenga los permisos descritos en este tema.  
  
 **Contraseña**  
 Escriba una contraseña segura para el inicio de sesión especificado en **Inicio de sesión**.  
    
 **Utilizar un servidor vinculado o un servidor remoto que ya está definido.**  
 Esta opción requiere un servidor vinculado o un servidor remoto que ya se ha definido. Para obtener más información, vea [Servidores vinculados &#40;motor de base de datos&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md) y [Servidores remotos](../../database-engine/configure-windows/remote-servers.md). Asegúrese de que el inicio de sesión utilizado para el servidor vinculado o el servidor remoto tiene una contraseña segura y solo tiene los permisos descritos en este tema.  
  
## <a name="see-also"></a>Vea también  
 [Crear una suscripción actualizable en una publicación transaccional](publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [View and Modify Replication Security Settings](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  (Ver y modificar la configuración de seguridad de la replicación)  
 [Suscripciones actualizables para replicación transaccional](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
