---
title: Obtener los campos de todos los eventos | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- extended events [SQL Server], getting fields
- xe
ms.assetid: 4e4ee03f-5bca-42ed-a37c-db1c82e3aad2
caps.latest.revision: 11
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fac62e2160086d920e3e73e770eaaf1cc82e0b88
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200799"
---
# <a name="get-the-fields-for-all-events"></a>Obtener los campos de todos los eventos
  Esta tarea se lleva a cabo con el Editor de consultas en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
 Una vez finalizadas las instrucciones de este procedimiento, la pestaña **Resultados** del Editor de consultas mostrará las columnas siguientes:  
  
-   package_name  
  
-   event_name  
  
-   event_field  
  
-   field_type  
  
-   column_type  
  
 Puede utilizar la información anterior al configurar sesiones de evento que utilizan el destino de creación de depósitos. Para obtener más información, vea [SQL Server Extended Events Targets](../../2014/database-engine/sql-server-extended-events-targets.md).  
  
## <a name="before-you-begin"></a>Antes de empezar  
 Antes de crear una sesión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Extended Events, resulta útil obtener información sobre los campos asociados a los eventos.  
  
## <a name="to-get-the-fields-for-all-events-using-query-editor"></a>Para obtener los campos de todos los eventos mediante el Editor de consultas  
  
-   En el Editor de consultas, emita las instrucciones siguientes.  
  
    ```  
    select p.name package_name, o.name event_name, c.name event_field, c.type_name field_type, c.column_type column_type  
    from sys.dm_xe_objects o  
    join sys.dm_xe_packages p  
          on o.package_guid = p.guid  
    join sys.dm_xe_object_columns c  
          on o.name = c.object_name  
    where o.object_type = 'event'  
    order by package_name, event_name  
    ```  
  
## <a name="see-also"></a>Vea también  
 [sys.dm_xe_objects &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql)   
 [sys.dm_xe_packages &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql)  
  
  
