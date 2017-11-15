---
title: "Creación de una suscripción actualizable en una publicación transaccional | Microsoft Docs"
ms.custom: 
ms.date: 07/21/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- updatable transactional subscriptions
- updateable transactional subscriptions, SSMS
ms.assetid: f9ef89ed-36f6-431b-8843-25d445ec137f
caps.latest.revision: "51"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8ce114ccceb58bbb21e226be2b029eac76ef4387
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="create-an-updatable-subscription-to-a-transactional-publication"></a>Crear una suscripción actualizable en una publicación transaccional

> [!NOTE]  
>  Esta característica sigue siendo compatible con las versiones de [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] entre 2012 y 2016.  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
 
Configure suscripciones actualizables en la página **Suscripciones actualizables** del **Asistente para nuevas suscripciones**. Esta página solo está disponible si ha habilitado una publicación transaccional para suscripciones actualizables. Para obtener más información sobre cómo habilitar las suscripciones actualizables, vea [Habilitar suscripciones actualizables para publicaciones transaccionales](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md).   
  
## <a name="to-configure-an-updatable-subscription-from-the-publisher"></a>Para configurar una suscripción actualizable desde el publicador  

1. Conéctese al publicador en Microsoft SQL Server Management Studio y, a continuación, expanda el nodo del servidor.

2. Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** .

3. Haga clic con el botón derecho en una publicación transaccional habilitada para actualizar suscripciones y, a continuación, haga clic en **Nuevas suscripciones**.

4. Siga las indicaciones del asistente para especificar opciones para la suscripción, por ejemplo dónde debe ejecutarse el Agente de distribución.

5. En la página **Suscripciones actualizables** del **Asistente para nuevas suscripciones**, asegúrese de que **Replicar está seleccionado**.

6. Seleccione una opción en la lista desplegable **Confirmar en el publicador**:

    * Para utilizar las suscripciones de actualización inmediata, seleccione **Confirmar cambios simultáneamente**. Si selecciona esta opción y la publicación permite suscripciones de actualización en cola (el valor predeterminado para suscripciones creadas con el Asistente para nueva publicación), la propiedad **update_mode** de la suscripción se establece en **failover**. Este modo le permite cambiar a la actualización en cola más adelante en caso necesario.

    * Para utilizar las suscripciones de actualización en cola, seleccione **Poner en cola cambios y confirmar cuando sea posible**. Si selecciona esta opción y la publicación permite suscripciones de actualización inmediata (el valor predeterminado para suscripciones creadas con el Asistente para nueva publicación), y el suscriptor se está ejecutando en SQL Server 2005 o una versión posterior, la propiedad **update_mode** de la suscripción se establece en queued failover. Este modo le permite cambiar a la actualización inmediata más adelante en caso necesario.

    Para obtener más información sobre cómo cambiar los modos de actualización, consulte [Cambiar entre modos de actualización para una suscripción transaccional actualizable](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md).

7. La página **Inicio de sesión para suscripciones actualizables** se muestra para las suscripciones que utilizan la actualización inmediata o tienen **update_mode** establecida en **queued failover**. En la página **Inicio de sesión para suscripciones actualizables**, especifique un servidor vinculado mediante el que se realicen las conexiones al publicador para las suscripciones de actualización inmediata. Las conexiones las utilizan los desencadenadores que se activan en el suscriptor y propagan los cambios al publicador. Seleccione una de las siguientes opciones:

    * **Crear un servidor vinculado que se conecte mediante la autenticación de SQL Server**. Seleccione esta opción si no ha definido un servidor remoto o un servidor vinculado entre el suscriptor y el publicador. La replicación crea un servidor vinculado automáticamente. La cuenta que especifique debe existir ya en el publicador.

    * **Utilizar un servidor vinculado o un servidor remoto que ya está definido.** Seleccione esta opción si ha definido un servidor remoto o un servidor vinculado entre el suscriptor y el publicador mediante [sp_addserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), [sp_addlinkedserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), SQL Server Management Studio u otro método.

    Para obtener información acerca de los permisos que requiere la cuenta del servidor vinculado, vea la sección sobre las **suscripciones de actualización** en [Escriba aquí la descripción del vínculo](../../../relational-databases/replication/security/secure-the-subscriber.md).

8. Finalice el asistente.

## <a name="to-configure-an-updatable-subscription-from-the-subscriber"></a>Para configurar una suscripción actualizable desde el suscriptor


1. Conéctese al suscriptor en SQL Server Management Studio y expanda el nodo de servidor.

2. Expanda la carpeta **Replicación** .

3. Haga clic con el botón secundario en la carpeta **Suscripciones locales** y, a continuación, haga clic en **Nuevas suscripciones**.

4. En la página **Publicación** del **Asistente para nuevas suscripciones**, seleccione **Buscar SQL Server Publisher** de la lista desplegable **Publicador**.

5. Conéctese al publicador en el cuadro de diálogo **Conectar al servidor** .

6. Seleccione una publicación transaccional habilitada para suscripciones de actualización en la página **Publicación**.

7. Siga las indicaciones del asistente para especificar opciones para la suscripción, por ejemplo dónde debe ejecutarse el Agente de distribución.

8. En la página **Suscripciones actualizables** del Asistente para nuevas suscripciones, asegúrese de que **Replicar** está seleccionado.

9. Seleccione una opción en la lista desplegable **Confirmar en el publicador**:

    * Para utilizar las suscripciones de actualización inmediata, seleccione **Confirmar cambios simultáneamente**. Si selecciona esta opción y la publicación permite suscripciones de actualización en cola (el valor predeterminado para suscripciones creadas con el Asistente para nueva publicación), la propiedad **update_mode** de la suscripción se establece en **failover**. Este modo le permite cambiar a la actualización en cola más adelante en caso necesario.

    * Para utilizar las suscripciones de actualización en cola, seleccione **Poner en cola cambios y confirmar cuando sea posible**. Si selecciona esta opción y la publicación permite suscripciones de actualización inmediata (el valor predeterminado para suscripciones creadas con el Asistente para nueva publicación), y el suscriptor se está ejecutando en SQL Server 2005 o una versión posterior, la propiedad **update_mode** de la suscripción se establece en **queued failover**. Este modo le permite cambiar a la actualización inmediata más adelante en caso necesario.

    Para obtener más información sobre cómo cambiar los modos de actualización, consulte [Cambiar entre modos de actualización para una suscripción transaccional actualizable](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md).

10. La página **Inicio de sesión para suscripciones actualizables** se muestra para las suscripciones que utilizan la actualización inmediata o tienen **update_mode** establecida en **queued failover**. En la página **Inicio de sesión para suscripciones actualizables**, especifique un servidor vinculado mediante el que se realicen las conexiones al publicador para las suscripciones de actualización inmediata. Las conexiones las utilizan los desencadenadores que se activan en el suscriptor y propagan los cambios al publicador. Seleccione una de las siguientes opciones:

    * **Crear un servidor vinculado que se conecte mediante la autenticación de SQL Server**. Seleccione esta opción si no ha definido un servidor remoto o un servidor vinculado entre el suscriptor y el publicador. La replicación crea un servidor vinculado automáticamente. La cuenta que especifique debe existir ya en el publicador.

    * **Utilizar un servidor vinculado o un servidor remoto que ya está definido.** Seleccione esta opción si ha definido un servidor remoto o un servidor vinculado entre el suscriptor y el publicador mediante [sp_addserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), [sp_addlinkedserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), SQL Server Management Studio u otro método.

    Para obtener información acerca de los permisos que requiere la cuenta del servidor vinculado, vea la sección sobre las **suscripciones de actualización** en [Escriba aquí la descripción del vínculo](../../../relational-databases/replication/security/secure-the-subscriber.md).

11. Finalice el asistente.

## <a name="see-also"></a>Vea también

[Updatable Subscriptions for Transactional Replication](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)

[Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)

[Crear una suscripción actualizable en una publicación transaccional con Transact-SQL](../../../relational-databases/replication/publish/create-updatable-subscription-to-transactional-publication.md) 

