---
title: "Concesión de acceso a un objeto de base de datos | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- granting access to database objects
ms.assetid: a44d9bbf-f58e-4734-b7f4-eb3b492b777b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5ccbacfe52541c59e12b992220f40806cae46bca
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="lesson-2-4---granting-access-to-a-database-object"></a>Lección 2-4: Concesión de acceso a un objeto de base de datos
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)] Como administrador, puede ejecutar la instrucción SELECT desde la tabla **Products** y la vista **vw_Names** y ejecutar el procedimiento **pr_Names**; en cambio, Mary no puede hacerlo. Para conceder a Mary los permisos necesarios, use la instrucción GRANT.  
  
### <a name="procedure-title"></a>Título del procedimiento  
  
1.  Ejecute la siguiente instrucción para conceder a `Mary` el permiso `EXECUTE` para el procedimiento almacenado `pr_Names` .  
  
    ```  
    GRANT EXECUTE ON pr_Names TO Mary;  
    GO  
    ```  
  
En este escenario, Mary solo puede tener acceso a la tabla **Products** si utiliza el procedimiento almacenado. Si desea que Mary pueda ejecutar una instrucción SELECT con la vista, también debe ejecutar `GRANT SELECT ON vw_Names TO Mary`. Para quitar el acceso a objetos de base de datos, use la instrucción REVOKE.  
  
> [!NOTE]  
> Si la tabla, la vista y el procedimiento almacenado no son propiedad del mismo esquema, la concesión de permisos es más compleja.  
  
## <a name="about-grant"></a>Acerca de GRANT  
Para ejecutar un procedimiento almacenado, debe tener permiso EXECUTE. Para tener acceso a datos y cambiarlos, debe tener permisos SELECT, INSERT, UPDATE y DELETE. La instrucción GRANT también se usa para otros permisos, como el permiso para crear tablas.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Resumen: Configurar permisos en objetos de base de datos](../t-sql/lesson-2-5-summary-configuring-permissions-on-database-objects.md)  
  
## <a name="see-also"></a>Ver también  
[GRANT &#40;Transact-SQL&#41;](../t-sql/statements/grant-transact-sql.md)  
[REVOKE &#40;Transact-SQL&#41;](../t-sql/statements/revoke-transact-sql.md)  
  
  
  
