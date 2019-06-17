---
title: Compatibilidad con versiones anteriores de IIS componentes no estaban detectado (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- IIS [Reporting Services]
ms.assetid: e794185a-0a77-480a-9aea-d09f8760a6b8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9cfae4d34ef825ac1781c90fda8d7e38c0299a1b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094776"
---
# <a name="iis-backward-compatibility-components-were-not-detected-upgrade-advisor"></a>No se detectaron componentes de compatibilidad con versiones anteriores de IIS (Asesor de actualizaciones)
  El Asesor de actualizaciones no ha detectado componentes y configuraciones de IIS que proporcionan la información utilizada por el programa de instalación para crear las nuevas URL de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 IIS incluye componentes que proporcionan información acerca de los directorios virtuales del Administrador de informes y del servidor de informes, y esos componentes no se instalan en el equipo del servidor de informes. La actualización puede continuar, pero ésta no volverá a crear las URL para el servidor de informes o para el Administrador de informes.  
  
## <a name="corrective-action"></a>Acción correctora  
 Tras finalizar la actualización, utilice la herramienta de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para establecer las URL para el servidor de informes o para el Administrador de informes. Utilice el Administrador de IIS para quitar los directorios virtuales que no necesite.  
  
 Para obtener más información, consulte [configurar una dirección URL &#40;SSRS Configuration Manager&#41; ](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de Reporting Services &#40;Asesor de actualizaciones&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
