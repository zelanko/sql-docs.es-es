---
title: Creación de un grupo de recursos | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2016
ms.prod: sql
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
ms.openlocfilehash: 5f992bfd1a132b33b125abd51e9b2fe8bc054756
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47801253"
---
# <a name="create-a-resource-pool"></a>Crear un grupo de recursos de servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Puede crear un grupo de recursos de servidor con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para comprender los principios de los grupos de recursos, consulte [Resource Governor Resource Pool](../../relational-databases/resource-governor/resource-governor-resource-pool.md).  
  
-   **Antes de empezar:**  [Limitaciones y restricciones](#LimitationsRestrictions), [Permisos](#Permissions)  
  
-   **Para crear un grupo de recursos, mediante:**  [SQL Server Management Studio](#CreRPProp), [Transact-SQL](#CreRPTSQL)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
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
  
1.  Ejecute la instrucción [CREATE RESOURCE POOL](../../t-sql/statements/create-resource-pool-transact-sql.md) o [CREATE EXTERNAL RESOURCE POOL](../../t-sql/statements/create-external-resource-pool-transact-sql.md) y especifique los valores de propiedad que quiere establecer.  
  
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
  
## <a name="see-also"></a>Ver también  
 [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Habilitar el regulador de recursos](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Grupo de recursos de servidor del regulador de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Cambiar la configuración del grupo de recursos de servidor](../../relational-databases/resource-governor/change-resource-pool-settings.md)   
 [Eliminar un grupo de recursos de servidor](../../relational-databases/resource-governor/delete-a-resource-pool.md)   
 [Configurar el regulador de recursos utilizando una plantilla](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)   
 [Grupos de cargas de trabajo del regulador de recursos](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Función clasificadora del regulador de recursos](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)   
 [ALTER EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-external-resource-pool-transact-sql.md)  
  
  
