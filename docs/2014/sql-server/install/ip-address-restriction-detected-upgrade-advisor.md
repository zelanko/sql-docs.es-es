---
title: Restricción de dirección IP detectada (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: 9a154455-c68f-4403-a3a7-b90f4d35eecb
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 487ced9f103fd10a581841595111f01a5710bd15
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952085"
---
# <a name="ip-address-restriction-detected-upgrade-advisor"></a>Se detectó una restricción de dirección IP (Asesor de actualizaciones)
  El Asesor de actualizaciones ha detectado una o varias restricciones de dirección IP en el sitio web de IIS que hospeda los directorios virtuales del servidor de informes o del Administrador de informes. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no proporciona compatibilidad nativa con las restricciones de dirección IP.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nativo.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 La instalación no puede definir las restricciones de dirección IP en URL creadas para un servidor de informes actualizado. La actualización puede continuar, pero las restricciones de dirección IP no se definirán en las URL de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="corrective-action"></a>Acción correctora  
 Tras la actualización, utilice ISA Server, su software de firewall u otra solución para permitir o denegar las solicitudes realizadas desde direcciones IP específicas al servidor de informes.  
  
## <a name="see-also"></a>Vea también  
 [Asesor de actualizaciones &#40;de Reporting Services upgrade issues&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
