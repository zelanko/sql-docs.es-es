---
title: 'Propiedades de paso de trabajo: nuevo paso de trabajo (página Opciones avanzadas) | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.stepadvanced.f1
ms.assetid: bdecfd4f-bcd8-4ba2-8ada-fbb636314f40
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 18924b7b6ccdf7e54782e575a265c8961f38397a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47762700"
---
# <a name="job-step-properties---new-job-step-advanced-page"></a>Propiedades de paso de trabajo - Nuevo paso de trabajo (página Opciones avanzadas)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

Use esta página para ver y cambiar las propiedades de un paso de trabajo del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="options"></a>Opciones  
**Acción en caso de éxito**  
Establece la acción que debe realizar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si el paso de trabajo se realiza correctamente.  
  
**Número de reintentos**  
Establece el número de veces que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] intenta volver a ejecutar un paso de trabajo con error.  
  
**Intervalo de reintento (minutos)**  
Establece el tiempo que espera el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entre los reintentos.  
  
**Acción en caso de error**  
Establece la acción que debe realizar el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si el paso de trabajo no se realiza correctamente.  
  
## <a name="options-for-transact-sql-job-steps"></a>Opciones de pasos de trabajo Transact-SQL  
**Archivo de salida**  
Establece el archivo que se utiliza para la salida desde el paso de trabajo. Esta opción solo está disponible para los miembros del rol fijo de servidor **sysadmin** .  
  
**...**  
Permite buscar el archivo que se utiliza para la salida desde el paso de trabajo.  
  
**Ver**  
En [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], este botón está deshabilitado para ver los archivos de salida. Para verlos, debe utilizar el Bloc de notas.  
  
**Anexar la salida al archivo existente**  
Anexa la salida al contenido existente del archivo. De lo contrario, el anterior contenido del archivo se sobrescribe cada vez que se ejecuta el paso de trabajo.  
  
**Registro en tabla**  
Registra la salida del paso de trabajo en la tabla **sysjobstepslogs** de la base de datos **msdb** .  
  
**Ver**  
Después de ejecutar el paso de trabajo al menos una vez, haga clic en **Ver** para consultar el resultado en la tabla.  
  
**Anexar salida a la entrada existente de la tabla**  
Anexa la salida al contenido existente de la tabla. De lo contrario, el anterior contenido de la tabla se sobrescribe cada vez que se ejecuta el paso de trabajo.  
  
**Incluir salida de paso en historial**  
Seleccione esta opción para incluir la salida del paso de trabajo en el historial de trabajos.  
  
**Ejecutar como usuario**  
Si es miembro del rol fijo de servidor **sysadmin** , puede seleccionar otro inicio de sesión de SQL para ejecutar este paso de trabajo.  
  
## <a name="options-for-operating-system-cmdexec-job-steps"></a>Opciones de pasos de trabajo del sistema operativo (CmdExec)  
**Archivo de salida**  
Establece el archivo que se utiliza para la salida desde el paso de trabajo.  
  
**...**  
Permite buscar el archivo que se utiliza para la salida desde el paso de trabajo.  
  
**Ver**  
En [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], este botón está deshabilitado para ver los archivos de salida. Para verlos, debe utilizar el Bloc de notas.  
  
**Anexar la salida al archivo existente**  
Anexa la salida del paso de trabajo al contenido anterior del archivo cada vez que se ejecuta.  
  
**Registro en tabla**  
Registra la salida del paso de trabajo en la tabla **sysjobstepslogs** de la base de datos **msdb** .  
  
**Ver**  
Después de ejecutar el paso de trabajo al menos una vez, haga clic en **Ver** para consultar el resultado en la tabla.  
  
**Anexar salida a la entrada existente de la tabla**  
Anexa la salida al contenido existente de la tabla. De lo contrario, el anterior contenido de la tabla se sobrescribe cada vez que se ejecuta el paso de trabajo.  
  
**Incluir salida de paso en historial**  
Seleccione esta opción para incluir la salida del paso de trabajo en el historial de trabajos.  
  
## <a name="options-for-powershell-job-steps"></a>Opciones de pasos de trabajo de PowerShell  
**Archivo de salida**  
Establece el archivo que se utiliza para la salida desde el paso de trabajo.  
  
**...**  
Permite buscar el archivo que se utiliza para la salida desde el paso de trabajo.  
  
**Ver**  
En [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], este botón está deshabilitado para ver los archivos de salida. Para verlos, debe utilizar el Bloc de notas.  
  
**Anexar la salida al archivo existente**  
Anexa la salida del paso de trabajo al contenido anterior del archivo cada vez que se ejecuta.  
  
**Registro en tabla**  
Registra la salida del paso de trabajo en la tabla **sysjobstepslogs** de la base de datos **msdb** .  
  
**Ver**  
Después de ejecutar el paso de trabajo al menos una vez, haga clic en **Ver** para consultar el resultado en la tabla.  
  
**Anexar salida a la entrada existente de la tabla**  
Anexa la salida al contenido existente de la tabla. De lo contrario, el anterior contenido de la tabla se sobrescribe cada vez que se ejecuta el paso de trabajo.  
  
**Incluir salida de paso en historial**  
Seleccione esta opción para incluir la salida del paso de trabajo en el historial de trabajos.  
  
## <a name="options-for-replication-queue-reader-job-steps"></a>Opciones de pasos de trabajo del Lector de cola de replicación  
**Server**  
Establece el servidor que se utiliza en un paso de trabajo de un lector de cola de replicación.  
  
**Base de datos**  
Establece la base de datos que se utiliza en un paso de trabajo de un lector de cola de replicación.  
  
## <a name="options-for-sql-server-analysis-services-job-steps"></a>Opciones de pasos de trabajo de SQL Server Analysis Services  
**Archivo de salida**  
Establece el archivo que se utiliza para la salida desde el paso de trabajo. Esta opción solo está disponible para los miembros del rol fijo de servidor **sysadmin** .  
  
**...**  
Permite buscar el archivo que se utiliza para la salida desde el paso de trabajo.  
  
**Ver**  
En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], este botón está deshabilitado para ver los archivos de salida. Para verlos, debe utilizar el Bloc de notas.  
  
**Anexar la salida al archivo existente**  
Anexa la salida al contenido existente del archivo. De lo contrario, el anterior contenido del archivo se sobrescribe cada vez que se ejecuta el paso de trabajo.  
  
**Registro en tabla**  
Registra la salida del paso de trabajo en la tabla **sysjobstepslogs** de la base de datos **msdb** .  
  
**Ver**  
Después de ejecutar el paso de trabajo al menos una vez, haga clic en **Ver** para consultar el resultado en la tabla.  
  
**Anexar salida a la entrada existente de la tabla**  
Anexa la salida al contenido existente de la tabla. De lo contrario, el anterior contenido de la tabla se sobrescribe cada vez que se ejecuta el paso de trabajo.  
  
**Incluir salida de paso en historial**  
Seleccione esta opción para incluir la salida del paso de trabajo en el historial de trabajos.  
  
## <a name="see-also"></a>Ver también  
[Administrar pasos de trabajo](../../ssms/agent/manage-job-steps.md)  
  
