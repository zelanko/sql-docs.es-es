---
title: Cambios en el comportamiento de las marcas de seguimiento | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- trace flags [SQL Server], behavior changes
ms.assetid: d739df96-2659-4383-8e10-194657632526
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 11d71e8401f6b870aaeb3f64f4145b509e3a3fe0
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065384"
---
# <a name="changes-to-behavior-of-trace-flags"></a>Cambios en el comportamiento de marcas de seguimiento
  Las marcas de seguimiento globales establecidos por una sesión surten efecto en otras sesiones de forma inmediata. Algunas marcas de seguimiento de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] no existen en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Le recomendamos deshabilitar todas las marcas de seguimiento antes de actualizar. Las marcas de seguimiento que modifican la disponibilidad de la base de datos o los modos de recuperación podrían impedir que se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] actualice correctamente la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Puede habilitar las marcas de seguimiento después de comprobar que sean necesarias y que siguen siendo válidas en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Si necesita volver a habilitar las marcas de seguimiento, debería realizar pruebas adicionales en su instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] admite marcas de seguimiento globales y de nivel de sesión. En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], es posible especificar las marcas de seguimiento como locales o globales utilizando un argumento adicional (-1) en el comando DBCC TRACEON. Si no se especifica este argumento, el valor predeterminado será local.  
  
 Además, en [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] , una marca de seguimiento establecida en la sesión a no surte efecto automáticamente en una sesión B ya existente. En su lugar, esta marca de seguimiento surte efecto solo después de la primera vez que se establece una marca de seguimiento en la sesión B. Este comportamiento no es determinista en [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] y es determinista en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores, donde las marcas de seguimiento globales establecidas en la sesión A se establecen inmediatamente en otras sesiones simultáneas.  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
