---
title: Restricción de dirección IP detectado (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: 9a154455-c68f-4403-a3a7-b90f4d35eecb
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4bbde8eb313d432a7a90cfa7f03c54f4c6aeb06f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63301380"
---
# <a name="ip-address-restriction-detected-upgrade-advisor"></a>Se detectó una restricción de dirección IP (Asesor de actualizaciones)
  El Asesor de actualizaciones ha detectado una o varias restricciones de dirección IP en el sitio web de IIS que hospeda los directorios virtuales del servidor de informes o del Administrador de informes. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no proporciona compatibilidad nativa con las restricciones de dirección IP.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Nativo.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 La instalación no puede definir las restricciones de dirección IP en URL creadas para un servidor de informes actualizado. La actualización puede continuar, pero las restricciones de dirección IP no se definirán en las URL de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="corrective-action"></a>Acción correctora  
 Tras la actualización, utilice ISA Server, su software de firewall u otra solución para permitir o denegar las solicitudes realizadas desde direcciones IP específicas al servidor de informes.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de Reporting Services &#40;Asesor de actualizaciones&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
