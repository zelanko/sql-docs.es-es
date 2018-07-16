---
title: Desarrollo seguro (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- development security [Reporting Services]
- security [Reporting Services], development
- security [Reporting Services], strategies
ms.assetid: 12161a6c-b93b-4312-9d27-0c922561eb9b
caps.latest.revision: 14
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 9ac01a3fd70fcbebf8a51075de580a81ad1e9d2b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37313335"
---
# <a name="secure-development-reporting-services"></a>Desarrollo seguro (Reporting Services)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] proporciona un sistema de seguridad sólido que puede ejecutar código en contextos de seguridad rigurosamente restringidos y definidos por el administrador. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] utiliza el sistema de seguridad [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], conocido como seguridad de acceso del código (o seguridad basada en evidencia). En seguridad de acceso del código, el usuario puede ser de confianza para tener acceso a un recurso, pero si el código que ejecuta no lo es, el acceso al recurso será denegado.  
  
 La seguridad basada en código, a diferencia de usuarios específicos, permite expresar la seguridad para ensamblados personalizados o datos, entrega, representación y extensiones de seguridad que desarrolla para [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. El código de extensión puede ejecutarlo cualquier cantidad de usuarios de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], todos los cuales son desconocidos durante proceso de desarrollo. Los ensamblados personalizados o extensiones que desarrolla requieren directivas de seguridad específicas en [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Estas directivas de seguridad se representan como tipos en [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Para obtener más información acerca de seguridad de acceso del código, consulte el tema "Seguridad de acceso del código" en la documentación de [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
## <a name="in-this-section"></a>En esta sección  
 [Seguridad de acceso del código en Reporting Services](code-access-security-in-reporting-services.md)  
 Introduce seguridad de acceso del código y configuración de directiva para los ensamblados personalizados y extensiones de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 [Descripción de las directivas de seguridad](understanding-security-policies.md)  
 Describe los varios tipos de ensamblado de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] y cómo la seguridad de acceso del código afecta a los permisos de código.  
  
 [Uso de los archivos de directivas de seguridad de Reporting Services](using-reporting-services-security-policy-files.md)  
 Describe los diferentes componentes [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] y los archivos de configuración de directiva correspondientes.  
  
  
