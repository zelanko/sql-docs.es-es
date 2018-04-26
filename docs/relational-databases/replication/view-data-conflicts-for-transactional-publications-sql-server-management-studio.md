---
title: Ver conflictos de datos para publicaciones transaccionales (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- queued updating subscriptions [SQL Server replication]
- viewing conflict information
ms.assetid: 9977dd75-b0de-4376-9c13-86d80567d8aa
caps.latest.revision: 36
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3d79dabd0b4acd7f58d424c2415c8e22bd3655da
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="view-data-conflicts-for-transactional-publications-sql-server-management-studio"></a>Ver conflictos de datos para publicaciones transaccionales (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Puede ver los conflictos surgidos en la replicación transaccional punto a punto y la replicación transaccional con suscripciones de actualización en cola en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visor de conflictos de replicación. Para obtener información sobre cómo se detectan y resuelven los conflictos, vea [Detección de conflictos en la replicación punto a punto](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md) y [Establecer opciones de resolución de conflictos de actualización en cola &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/publish/set-queued-updating-conflict-resolution-options-sql-server-management-studio.md).  
  
 Que haya datos disponibles sobre los conflictos depende del tipo de replicación y del período de retención del conflicto.  
  
-   En el caso de la replicación punto a punto, el Agente de distribución genera un error de forma predeterminada cuando detecta un conflicto. Se registra un error de conflicto en el registro de errores, pero no se registra ningún dato de conflicto en la tabla de conflictos, por lo que no está disponible para verse. Si el Agente de distribución puede continuar, se registra un conflicto localmente en cada nodo donde se detectó. Para obtener más información, vea "Controlar los conflictos" en [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
-   En el caso de las suscripciones de actualización en cola, hay datos disponibles de cada conflicto. Los datos de conflictos están disponibles en el Visor de conflictos de replicación durante el tiempo especificado como período de retención de conflictos, con un valor predeterminado de 14 días. Para establecer el período de retención de conflictos, realice cualquiera de las acciones siguientes:  
  
    -   Especifique un valor de retención para el parámetro @conflict_retention de [sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md).  
  
    -   Especifique el valor **'conflict_retention'** para el parámetro @property y un valor de retención para el parámetro @value de [sp_changepublication](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md).  
  
### <a name="to-view-conflicts"></a>Para ver conflictos  
  
1.  Conéctese al servidor adecuado en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y, a continuación, expanda el nodo de servidor:  
  
    -   En el caso de la replicación punto a punto, éste es el nodo en el que se produjo el conflicto.  
  
    -   Para las suscripciones de actualización, es el publicador.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** .  
  
3.  Haga clic con el botón secundario en la publicación para la que desea ver los conflictos y, a continuación, haga clic en **Ver conflictos**.  
  
4.  En el cuadro de diálogo **Seleccionar tabla de conflictos** , seleccione una base de datos, una publicación y una tabla para ver los conflictos correspondientes.  
  
5.  En el Visor de conflictos de replicación, puede:  
  
    -   Filtrar filas con los botones que aparecen a la derecha de la cuadrícula superior.  
  
    -   Seleccionar una fila en la cuadrícula superior para ver la información de esa fila en la cuadrícula inferior.  
  
    -   Seleccionar una o más filas en la cuadrícula superior y hacer clic en **Quitar**para quitar las filas de la tabla de metadatos de conflictos.  
  
    -   Hacer clic en el botón de propiedades (**…**) para ver más información acerca de la columna involucrada en el conflicto.  
  
    -   Seleccionar **Registrar los detalles de este conflicto** para registrar los datos del conflicto en un archivo. Para especificar la ubicación del archivo, elija el menú **Ver** y haga clic en **Opciones**. Escriba un valor o haga clic en el botón Examinar (**...**) y navegue al archivo apropiado. Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Opciones** .  
  
6.  Cierre el Visor de conflictos de replicación.  
  
## <a name="see-also"></a>Ver también  
 [Replicación transaccional punto a punto](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Queued Updating Conflict Detection and Resolution](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)  
  
  
