---
title: Filtros ISAPI ha detectado en el sitio del servidor de informes (Asesor de actualizaciones) | Documentos de Microsoft
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
- ISAPI filters
- report servers [Reporting Services], upgrade issues
ms.assetid: dd30560d-9e16-47c7-ba68-a9743a657e4e
caps.latest.revision: 12
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 18a9aab0737cb6d5127bbb3357d307c9c8f03aef
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198093"
---
# <a name="isapi-filters-detected-on-the-report-server-site-upgrade-advisor"></a>Se han detectado filtros ISAPI en el sitio del servidor de informes (Asesor de actualizaciones)
  El Asesor de actualizaciones ha detectado uno o más filtros ISAPI en el sitio web que hospeda los directorios virtuales del Administrador de informes y del servidor de informes. Filtros ISAPI no se admiten en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Nativo.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 Antes de actualizar, compruebe si los filtros ISAPI del sitio web están siendo utilizados por aplicaciones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Si no necesita el filtro ISAPI, puede actualizar el servidor de informes. La instalación creará las URL predeterminadas, sin compatibilidad con el filtro ISAPI que se ejecuta en IIS. Si necesita el filtro ISAPI, no lleve a cabo la actualización hasta que encuentre una forma alternativa de hospedar el filtro ISAPI (por ejemplo, utilizando ISA Server u hospedándolo en IIS). El servidor de informes admite ASP.NET HTTPModules como reemplazo de los filtros ISAPI en determinadas situaciones. Para obtener más información, vea la documentación de ASP.NET en MSDN.  
  
## <a name="corrective-action"></a>Acción correctora  
 Evalúe y utilice una solución independiente para hospedar los filtros ISAPI requeridos en la implementación.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de Reporting Services &#40;Asesor de actualizaciones&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  