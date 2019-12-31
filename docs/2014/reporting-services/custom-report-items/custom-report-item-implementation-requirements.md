---
title: Requisitos de implementación de elementos de informe personalizados | Microsoft Docs
ms.custom: ''
ms.date: 11/25/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- custom report items
ms.assetid: cfacd816-00d6-4a3d-be72-1bba6f7f6886
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0000e0c7a5933003544de22b60a8adc4d9c59c82
ms.sourcegitcommit: 7183735e38dd94aa3b9bab2b73ccab54c916ff86
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/02/2019
ms.locfileid: "74684445"
---
# <a name="custom-report-item-implementation-requirements"></a>Requisitos de implementación de elementos de informe personalizados
  En este tema se explican los requisitos previos para desarrollar e implementar elementos de informe personalizados.  
  
## <a name="development-and-deployment-requirements"></a>Requisitos de implementación y desarrollo  
 El desarrollo de un elemento de informe personalizado para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] exige lo siguiente:  
  
-   Acceso administrativo a un servidor que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecuta [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] con [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]y.  
  
-   [!INCLUDE[vsprvsext](../../includes/vsprvsext-md.md)]o superior con el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] kit de desarrollo de software (SDK) de instalado.  
  
-   Acceso a la documentación de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
-   Conocimientos sobre la creación de componentes y los espacios de nombres del modelo de componentes de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Para obtener más información, vea los temas sobre la creación de componentes y los espacios de nombres del modelo de componentes en Visual Studio en msdn.microsoft.com.  
  
## <a name="language-and-namespace-requirements"></a>Requisitos del espacio de nombres y lenguaje  
 Los elementos de informe personalizados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admiten totalmente [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Puede desarrollar elementos de informe personalizados utilizando su elección de lenguajes compatibles con .NET.  
  
 
  [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ofrece al desarrollador de software muchas herramientas y características para simplificar y acelerar los ciclos reiterativos de codificación, depuración y prueba, además de facilitar la implementación. 
  [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK incluye los compiladores de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] y C#, y herramientas relacionadas.  
  
-   Los elementos de informe personalizados utilizan los espacios de nombres `Microsoft.ReportDesigner` y <xref:Microsoft.ReportingServices.Interfaces>. Están almacenados en los ensamblados Microsoft.ReportingServices.Interfaces.DLL y Microsoft.ReportingServices.Designer.DLL, que se instalan como parte de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   Los componentes de tiempo de diseño de elementos de informe personalizados necesitan implementar las interfaces del espacio de nombres <xref:System.ComponentModel> en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. El <xref:System.ComponentModel> se documenta en la documentación de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
> [!IMPORTANT]  
>  De forma predeterminada, [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] se instala con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a diferencia de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK. Los vínculos al contenido de SDK de esta sección solo funcionarán si el SDK está instalado en el equipo y su documentación está incluida en la colección de Libros en pantalla. Después de instalar el SDK de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], puede agregar la documentación del SDK a la colección y la tabla de contenido de Libros en pantalla si sigue las instrucciones de [Agregar o quitar la documentación del producto para SQL Server](../../2014-toc/index.yml).  
  
## <a name="see-also"></a>Véase también  
 [Crear un componente de tiempo de ejecución de elemento de informe personalizado](creating-a-custom-report-item-run-time-component.md)   
 [Crear un componente de tiempo de diseño de elemento de informe personalizado](creating-a-custom-report-item-design-time-component.md)   
 [Cómo: implementar un elemento de informe personalizado](how-to-deploy-a-custom-report-item.md)   
 [Bibliotecas de clases de elementos de informe personalizadas](custom-report-item-class-libraries.md)  
  
  
