---
title: Habilitar la integración con CLR | Microsoft Docs
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
ms.openlocfilehash: 07066dc7ffbd48273ace55e0c9867661b2cbfe59
ms.sourcegitcommit: 445842da7c7d216b94a9576e382164c67f54e19a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/30/2019
ms.locfileid: "71680849"
---
# <a name="clr-integration---enabling"></a>Integración CLR: habilitar
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  La característica de integración de Common Language Runtime (CLR) está desactivada de forma predeterminada y se debe habilitar para utilizar objetos que se implementan utilizando la integración CLR. Para habilitar la integración con CLR, utilice la opción **clr enabled** del **sp_configure** procedimiento almacenado en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:  
  
```sql  
EXEC sp_configure 'clr enabled', 1;  
RECONFIGURE;  
GO  
```  
  
 Puede deshabilitar la integración de CLR estableciendo la opción **clr enabled** en 0. Al deshabilitar la integración con CLR, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deja de ejecutar todas las rutinas CLR definidas por el usuario y descarga todos los dominios de aplicación. Las características que dependen de CLR, como el tipo de datos **hierarchyid** , la función `FORMAT`, la replicación y la administración basada en directivas, no se ven afectadas por esta configuración y seguirán funcionando.
  
> [!NOTE]  
>  Para habilitar la integración con CLR, debe tener el permiso de nivel de servidor ALTER SETTINGs, que se mantiene implícitamente por parte de los miembros de los roles fijos de servidor **sysadmin** y **ServerAdmin** .  
  
> [!NOTE]  
>  Es posible que los equipos configurados con grandes cantidades de memoria y un gran número de procesadores no puedan cargar la característica de integración CLR de SQL Server al iniciar el servidor. Para solucionar este problema, inicie el servidor con la opción **de** inicio del servicio gmemory_to_reserve[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y especifique un valor de memoria suficientemente grande. Para más información, consulte [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
> [!NOTE]  
>  No se admite la ejecución de Common Language Runtime (CLR) con "agrupación ligera". Antes de habilitar la integración CLR, debe deshabilitar la agrupación ligera. Para obtener más información, consulte [lightweight pooling Server Configuration Option](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md).  
  
## <a name="see-also"></a>Vea también  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [clr enabled (opción de configuración del servidor)](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [Roles de nivel de servidor](../../relational-databases/security/authentication-access/server-level-roles.md)  
  
  
