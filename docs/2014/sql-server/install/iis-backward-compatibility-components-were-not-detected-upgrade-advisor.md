---
title: No se detectaron componentes de compatibilidad con versiones anteriores de IIS (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- IIS [Reporting Services]
ms.assetid: e794185a-0a77-480a-9aea-d09f8760a6b8
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: dbf5686d4a947cb8629675368c59c8039c93835e
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952505"
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
  
 Para obtener más información, vea [configurar una &#40;dirección URL&#41; SSRS Configuration Manager](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) en los libros en pantalla de @no__t 3.  
  
## <a name="see-also"></a>Vea también  
 [Asesor de actualizaciones &#40;de Reporting Services upgrade issues&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
