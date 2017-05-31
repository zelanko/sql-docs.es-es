---
title: Agregar publicador | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.monitor.addpublisher.f1
helpviewer_keywords:
- Add Publisher dialog box
ms.assetid: 4b57e298-655f-42c2-82bc-25cdad94a194
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 86d2654bba26b7bcd1a5c758b8d609d6e2df0286
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="add-publisher"></a>Agregar publicador
  El cuadro de diálogo **Agregar publicador** permite agregar uno o varios publicadores en el panel izquierdo del Monitor de replicación. Después de agregar un publicador, selecciónelo en el panel izquierdo para mostrar información del publicador en el panel derecho.  
  
## <a name="options"></a>Opciones  
 **Agregar**  
 Haga clic en para seleccionar el tipo de publicador que se agregará a fin de abrir el cuadro de diálogo **Conectar al servidor** . Las opciones son:  
  
-   **Agregar publicador de SQL Server...**  
  
     Conéctese al publicador mediante el cuadro de diálogo **Conectar al servidor** .  
  
-   **Agregar publicador de Oracle...**  
  
     Conéctese al distribuidor de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asociado con el publicador de Oracle mediante el cuadro de diálogo **Conectar al servidor** .  
  
-   **Especificar un distribuidor y agregar sus publicadores…**  
  
     Conéctese al distribuidor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] asociado con uno o varios publicadores mediante el cuadro de diálogo **Conectar al servidor** .  
  
 Después de conectarse correctamente al publicador o al distribuidor, el nombre de cada publicador y su distribuidor se muestran en la cuadrícula de la parte superior del cuadro de diálogo.  
  
> [!NOTE]  
>  El distribuidor y el publicador normalmente se ejecutan en la misma instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pero el distribuidor puede ejecutarse en otra instancia (esta configuración se conoce como distribuidor remoto).  
  
 **Quitar**  
 Seleccione un publicador en la cuadrícula de la parte superior del cuadro de diálogo y haga clic en **Quitar** para quitar el publicador de la lista de publicadores que se van a agregar.  
  
> [!NOTE]  
>  Este botón no se puede utilizar para quitar un publicador que ya aparece en el Monitor de replicación. Para quitar un publicador que ya aparece en Monitor de replicación, haga clic con el botón secundario en el publicador en el panel izquierdo y, a continuación, haga clic en **Quitar**.  
  
 **Conectar automáticamente cuando se inicia el Monitor de replicación**  
 Active esta casilla para permitir que el Monitor de replicación se conecte automáticamente con el distribuidor y recupere información de estado para el publicador seleccionado en la cuadrícula de la parte superior del cuadro de diálogo. Si esta casilla está desactivada, debe conectarse manualmente después de iniciar el Monitor de replicación: haga clic con el botón secundario en el publicador en el panel izquierdo del Monitor de replicación y, a continuación, haga clic en **Conectar**.  
  
 **Actualizar automáticamente el estado de este publicador y sus publicaciones**  
 Active esta casilla para permitir que el Monitor de replicación actualice automáticamente el estado del publicador seleccionado en la cuadrícula de la parte superior del cuadro de diálogo. Si esta opción está activada, el Monitor de replicación sondea el distribuidor buscando información de estado en el publicador y sus publicaciones. El intervalo de sondeo se establece mediante la opción **Frecuencia de actualización** . Para obtener más información sobre la actualización en el Monitor de replicación, consulte [Almacenamiento en caché, actualización y rendimiento del Monitor de replicación](../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md).  
  
 **Frecuencia de actualización**  
 Escriba un valor (en segundos) para especificar la frecuencia con la que el Monitor de replicación debe sondear el distribuidor en búsqueda de información de estado. Los valores más bajos producen un sondeo más frecuente, lo que puede afectar al rendimiento del distribuidor si se supervisa un gran número de publicadores. Se recomienda probar el sistema para determinar un valor adecuado. El valor **Frecuencia de actualización** también se utiliza si se selecciona **Actualizar automáticamente** en cualquiera de las ventanas de detalle del Monitor de replicación.  
  
 **Mostrar estos publicadores en el siguiente grupo**  
 Seleccione un grupo de publicadores de la lista. El publicador se muestra en este grupo en el panel izquierdo. Los grupos proporcionan una forma de organizar los publicadores y no afectan al funcionamiento de la replicación. Si no hay ningún grupo definido o si desea crear uno nuevo, haga clic en **Nuevo grupo**.  
  
 **Nuevo grupo**  
 Haga clic aquí para crear un nuevo grupo de publicadores. Un grupo de publicadores proporciona una forma cómoda de organizar publicadores en el Monitor de replicación. Los grupos no afectan a la replicación de datos ni a la relación entre los servidores de una topología de replicación.  
  
## <a name="see-also"></a>Vea también  
 [Iniciar el Monitor de replicación](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [Supervisar la replicación](../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
