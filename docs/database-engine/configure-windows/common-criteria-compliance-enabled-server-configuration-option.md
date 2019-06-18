---
title: Configuración de compatibilidad con criterio común habilitada | Microsoft Docs
ms.custom: ''
ms.date: 08/21/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- common criteria compliance
helpviewer_keywords:
- CC (common criteria) [Database Engine]
- common criteria compliance [Database Engine]
- Risidual Information Protection [Database Engine]
- RIP (Residual Information Protection)
ms.assetid: 61766eea-c450-408d-af33-fbe7ef8c9ff2
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 533cdfe3b83b8b759129a27a6dc1699298dd3f13
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62817972"
---
# <a name="common-criteria-compliance-enabled-server-configuration"></a>Configuración de compatibilidad con criterio común habilitada
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La opción de compatibilidad con el criterio común habilita los elementos siguientes necesarios para los [Common Criteria for Information Technology Security Evaluation](https://www.commoncriteriaportal.org/) (Criterios comunes para la evaluación de seguridad de tecnologías de la información).  
  
|Criterios|Descripción|  
|--------------|-----------------|  
|Protección de información residual (RIP)|RIP requiere que una asignación de memoria se sobrescriba con un patrón de bits conocido antes de que la memoria se reasigne a un nuevo recurso. Ajustarse al estándar RIP puede contribuir a mejorar la seguridad; sin embargo, sobrescribir la asignación de memoria puede ralentizar el rendimiento. Una vez habilitada la opción common criteria compliance enabled, se produce la sobrescritura.|  
|La capacidad para ver estadísticas de inicio de sesión|Una vez habilitada la opción common criteria compliance enabled, se habilita la auditoría de inicio de sesión. Cada vez que un usuario inicia sesión correctamente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se muestra la información acerca del último inicio de sesión correcto, el último inicio de sesión incorrecto y el número de intentos realizados entre la hora del último inicio de sesión correcto y la hora actual. Estas estadísticas de inicio de sesión se pueden ver consultando la vista de administración dinámica [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) .|  
|La columna `GRANT` no debe invalidar la tabla `DENY`|Una vez habilitada la opción common criteria compliance enabled, una instrucción `DENY` de nivel de tabla tiene prioridad sobre una instrucción `GRANT` de nivel de columna. Cuando la opción no está habilitada, una instrucción `GRANT` de columna tiene prioridad sobre una instrucción `DENY` de tabla.|  
  
 La opción common criteria compliance enabled es una opción avanzada. Solo se evalúan y certifican los criterios comunes para las ediciones Enterprise y Datacenter. Para obtener el estado más reciente de la certificación de criterios comunes, consulte el sitio web [Criterios comunes de Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkId=616319) .  
  
> [!IMPORTANT]  
>  Además de habilitar la opción common criteria compliance enabled, también debe descargar y ejecutar un script que termine la configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para cumplir con el nivel de garantía de evaluación 4+ (EAL4+) de Criterio común. Este script se puede descargar desde el sitio web sobre [Criterio común de Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkId=616319) .  
  
 Si está usando el procedimiento almacenado del sistema `sp_configure` para cambiar la configuración, solo podrá cambiar la opción common criteria compliance enabled si Mostrar opciones avanzadas está establecido en 1. La configuración surte efecto cuando se reinicia el servidor. Los valores posibles son 0 y 1:  
  
-   0 indica que no está habilitada la opción de cumplimiento del criterio común. Ésta es la opción predeterminada.  
  
-   1 indica que está habilitada la opción de cumplimiento del criterio común.  
  
## <a name="examples"></a>Ejemplos  
 El siguiente ejemplo habilita el cumplimiento del criterio común.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'common criteria compliance enabled', 1;  
GO  
RECONFIGURE WITH OVERRIDE; 
GO  
```  

Reinicie [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].
  
## <a name="see-also"></a>Consulte también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)
