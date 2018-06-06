---
title: Página Especificar opciones de grupo de disponibilidad (Asistente para nuevo grupo de disponibilidad/Asistente para agregar base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.newagwizard.specifyagname.f1
- sql13.swb.adddatabasewizard.specifyagname.f1
ms.assetid: dcb6374d-becb-4c6c-b88c-5a8273f8aa38
caps.latest.revision: 13
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1938b41ea4d23bc92e0c18a5a5ec7ccbcd2f8b8e
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2018
ms.locfileid: "34771351"
---
# <a name="specify-availability-group-options-page"></a>Página Especificar opciones de grupo de disponibilidad
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  En este tema se describen las opciones de la página **Especificar nombre de grupo de disponibilidad** . Este tema lo utilizan [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] y [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
##  <a name="PageOptions"></a> Especificar opciones de grupo de disponibilidad  
 **Nombre del grupo de disponibilidad**  
 Especifique el nombre del grupo de disponibilidad. En el caso de un nuevo grupo de disponibilidad, especifique un identificador válido de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que sea exclusivo en todos los grupos de disponibilidad del clúster de conmutación por error de Windows Server (WSFC). La longitud máxima del nombre de un grupo de disponibilidad es 128 caracteres.  

 **Tipo de clúster** Después, especifique el tipo de clúster. Los tipos de clúster posibles dependen de la versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y del sistema operativo. Elija una de las opciones de la siguiente lista:

   * **Clústeres de conmutación por error de Windows Server**
   
      Use esta opción cuando el grupo de disponibilidad se hospede en instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que pertenecen a un clúster de conmutación por error de Windows Server para alta disponibilidad y recuperación ante desastres. Esto es válido en todas las versiones compatibles de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. 

   * **EXTERNAL**
      
      Use esta opción cuando el grupo de disponibilidad se hospede en una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que esté administrada por una tecnología de clúster externo para alta disponibilidad y recuperación ante desastres (por ejemplo, Pacemaker en Linux). Válido para [!INCLUDE[sssqlv14](../../../includes/sssqlv14-md.md)] y versiones posteriores.

   * **NONE**
      
      Use esta opción cuando el grupo de disponibilidad se hospede en una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que no esté administrada por una tecnología de clúster para el equilibrio de carga y el escalado de lectura. Válido para [!INCLUDE[sssqlv14](../../../includes/sssqlv14-md.md)] y versiones posteriores. 
 
   **Detección del estado del nivel de la base de datos** Active esta casilla para habilitar la opción de detección del estado del nivel de la base de datos (DB_FAILOVER) del grupo de disponibilidad. La detección del estado de la base de datos advierte cuando una base de datos deja de estar en estado en línea, cuando algo va mal, y activará la conmutación automática por error del grupo de disponibilidad. Vea [Opción de conmutación por error de detección del estado del nivel de la base de datos de un grupo de disponibilidad](sql-server-always-on-database-health-detection-failover-option.md).


Select Databases Page (New Availability Group Wizard and Add Database Wizard)  
  
##  <a name="LaunchWiz"></a> Tareas relacionadas  
  
-   [Usar el cuadro de diálogo Nuevo grupo de disponibilidad &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Usar el Asistente para agregar una base de datos al grupo de disponibilidad &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>Ver también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
