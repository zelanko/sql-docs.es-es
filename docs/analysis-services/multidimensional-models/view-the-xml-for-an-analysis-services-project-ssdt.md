---
title: "Ver el código XML para un análisis de servicios de proyecto (SSDT) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: projects [Analysis Services], viewing XML
ms.assetid: dd1a4bc6-57b5-47df-8619-09f921aa6351
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 98c7d19f1b6ff424480d9e15b643b21a7dfcadcb
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="view-the-xml-for-an-analysis-services-project-ssdt"></a>Ver el XML de un proyecto de Analysis Services (SSDT)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Cuando se trabaja con un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos en modo de proyecto, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] crea una definición XML para cada objeto de la carpeta del proyecto. Puede ver el contenido del archivo XML de cada objeto en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. También puede editar el archivo XML directamente, aunque en la mayoría de los casos no es aconsejable hacerlo porque podría realizar cambios que eviten que [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]lea el archivo XML.  
  
> [!NOTE]  
>  El código XML de todo un proyecto no se puede ver, sino que hay que ver el código de cada objeto, ya que hay un archivo independiente por objeto. La única manera de ver el código para todo un proyecto consiste en generar el proyecto y ver el ASSL de código en el \<nombre del proyecto >. asdatabase.  
  
### <a name="to-view-the-xml-code-for-an-object"></a>Para ver el código XML de un objeto  
  
1.  Abra el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Haga clic con el botón derecho en el objeto en el Explorador de soluciones y, después, haga clic en **Ver código**.  
  
     El código XML del objeto se muestra en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Generar proyectos de Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)  
  
  
