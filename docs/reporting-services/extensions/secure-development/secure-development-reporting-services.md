---
title: Desarrollo seguro (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: extensions
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- development security [Reporting Services]
- security [Reporting Services], development
- security [Reporting Services], strategies
ms.assetid: 12161a6c-b93b-4312-9d27-0c922561eb9b
caps.latest.revision: 15
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 00bd472c52b756f3b54271a0046e0eb19b400c51
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="secure-development-reporting-services"></a>Desarrollo seguro (Reporting Services)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] proporciona un sistema de seguridad sólido que puede ejecutar código en contextos de seguridad rigurosamente restringidos y definidos por el administrador. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] utiliza el sistema de seguridad [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], conocido como seguridad de acceso del código (o seguridad basada en evidencia). En seguridad de acceso del código, el usuario puede ser de confianza para tener acceso a un recurso, pero si el código que ejecuta no lo es, el acceso al recurso será denegado.  
  
 La seguridad basada en código, a diferencia de usuarios específicos, permite expresar la seguridad para ensamblados personalizados o datos, entrega, representación y extensiones de seguridad que desarrolla para [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. El código de extensión puede ejecutarlo cualquier cantidad de usuarios de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], todos los cuales son desconocidos durante proceso de desarrollo. Los ensamblados personalizados o extensiones que desarrolla requieren directivas de seguridad específicas en [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Estas directivas de seguridad se representan como tipos en [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]. Para obtener más información acerca de seguridad de acceso del código, consulte el tema "Seguridad de acceso del código" en la documentación de [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
## <a name="in-this-section"></a>En esta sección  
 [Seguridad de acceso del código en Reporting Services](../../../reporting-services/extensions/secure-development/code-access-security-in-reporting-services.md)  
 Introduce seguridad de acceso del código y configuración de directiva para los ensamblados personalizados y extensiones de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 [Descripción de las directivas de seguridad](../../../reporting-services/extensions/secure-development/understanding-security-policies.md)  
 Describe los varios tipos de ensamblado de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] y cómo la seguridad de acceso del código afecta a los permisos de código.  
  
 [Uso de los archivos de directivas de seguridad de Reporting Services](../../../reporting-services/extensions/secure-development/using-reporting-services-security-policy-files.md)  
 Describe los diferentes componentes [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] y los archivos de configuración de directiva correspondientes.  
  
  
