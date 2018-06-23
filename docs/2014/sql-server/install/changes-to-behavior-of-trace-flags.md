---
title: Cambios en el comportamiento de las marcas de seguimiento | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- trace flags [SQL Server], behavior changes
ms.assetid: d739df96-2659-4383-8e10-194657632526
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f03a9db47c6296e7d1c4ab764488c44d343393c7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113959"
---
# <a name="changes-to-behavior-of-trace-flags"></a>Cambios en el comportamiento de marcas de seguimiento
  Las marcas de seguimiento globales establecidos por una sesión surten efecto en otras sesiones de forma inmediata. Algunas marcas de seguimiento de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] no existen en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Le recomendamos deshabilitar todas las marcas de seguimiento antes de actualizar. Las marcas de seguimiento que modifican los modos de disponibilidad o de recuperación de base de datos, es posible que el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] actualice correctamente la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Puede habilitar las marcas de seguimiento después de comprobar que sean necesarias y que siguen siendo válidas en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Si necesita volver a habilitar las marcas de seguimiento, debería realizar pruebas adicionales en su instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] admite marcas de seguimiento globales y de nivel de sesión. En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], es posible especificar las marcas de seguimiento como locales o globales utilizando un argumento adicional (-1) en el comando DBCC TRACEON. Si no se especifica este argumento, el valor predeterminado será local.  
  
 Además, en [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], una marca de seguimiento establecida en la sesión A no tiene efecto automáticamente en una sesión b ya existente En su lugar, esta marca de seguimiento surte efecto después de la primera vez que se establece una marca de seguimiento en la sesión B. Este comportamiento es no determinista en [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] y es determinista en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores, donde se establecen las marcas de seguimiento globales establecidos en la sesión A inmediatamente en otras sesiones simultáneas.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
