---
title: Habilitar la integración con CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- clr enabled option
- common language runtime [SQL Server], enabling
ms.assetid: eb3e9c64-7486-42e7-baf6-c956fb311a2c
author: rothja
ms.author: jroth
ms.openlocfilehash: d7187906f1376deb81ca7ff4770af7b12b63c022
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84953675"
---
# <a name="enabling-clr-integration"></a>Habilitar la integración con CLR
  La característica de integración de Common Language Runtime (CLR) está desactivada de forma predeterminada y se debe habilitar para utilizar objetos que se implementan utilizando la integración CLR. Para habilitar la integración con CLR, utilice la opción **clr enabled** del **sp_configure** procedimiento almacenado:  
  
```  
  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'clr enabled', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
 Puede deshabilitar la integración de CLR estableciendo la opción **clr enabled** en 0. Al deshabilitar la integración CLR, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deja de ejecutar todas las rutinas CLR y descarga todos los dominios de aplicación.  
  
> [!NOTE]  
>  Para habilitar la integración con CLR, debe tener el permiso de nivel de servidor ALTER SETTINGs, que se mantiene implícitamente por parte de los miembros de los roles fijos de servidor **sysadmin** y **ServerAdmin** .  
  
> [!NOTE]  
>  Es posible que los equipos configurados con grandes cantidades de memoria y un gran número de procesadores no puedan cargar la característica de integración CLR de SQL Server al iniciar el servidor. Para solucionar este problema, inicie el servidor con la opción de inicio del servicio **-gmemory_to_reserve** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y especifique un valor de memoria suficientemente grande. Para más información, consulte [Opciones de inicio del servicio de motor de base de datos](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
> [!NOTE]  
>  No se admite la ejecución de Common Language Runtime (CLR) con "agrupación ligera". Antes de habilitar la integración CLR, debe deshabilitar la agrupación ligera. Para obtener más información, consulte [lightweight pooling (opción de configuración del servidor)](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md).  
  
## <a name="see-also"></a>Consulte también  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [clr enabled (opción de configuración del servidor)](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql)   
 [Roles de nivel de servidor](../security/authentication-access/server-level-roles.md)  
  
  
