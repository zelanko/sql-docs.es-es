---
title: Se detectaron elementos de informe personalizados en el servidor de informes (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- custom report items, upgrading
ms.assetid: aee32006-65b2-4dfe-9570-d85a249d17b2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: feacf6aa6f233f85a67b43e7b72d3a50913991bf
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059326"
---
# <a name="custom-report-items-were-detected-on-the-report-server-upgrade-advisor"></a>Se detectaron elementos de informe personalizados en el servidor de informes (Asesor de actualizaciones)
  Los elementos de informe personalizados que se crearon para versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no son compatibles con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . La actualización puede continuar, pero los informes que utilicen algún elemento de informe personalizado no funcionarán correctamente. El Asesor de actualizaciones ha detectado elementos de informe personalizados. La actualización puede continuar, pero debe mover manualmente los archivos de elementos de informes personalizados a la nueva carpeta de instalación una vez completada la actualización.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** Modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] &#124; Modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 El Asesor de actualizaciones ha detectado configuraciones de extensión de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] personalizada en los archivos de configuración, lo que indica que la instalación incluye uno o más ensamblados personalizados para informes.  
  
## <a name="corrective-action"></a>Acción correctora  
 Una vez completada la actualización, mueva manualmente los archivos de elementos de informes personalizados a la nueva carpeta de instalación.  
  
## <a name="see-also"></a>Consulte también  
 [Reporting Services problemas de actualización &#40;el asesor de actualizaciones&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
