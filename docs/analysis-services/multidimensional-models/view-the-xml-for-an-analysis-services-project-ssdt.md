---
title: Ver el código XML para un análisis de servicios de proyecto (SSDT) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b1542c33d67c95c1c7154d08dbffd550b5f8cc72
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="view-the-xml-for-an-analysis-services-project-ssdt"></a>Ver el XML de un proyecto de Analysis Services (SSDT)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Al trabajar con una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el modo de proyecto, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] crea una definición XML para cada objeto de la carpeta del proyecto. Puede ver el contenido del archivo XML de cada objeto en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. También puede editar el archivo XML directamente, aunque en la mayoría de los casos no es aconsejable hacerlo porque podría realizar cambios que eviten que [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]lea el archivo XML.  
  
> [!NOTE]  
>  El código XML de todo un proyecto no se puede ver, sino que hay que ver el código de cada objeto, ya que hay un archivo independiente por objeto. La única manera de ver el código para todo un proyecto consiste en generar el proyecto y ver el ASSL de código en el \<nombre del proyecto >. asdatabase.  
  
### <a name="to-view-the-xml-code-for-an-object"></a>Para ver el código XML de un objeto  
  
1.  Abra el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Haga clic con el botón derecho en el objeto en el Explorador de soluciones y, después, haga clic en **Ver código**.  
  
     El código XML del objeto se muestra en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Compilar proyectos de Analysis Services & #40; SSDT & #41;](../../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)  
  
  
