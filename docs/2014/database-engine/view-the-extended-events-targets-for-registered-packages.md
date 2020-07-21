---
title: Ver los destinos de eventos extendidos para los paquetes registrados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- targets [SQL Server extended events]
- viewing event targets
- extended events [SQL Server], viewing targets
ms.assetid: 4985aa5f-ac99-49f6-852c-9d25916549e9
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 8e796d141ef943399fc2469c232b34b1956cef3b
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84927344"
---
# <a name="view-the-extended-events-targets-for-registered-packages"></a>Ver los destinos de eventos extendidos de los paquetes registrados
  Antes de crear una sesión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Extended Events, es útil determinar qué destinos de eventos extendidos están disponibles. Esta tarea implica el uso del Editor de consultas en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para realizar el procedimiento siguiente.  
  
 Una vez finalizadas las instrucciones de este procedimiento, la pestaña **Resultados** del Editor de consultas mostrará las dos columnas siguientes:  
  
-   package_name  
  
-   target_name  
  
## <a name="to-view-the-extended-events-targets-for-registered-packages-using-query-editor"></a>Para ver los destinos de eventos extendidos para los paquetes registrados mediante el Editor de consultas  
  
-   En el Editor de consultas, emita las instrucciones siguientes.  
  
    ```  
    USE msdb  
    SELECT p.name package_name, o.name target_name  
    FROM sys.dm_xe_objects o  
    JOIN sys.dm_xe_packages p  
         ON o.package_guid = p.guid  
    WHERE o.object_type = 'target'  
    ```  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server destinos de eventos extendidos](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [Sys. dm_xe_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql)   
 [sys.dm_xe_packages &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql)  
  
  
