---
title: Microsoft SQL Server Reporting Services el servicio compartido de SharePoint está instalado en paralelo (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6ae1017e-129b-4702-9ea7-00ac9b024062
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 529e07dc7beed8dc37741f6c9dab0b0b080d4898
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952695"
---
# <a name="microsoft-sql-server-reporting-services-sharepoint-shared-service-is-installed-side-by-side-upgrade-advisor"></a>El servicio compartido de SharePoint de Microsoft SQL Server Reporting Services está instalado en paralelo (Asesor de actualizaciones)
  El asesor de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] actualizaciones ha detectado que el servicio compartido de SharePoint está instalado en paralelo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]con una versión anterior de.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modo de SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 El asesor de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] actualizaciones ha detectado que el servicio compartido de SharePoint está instalado en paralelo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] con una versión anterior de que no se basa en la arquitectura del servicio compartido de SharePoint. La actualización se ha bloqueado porque en el equipo existen tecnologías antiguas y nuevas relacionadas con SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instaladas en paralelo.  
  
## <a name="corrective-action"></a>Acción correctora  
 Para continuar con la actualización, debe desinstalar una de las instalaciones existentes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Después de quitar una de las instalaciones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vuelva a ejecutar el Asesor de actualizaciones para confirmar que no hay ningún otro problema con la actualización.  
  
  
