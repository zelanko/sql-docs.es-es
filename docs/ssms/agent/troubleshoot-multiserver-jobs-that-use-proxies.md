---
title: Solucionar problemas de trabajos multiservidor que usan servidores proxy | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- proxies [SQL Server Agent], multiserver jobs
- jobs [SQL Server Agent], multiserver jobs using proxies
ms.assetid: fc579bd3-010c-4f72-8b5c-d0cc18a1f280
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6a02ace1fe1ba285bc340b9dca87112325f97210
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="troubleshoot-multiserver-jobs-that-use-proxies"></a>Solucionar problemas de trabajos multiservidor que usan servidores proxy
Los trabajos distribuidos que tienen pasos asociados a un proxy se ejecutan en el contexto de la cuenta de proxy del servidor de destino. Si se producen errores en los pasos de trabajo que utilizan cuentas de proxy cuando se descargan desde el servidor maestro, busque en la columna **error_message** de la tabla **sysdownloadlist** de la base de datos **msdb** los siguientes mensajes de error:  
  
-   "Este trabajo requiere una cuenta de proxy, pero la coincidencia de proxy se ha deshabilitado en el servidor de destino."  
  
    Para solucionar este error, establezca la subclave del registro **\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\MSSQL.***\<n*>**\SQLServerAgent\AllowDownloadedJobsToMatchProxyName** en **1 (true)**. De manera predeterminada, esta subclave está establecida en **0** (**false**). El valor de **MSSQL.**\<*n*> es el nombre de la instancia; por ejemplo, **MSSQL.1** o **MSSQL.3**.  
  
-   "No se encontró el proxy".  
  
    Para resolver este error, asegúrese de que existe una cuenta de proxy en el servidor de destino con el mismo nombre que la cuenta de proxy del servidor maestro en la que se ejecuta el paso de trabajo.  
  
> [!CAUTION]  
> [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry_md.md)]  
  
## <a name="see-also"></a>Vea también  
[Crear un entorno multiservidor](../../ssms/agent/create-a-multiserver-environment.md)  
  

