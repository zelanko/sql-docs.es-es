---
title: Filtros ISAPI ha detectado en el sitio del servidor de informes (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- ISAPI filters
- report servers [Reporting Services], upgrade issues
ms.assetid: dd30560d-9e16-47c7-ba68-a9743a657e4e
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 7b30b585fc0448f04be2ee98c23f53794675fefe
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48192215"
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
  
  
