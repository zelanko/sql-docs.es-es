---
title: Sincronizar una suscripción mediante el Administrador de sincronización de Windows (Administrador de sincronización de Windows) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- synchronization [SQL Server replication], Windows Synchronization Manager
- Windows Synchronization Manager
ms.assetid: 80f15dd6-e84d-4f96-9866-5b34ea531f1e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8ecac95d4cad190133d54e73862d607a719ac9c1
ms.sourcegitcommit: 3cfedfeba377560d460ca3e42af1e18824988c07
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/05/2019
ms.locfileid: "59042204"
---
# <a name="synchronize-a-subscription-using-windows-synchronization-manager-windows-synchronization-manager"></a>Sincronizar una suscripción mediante el Administrador de sincronización de Windows (Administrador de sincronización de Windows)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows solo se puede usar para sincronizar suscripciones con publicaciones de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si se está ejecutando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el mismo equipo que el Administrador de sincronización (también se puede usar para sincronizar archivos y páginas web sin conexión). Para utilizar el Administrador de sincronización:  
  
1.  Habilite la sincronización de suscripciones de extracción con el Administrador de sincronización de Windows en el cuadro de diálogo **Propiedades de suscripción - \<Suscriptor>: \<BaseDeDatosDeSuscripción>**. Para más información sobre el acceso a este cuadro de diálogo, vea [View and Modify Publication Properties](view-and-modify-pull-subscription-properties.md) (Ver y modificar las propiedades de una suscripción de extracción).  
  
2.  Obtenga acceso al Administrador de sincronización a través del menú **Inicio** en Windows.  
  
 El Administrador de sincronización permite utilizar el Solucionador interactivo para las suscripciones de mezcla. Generalmente, los conflictos detectados durante la sincronización se resuelven automáticamente, pero si se habilita la resolución interactiva, el usuario puede solucionarlos durante la sincronización. Si se realiza una sincronización fuera del Administrador de sincronización de Windows (por ejemplo, una sincronización programada o una sincronización a petición en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o en el Monitor de replicación), los conflictos se resuelven automáticamente sin intervención del usuario, según la resolución especificada para el artículo.  
  
> [!NOTE]  
>  A partir de [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] y [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)], las versiones de 64 bits del Administrador de sincronización de Windows no pueden detectar las suscripciones de 32 bits.  
  
### <a name="to-enable-the-synchronization-of-pull-subscriptions-with-windows-synchronization-manager"></a>Para habilitar la sincronización de suscripciones de extracción con el Administrador de sincronización de Windows  
  
1.  En la página **General** del cuadro de diálogo **Propiedades de la suscripción - \<Suscriptor>: \<baseDeDatosDeSuscripción>**, seleccione un valor de **Habilitar** para la opción **Utilizar el Administrador de sincronización de Windows**.  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-synchronize-a-pull-subscription-with-synchronization-manager"></a>Para sincronizar una suscripción de extracción con el Administrador de sincronización  
  
1.  Inicie el Administrador de sincronización mediante uno de los métodos siguientes:  
  
    -   En Internet Explorer, haga clic en el menú **Herramientas**y, a continuación, en **Sincronizar**.  
  
    -   Haga clic en **Inicio**, seleccione **Programas** o **Todos los programas**, **Accesorios**y, después, haga clic en **Sincronizar**.  
  
    -   Haga clic en **Inicio**y, a continuación, en **Ejecutar** En el **ejecutar** cuadro de diálogo, escriba `mobsync.exe` en el **abierto** campo y, a continuación, haga clic en **Aceptar**.  
  
2.  En el cuadro de diálogo **Elementos para sincronizar** , seleccione las suscripciones para sincronizar. Las suscripciones se enumeran en las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas en el equipo.  
  
3.  Haga clic en **Sincronizar**.  
  
### <a name="to-reinitialize-a-pull-subscription-with-synchronization-manager"></a>Para reinicializar una suscripción de extracción con el Administrador de sincronización  
  
1.  En el cuadro de diálogo **Elementos para sincronizar** , seleccione una suscripción y, a continuación, haga clic en **Propiedades**.  
  
2.  En el cuadro de diálogo **Propiedades de suscripción de SQL Server** , haga clic en **Reinicializar suscripción**.  
  
3.  Haga clic en **Sí**.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     La próxima vez que se sincronice la suscripción, se aplicará de manera predeterminada una nueva instantánea a la base de datos de suscripciones. Para obtener más información, vea [Reinicializar suscripciones](reinitialize-subscriptions.md).  
  
> [!NOTE]  
>  La replicación de mezcla permite que cualquier cambio pendiente se cargue en el publicador antes de que se aplique la instantánea, pero esta opción no está disponible en el Administrador de sincronización. Para cargar los cambios, sincronice la suscripción antes de reinicializarla.  
  
### <a name="to-set-properties-for-a-pull-subscription-in-synchronization-manager"></a>Para establecer propiedades de una suscripción de extracción en el Administrador de sincronización.  
  
1.  En el cuadro de diálogo **Elementos para sincronizar** , seleccione una suscripción y, a continuación, haga clic en **Propiedades**.  
  
2.  Vea y modifique las propiedades de las siguientes pestañas:  
  
    -   **Identificación**  
  
    -   **Inicio de sesión del suscriptor**, **Inicio de sesión del distribuidor**e **Inicio de sesión del publicador** (solamente para la replicación de mezcla)  
  
    -   **Información del servidor web** (para suscripciones de mezcla en suscriptores que ejecuten SQL Server 2005 o posterior)  
  
    -   **Otros**  
  
     Se recomienda utilizar la autenticación de Windows para todas las conexiones. Para obtener información sobre los permisos que requieren el Agente de distribución y el Agente de mezcla, vea [Replication Agent Security Model](security/replication-agent-security-model.md).  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-remove-a-pull-subscription-from-synchronization-manager"></a>Para quitar una suscripción de extracción en el Administrador de sincronización  
  
1.  En el cuadro de diálogo **Elementos para sincronizar** , seleccione una suscripción y, a continuación, haga clic en **Propiedades**.  
  
2.  En el cuadro de diálogo **Propiedades de suscripción de SQL Server** , haga clic en **Quitar suscripción**.  
  
3.  Seleccione una opción en el cuadro de diálogo **Quitar suscripción** .  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-use-the-interactive-resolver"></a>Para utilizar el Solucionador interactivo  
  
1.  Habilite el artículo y la suscripción para utilizar la resolución interactiva. Para más información, vea [Especificar la resolución interactiva de conflictos para artículos de mezcla](../../relational-databases/replication/publish/specify-merge-replication-properties.md#interactive-conflict-resolution).  
  
2.  Después de que la suscripción comienza la sincronización en el Administrador de sincronización, el Solucionador interactivo se inicia automáticamente si la resolución interactiva de conflictos está habilitada y hay conflictos en uno o varios artículos. El Solucionador interactivo muestra un conflicto cada vez, con una sugerencia de resolución para cada conflicto (basada en el solucionador especificado al crear la publicación y la suscripción).  
  
3.  Opcionalmente, edite cualquiera de las columnas que se muestran en el Solucionador interactivo y, a continuación, haga clic en uno de los siguientes botones para solucionar el conflicto:  
  
    -   **Aceptar sugerencia**  
  
    -   **Aceptar publicador**  
  
    -   **Aceptar suscriptor**  
  
    -   **Resolver todos automáticamente** (se resuelven todos los conflictos actuales sin más intervención)  
  
     A continuación, se aplica la fila seleccionada al publicador y/o suscriptor; se propaga a otros nodos de la topología durante sincronizaciones posteriores.  
  
> [!NOTE]  
>  Las ediciones se aplican solamente si son parte de la fila que se ha seleccionado para la resolución. Por ejemplo, si realiza ediciones en **Publicador**, y, a continuación, hace clic en **Aceptar suscriptor**, se descartan las ediciones.  
  
## <a name="see-also"></a>Vea también  
 [Interactive Conflict Resolution](merge/advanced-merge-replication-conflict-interactive-resolution.md)  
