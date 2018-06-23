---
title: Base de datos de instantáneas con grupos de disponibilidad AlwaysOn (SQL Server) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- database snapshots [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 7432da1c-ce2f-4cd9-af41-54c97744166b
caps.latest.revision: 5
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: a9db739495dc8f11c77d518815fe46d1b7f03e01
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103908"
---
# <a name="database-snapshots-with-alwayson-availability-groups-sql-server"></a>Instantáneas de bases de datos con grupos de disponibilidad AlwaysOn (SQL Server)
  Puede crear una instantánea de base de datos en una base de datos primaria o secundaria en un grupo de disponibilidad. El rol de réplica debe ser PRIMARY o SECONDARY y no debe encontrarse en el estado RESOLVING.  
  
 Se recomienda que el estado de sincronización de la base de datos sea SYNCHRONIZING o SYNCHRONIZED cuando se crea una instantánea de base de datos. Sin embargo, las instantáneas de base de datos pueden crearse cuando el estado de sincronización de la base de datos sea NOT SYNCHRONIZING.  
  
 Una instantánea de base de datos debe seguir funcionando aunque la réplica se DESCONECTE de la réplica primaria.  
  
 Algunas condiciones de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] pueden hacer que la base de datos de origen y sus instantáneas de base de datos se reinicien y desconecten temporalmente a los usuarios. Estas condiciones son:  
  
-   La réplica principal cambia los roles, ya sea porque la réplica principal actual se queda sin conexión y vuelve a conectarse en la misma instancia del servidor o porque se produce un error en el grupo de disponibilidad.  
  
-   La base de datos entra en el rol secundario.  
  
 Si se produce una conmutación por error de la réplica de disponibilidad que hospeda las instantáneas de base de datos, estas permanecen en la instancia del servidor donde se crearon. Los usuarios pueden seguir usando las instantáneas tras la conmutación por error. Si el rendimiento es importante en el entorno, se recomienda crear instantáneas de base de datos solo en las bases de datos secundarias que estén hospedadas por una réplica secundaria configurada para el modo de conmutación por error manual.  Si alguna vez realiza una conmutación por error manual del grupo de disponibilidad en esta réplica secundaria, puede crear un conjunto de instantáneas de base de datos en otra réplica secundaria, redirigir a los clientes a las nuevas instantáneas de base de datos y quitar todas las instantáneas de las bases de datos principales.  
  
## <a name="see-also"></a>Vea también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Instantáneas de bases de datos &#40;SQL Server&#41;](../../../relational-databases/databases/database-snapshots-sql-server.md)  
  
  