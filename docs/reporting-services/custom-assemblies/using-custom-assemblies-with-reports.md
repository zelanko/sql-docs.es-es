---
title: Usar ensamblados personalizados con informes | Documentos de Microsoft
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
- custom assemblies [Reporting Services]
- assemblies [Reporting Services], custom
- custom assemblies [Reporting Services], about custom assemblies
ms.assetid: 53d141d0-2185-466a-84dc-7b90d284da3d
caps.latest.revision: 32
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 0931134ffb0a1511a02a1919d0e68acc55d5f34b
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="using-custom-assemblies-with-reports"></a>Usar ensamblados personalizados con informes
  En [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], puede escribir código personalizado para los valores de elementos de informe, estilos y formato. Por ejemplo, puede utilizar código personalizado para dar formato a las monedas según la configuración regional, marcar ciertos valores con formato especial o aplicar otras reglas de negocios en vigor en la compañía. Una manera de incluir este código en los informes consiste en crear un ensamblado de código personalizado usando el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que puede hacer referencia desde dentro de los archivos de definición de informe. El servidor llama a las funciones de los ensamblados personalizados cuando se ejecuta un informe. Los ensamblados personalizados se pueden utilizar para recuperar funciones especializadas que piensa utilizar en los informes.  
  
## <a name="in-this-section"></a>En esta sección  
 [Hacer referencia a ensamblados en un archivo RDL](../../reporting-services/custom-assemblies/referencing-assemblies-in-an-rdl-file.md)  
 Describe cómo hacer referencia a ensamblados personalizados en un archivo de lenguaje RDL (Report Definition Language).  
  
 [Implementar un ensamblado personalizado](../../reporting-services/custom-assemblies/deploying-a-custom-assembly.md)  
 Describe cómo implementar un ensamblado personalizado en el Diseñador de informes y el servidor de informes.  
  
 [Usar ensamblados personalizados con nombre seguro](../../reporting-services/custom-assemblies/using-strong-named-custom-assemblies.md)  
 Describe cómo utilizar ensamblados personalizados con nombres seguros.  
  
 [Validar los permisos en ensamblados personalizados](../../reporting-services/custom-assemblies/asserting-permissions-in-custom-assemblies.md)  
 Describe cómo implementar los ensamblados personalizados con permisos limitados  concretos, y cómo validar esos permisos en el código.  
  
 [Obtener acceso a ensamblados personalizados a través de expresiones](../../reporting-services/custom-assemblies/accessing-custom-assemblies-through-expressions.md)  
 Describe cómo llamar a los métodos de ensamblado personalizados como expresiones de informe en las definiciones de informe.  
  
 [Inicializar objetos de ensamblado personalizado](../../reporting-services/custom-assemblies/initializing-custom-assembly-objects.md)  
 Describe cómo inicializar los valores para los objetos de ensamblado personalizados llamados desde un informe.  
  
 [Cómo: depurar los ensamblados personalizados](../../reporting-services/custom-assemblies/how-to-debug-custom-assemblies.md)  
 Describe cómo depurar el código de ensamblado personalizado.  
  
## <a name="see-also"></a>Vea también  
 [Lenguaje de definición de informe &#40; SSRS &#41;](../../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
