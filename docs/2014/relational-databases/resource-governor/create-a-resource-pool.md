---
title: Creación de un grupo de recursos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- resource pools [SQL Server], create
- Resource Governor, resource pool create
ms.assetid: 44dd0567-a4c8-4c72-89ff-e76f6ddef344
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f4d18ef352c3e5ab6342e573d16bc3deaed5db72
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52753967"
---
# <a name="create-a-resource-pool"></a>Crear un grupo de recursos de servidor
  Puede crear un grupo de recursos de servidor con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   **Antes de empezar:**  [Limitaciones y restricciones](#LimitationsRestrictions), [permisos](#Permissions)  
  
-   **Para crear un recurso de grupo, mediante:**  [SQL Server Management Studio](#CreRPProp), [Transact-SQL](#CreRPTSQL)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="LimitationsRestrictions"></a> Limitaciones y restricciones  
 El porcentaje máximo de uso de la CPU debe ser igual o superior al porcentaje mínimo de uso de la CPU. El porcentaje máximo de uso de memoria debe ser igual o superior al porcentaje mínimo de uso de memoria.  
  
 Las sumas de los porcentajes mínimos de uso de la CPU y los porcentajes mínimos de uso de memoria de todos los grupos de recursos de servidor no deben superar el 100 por cien.  
  
###  <a name="Permissions"></a> Permissions  
 Para crear un grupo de recursos de servidor se requiere un permiso CONTROL SERVER.  
  
##  <a name="CreRPProp"></a> Crear un grupo de recursos de servidor mediante SQL Server Management Studio  
 **Para crear un grupo de recursos de servidor con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra el Explorador de objetos y expanda de forma recursiva el nodo **Administración** hasta e incluyendo el nodo **Regulador de recursos**.  
  
2.  Haga clic con el botón derecho en **Regulador de recursos**y, luego, haga clic en **Propiedades**.  
  
3.  En la cuadrícula **Grupos de recursos de servidor** , haga clic en la primera columna de la fila vacía. Esta columna tiene como etiqueta un asterisco (*).  
  
4.  Haga doble clic en la celda vacía de la columna **Nombre** . Escriba el nombre que desee utilizar con el grupo de recursos de servidor.  
  
5.  Haga clic o doble clic en cualquier otra celda de la fila que desea cambiar, y especifique los nuevos valores.  
  
6.  Haga clic en **Aceptar**para guardar los cambios.  
  
##  <a name="CreRPTSQL"></a> Crear un grupo de recursos de servidor mediante Transact-SQL  
 **Para crear un grupo de recursos de servidor con [!INCLUDE[tsql](../../includes/tsql-md.md)]**  
  
1.  Ejecute la instrucción `CREATE RESOURCE POOL` especificando los valores de propiedad que desea establecer.  
  
2.  Ejecute la instrucción **ALTER RESOURCE GOVERNOR RECONFIGURE** .  
  
### <a name="example-transact-sql"></a>Ejemplo (Transact-SQL)  
 En el ejemplo siguiente se crea un grupo de recursos de servidor denominado `poolAdhoc`.  
  
```  
CREATE RESOURCE POOL poolAdhoc  
WITH (MAX_CPU_PERCENT = 20);  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Regulador de recursos](resource-governor.md)   
 [Habilitar el regulador de recursos](enable-resource-governor.md)   
 [Resource Governor Resource Pool](resource-governor-resource-pool.md)   
 [Cambiar la configuración del grupo de recursos de servidor](change-resource-pool-settings.md)   
 [Eliminar un grupo de recursos de servidor](delete-a-resource-pool.md)   
 [Configurar el regulador de recursos utilizando una plantilla](configure-resource-governor-using-a-template.md)   
 [Grupos de cargas de trabajo del regulador de recursos](resource-governor-workload-group.md)   
 [Función clasificadora del regulador de recursos](resource-governor-classifier-function.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-resource-pool-transact-sql)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-resource-governor-transact-sql)  
  
  
