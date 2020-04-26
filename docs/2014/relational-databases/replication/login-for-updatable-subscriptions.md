---
title: Inicio de sesión para suscripciones actualizables | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newsubwizard.updatablesubscriptionslogin.f1
ms.assetid: 301ea227-0455-40ba-9009-d38f8676b325
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d8162c7654d99cd2ebab41d290c0a39c6c686686
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/25/2020
ms.locfileid: "63058101"
---
# <a name="login-for-updatable-subscriptions"></a>Inicio de sesión para suscripciones actualizables
  Si ha seleccionado **Replicar** en la página **Suscripciones actualizables** de este asistente, debe especificar una cuenta en el suscriptor bajo la que se realizan las conexiones al publicador para las suscripciones de actualización inmediata. Las conexiones las utilizan los desencadenadores que se activan en el suscriptor y propagan los cambios al publicador. Esta cuenta es necesaria aunque se haya seleccionado **Poner en cola cambios y confirmar cuando sea posible** en la página **Suscripciones actualizables** , porque, de forma predeterminada, el Asistente para nueva suscripción configura la actualización en cola con la capacidad para cambiar a actualización inmediata si es necesario.  
  
> [!IMPORTANT]  
>  La cuenta especificada para la conexión solo debe tener permiso para insertar, actualizar y eliminar datos en las vistas que crea la replicación en la base de datos de publicaciones; no debe tener ningún permiso adicional. Conceda permisos para las vistas de la base de datos de publicación cuyo nombre tenga el formato **syncobj_**_\<númerohexadecimal>_ a la cuenta que configuró en cada suscriptor.  
  
 Hay tres opciones disponibles para el tipo de conexión:  
  
-   Un servidor vinculado o un servidor remoto previamente definido.  
  
-   Un servidor vinculado que crea la replicación; la conexión se establece con las credenciales especificadas en este asistente.  
  
-   Un servidor vinculado que crea la replicación; la conexión se establece con las credenciales del usuario que realiza el cambio en el suscriptor.  
  
 Las dos primeras opciones se pueden especificar en este asistente. La última opción solo se puede especificar mediante [sp_link_publication &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql); Especifique un valor de **1** para el parámetro **@security_mode**.  
  
## <a name="options"></a>Opciones  
 **Crear un servidor vinculado que se conecte mediante el siguiente inicio de sesión para la Autenticación de SQL Server:**  
 La replicación crea un servidor vinculado utilizando las credenciales especificadas en los campos **Inicio de sesión** y **Contraseña** .  
  
 **Inicio de sesión**  
 Escriba un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión que tenga solo los permisos descritos en este tema.  
  
 **Contraseña**  
 Escriba una contraseña segura para el inicio de sesión especificado en **Inicio de sesión**.  
  
 **Confirm Password**  
 Vuelva a escribir la contraseña para confirmar que se ha escrito correctamente.  
  
 **Utilizar un servidor vinculado o un servidor remoto que ya está definido.**  
 Esta opción requiere un servidor vinculado o un servidor remoto que ya se ha definido. Para obtener más información, vea [Servidores vinculados &#40;motor de base de datos&#41;](../linked-servers/linked-servers-database-engine.md) y [Servidores remotos](../../database-engine/configure-windows/remote-servers.md). Asegúrese de que el inicio de sesión utilizado para el servidor vinculado o el servidor remoto tiene una contraseña segura y solo tiene los permisos descritos en este tema.  
  
## <a name="see-also"></a>Consulte también  
 [Crear una suscripción actualizable a una publicación transaccional](publish/create-an-updatable-subscription-to-a-transactional-publication.md)   
 [Ver y modificar la configuración de seguridad de la replicación](security/view-and-modify-replication-security-settings.md)   
 [Suscripciones actualizables para la replicación transaccional](transactional/updatable-subscriptions-for-transactional-replication.md)   
 [Subscribe to Publications](subscribe-to-publications.md)  
  
  
