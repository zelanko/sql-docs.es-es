---
title: Exploración directa del servidor de informes (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 3d2814a4-318a-45ed-b093-1e852fab561f
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 6945828b2eba829c32d717c13393c9fbda4fc43e
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952212"
---
# <a name="direct-browsing-to-report-server-upgrade-advisor"></a>Exploración directa del servidor de informes (Asesor de actualizaciones)
  El asesor de actualizaciones ha detectado la instalación actual de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está explorando directamente el directorio virtual del servidor de informes.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modo de SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 El asesor de actualizaciones ha detectado la instalación actual de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está navegando directamente al directorio virtual del servidor de informes, por ejemplo, **http://\<nombre del servidor >/ReportServer**. Esto no se admite en las versiones actuales de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
> [!NOTE]  
>  Esta regla es una advertencia y la actualización no se bloquea.  
  
## <a name="corrective-action"></a>Acción correctora  
 Examine el uso de la interfaz de usuario de SharePoint para bibliotecas de documentos o use **http://\<nombre de servidor > sitio de/sharepoint >/_vti_bin/ReportServer**.  
  
  
