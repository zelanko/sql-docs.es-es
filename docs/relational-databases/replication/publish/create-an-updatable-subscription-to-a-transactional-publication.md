---
title: "Crear una suscripci&#243;n actualizable a una publicaci&#243;n transaccional (Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "07/21/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Puede actualizables suscripciones transaccionales"
  - "puede actualizar las suscripciones transaccionales, SSMS"
ms.assetid: f9ef89ed-36f6-431b-8843-25d445ec137f
caps.latest.revision: 51
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 51
---
# Crear una suscripci&#243;n actualizable a una publicaci&#243;n transaccional (Management Studio)

> [!NOTE]  
>  Esta característica sigue siendo compatible con las versiones de [!INCLUDE[ssNoVersion_md](../../../includes/ssnoversion-md.md)] entre 2012 y 2016.  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
 
Configurar suscripciones actualizables en el **suscripciones actualizables** página de la **Asistente para nueva suscripción**. Esta página solo está disponible si ha habilitado una publicación transaccional para suscripciones actualizables. Para obtener más información acerca de cómo habilitar las suscripciones actualizables, vea [Habilitar suscripciones de actualización para publicaciones transaccionales](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md).   
  
## Para configurar una suscripción actualizable desde el publicador  

1. Conectar al publicador en Microsoft SQL Server Management Studio y, a continuación, expanda el nodo del servidor.

2. Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** .

3. Haga clic en una publicación transaccional habilitada para suscripciones de actualización y, a continuación, haga clic en **nuevas suscripciones**.

4. Siga las indicaciones del asistente para especificar opciones para la suscripción, por ejemplo dónde debe ejecutarse el Agente de distribución.

5. En el **suscripciones actualizables** página de la **Asistente para nueva suscripción**, asegúrese de **replicar** está seleccionada.

6. Seleccione una opción de la **Confirmar en el publicador** lista desplegable:

    * Para utilizar suscripciones de actualización inmediata, seleccione **Confirmar cambios simultáneamente**. Si selecciona esta opción y la publicación permite suscripciones de actualización en cola (el valor predeterminado para las publicaciones creadas con el Asistente para nueva publicación), la propiedad de suscripción **update_mode** está establecido en **conmutación por error**. Este modo le permite cambiar a la actualización en cola más adelante en caso necesario.

    * Para utilizar suscripciones de actualización en cola, seleccione **poner en cola cambios y confirmar cuando sea posible**. Si selecciona esta opción y la publicación permite suscripciones de actualización inmediata (el valor predeterminado para las publicaciones creadas con el Asistente para nueva publicación), y el suscriptor está ejecutando SQL Server 2005 o una versión posterior, la propiedad de suscripción **update_mode** se establece en cola de conmutación por error. Este modo le permite cambiar a la actualización inmediata más adelante en caso necesario.

    Para obtener información acerca de cómo cambiar los modos de actualización, vea [cambiar entre modos actualizar para una suscripción transaccional actualizable](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md).

7. La **Inicio de sesión para suscripciones actualizables** página aparece para las suscripciones que utilizan la actualización inmediata o tienen **update_mode** establecido en **en cola la conmutación por error**. En la **Inicio de sesión para suscripciones actualizables** página, especifique un servidor vinculado que se realizan las conexiones al publicador para suscripciones de actualización inmediata. Las conexiones las utilizan los desencadenadores que se activan en el suscriptor y propagan los cambios al publicador. Seleccione una de las siguientes opciones:

    * **Crear un servidor vinculado que se conecte mediante autenticación de SQL Server.** Seleccione esta opción si no ha definido un servidor remoto o un servidor vinculado entre el suscriptor y el publicador. La replicación crea un servidor vinculado automáticamente. La cuenta que especifique debe existir ya en el publicador.

    * **Utilizar un servidor vinculado o un servidor remoto que ya está definido.** Seleccione esta opción si ha definido un servidor remoto o vinculado entre el suscriptor y el publicador mediante [sp_addserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), [sp_addlinkedserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), SQL Server Management Studio u otro método.

    Para obtener información acerca de los permisos requeridos por la cuenta del servidor vinculado, consulte el **suscripciones de actualización en cola** de [Escriba la descripción del vínculo](../../../relational-databases/replication/security/secure-the-subscriber.md).

8. Finalice el asistente.

## Para configurar una suscripción actualizable desde el suscriptor


1. Conéctese al suscriptor en SQL Server Management Studio y, a continuación, expanda el nodo del servidor.

2. Expanda la carpeta **Replicación** .

3. Haga clic en el **suscripciones locales** carpeta y, a continuación, haga clic en **nuevas suscripciones**.

4. En el **publicación** página de la **Asistente para nueva suscripción**, seleccione **Buscar publicador de SQL Server** desde el **Publisher** lista desplegable.

5. Conéctese al publicador en el cuadro de diálogo **Conectar al servidor** .

6. Seleccione una publicación transaccional habilitada para suscripciones de actualización en el **publicación** página.

7. Siga las indicaciones del asistente para especificar opciones para la suscripción, por ejemplo dónde debe ejecutarse el Agente de distribución.

8. En el **suscripciones actualizables** página del Asistente de suscripción nueva, asegúrese de **replicar** está seleccionada.

9. Seleccione una opción de la **Confirmar en el publicador** lista desplegable:

    * Para utilizar suscripciones de actualización inmediata, seleccione **Confirmar cambios simultáneamente**. Si selecciona esta opción y la publicación permite suscripciones de actualización en cola (el valor predeterminado para las publicaciones creadas con el Asistente para nueva publicación), la propiedad de suscripción **update_mode** está establecido en **conmutación por error**. Este modo le permite cambiar a la actualización en cola más adelante en caso necesario.

    * Para utilizar suscripciones de actualización en cola, seleccione **poner en cola cambios y confirmar cuando sea posible**. Si selecciona esta opción y la publicación permite suscripciones de actualización inmediata (el valor predeterminado para las publicaciones creadas con el Asistente para nueva publicación), y el suscriptor está ejecutando SQL Server 2005 o una versión posterior, la propiedad de suscripción **update_mode** se establece en cola a **conmutación por error**. Este modo le permite cambiar a la actualización inmediata más adelante en caso necesario.

    Para obtener información acerca de cómo cambiar los modos de actualización, vea [cambiar entre modos actualizar para una suscripción transaccional actualizable](../../../relational-databases/replication/administration/switch-between-update-modes-for-an-updatable-transactional-subscription.md).

10. La **Inicio de sesión para suscripciones actualizables** página aparece para las suscripciones que utilizan la actualización inmediata o tienen **update_mode** establecido en cola a **conmutación por error**. En la **Inicio de sesión para suscripciones actualizables** página, especifique un servidor vinculado que se realizan las conexiones al publicador para suscripciones de actualización inmediata. Las conexiones las utilizan los desencadenadores que se activan en el suscriptor y propagan los cambios al publicador. Seleccione una de las siguientes opciones:

    * **Crear un servidor vinculado que se conecte mediante autenticación de SQL Server.** Seleccione esta opción si no ha definido un servidor remoto o un servidor vinculado entre el suscriptor y el publicador. La replicación crea un servidor vinculado automáticamente. La cuenta que especifique debe existir ya en el publicador.

    * **Utilizar un servidor vinculado o un servidor remoto que ya está definido.** Seleccione esta opción si ha definido un servidor remoto o vinculado entre el suscriptor y el publicador mediante [sp_addserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), [sp_addlinkedserver (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), SQL Server Management Studio u otro método.

    Para obtener información acerca de los permisos requeridos por la cuenta del servidor vinculado, consulte el **suscripciones de actualización en cola** de [Escriba la descripción del vínculo](../../../relational-databases/replication/security/secure-the-subscriber.md).

11. Finalice el asistente.

## Vea también

[Suscripciones actualizables para replicación transaccional](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)

[Crear una publicación](../../../relational-databases/replication/publish/create-a-publication.md)

[Crear una suscripción actualizable en una publicación transaccional con Transact-SQL](../../../relational-databases/replication/publish/create-updatable-subscription-to-transactional-publication.md) 
