---
title: Ver el XML para una Analysis Services (SSDT) del proyecto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- projects [Analysis Services], viewing XML
ms.assetid: dd1a4bc6-57b5-47df-8619-09f921aa6351
caps.latest.revision: 12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: df5f976c08f6c16b73628ce96b459f6fd8b0fc5b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37187232"
---
# <a name="view-the-xml-for-an-analysis-services-project-ssdt"></a>Ver el XML de un proyecto de Analysis Services (SSDT)
  Al trabajar con una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el modo de proyecto, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] crea una definición XML para cada objeto de la carpeta del proyecto. Puede ver el contenido del archivo XML de cada objeto en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. También puede editar el archivo XML directamente, aunque en la mayoría de los casos no es aconsejable hacerlo porque podría realizar cambios que eviten que [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]lea el archivo XML.  
  
> [!NOTE]  
>  El código XML de todo un proyecto no se puede ver, sino que hay que ver el código de cada objeto, ya que hay un archivo independiente por objeto. La única manera de ver el código de todo un proyecto consiste en compilar el proyecto y ver el ASSL de código en el \<nombre del proyecto >. asdatabase.  
  
### <a name="to-view-the-xml-code-for-an-object"></a>Para ver el código XML de un objeto  
  
1.  Abra el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Haga clic con el botón derecho en el objeto en el Explorador de soluciones y, después, haga clic en **Ver código**.  
  
     El código XML del objeto se muestra en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Compilar proyectos de Analysis Services &#40;SSDT&#41;](build-analysis-services-projects-ssdt.md)  
  
  
