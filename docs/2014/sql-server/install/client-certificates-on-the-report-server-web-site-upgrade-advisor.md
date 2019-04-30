---
title: Certificados de cliente en el sitio web de servidor de informes (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: 5ecce26b-99df-4109-8e51-d150d369dff7
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 808bb63a527e8c08063d934fd6a378e1955b7617
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63205091"
---
# <a name="client-certificates-on-the-report-server-web-site-upgrade-advisor"></a>Certificados de cliente en el sitio web del servidor de informes (Asesor de actualizaciones)
  El Asesor de actualizaciones detectó uno o más certificados de cliente en el sitio web de IIS que hospeda el servidor de informes o los directorios virtuales del Administrador de informes.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no admite el uso de certificados de cliente para autenticar a los usuarios. La actualización puede continuar, pero el servidor de informes actualizado no utilizará los certificados de cliente.  
  
## <a name="corrective-action"></a>Acción correctora  
 Tendrá que utilizar una solución independiente como ISA Server para asegurarse de que se cumplen todos los requisitos de autenticación de certificados de cliente.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de Reporting Services &#40;Asesor de actualizaciones&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
