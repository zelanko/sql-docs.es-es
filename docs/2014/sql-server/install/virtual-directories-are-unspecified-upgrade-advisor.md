---
title: Los directorios virtuales no están especificados (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- virtual directories [Reporting Services]
ms.assetid: 7d32b560-49d6-4558-b5d6-9127067f82d6
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: c9ee7f745fc683a9ed93f2ca09ac94e1bf580f71
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952381"
---
# <a name="virtual-directories-are-unspecified-upgrade-advisor"></a>Los directorios virtuales no están especificados (Asesor de actualizaciones)
  El Asesor de actualizaciones no ha detectado ninguna configuración de directorios virtuales para el servicio web del servidor de informes o para el Administrador de informes. Una vez completada la actualización, debe configurar las reservas de direcciones URL para el servidor de informes mediante el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 La actualización de una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] incluye reservar nuevas URL para el servicio web del servidor de informes y para el Administrador de informes. El Asesor de actualizaciones no ha detectado directorios virtuales para el servidor de informes o para el Administrador de informes de la instancia que se va a actualizar y, por consiguiente, el proceso de actualización no pudo recopilar información suficiente para crear las reservas de direcciones URL del servidor de informes actualizado. La actualización puede continuar, pero el directorio virtual del servidor de informes o del Administrador de informes quedará sin definir después de la instalación de la actualización.  
  
## <a name="corrective-action"></a>Acción correctora  
 Tras finalizar la actualización, use el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para establecer las direcciones URL para el servidor de informes y para el Administrador de informes. Use el administrador de IIS para quitar los directorios virtuales que ya no necesite.  
  
 Para obtener más información, vea [configurar una &#40;dirección URL&#41; SSRS Configuration Manager](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) en los libros en pantalla de @no__t 3.  
  
## <a name="see-also"></a>Vea también  
 [Asesor de actualizaciones &#40;de Reporting Services upgrade issues&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
