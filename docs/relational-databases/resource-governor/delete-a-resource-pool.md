---
title: Eliminación de un grupo de recursos de servidor | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, resource pool delete
- resource pools [SQL Server], delete
ms.assetid: 3bdd348b-6582-4ffa-80ef-d49e50596ce5
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 65ebdd2cfac33202437d0c6f515a838ed71e9534
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720486"
---
# <a name="delete-a-resource-pool"></a>Eliminar un grupo de recursos de servidor
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Puede eliminar un grupo de recursos de servidor utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o Transact-SQL.  
  
-   **Antes de empezar:**  [Limitaciones y restricciones](#LimitationsRestrictions), [Permisos](#Permissions)  
  
-   **Para eliminar un grupo de recursos de servidor con:** [SQL Server Management Studio](#DelRPSSMS), [Transact-SQL](#DelRPTSQL)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
 No se puede eliminar un grupo de recursos de servidor si contiene grupos de cargas de trabajo.  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> Limitaciones y restricciones  
 No se pueden eliminar los grupos de recursos de servidor predeterminados o internos del regulador de recursos. No se puede eliminar un grupo de recursos de servidor si contiene grupos de cargas de trabajo. Para obtener más información, consulte [Delete a Workload Group](../../relational-databases/resource-governor/delete-a-workload-group.md).  
  
###  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Para eliminar un grupo de recursos de servidor se requiere un permiso CONTROL SERVER.  
  
##  <a name="delete-a-resource-pool-using-object-explorer"></a><a name="DelRPSSMS"></a> Eliminar un grupo de recursos de servidor mediante el Explorador de objetos  
 **Para eliminar un grupo de recursos de servidor mediante SQL Server Management Studio**  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra el Explorador de objetos y expanda de forma recursiva el nodo **Administración** hasta e incluyendo el nodo **Regulador de recursos**.  
  
2.  Haga clic con el botón derecho en el grupo de recursos que va a eliminar y luego haga clic en **Eliminar**.  
  
3.  En la ventana **Eliminar objeto** aparece el grupo de recursos de servidor en la lista **Objeto que se va a eliminar** . Para eliminar el grupo de recursos de servidor, haga clic en **Aceptar**.  

    > [!NOTE]  
    >  Si el grupo de recursos de servidor que intenta eliminar contiene un grupo de cargas de trabajo, esta acción provocará un error.  
  
##  <a name="delete-a-resource-pool-using-transact-sql"></a><a name="DelRPTSQL"></a> Eliminar un grupo de recursos de servidor mediante Transact-SQL  
 **Para eliminar un grupo de recursos de servidor mediante Transact-SQL**  
  
1.  Ejecute la instrucción **DROP RESOURCE POOL** o **DROP EXTERNAL RESOURCE POOL** y especifique el nombre del grupo de recursos que quiere eliminar.  
  
2.  Ejecute la instrucción **ALTER RESOURCE GOVERNOR RECONFIGURE** .  
  
### <a name="example-transact-sql"></a>Ejemplo (Transact-SQL)  
 En el ejemplo siguiente se quita un grupo de cargas de trabajo denominado `poolAdhoc`.  
  
```  
DROP RESOURCE POOL poolAdhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Grupo de recursos de servidor del regulador de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Crear un grupo de recursos de servidor](../../relational-databases/resource-governor/create-a-resource-pool.md)   
 [Cambiar la configuración del grupo de recursos de servidor](../../relational-databases/resource-governor/change-resource-pool-settings.md)   
 [Grupos de cargas de trabajo del regulador de recursos](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Función clasificadora del regulador de recursos](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [DROP WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/drop-workload-group-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [DROP EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-external-resource-pool-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)  
  
  
