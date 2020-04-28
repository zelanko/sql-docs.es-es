---
title: Filtros ISAPI detectados en el sitio del servidor de informes (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- ISAPI filters
- report servers [Reporting Services], upgrade issues
ms.assetid: dd30560d-9e16-47c7-ba68-a9743a657e4e
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: a2b811955839eb22e3325d64c55454b92a6b1b8c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952444"
---
# <a name="isapi-filters-detected-on-the-report-server-site-upgrade-advisor"></a>Se han detectado filtros ISAPI en el sitio del servidor de informes (Asesor de actualizaciones)
  El Asesor de actualizaciones ha detectado uno o más filtros ISAPI en el sitio web que hospeda los directorios virtuales del Administrador de informes y del servidor de informes. Los Filtros ISAPI no se admiten en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Nativos.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 Antes de actualizar, compruebe si los filtros ISAPI del sitio web están siendo utilizados por aplicaciones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Si no necesita el filtro ISAPI, puede actualizar el servidor de informes. La instalación creará las URL predeterminadas, sin compatibilidad con el filtro ISAPI que se ejecuta en IIS. Si necesita el filtro ISAPI, no lleve a cabo la actualización hasta que encuentre una forma alternativa de hospedar el filtro ISAPI (por ejemplo, utilizando ISA Server u hospedándolo en IIS). El servidor de informes admite ASP.NET HTTPModules como reemplazo de los filtros ISAPI en determinadas situaciones. Para obtener más información, vea la documentación de ASP.NET en MSDN.  
  
## <a name="corrective-action"></a>Acción correctora  
 Evalúe y utilice una solución independiente para hospedar los filtros ISAPI requeridos en la implementación.  
  
## <a name="see-also"></a>Consulte también  
 [Reporting Services problemas de actualización &#40;el asesor de actualizaciones&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
