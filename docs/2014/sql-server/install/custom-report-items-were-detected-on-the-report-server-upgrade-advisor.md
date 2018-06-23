---
title: Se detectaron elementos de informe personalizados en el servidor de informes (Asesor de actualizaciones) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- custom report items, upgrading
ms.assetid: aee32006-65b2-4dfe-9570-d85a249d17b2
caps.latest.revision: 14
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 6395fceff333f29c1fa7d5dbc29ecad7bebdadd4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104630"
---
# <a name="custom-report-items-were-detected-on-the-report-server-upgrade-advisor"></a>Se detectaron elementos de informe personalizados en el servidor de informes (Asesor de actualizaciones)
  Elementos de informe personalizados que se crearon para versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no son compatibles con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. La actualización puede continuar, pero los informes que utilicen algún elemento de informe personalizado no funcionarán correctamente. El Asesor de actualizaciones ha detectado elementos de informe personalizados. La actualización puede continuar, pero debe mover manualmente los archivos de elementos de informes personalizados a la nueva carpeta de instalación una vez completada la actualización.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** Modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] &#124; Modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 El Asesor de actualizaciones ha detectado configuraciones de extensión de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] personalizada en los archivos de configuración, lo que indica que la instalación incluye uno o más ensamblados personalizados para informes.  
  
## <a name="corrective-action"></a>Acción correctora  
 Una vez completada la actualización, mueva manualmente los archivos de elementos de informes personalizados a la nueva carpeta de instalación.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de Reporting Services &#40;Asesor de actualizaciones&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  