---
title: Propiedades de Agente SQL Server (página Sistema de trabajo) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.ag.agent.job.f1
ms.assetid: e171d13e-1302-4f0e-88be-67d656aec8d3
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 728f3cc395ec9e02b3e64236aa52e5b6cf99d8ca
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37202355"
---
# <a name="sql-server-agent-properties-job-system-page"></a>Propiedades de Agente SQL Server (página Sistema de trabajo)
  Utilice esta página para ver y modificar la forma en que el servicio Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administra los trabajos.  
  
## <a name="options"></a>Opciones  
 **Intervalo de tiempo de espera de cierre (en segundos)**  
 Especifica el número de segundos que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] espera a que los trabajos finalicen antes del cierre. Si el trabajo sigue en ejecución después del intervalo especificado, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detendrá de manera obligatoria el trabajo.  
  
 **Usar una cuenta de proxy de usuarios que no sean administradores**  
 Establece una cuenta de proxy de usuarios que no sean administradores para el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y las versiones posteriores admiten varios servidores proxy; por tanto, esta opción solo es aplicable al administrar versiones del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
 **Nombre de usuario.**  
 Escriba el nombre del usuario de la cuenta proxy de usuarios que no sean administradores. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite varios servidores proxy; por tanto, esta opción solo es aplicable al administrar versiones del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
 **Contraseña**  
 Escriba la contraseña del usuario de la cuenta proxy de usuarios que no sean administradores. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y las versiones posteriores admiten varios servidores proxy; por tanto, esta opción solo es aplicable al administrar versiones del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 **Dominio**  
 Escriba el dominio del usuario de la cuenta proxy de usuarios que no sean administradores. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite varios servidores proxy; por tanto, esta opción solo es aplicable al administrar versiones del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Implementar trabajos](implement-jobs.md)  
  
  
