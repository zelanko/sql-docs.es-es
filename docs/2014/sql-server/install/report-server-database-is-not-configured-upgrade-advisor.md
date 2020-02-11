---
title: La base de datos del servidor de informes no está configurada (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: b964300c-b220-4244-9fa6-c0c6a57760f6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: bb5dd5968930319532a29ff7c3909c36af99b3a0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "71952110"
---
# <a name="report-server-database-is-not-configured-upgrade-advisor"></a>La base de datos del servidor de informes no está configurada (Asesor de actualizaciones)
  La actualización está bloqueada debido a una configuración del servidor de informes incompleta. La base de datos del servidor de informes no está configurada.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modo nativo &#124; [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modo de SharePoint.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 La instalación solo puede actualizar una instancia del servidor de informes que esté totalmente configurada. Para continuar, debe configurar la base de datos del servidor de informes o usar el **Panel de control** de Microsoft Windows para quitar la característica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del servidor de informes de la instalación. Tras quitar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], puede actualizar otros componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="corrective-action"></a>Acción correctora  
 Si no configuró la base de datos del servidor de informes, éste no estará operativo y debería eliminarse antes de la actualización.  
  
 Para obtener información adicional sobre cómo desinstalar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , vea [desinstalar Reporting Services 2012](https://technet.microsoft.com/library/hh479745.aspx\(v=sql.11\)). En este tema se describe cómo desinstalar una versión concreta; los procedimientos son similares para versiones anteriores.  
  
## <a name="see-also"></a>Consulte también  
 [Reporting Services problemas de actualización &#40;el asesor de actualizaciones&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
