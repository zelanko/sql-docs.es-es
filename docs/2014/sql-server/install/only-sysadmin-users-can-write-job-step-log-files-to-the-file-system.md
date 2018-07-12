---
title: Solo los usuarios sysadmin pueden escribir archivos de registro de paso de trabajo en el sistema de archivos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- job step log files [SQL Server Agent]
- log files [SQL Server Agent]
- writing job step log files
ms.assetid: d26a7cef-1a60-4c95-b9df-f8b4fec59f9b
caps.latest.revision: 24
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6b31dace7b76d068187b495d6e63517967a6c0f9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37151956"
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
  
  
