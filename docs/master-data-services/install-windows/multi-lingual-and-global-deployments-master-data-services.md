---
title: Implementaciones multilingües y globales
description: Master Data Services admite la implementación de componentes y herramientas en todos los idiomas admitidos por SQL Server.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: c3d485f8-867c-4aa2-a90d-f38fda192534
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 02cd12f7216e3f73c31be931ab23d47450bcdaaa
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85883851"
---
# <a name="multi-lingual-and-global-deployments-master-data-services"></a>Implementaciones plurilingües y globales (Master Data Services)

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] admite la implementación de componentes y herramientas en todos los idiomas que admite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información, consulte [Local Language Versions in SQL Server](../../sql-server/install/local-language-versions-in-sql-server.md).  
  
## <a name="how-languages-are-used"></a>Cómo se utilizan los idiomas  
 En la siguiente tabla se describe la compatibilidad de idioma para los componentes y herramientas de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .  
  
|Componente o herramienta|Descripción|  
|-----------------------|-----------------|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] ssNoVersion|Seleccione el programa de instalación en inglés si quiere que la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] esté disponible y sea compatible con idiomas distintos al del programa de instalación. Para obtener más información, vea la descripción de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] a continuación.|  
|[!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]|El idioma del programa de instalación determina el idioma de [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] . Por ejemplo, si elige alemán para el idioma del programa de instalación, [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] estará disponible en alemán en ese equipo.|  
|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]|Al ejecutar el programa de instalación en inglés, la aplicación web de [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] está disponible y se admite en todos los idiomas de la aplicación. [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] se puede mostrar en cualquiera de esos idiomas de la aplicación y acepta entradas específicas de la configuración regional según las preferencias de idioma del explorador web del cliente. Si las preferencias de idioma se configuran para un idioma de aplicación no compatible, [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] establecerá como valor predeterminado el idioma inglés.<br /><br /> Al ejecutar el programa de instalación en un idioma que no sea el inglés, se incluyen recursos para los otros idiomas de la aplicación [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] , pero no constituirá un escenario admitido para que los clientes utilicen en un idioma distinto al seleccionado en el programa de instalación. Si intenta obtener acceso a [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] en un idioma diferente al idioma del programa de instalación, podría experimentar problemas con la visualización de la información y entradas en la aplicación.|  
|Base de datos de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|La información en la base de datos [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] no es específica de ninguna configuración regional. Esto habilita a [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] para determinar cómo mostrar información, como por ejemplo fechas y números, en el formato determinado por las preferencias de idioma del explorador web del cliente.|  
  
## <a name="see-also"></a>Consulte también  
 [Instalar Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
