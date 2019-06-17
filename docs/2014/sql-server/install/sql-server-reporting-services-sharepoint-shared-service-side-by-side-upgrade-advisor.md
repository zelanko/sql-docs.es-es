---
title: Microsoft SQL Server Reporting Services servicio compartido de SharePoint está instalado en paralelo (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 6ae1017e-129b-4702-9ea7-00ac9b024062
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: cfa2eb99a475cb8f8bce8a0a1101edd767997aef
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091855"
---
# <a name="microsoft-sql-server-reporting-services-sharepoint-shared-service-is-installed-side-by-side-upgrade-advisor"></a>El servicio compartido de SharePoint de Microsoft SQL Server Reporting Services está instalado en paralelo (Asesor de actualizaciones)
  Asesor de actualizaciones ha detectado [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servicio compartido de SharePoint se instala en paralelo con una versión anterior de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modo de SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 Asesor de actualizaciones ha detectado [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servicio compartido de SharePoint se instala en paralelo con una versión anterior de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que no se basa en la arquitectura del servicio compartido de SharePoint. La actualización se ha bloqueado porque en el equipo existen tecnologías antiguas y nuevas relacionadas con SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instaladas en paralelo.  
  
## <a name="corrective-action"></a>Acción correctora  
 Para continuar con la actualización, debe desinstalar una de las instalaciones existentes de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Después de quitar una de las instalaciones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vuelva a ejecutar el Asesor de actualizaciones para confirmar que no hay ningún otro problema con la actualización.  
  
  
