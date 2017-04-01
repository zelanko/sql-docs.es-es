---
title: "common criteria compliance enabled (opci&#243;n de configuraci&#243;n del servidor) | Microsoft Docs"
ms.custom: ""
ms.date: "03/02/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "common criteria compliance"
helpviewer_keywords: 
  - "CC (Criterio común) [motor de base de datos]"
  - "compatibilidad con Criterio común [motor de base de datos]"
  - "Protección de información residual [motor de base de datos]"
  - "RIP (Protección de información residual)"
ms.assetid: 61766eea-c450-408d-af33-fbe7ef8c9ff2
caps.latest.revision: 24
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# common criteria compliance enabled (opci&#243;n de configuraci&#243;n del servidor)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La opción common criteria compliance enabled habilita los siguientes elementos necesarios para Criterio común.  
  
|Criterios|Descripción|  
|--------------|-----------------|  
|Protección de información residual (RIP)|RIP requiere que una asignación de memoria se sobrescriba con un patrón de bits conocido antes de que la memoria se reasigne a un nuevo recurso. Ajustarse al estándar RIP puede contribuir a mejorar la seguridad; sin embargo, sobrescribir la asignación de memoria puede ralentizar el rendimiento. Una vez habilitada la opción common criteria compliance enabled, se produce la sobrescritura.|  
|La capacidad para ver estadísticas de inicio de sesión|Una vez habilitada la opción common criteria compliance enabled, se habilita la auditoría de inicio de sesión. Cada vez que un usuario inicia sesión correctamente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se muestra la información acerca del último inicio de sesión correcto, el último inicio de sesión incorrecto y el número de intentos realizados entre la hora del último inicio de sesión correcto y la hora actual. Estas estadísticas de inicio de sesión se pueden ver consultando la vista de administración dinámica [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md).|  
|La columna GRANT no debe invalidar la tabla DENY|Una vez habilitada la opción common criteria compliance enabled, una instrucción DENY de nivel de tabla tiene prioridad sobre una instrucción GRANT de nivel de columna. Cuando no está habilitada la opción, una instrucción GRANT de columna tiene prioridad sobre una instrucción DENY de tabla.|  
  
 La opción common criteria compliance enabled es una opción avanzada. Solo se evalúan y certifican los criterios comunes para las ediciones Enterprise y Datacenter. Para obtener el estado más reciente de la certificación de criterios comunes, consulte el sitio web [Criterios comunes de Microsoft SQL Server](http://go.microsoft.com/fwlink/?LinkId=616319) .  
  
> [!IMPORTANT]  
>  Además de habilitar la opción common criteria compliance enabled, también debe descargar y ejecutar un script que termine la configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para cumplir con el nivel de garantía de evaluación 4+ (EAL4+) de Criterio común. Este script se puede descargar desde el sitio web sobre [Criterio común de Microsoft SQL Server](http://go.microsoft.com/fwlink/?LinkId=616319) .  
  
 Si está utilizando el procedimiento almacenado del sistema sp_configure para cambiar la configuración, solo podrá cambiar la opción common criteria compliance enabled si Mostrar opciones avanzadas está establecido en 1. La configuración surte efecto cuando se reinicia el servidor. Los valores posibles son 0 y 1:  
  
-   0 indica que no está habilitada la opción de cumplimiento del criterio común. Ésta es la opción predeterminada.  
  
-   1 indica que está habilitada la opción de cumplimiento del criterio común.  
  
## Ejemplos  
 El siguiente ejemplo habilita el cumplimiento del criterio común.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'common criteria compliance enabled', 1;  
GO  
RECONFIGURE  
GO  
```  
  
## Vea también  
 [Opciones de configuración de servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  