---
title: Ver o modificar trabajos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], modifying
- jobs [SQL Server Agent], viewing
- modifying jobs
- viewing jobs
- SQL Server Agent jobs, viewing
- SQL Server Agent jobs, modifying
- displaying jobs
ms.assetid: 57f649b8-190c-4304-abd7-7ca5297deab7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5d0d731d25c20597be3ac84adfacd8973e4a51cd
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85001707"
---
# <a name="view-or-modify-jobs"></a>Ver o modificar trabajos
  Puede ver cualquier trabajo que haya creado. Asimismo, después de ejecutar un trabajo, puede ver su historial. El historial de un trabajo le permite ver cuándo se ejecutó el trabajo, el estado del trabajo en conjunto y el estado de cada paso del trabajo. Puede ver si el trabajo ha tenido algún error en el pasado, cuándo finalizó correctamente por última vez y qué salida ha creado el trabajo cada vez que se ha ejecutado. Los miembros del rol fijo de servidor **sysadmin** pueden ver o modificar cualquier trabajo, con independencia de quién sea el propietario.  
  
> [!NOTE]  
>  Para que exista un historial de trabajos, éste debe haberse ejecutado al menos una vez. Puede limitar el tamaño total del registro de historial de trabajos y el tamaño por trabajo.  
  
 Por último, puede modificar un trabajo para satisfacer nuevos requisitos. Puede modificar:  
  
-   Opciones de respuesta  
  
-   Programaciones  
  
-   Pasos de trabajo  
  
-   Propiedad  
  
-   Categoría de trabajo  
  
-   Servidores de destino (solo para trabajos multiservidor)  
  
 Para asegurarse de que los cambios en los trabajos multiservidor surten efecto, debe exponer los cambios en la lista de descarga con el fin de que los servidores de destino puedan descargar el trabajo actualizado. Para asegurarse de que los servidores de destino tienen las definiciones de trabajos más actuales, exponga una instrucción INSERT después de actualizar el trabajo multiservidor, de la forma siguiente:  
  
```  
EXECUTE sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
 Para obtener más información, vea [sp_purge_jobhistory &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql).  
  
 Los miembros del rol fijo de servidor **sysadmin** pueden ver la definición o el historial de cualquier trabajo, y pueden modificar cualquier trabajo.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Descripción**|**Tema**|  
|Describe cómo ver trabajos del Agente [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|[View a Job](view-a-job.md)|  
|Describe cómo ver el registro del historial de trabajos del Agente [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|[Ver el historial de trabajos](view-the-job-history.md)|  
|Describe cómo eliminar el contenido del registro del historial de trabajos del Agente [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|[Clear the Job History Log](clear-the-job-history-log.md)|  
|Describe cómo establecer límites de tamaño para los registros de historial de trabajos del Agente [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|[Resize the Job History Log](resize-the-job-history-log.md)|  
|Describe cómo cambiar las propiedades de los trabajos del Agente [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|[Modify a Job](modify-a-job.md)|  
  
## <a name="see-also"></a>Consulte también  
 [dbo.sysjobhistory &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/dbo-sysjobhistory-transact-sql)  
  
  
