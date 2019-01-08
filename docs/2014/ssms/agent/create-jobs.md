---
title: Crear trabajos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], creating
- SQL Server Agent jobs, creating
ms.assetid: 465fb7fc-7622-4252-a178-ea51691c935b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 986e38ef42fe1af2aba8ba1625225a336f29158d
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52751317"
---
# <a name="create-jobs"></a>Crear trabajos
  Un trabajo es una serie específica de operaciones que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realiza secuencialmente. Un trabajo puede realizar una amplia variedad de actividades, incluidos scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] , aplicaciones de símbolo del sistema, scripts de Microsoft ActiveX, paquetes de Integration Services, comandos y consultas de Analysis Services o tareas de replicación. Los trabajos pueden ejecutar tareas repetitivas o que se pueden programar, y pueden notificar automáticamente a los usuarios el estado del trabajo mediante alertas, lo cual simplifica en gran medida la administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para crear un trabajo, el usuario debe ser miembro de uno de los roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o del rol fijo de servidor **sysadmin** . Solo pueden editar el trabajo el propietario de éste o los miembros del rol **sysadmin** . Los miembros del rol **sysadmin** pueden asignar el valor de propiedad de trabajo a otros usuarios, y pueden ejecutar cualquier trabajo, independientemente del propietario del trabajo. Para más información sobre los roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [Roles fijos de base de datos del Agente SQL Server](sql-server-agent-fixed-database-roles.md).  
  
 Se puede escribir un trabajo para que se ejecute en la instancia local de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o en varias instancias de una empresa. Para ejecutar trabajos en varios servidores, debe configurar al menos un servidor maestro, y uno o más servidores de destino. Para más información sobre los servidores maestros y de destino, consulte [Administración automatizada en una empresa](automated-administration-across-an-enterprise.md).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] El Agente registra la información del trabajo y de los pasos de trabajo en el historial de trabajos.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Descripción**|**Tema**|  
|Describe cómo crear un trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|[Crear un trabajo](create-a-job.md)|  
|Describe cómo volver a asignar a otro usuario la propiedad de los trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|[Give Others Ownership of a Job](give-others-ownership-of-a-job.md)|  
|Describe cómo configurar el registro de historial de trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|[Set Up the Job History Log](set-up-the-job-history-log.md)|  
  
## <a name="see-also"></a>Vea también  
 [Administrar pasos de trabajo](manage-job-steps.md)   
 [Administración automatizada en una empresa](automated-administration-across-an-enterprise.md)   
 [Crear y adjuntar programaciones a trabajos](create-and-attach-schedules-to-jobs.md)   
 [Ejecución de trabajos](run-jobs.md)   
 [Ver o modificar trabajos](view-or-modify-jobs.md)  
  
  
