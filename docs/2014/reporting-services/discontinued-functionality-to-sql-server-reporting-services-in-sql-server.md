---
title: Funcionalidad no incluida
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.prod: reporting-services-2014, sql-server-2014
ms.reviewer: ''
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 3a5472859c582e026fc0c5aafac21abccdc93044
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63165347"
---
# <a name="discontinued-functionality-in-sql-server-reporting-services-ssrs"></a>Funcionalidad no incluida en SQL Server Reporting Services (SSRS)

  Este tema describe las características de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] que ya no están disponibles en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. No se avisa de la compatibilidad que ya no se incluye con versiones concretas del sistema operativo o de [!INCLUDE[msCoName](../includes/msconame-md.md)] Internet Information Services (IIS). Para obtener más información sobre los requisitos previos del sistema, consulte [requisitos de Hardware y Software para instalar SQL Server 2014](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
 En este tema:  
  
- [Funcionalidad no incluida SQL Server 2014 Reporting Services](#bkmk_sql14)  
  
- [Funcionalidad no incluida SQL Server 2012 Reporting Services](#bkmk_rc0)  
  
- [Funcionalidad no incluida SQL Server 2008 R2 Reporting Services](#bkmk_kj)  
  
##  <a name="bkmk_sql14"></a> [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Funcionalidad de Reporting Services no incluida

 Ninguna característica de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ha dejado de incluirse en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
##  <a name="bkmk_rc0"></a> [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Funcionalidad de Reporting Services no incluida

 En esta sección se describen las funciones de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no incluidas en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
 Ninguna característica de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ha dejado de incluirse en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
##  <a name="bkmk_kj"></a> Funcionalidad no incluida SQL Server 2008 R2 Reporting Services

 En esta sección se describen los elementos que han dejado de incluirse en [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
> [!NOTE]  
> Dado que SQL Server 2008 R2 es una actualización de versión menor de SQL Server 2008, recomendamos también revisar el contenido en la sección de SQL Server 2008.
  
### <a name="64-bit-platform-support"></a>Compatibilidad con plataformas de 64 bits

 A partir de [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)], el componente de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ya no admite servidores basados en Itanium que ejecuten Windows Server 2003 o Windows Server 2003 R2. [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sigue admitiendo otros sistemas operativos de 64 bits, incluido Windows Server 2008 para sistemas basados en Itanium y Windows Server 2008 R2 para sistemas basados en Itanium. Para actualizar a [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] desde una instalación de [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] con [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en una edición del sistema basada en Itanium de Windows Server 2003 o Windows Server 2003 R2, primero debe actualizar el sistema operativo.  
  
### <a name="data-source-credentials-in-url-access"></a>Credenciales del origen de datos en el acceso con dirección URL

 Las cadenas del parámetro de acceso con dirección URL *dsu:datasourcename=value* y *dsp:datasourcename=value* ahora no se usan. En las versiones anteriores, estas cadenas de parámetros se almacenaban en texto sin formato en la memoria caché del explorador, que no es segura.  
  
## <a name="next-steps"></a>Pasos siguientes

 - [¿Qué novedades &#40;Reporting Services&#41;](what-s-new-reporting-services.md)
 - [Cambios de comportamiento de SQL Server Reporting Services en SQL Server 2014](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)
 - [Características desusadas de SQL Server Reporting Services en SQL Server 2014](deprecated-features-in-sql-server-reporting-services-ssrs.md)