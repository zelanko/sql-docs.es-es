---
title: Crear una suscripción actualizable en una publicación transaccional (Management Studio) | Documentos de Microsoft
ms.custom: ''
ms.date: 07/20/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2014
helpviewer_keywords:
- updateable transactional subscriptions
- updateable transactional subscriptions, SSMS
ms.assetid: f9ef89ed-36f6-431b-8843-25d445ec137f
caps.latest.revision: 46
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f7eaf65c28de437c1340d1c3a1f90c18d1816e37
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103767"
---
# <a name="create-an-updatable-subscription-to-a-transactional-publication-management-studio"></a>Crear una suscripción actualizable a una publicación transaccional [Management Studio]

> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
 
Configure suscripciones actualizables en la página **Suscripciones actualizables** del **Asistente para nuevas suscripciones**. Esta página solo está disponible si ha habilitado una publicación transaccional para suscripciones actualizables. Para obtener más información sobre cómo habilitar las suscripciones actualizables, vea [Habilitar suscripciones actualizables para publicaciones transaccionales](enable-updating-subscriptions-for-transactional-publications.md).   
  
## <a name="to-configure-an-updatable-subscription-from-the-publisher"></a>Para configurar una suscripción actualizable desde el publicador  

1. Conéctese al publicador en Microsoft SQL Server Management Studio y, a continuación, expanda el nodo del servidor.

2. Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** .

3. Haga clic con el botón derecho en una publicación transaccional habilitada para actualizar suscripciones y, a continuación, haga clic en **Nuevas suscripciones**.

4. Siga las indicaciones del asistente para especificar opciones para la suscripción, por ejemplo dónde debe ejecutarse el Agente de distribución.

5. En la página **Suscripciones actualizables** del **Asistente para nuevas suscripciones**, asegúrese de que **Replicar está seleccionado**.

6. Seleccione una opción en la lista desplegable **Confirmar en el publicador**:

    * Para utilizar las suscripciones de actualización inmediata, seleccione **Confirmar cambios simultáneamente**. Si selecciona esta opción y la publicación permite suscripciones de actualización en cola (el valor predeterminado para suscripciones creadas con el Asistente para nueva publicación), la propiedad **update_mode** de la suscripción se establece en **failover**. Este modo le permite cambiar a la actualización en cola más adelante en caso necesario.

    * Para utilizar las suscripciones de actualización en cola, seleccione **Poner en cola cambios y confirmar cuando sea posible**. Si selecciona esta opción y la publicación permite suscripciones de actualización inmediata (el valor predeterminado para suscripciones creadas con el Asistente para nueva publicación), y el suscriptor se está ejecutando en SQL Server 2005 o una versión posterior, la propiedad **update_mode** de la suscripción se establece en queued failover. Este modo le permite cambiar a la actualización inmediata más adelante en caso necesario.

    Para obtener más información sobre cómo cambiar los modos de actualización, consulte [Cambiar entre modos de actualización para una suscripción transaccional actualizable](../administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md).

7. La página **Inicio de sesión para suscripciones actualizables** se muestra para las suscripciones que utilizan la actualización inmediata o tienen **update_mode** establecida en **queued failover**. En la página **Inicio de sesión para suscripciones actualizables**, especifique un servidor vinculado mediante el que se realicen las conexiones al publicador para las suscripciones de actualización inmediata. Las conexiones las utilizan los desencadenadores que se activan en el suscriptor y propagan los cambios al publicador. Seleccione una de las siguientes opciones:

    * **Crear un servidor vinculado que se conecte mediante la autenticación de SQL Server**. Seleccione esta opción si no ha definido un servidor remoto o un servidor vinculado entre el suscriptor y el publicador. La replicación crea un servidor vinculado automáticamente. La cuenta que especifique debe existir ya en el publicador.

    * **Utilizar un servidor vinculado o un servidor remoto que ya está definido.** Seleccione esta opción si ha definido un servidor remoto o un servidor vinculado entre el suscriptor y el publicador mediante [sp_addserver (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addserver-transact-sql), [sp_addlinkedserver (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql), SQL Server Management Studio u otro método.

    Para obtener información acerca de los permisos que requiere la cuenta del servidor vinculado, vea la sección sobre las **suscripciones de actualización** en [Escriba aquí la descripción del vínculo](../security/secure-the-subscriber.md).

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

    Para obtener más información sobre cómo cambiar los modos de actualización, consulte [Cambiar entre modos de actualización para una suscripción transaccional actualizable](../administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md).

10. La página **Inicio de sesión para suscripciones actualizables** se muestra para las suscripciones que utilizan la actualización inmediata o tienen **update_mode** establecida en **queued failover**. En la página **Inicio de sesión para suscripciones actualizables**, especifique un servidor vinculado mediante el que se realicen las conexiones al publicador para las suscripciones de actualización inmediata. Las conexiones las utilizan los desencadenadores que se activan en el suscriptor y propagan los cambios al publicador. Seleccione una de las siguientes opciones:

    * **Crear un servidor vinculado que se conecte mediante la autenticación de SQL Server**. Seleccione esta opción si no ha definido un servidor remoto o un servidor vinculado entre el suscriptor y el publicador. La replicación crea un servidor vinculado automáticamente. La cuenta que especifique debe existir ya en el publicador.

    * **Utilizar un servidor vinculado o un servidor remoto que ya está definido.** Seleccione esta opción si ha definido un servidor remoto o un servidor vinculado entre el suscriptor y el publicador mediante [sp_addserver (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addserver-transact-sql), [sp_addlinkedserver (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql), SQL Server Management Studio u otro método.

    Para obtener información acerca de los permisos que requiere la cuenta del servidor vinculado, vea la sección sobre las **suscripciones de actualización** en [Escriba aquí la descripción del vínculo](../security/secure-the-subscriber.md).

11. Finalice el asistente.

## <a name="see-also"></a>Vea también

[Updatable Subscriptions for Transactional Replication](../transactional/updatable-subscriptions-for-transactional-replication.md)

[Create a Publication](create-a-publication.md)

[Crear una suscripción actualizable en una publicación transaccional con Transact-SQL](../create-updatable-subscription-transactional-publication-transact-sql.md) 
 
  
