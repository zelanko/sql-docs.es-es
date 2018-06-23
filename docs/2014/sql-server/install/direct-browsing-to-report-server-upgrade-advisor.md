---
title: Exploración en el servidor de informes (Asesor de actualizaciones) directa | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3d2814a4-318a-45ed-b093-1e852fab561f
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: f08bc5d25eed160b814bfcdc255e1f198836da2b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103951"
---
# <a name="direct-browsing-to-report-server-upgrade-advisor"></a>Exploración directa del servidor de informes (Asesor de actualizaciones)
  El Asesor de actualizaciones ha detectado la instalación actual de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] explora directamente al directorio virtual del servidor de informes.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo de SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 El Asesor de actualizaciones ha detectado la instalación actual de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] explora directamente en el directorio virtual del servidor de informes, por ejemplo **http://\<nombre del servidor > / ReportServer**. Esto no se admite en las versiones actuales de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
> [!NOTE]  
>  Esta regla es una advertencia y la actualización no se bloquea.  
  
## <a name="corrective-action"></a>Acción correctora  
 Examine mediante la interfaz de usuario de SharePoint para las bibliotecas de documentos o use **http://\<nombre del servidor > / sitio de sharepoint >/_vti_bin/reportserver**.  
  
  