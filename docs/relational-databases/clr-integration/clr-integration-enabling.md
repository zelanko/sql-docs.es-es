---
title: "Habilitar la integración CLR | Documentos de Microsoft"
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- clr enabled option
- common language runtime [SQL Server], enabling
ms.assetid: eb3e9c64-7486-42e7-baf6-c956fb311a2c
caps.latest.revision: "19"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 86547cd78253d17ccacebe1d9b0db9e3cdda0c8a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="clr-integration---enabling"></a>Integración de CLR - habilitar
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]La característica de integración de common language runtime (CLR) está desactivada de forma predeterminada y debe habilitarse para poder utilizar los objetos que se implementan mediante la integración de CLR. Para habilitar la integración CLR, use la **clr habilitado** opción de la **sp_configure** procedimiento almacenado en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:  
  
```tsql  
  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'clr enabled', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
 Puede deshabilitar la integración CLR estableciendo la **clr habilitado** opción en 0. Al deshabilitar la integración CLR, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deja de ejecutar todas las rutinas CLR y descarga todos los dominios de aplicación.  
  
> [!NOTE]  
>  Para habilitar la integración CLR, debe tener permiso de nivel de servidor ALTER SETTINGS, que se concede implícitamente a los miembros de la **sysadmin** y **serveradmin** roles fijos de servidor.  
  
> [!NOTE]  
>  Es posible que los equipos configurados con grandes cantidades de memoria y un gran número de procesadores no puedan cargar la característica de integración CLR de SQL Server al iniciar el servidor. Para solucionar este problema, inicie el servidor mediante el **-gmemory_to_reserve** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] opción de inicio del servicio y especifique un valor de memoria suficientemente grande. Para más información, consulte [Database Engine Service Startup Options](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
> [!NOTE]  
>  No se admite la ejecución de Common Language Runtime (CLR) con "agrupación ligera". Antes de habilitar la integración CLR, debe deshabilitar la agrupación ligera. Para obtener más información, consulte [lightweight pooling Server Configuration Option](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md).  
  
## <a name="see-also"></a>Vea también  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [clr enabled (opción de configuración del servidor)](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [Roles de nivel de servidor](../../relational-databases/security/authentication-access/server-level-roles.md)  
  
  
