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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952212"
---
# <a name="direct-browsing-to-report-server-upgrade-advisor"></a>Exploración directa del servidor de informes (Asesor de actualizaciones)
  El asesor de actualizaciones ha detectado que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] la instalación actual de está navegando directamente al directorio virtual del servidor de informes.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modo de SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 El asesor de actualizaciones ha detectado que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] la instalación actual de está navegando directamente al directorio virtual del servidor de informes; por ejemplo, **http://\<nombre de servidor>/ReportServer**. Esto no se admite en las versiones actuales de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
> [!NOTE]  
>  Esta regla es una advertencia y la actualización no se bloquea.  
  
## <a name="corrective-action"></a>Acción correctora  
 Examine el uso de la interfaz de usuario de SharePoint para bibliotecas de documentos o use el **nombre del servidor de http://\<>> sitio de/SharePoint/_vti_bin/ReportServer**.  
  
  
