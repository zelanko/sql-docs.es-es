---
title: "Ejecutar conjuntos de recopilación de la utilidad y que no sean de la utilidad en la misma instancia SQL | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ca7ee9b3-ef9a-4ba4-83d0-9ee9f80dab27
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d6f1a687472d2ee83f48fe273008a0d60f51bc58
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="run-utility-and-non-utility-collection-sets-on-same-sql-instance"></a>Ejecutar conjuntos de recopilación de la utilidad y que no sean de la utilidad en la misma instancia SQL
  El conjunto de recopilación de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se admite en paralelo con conjuntos de recopilación que no sean de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Es decir, otros conjuntos de recopilación pueden supervisar una instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mientras pertenezca a una utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Sin embargo, debe deshabilitar la funcionalidad de recopilación de datos de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mientras la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se esté inscribiendo en la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Una vez se haya inscrito la instancia con el UCP, puede reiniciar los conjuntos de recopilación de la utilidad que no sea de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Sin embargo, debe tener en cuenta que todos los conjuntos de recopilación en la instancia administrada cargarán sus datos en el almacén de administración de datos de la utilidad (UMDW); el nombre del archivo de datos de la utilidad es sysutility_mdw.  
  
 Para ejecutar los conjuntos de recopilación de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en paralelo con conjuntos de recopilación que no sean de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , tenga en cuenta los siguientes puntos:  
  
-   Se admiten conjuntos de recopilación en paralelo.  
  
-   Debe deshabilitar los recopiladores de datos existentes mientras inscriba instancias en la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Para pasar los requisitos de validación, debe ejecutar los siguientes procedimientos almacenados en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de crear un UCP, y en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de inscribirla en la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
    ```  
    exec msdb.dbo.sp_syscollector_set_warehouse_database_name NULL  
    exec msdb.dbo.sp_syscollector_set_warehouse_instance_name NULL  
    ```  
  
     Si no ejecuta estos procedimientos almacenados antes de iniciar el Asistente para crear UCP y el Asistente para agregar instancia administrada, se producirá un error en la operación.  
  
-   Debe utilizar el almacén de administración de datos de la utilidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (sysutility_mdw) para todos los conjuntos de recopilación en una instancia administrada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Características y tareas de la utilidad de SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Configurar el almacenamiento de datos del punto de control de la utilidad &#40;Utilidad de SQL Server&#41;](../../relational-databases/manage/configure-your-utility-control-point-data-warehouse-sql-server-utility.md)  
  
  
