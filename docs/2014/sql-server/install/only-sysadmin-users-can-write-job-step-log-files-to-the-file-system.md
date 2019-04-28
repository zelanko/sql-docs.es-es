---
title: Solo los usuarios sysadmin pueden escribir archivos de registro de paso de trabajo en el sistema de archivos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- job step log files [SQL Server Agent]
- log files [SQL Server Agent]
- writing job step log files
ms.assetid: d26a7cef-1a60-4c95-b9df-f8b4fec59f9b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2cb21caf909303fb751d9d616ef67efbac355425
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62806033"
---
# <a name="only-sysadmin-users-can-write-job-step-log-files-to-the-file-system"></a>Los administradores del sistema son los únicos usuarios que pueden escribir archivos de registro de paso de trabajo en el sistema de archivos
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] escribe opcionalmente un registro para cada paso de trabajo.  
  
## <a name="component"></a>Componente  
 e[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]   
  
## <a name="description"></a>Descripción  
 En [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente puede escribir registros en el sistema de archivos para los trabajos que pertenecen a los miembros de la **sysadmin** rol fijo de servidor. Si el propietario del trabajo no es un miembro de la **sysadmin** rol y si la cuenta de proxy está habilitada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente puede escribir registros en el sistema de archivos con las credenciales de la cuenta de proxy.  
  
 Después de actualizar, los trabajos que pertenecen a los usuarios que no son miembros de la **sysadmin** rol fijo de servidor ya no puede escribir registros en el sistema de archivos. En su lugar, estos usuarios pueden seleccionar la opción de escribir los registros en una tabla en la **msdb** base de datos. Los miembros de la **sysadmin** función todavía puede escribir archivos de registro en el sistema de archivos.  
  
## <a name="corrective-action"></a>Acción correctora  
 Después de actualizar, los trabajos que pertenecen a los usuarios que no son miembros de la **sysadmin** rol seguirá ejecutándose, pero no se crearán los registros. Para iniciar los pasos de trabajo en una tabla, los usuarios que no son miembros de la **sysadmin** rol debe actualizar manualmente sus trabajos.  
  
 Para obtener más información, vea los temas "Crear trabajos", "Crear pasos de trabajo" y "Controlar varios pasos del trabajo" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización del Agente SQL Server](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
