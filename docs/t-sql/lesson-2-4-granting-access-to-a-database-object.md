---
title: Conceder acceso a un objeto de base de datos | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- granting access to database objects
ms.assetid: a44d9bbf-f58e-4734-b7f4-eb3b492b777b
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 7cc5c15a44f16e4049974ff76095a389348707c7
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-2-4---granting-access-to-a-database-object"></a>Lección 2-4-conceder acceso a un objeto de base de datos
Como administrador, puede ejecutar la instrucción SELECT desde la tabla **Products** y la vista **vw_Names** , y ejecutar el procedimiento **pr_Names** ; en cambio, Mary no puede hacerlo. Para conceder a Mary los permisos necesarios, use la instrucción GRANT.  
  
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
  
## <a name="see-also"></a>Vea también  
[GRANT &#40;Transact-SQL&#41;](../t-sql/statements/grant-transact-sql.md)  
[REVOKE &#40;Transact-SQL&#41;](../t-sql/statements/revoke-transact-sql.md)  
  
  
  

