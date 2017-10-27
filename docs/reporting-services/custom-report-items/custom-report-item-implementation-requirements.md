---
title: "Requisitos de implementación de elemento de informe personalizado | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom report items
ms.assetid: cfacd816-00d6-4a3d-be72-1bba6f7f6886
caps.latest.revision: 22
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 43770b0b167e2a40874d1b8f31b3b146e62ec2b5
ms.contentlocale: es-es
ms.lasthandoff: 08/12/2017

---
# <a name="custom-report-item-implementation-requirements"></a>Requisitos de implementación de elementos de informe personalizados
  En este tema se explican los requisitos previos para desarrollar e implementar elementos de informe personalizados.  
  
## <a name="development-and-deployment-requirements"></a>Requisitos de implementación y desarrollo  
 Desarrollar un elemento de informe personalizado para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] requiere lo siguiente:  
  
-   Acceso administrativo a un servidor que ejecuta [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
-   [!INCLUDE[vsprvsext](../../includes/vsprvsext-md.md)]o posterior con el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] kit de desarrollo de software (SDK) instalado.  
  
-   Acceso a la documentación de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
-   Conocimientos sobre la creación de componentes y los espacios de nombres del modelo de componentes de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Para obtener más información, vea los temas sobre la creación de componentes y los espacios de nombres del modelo de componentes en Visual Studio en msdn.microsoft.com.  
  
## <a name="language-and-namespace-requirements"></a>Requisitos del espacio de nombres y lenguaje  
 Los elementos de informe personalizados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admiten totalmente [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Puede desarrollar elementos de informe personalizados utilizando su elección de lenguajes compatibles con .NET.  
  
 [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ofrece al desarrollador de software muchas herramientas y características para simplificar y acelerar los ciclos reiterativos de codificación, depuración y prueba, además de facilitar la implementación. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK incluye los compiladores de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] y C#, y herramientas relacionadas.  
  
-   Uso de elementos de informe personalizados el **Microsoft.ReportDesigner** y <xref:Microsoft.ReportingServices.Interfaces> los espacios de nombres. Están almacenados en los ensamblados Microsoft.ReportingServices.Interfaces.DLL y Microsoft.ReportingServices.Designer.DLL, que se instalan como parte de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   Los componentes de tiempo de diseño de elementos de informe personalizados necesitan implementar las interfaces del espacio de nombres <xref:System.ComponentModel> en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. El <xref:System.ComponentModel> se documenta en la documentación de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
> [!IMPORTANT]  
>  De forma predeterminada, [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] se instala con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a diferencia de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK. Los vínculos al contenido de SDK de esta sección solo funcionarán si el SDK está instalado en el equipo y su documentación está incluida en la colección de Libros en pantalla. Después de haber instalado la [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK, puede agregar la documentación del SDK a la colección de libros en pantalla y la tabla de contenido siguiendo las instrucciones de [agregar o quitar la documentación del producto para SQL Server](http://msdn.microsoft.com/library/ef798cc8-87cf-4d60-a7bf-9e061bdd0052).  
  
## <a name="see-also"></a>Vea también  
 [Crear un componente de tiempo de ejecución del elemento de informe personalizado](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [Crear un componente de tiempo de diseño de elemento de informe personalizado](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)   
 [Cómo: implementar un elemento de informe personalizado](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)   
 [Bibliotecas de clases de elemento de informe personalizado](../../reporting-services/custom-report-items/custom-report-item-class-libraries.md)  
  
  

