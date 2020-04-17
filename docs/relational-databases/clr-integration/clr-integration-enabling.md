---
title: Habilitación de la integración de CLR ( Habilitar la integración de Microsoft Docs
description: Microsoft SQL Server que hospeda CLR se denomina integración de CLR, que está deshabilitada de forma predeterminada. Use el procedimiento almacenado sp_configure para habilitar la integración de CLR.
ms.custom: ''
ms.date: 09/17/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- clr enabled option
- common language runtime [SQL Server], enabling
ms.assetid: eb3e9c64-7486-42e7-baf6-c956fb311a2c
author: rothja
ms.author: jroth
ms.openlocfilehash: 7d161135c8c8b0c7d7932eb08aa98509efc4bc45
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488120"
---
# <a name="clr-integration---enabling"></a>Integración CLR: habilitar
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  La característica de integración de Common Language Runtime (CLR) está desactivada de forma predeterminada y se debe habilitar para utilizar objetos que se implementan utilizando la integración CLR. Para habilitar la integración de CLR, utilice la [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]opción clr **enabled** del procedimiento almacenado **sp_configure** en:  
  
```sql  
EXEC sp_configure 'clr enabled', 1;  
RECONFIGURE;  
GO  
```  
  
 Puede deshabilitar la integración de CLR estableciendo la opción **clr enabled** en 0. Cuando deshabilita la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integración de CLR, deja de ejecutar todas las rutinas CLR definidas por el usuario y descarga todos los dominios de aplicación. Las características que se basan en CLR, como `FORMAT` el tipo de datos **hierarchyid,** la función, la replicación y la administración basada en directivas, no se ven afectadas por esta configuración y seguirán funcionando.
  
> [!NOTE]  
>  Para habilitar la integración de CLR, debe tener el permiso de nivel de servidor ALTER SETTINGS, que los miembros de los roles fijos de servidor **sysadmin** y **serveradmin** mantienen implícitamente.  
  
> [!NOTE]  
>  Es posible que los equipos configurados con grandes cantidades de memoria y un gran número de procesadores no puedan cargar la característica de integración CLR de SQL Server al iniciar el servidor. Para solucionar este problema, inicie el servidor mediante la opción de inicio del servicio **-gmemory_to_reserve** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y especifique un valor de memoria lo suficientemente grande. Para más información, consulte [Opciones de inicio del servicio de motor de base de datos](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
> [!NOTE]  
>  No se admite la ejecución de Common Language Runtime (CLR) con "agrupación ligera". Antes de habilitar la integración CLR, debe deshabilitar la agrupación ligera. Para obtener más información, consulte [lightweight pooling (opción de configuración del servidor)](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md).  
  
## <a name="see-also"></a>Consulte también  
 [sp_configure &#40;&#41;Transact-SQLTransact-SQL](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [clr habilitado Opción de configuración del servidor](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQLTransact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [GRANT &#40;&#41;Transact-SQLTransact-SQL](../../t-sql/statements/grant-transact-sql.md)   
 [Roles de nivel de servidor](../../relational-databases/security/authentication-access/server-level-roles.md)  
  
  
