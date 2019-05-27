---
title: Exploración en el servidor de informes (Asesor de actualizaciones) directa | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3d2814a4-318a-45ed-b093-1e852fab561f
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 870937f4dffe356ca2216335c74566efc73d2a52
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66095535"
---
# <a name="direct-browsing-to-report-server-upgrade-advisor"></a>Exploración directa del servidor de informes (Asesor de actualizaciones)
  El Asesor de actualizaciones ha detectado que la instalación actual de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] explora directamente al directorio virtual del servidor de informes.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo de SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 El Asesor de actualizaciones ha detectado que la instalación actual de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está explorando directamente en el directorio virtual del servidor de informes, por ejemplo **http://\<nombre del servidor > / ReportServer**. Esto no se admite en las versiones actuales de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
> [!NOTE]  
>  Esta regla es una advertencia y la actualización no se bloquea.  
  
## <a name="corrective-action"></a>Acción correctora  
 Examinar mediante la interfaz de usuario de SharePoint para las bibliotecas de documentos o usar **http://\<nombre del servidor > / sitio de sharepoint >/_vti_bin/reportserver**.  
  
  
