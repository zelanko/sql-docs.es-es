---
title: "Cambio de la configuración del grupo de recursos de servidor | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Resource Governor, resource pool alter
- resource pools [SQL Server], alter
ms.assetid: 49438285-a011-4dac-bd4f-f35cd90fda61
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 27adde47bca4c894d044940d00bc6867e6f8e58f
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="change-resource-pool-settings"></a>Cambiar la configuración del grupo de recursos de servidor
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Puede modificar la configuración del grupo de recursos de servidor mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions), [Permissions](#Permissions)  
  
-   **To change the settings for a resource pool, using:**  [SQL Server Management Studio](#ChgRPProp), [Transact-SQL](#ChgRPTSQL)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="LimitationsRestrictions"></a> Limitaciones y restricciones  
 El porcentaje máximo de uso de la CPU debe ser igual o superior al porcentaje mínimo de uso de la CPU. El porcentaje máximo de uso de memoria debe ser igual o superior al porcentaje mínimo de uso de memoria.  
  
 Las sumas de los porcentajes mínimos de uso de la CPU y los porcentajes mínimos de uso de memoria de todos los grupos de recursos de servidor no deben superar el 100 por cien.  
  
###  <a name="Permissions"></a> Permisos  
 Para cambiar la configuración del grupo de recursos de servidor se requiere el permiso CONTROL SERVER.  
  
##  <a name="ChgRPProp"></a> Cambiar la configuración del grupo de recursos de servidor mediante SQL Server Management Studio  
 **Para cambiar la configuración del grupo de recursos de servidor utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra el Explorador de objetos y expanda de forma recursiva el nodo **Administración** hasta **Grupos de recursos de servidor**, con este último incluido.  
  
2.  Haga clic con el botón derecho en el grupo de recursos que va a modificar y, luego, haga clic en **Propiedades**.  
  
3.  En la página **Propiedades del regulador de recursos** , seleccione la fila del grupo de recursos de servidor en la cuadrícula **Grupos de recursos de servidor** si no está seleccionada automáticamente.  
  
4.  Haga clic o doble clic en las celdas de la fila que va a cambiar y especifique los nuevos valores.  
  
5.  Haga clic en **Aceptar**para guardar los cambios.  
  
##  <a name="ChgRPTSQL"></a> Cambiar la configuración del grupo de recursos de servidor mediante Transact-SQL  
 **Para cambiar la configuración del grupo de recursos de servidor utilizando [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  Ejecute la instrucción **ALTER RESOURCE POOL** o **ALTER EXTERNAL RESOURCE POOL** y especifique los valores de propiedad que quiere cambiar.  
  
2.  Ejecute la instrucción **ALTER RESOURCE GOVERNOR RECONFIGURE** .  
  
### <a name="example-transact-sql"></a>Ejemplo (Transact-SQL)  
 En el siguiente ejemplo se cambia el valor de porcentaje máximo de uso de la CPU del grupo de recursos de servidor denominado `poolAdhoc`.  
  
```  
ALTER RESOURCE POOL poolAdhoc  
WITH (MAX_CPU_PERCENT = 25);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Habilitar el regulador de recursos](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Crear un grupo de recursos de servidor](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [Eliminar un grupo de recursos de servidor](../../relational-databases/resource-governor/delete-a-resource-pool.md)   
 [Grupos de cargas de trabajo del regulador de recursos](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Función clasificadora del regulador de recursos](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)  
  
  

