---
title: Base de datos de servidor de informes no está configurada (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: b964300c-b220-4244-9fa6-c0c6a57760f6
caps.latest.revision: 14
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: ccaed3fdebca2f242b1a638315e29915ddfc08d2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37249585"
---
# <a name="report-server-database-is-not-configured-upgrade-advisor"></a>La base de datos del servidor de informes no está configurada (Asesor de actualizaciones)
  La actualización está bloqueada debido a una configuración del servidor de informes incompleta. La base de datos del servidor de informes no está configurada.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** Modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] &#124; Modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 La instalación solo puede actualizar una instancia del servidor de informes que esté totalmente configurada. Para continuar, debe configurar la base de datos del servidor de informes, o utilizar Microsoft Windows **Panel de Control** para quitar la característica de servidor de informes desde el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalación. Tras quitar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], puede actualizar otros componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="corrective-action"></a>Acción correctora  
 Si no configuró la base de datos del servidor de informes, éste no estará operativo y debería eliminarse antes de la actualización.  
  
 Para obtener más información sobre cómo desinstalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , consulte [desinstalar Reporting Services 2012](http://technet.microsoft.com/library/hh479745.aspx\(v=sql.11\)). En este tema se describe cómo desinstalar una versión concreta; los procedimientos son similares para versiones anteriores.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de Reporting Services &#40;Asesor de actualizaciones&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
