---
title: Certificados de cliente en el sitio web del servidor de informes (Asesor de actualizaciones) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: 5ecce26b-99df-4109-8e51-d150d369dff7
caps.latest.revision: 12
author: markingmyname
ms.author: maghan
manager: jhubbard
ms.openlocfilehash: 4d08cf58e6908aa8aba187e1e192a05b85b95c96
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106684"
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
  
  