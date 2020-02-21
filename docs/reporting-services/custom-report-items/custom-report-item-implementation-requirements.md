---
title: Requisitos de implementación de elementos de informe personalizados | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-report-items
ms.topic: reference
helpviewer_keywords:
- custom report items
ms.assetid: cfacd816-00d6-4a3d-be72-1bba6f7f6886
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e25938d690d6e1046d1d0e75ae5a4952b05d4615
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "73594518"
---
# <a name="custom-report-item-implementation-requirements"></a>Requisitos de implementación de elementos de informe personalizados
  En este tema se explican los requisitos previos para desarrollar e implementar elementos de informe personalizados.  
  
## <a name="development-and-deployment-requirements"></a>Requisitos de implementación y desarrollo  
 El desarrollo de un elemento de informe personalizado para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] exige lo siguiente:  
  
-   Acceso administrativo a un servidor que ejecuta [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
-   [!INCLUDE[vsprvsext](../../includes/vsprvsext-md.md)] o superior con el kit de desarrollo de software (SDK) de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] instalado.  
  
-   Acceso a la documentación de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
-   Conocimientos sobre la creación de componentes y los espacios de nombres del modelo de componentes de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
## <a name="language-and-namespace-requirements"></a>Requisitos del espacio de nombres y lenguaje  
 Los elementos de informe personalizados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admiten totalmente [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Puede desarrollar elementos de informe personalizados utilizando su elección de lenguajes compatibles con .NET.  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ofrece al desarrollador de software muchas herramientas y características para simplificar y acelerar los ciclos reiterativos de codificación, depuración y prueba, además de facilitar la implementación. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK incluye los compiladores de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] y C#, y herramientas relacionadas.  
  
-   Los elementos de informe personalizados usan los espacios de nombres **Microsoft.ReportDesigner** y <xref:Microsoft.ReportingServices.Interfaces>. Están almacenados en los ensamblados Microsoft.ReportingServices.Interfaces.DLL y Microsoft.ReportingServices.Designer.DLL, que se instalan como parte de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   Los componentes de tiempo de diseño de elementos de informe personalizados necesitan implementar las interfaces del espacio de nombres <xref:System.ComponentModel> en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. El <xref:System.ComponentModel> se documenta en la documentación de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  

## <a name="see-also"></a>Consulte también  
 [Creación de un componente de tiempo de ejecución de elemento de informe personalizado](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [Creación de un componente de tiempo de diseño de elemento de informe personalizado](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)   
 [Cómo: Implementación de un elemento de informe personalizado](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)   
 [Bibliotecas de clases de elemento de informe personalizado](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)  
  
  
