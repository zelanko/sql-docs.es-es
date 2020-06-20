---
title: Certificados de cliente en el sitio web del servidor de informes (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], upgrade issues
ms.assetid: 5ecce26b-99df-4109-8e51-d150d369dff7
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 563a64e695ef552a712a5678f56d38fdfbff619f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059363"
---
# <a name="client-certificates-on-the-report-server-web-site-upgrade-advisor"></a>Certificados de cliente en el sitio web del servidor de informes (Asesor de actualizaciones)
  El Asesor de actualizaciones detectó uno o más certificados de cliente en el sitio web de IIS que hospeda el servidor de informes o los directorios virtuales del Administrador de informes.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modo nativo.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descripción  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] admite el uso de certificados de cliente para autenticar a los usuarios. La actualización puede continuar, pero el servidor de informes actualizado no utilizará los certificados de cliente.  
  
## <a name="corrective-action"></a>Acción correctora  
 Tendrá que utilizar una solución independiente como ISA Server para asegurarse de que se cumplen todos los requisitos de autenticación de certificados de cliente.  
  
## <a name="see-also"></a>Consulte también  
 [Reporting Services problemas de actualización &#40;el asesor de actualizaciones&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
