---
title: 'Propiedades de grupo de disponibilidad: Nuevo grupo de disponibilidad (página Preferencias de copia de seguridad) | Documentos de Microsoft'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.availabilitygroupproperties.backuppreferences.f1
helpviewer_keywords:
- read-only routing
ms.assetid: 65fff22d-5963-4a8c-8b31-fe9ab247a03e
caps.latest.revision: 6
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 9b6e5c1753a7d627e482029fc416928545efc05b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109013"
---
# <a name="availability-group-properties-new-availability-group-backup-preferences-page"></a>Propiedades de grupo de disponibilidad: Nuevo grupo de disponibilidad (página Preferencias de copia de seguridad)
  Utilice este cuadro de diálogo para ver y cambiar las preferencias de copia de seguridad del grupo de disponibilidad seleccionado.  
  
 **Para ver las propiedades del grupo de disponibilidad**  
  
-   [Ver las propiedades del grupo de disponibilidad &#40;SQL Server&#41;](view-availability-group-properties-sql-server.md)  
  
-   [Usar el Panel de AlwaysOn &#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="where-should-backups-occur"></a>¿Dónde deben realizarse las copias de seguridad?  
 **Preferir secundaria**  
 Especifica que las copias de seguridad se deben realizar en una réplica secundaria a menos que la réplica principal sea la única réplica en línea. En ese caso, la copia de seguridad se debe realizar en la réplica principal. Ésta es la opción predeterminada.  
  
 **Solo secundaria**  
 Especifica que las copias de seguridad no deben realizarse nunca en la réplica principal. Si la réplica principal es la única réplica en línea, no se debe realizar la copia de seguridad.  
  
 **Principal**  
 Especifica que las copias de seguridad deben realizarse siempre en la réplica principal. Esta opción es útil si necesita usar características de copia de seguridad, como crear copias de seguridad diferenciales, que no se admiten cuando la copia de seguridad se ejecuta en una réplica secundaria.  
  
 **Cualquier réplica**  
 Especifica que, de acuerdo con sus preferencias, los trabajos de copia de seguridad omitan el rol de las réplicas de disponibilidad cuando la réplica realiza copias de seguridad. Tenga en cuenta que los trabajos de copia de seguridad pueden evaluar otros factores, como la prioridad de copia de seguridad de cada réplica de disponibilidad junto con su estado operativo y de conexión.  
  
> [!IMPORTANT]  
>  No se aplica el valor de preferencia de copia de seguridad. La interpretación de esta preferencia depende de la lógica, si existe, del script con los trabajos de copia de seguridad ejecutado para las bases de datos de un grupo de disponibilidad dado. Para obtener más información, consulte [secundarias activas: copia de seguridad en réplicas secundarias (grupos de disponibilidad AlwaysOn)](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md).  
  
## <a name="replica-backup-priorities"></a>Prioridades de copia de seguridad de réplica  
 Esta cuadrícula muestra la prioridad de copia de seguridad actual de cada instancia de servidor que hospeda una réplica para el grupo de disponibilidad. Utilice esta cuadrícula para cambiar la prioridad de copia de seguridad de una o varias réplicas de disponibilidad.  
  
 **Instancia del servidor**  
 El nombre de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda la réplica de disponibilidad.  
  
 **Prioridad de copia de seguridad (Mínima=1, Máxima=100)**  
 Especifica la prioridad para realizar copias de seguridad en esta réplica en relación con las otras réplicas del mismo grupo de disponibilidad. El valor es un número entero en el intervalo de 0..100. 1 indica la prioridad mínima y 100 indica la prioridad máxima. Si **Prioridad de copia de seguridad** = 1, la réplica de disponibilidad se elegiría para realizar copias de seguridad solamente si no hay réplicas de disponibilidad con mayor prioridad disponibles actualmente.  
  
 **Excluir réplica**  
 Seleccione esta opción si no desea que nunca se elija esta réplica de disponibilidad para realizar copias de seguridad. Esto es útil, por ejemplo, para una réplica de disponibilidad remota en la que no desee nunca realizar la conmutación por error para las copias de seguridad.  
  
## <a name="see-also"></a>Vea también  
 [Secundarias activas: Copia de seguridad en réplicas secundarias (grupos de disponibilidad AlwaysOn)](active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)   
 [ALTER AVAILABILITY GROUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-availability-group-transact-sql)  
  
  
