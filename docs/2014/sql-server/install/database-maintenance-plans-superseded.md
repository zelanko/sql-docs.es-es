---
title: Planes de mantenimiento de bases de datos reemplazados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- suspended database maintenance plans
- database maintenance plans [SQL Server Agent]
- maintenance plans [SQL Server Agent]
ms.assetid: efac127c-6c81-4c7a-a6c4-9aae5d15545d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7d41763582632a92b3a38bdbd67ee55b65f95b6d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66095763"
---
# <a name="database-maintenance-plans-superseded"></a>Se han reemplazado los planes de mantenimiento de bases de datos
    
## <a name="component"></a>Componente  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agente de  
  
## <a name="description"></a>Descripción  
 Los planes de mantenimiento de bases de datos existentes se actualizarán y continuarán funcionando. Sin embargo, no podrá crear nuevos planes de mantenimiento de bases de datos utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para ver los planes de mantenimiento en el Explorador de objetos, expanda Administración y, a continuación, expanda Heredado. Puede migrar los planes de mantenimiento de bases de datos existentes al nuevo formato seleccionando **migrar** en el menú contextual de cualquier plan de mantenimiento de bases de datos. Dado que la nueva característica de plan de mantenimiento no sustituye directamente a los planes de mantenimiento de bases de datos, es posible que se pierda alguna funcionalidad tras la migración. Al migrar un plan de mantenimiento de bases de datos no se elimina el plan anterior, por lo que puede probar su funcionalidad como plan de mantenimiento antes de quitar el plan anterior.  
  
 Las características siguientes ya no se admiten dentro de los planes de mantenimiento de bases de datos:  
  
-   Trasvase de registros  
  
-   La opción **intentar reparar los problemas secundarios** de la tarea de comprobación de integridad de la **base de datos**  
  
## <a name="corrective-action"></a>Acción correctora  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] evita que el trasvase de registros se incluya en un plan de mantenimiento de bases de datos. Para obtener más información, vea "Trasvase de registros" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
