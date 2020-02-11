---
title: Información general del Monitor de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.sqlservermonitor.main.f1
helpviewer_keywords:
- SQL Server Monitor [SQL Server]
ms.assetid: 048ae16d-31c3-489a-9f1e-1400a3bacd39
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 889e0c5a54477a1532aa9ec2760fad890a671618
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62755182"
---
# <a name="sql-server-monitor-overview"></a>Información general del Monitor de SQL Server
  Monitor de SQL Server no realiza funciones de supervisión, sino que hospeda módulos que sí lo hacen. Los módulos del Monitor de SQL Server incluyen el Monitor de replicación y el Monitor de creación de reflejo de la base de datos.  
  
 Para utilizar uno de estos módulos, selecciónelo en el menú **Ir** . El módulo seleccionado actualmente posee el contenido de los paneles de navegación y de detalles, la interacción con el usuario en los paneles de detalles y las consultas de contenido y estado.  
  
> [!NOTE]  
>  Para obtener más información sobre estos monitores, vea [Supervisar la replicación](../../relational-databases/replication/monitoring-replication.md) y [Supervisar la creación de reflejo de la base de datos &#40;SQL Server&#41;](../database-mirroring/database-mirroring-sql-server.md).  
  
## <a name="permissions"></a>Permisos  
  
-   Monitor de replicación  
  
     Para supervisar la replicación, debe ser miembro del rol fijo de servidor **sysadmin** en el distribuidor o miembro del rol fijo de base de datos **replmonitor** en la base de datos de distribución. Un administrador del sistema puede agregar cualquier usuario al rol **replmonitor** , que permite a un usuario ver la actividad de replicación en el Monitor de replicación; sin embargo, el usuario no puede administrar la replicación.  
  
-   Monitor de creación de reflejo de la base de datos  
  
     Para supervisar la creación de reflejo de la base de datos, debe ser miembro del rol fijo de servidor **sysadmin** o del rol fijo de base de datos **dbm_monitor** en la instancia del servidor. Si solo es miembro de **sysadmin** o **dbm_monitor** en una de las instancias del servidor asociado, el monitor únicamente puede conectarse a dicho asociado; no puede recuperar información del otro asociado. Para más información, consulte [Database Mirroring Monitor Overview](../database-mirroring/database-mirroring-monitor-overview.md).  
  
## <a name="menu-options"></a>Opciones de menú  
 El Monitor de SQL Server tiene un menú que incluye comandos relacionados con la aplicación. Este menú también contiene comandos del módulo seleccionado.  
  
 Las siguientes opciones de menú pertenecen al Monitor de SQL Server.  
  
 **Archivo**  
 Este menú contiene el comando **Salir** .  
  
 **Acción**  
 Contiene el menú contextual del nodo seleccionado en el árbol de navegación.  
  
 **Go**  
 Contiene una lista de componentes de supervisión  
  
-   Creación de reflejo de la base de datos  
  
-   Replicación  
  
 **Para utilizar SQL Server Management Studio a fin de supervisar la creación de reflejo de la base de datos**  
  
-   [Iniciar el Monitor de creación de reflejo de la base de datos &#40;SQL Server Management Studio&#41;](../database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar la creación de reflejo de la base de datos &#40;SQL Server&#41;](../database-mirroring/database-mirroring-sql-server.md)  
  
  
