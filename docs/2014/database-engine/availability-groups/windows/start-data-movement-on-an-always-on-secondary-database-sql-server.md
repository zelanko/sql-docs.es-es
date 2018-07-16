---
title: Iniciar el movimiento de datos en una base de datos secundaria AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], databases
ms.assetid: 498eb3fb-6a43-434d-ad95-68a754232c45
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cbec6a7aa6c1ac92dbf64fe018800a223084e4e7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37252797"
---
# <a name="start-data-movement-on-an-alwayson-secondary-database-sql-server"></a>Iniciar el movimiento de datos en una base de datos secundaria AlwaysOn (SQL Server)
  Este tema contiene información sobre cómo iniciar la sincronización de datos después de agregar una base de datos a un grupo de disponibilidad AlwaysOn. Para cada nueva réplica principal, las bases de datos secundarias deben estar preparadas en las instancias de servidor que hospedan las réplicas secundarias. Después, cada una de estas bases de datos secundarias se debe unir manualmente al grupo de disponibilidad.  
  
> [!NOTE]  
>  Si las rutas de acceso de archivos son idénticas en cada instancia de servidor que hospeda una réplica de disponibilidad para un grupo de disponibilidad, el [Asistente para nuevo grupo de disponibilidad](use-the-availability-group-wizard-sql-server-management-studio.md), el [Asistente para agregar réplica al grupo de disponibilidad](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)o el [Asistente para agregar base de datos al grupo de disponibilidad](availability-group-add-database-to-group-wizard.md) pueden iniciar automáticamente la sincronización de datos.  
  
 Para iniciar manualmente la sincronización de datos, debe conectarse, a su vez, a cada instancia de servidor que esté hospedando una réplica secundaria para el grupo de disponibilidad y completar los pasos siguientes:  
  
1.  Restaure las copias de seguridad actuales de cada base de datos principal y del registro de transacciones (mediante RESTORE WITH NORECOVERY). Puede usar alguna de las alternativas siguientes:  
  
    -   Restaure manualmente una copia de seguridad reciente de la base de datos principal utilizando RESTORE WITH NORECOVERY y restaure después cada copia de seguridad de registros posterior utilizando RESTORE WITH NORECOVERY. Realice esta secuencia de restauración en cada instancia del servidor que hospeda una réplica secundaria del grupo de disponibilidad.  
  
         **Para obtener más información:**  
  
         [Preparar manualmente una base de datos secundaria para un grupo de disponibilidad &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
    -   Si va a agregar una o varias bases de datos principales de trasvase de registros en un grupo de disponibilidad, es posible que pueda migrar una o varias de sus bases de datos secundarias correspondientes de los grupos de trasvase de registros a los grupos de disponibilidad AlwaysOn. Para migrar una base de datos secundaria de trasvase de registros, es necesario usar el mismo nombre de base de datos que la base de datos principal que reside en una instancia de servidor que hospeda una réplica secundaria para el grupo de disponibilidad. Además, el grupo de disponibilidad debe configurarse de modo que la réplica principal se prefiera para las copias de seguridad y sea candidata para realizar copias de seguridad (es decir, que la prioridad de copia de seguridad sea > 0). Una vez que el trabajo de copia de seguridad se ejecute en la base de datos principal, tendrá que deshabilitar el trabajo de copia de seguridad y, una vez que el trabajo de restauración se haya ejecutado en una base de datos secundaria, deshabilitar el trabajo de restauración.  
  
        > [!NOTE]  
        >  Después de crear todas las bases de datos secundarias para el grupo de disponibilidad, si desea realizar copias de seguridad en las réplicas secundarias, deberá configurar de nuevo la preferencia de copia de seguridad automatizada del grupo de disponibilidad.  
  
         **Para obtener más información:**  
  
         [Requisitos previos para migrar de trasvase de registros a grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](prereqs-migrating-log-shipping-to-always-on-availability-groups.md)  
  
         [Configurar la copia de seguridad en réplicas de disponibilidad &#40;SQL Server&#41;](configure-backup-on-availability-replicas-sql-server.md)  
  
2.  En cuanto sea posible, una cada base de datos secundaria preparada al grupo de disponibilidad.  
  
     **Para obtener más información:**  
  
     [Combinar una base de datos secundaria con un grupo de disponibilidad &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
##  <a name="LaunchWiz"></a> Tareas relacionadas  
  
-   [Usar el cuadro de diálogo Nuevo grupo de disponibilidad &#40;SQL Server Management Studio&#41;](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Usar el Asistente para agregar una réplica al grupo de disponibilidad &#40;SQL Server Management Studio&#41;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar el Asistente para agregar una base de datos al grupo de disponibilidad &#40;SQL Server Management Studio&#41;](availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>Vea también  
 [Información general de grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
