---
description: Solucionar problemas de trabajos multiservidor que usan servidores proxy
title: Solucionar problemas de trabajos multiservidor que usan servidores proxy
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- proxies [SQL Server Agent], multiserver jobs
- jobs [SQL Server Agent], multiserver jobs using proxies
ms.assetid: fc579bd3-010c-4f72-8b5c-d0cc18a1f280
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2cc15f5e73a52a74d5b73dfa8df704123f122b66
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038751"
---
# <a name="troubleshoot-multiserver-jobs-that-use-proxies"></a>Solucionar problemas de trabajos multiservidor que usan servidores proxy
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Azure SQL Managed Instance](/azure/sql-database/sql-database-managed-instance), actualmente son compatibles la mayoría de las características del Agente SQL Server. Consulte [Diferencias entre T-SQL de Azure SQL Managed Instance y SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para más información.

Los trabajos distribuidos que tienen pasos asociados a un proxy se ejecutan en el contexto de la cuenta de proxy del servidor de destino. Si se producen errores en los pasos de trabajo que utilizan cuentas de proxy cuando se descargan desde el servidor maestro, busque en la columna **error_message** de la tabla **sysdownloadlist** de la base de datos **msdb** los siguientes mensajes de error:  
  
-   "Este trabajo requiere una cuenta de proxy, pero la coincidencia de proxy se ha deshabilitado en el servidor de destino."  
  
    Para solucionar este error, establezca la subclave del Registro **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL.** _\<n\>_ **\SQLServerAgent\AllowDownloadedJobsToMatchProxyName** en **1 (true)** . De manera predeterminada, esta subclave está establecida en **0** (**false**). El valor de **MSSQL.** \<*n*> es el nombre de instancia; por ejemplo, **MSSQL.1** o **MSSQL.3**.  
  
-   "No se encontró el proxy".  
  
    Para resolver este error, asegúrese de que existe una cuenta de proxy en el servidor de destino con el mismo nombre que la cuenta de proxy del servidor maestro en la que se ejecuta el paso de trabajo.  
  
> [!CAUTION]  
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
## <a name="see-also"></a>Consulte también  
[Crear un entorno multiservidor](../../ssms/agent/create-a-multiserver-environment.md)  
