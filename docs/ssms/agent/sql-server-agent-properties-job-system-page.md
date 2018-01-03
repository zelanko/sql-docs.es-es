---
title: "Propiedades de Agente SQL Server (página Sistema de trabajo) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ag.agent.job.f1
ms.assetid: e171d13e-1302-4f0e-88be-67d656aec8d3
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ddaf9fe88289bb05c312539fdd60f83d55e0ca8b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sql-server-agent-properties-job-system-page"></a>Propiedades de Agente SQL Server (página Sistema de trabajo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Use esta página para ver y modificar la forma en que el servicio del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] administra los trabajos.  
  
## <a name="options"></a>.  
**Intervalo de tiempo de espera de cierre (en segundos)**  
Especifica el número de segundos que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] espera a que los trabajos finalicen antes del cierre. Si el trabajo sigue en ejecución después del intervalo especificado, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] detendrá de manera obligatoria el trabajo.  
  
**Usar una cuenta de proxy de usuarios que no sean administradores**  
Establece una cuenta de proxy de usuarios que no sean administradores para el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] y las versiones posteriores admiten varios servidores proxy; por tanto, esta opción solo es aplicable al administrar versiones del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] anteriores a [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
**User name**  
Escriba el nombre del usuario de la cuenta proxy de usuarios que no sean administradores. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] admite varios servidores proxy; por tanto, esta opción solo es aplicable al administrar versiones del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] anteriores a [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
**Contraseña**  
Escriba la contraseña del usuario de la cuenta proxy de usuarios que no sean administradores. [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)] y las versiones posteriores admiten varios servidores proxy; por tanto, esta opción solo es aplicable al administrar versiones del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] anteriores a [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)].  
  
**Dominio**  
Escriba el dominio del usuario de la cuenta proxy de usuarios que no sean administradores. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] admite varios servidores proxy; por tanto, esta opción solo es aplicable al administrar versiones del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] anteriores a [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
## <a name="see-also"></a>Ver también  
[Implementar trabajos](../../ssms/agent/implement-jobs.md)  
  
