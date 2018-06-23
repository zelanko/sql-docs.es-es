---
title: Creación de un análisis de servicios de proyecto (Tutorial de minería de datos básicos) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 784c0401-0358-4117-9c85-4e8220ce71d9
caps.latest.revision: 50
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d650feead984a358d169851fba246215a58b6d34
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312533"
---
# <a name="creating-an-analysis-services-project-basic-data-mining-tutorial"></a>Crear un proyecto de Analysis Services (Tutorial básico de minería de datos)
  Cada [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] proyecto define los objetos de una sola [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] base de datos. Una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] puede contener muchos tipos diferentes de objetos  
  
-   Modelos multidimensionales (cubos)  
  
-   Estructuras de minería de datos y modelos de minería de datos  
  
-   Objetos auxiliares como orígenes de datos, vistas del origen de datos y ensamblados personalizados  
  
 Tenga en cuenta que **no** se necesita un cubo para realizar tareas de minería de datos. Si necesita realizar minería de datos en un cubo existente, debe agregar los modelos de minería de datos al mismo proyecto que utilizó para generar el cubo. Sin embargo, para la mayoría de los fines se pueden generar los modelos en orígenes de datos relacionales, como un almacenamiento de datos, y obtener mejor rendimiento si no se emplea un cubo.  
  
 En este tutorial utilizará un almacenamiento de datos relacional, [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)], como el origen de datos. Implementará todos los objetos de minería de datos en un [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] base de datos denominada `BasicDataMining`, que se usa solo para la minería de datos.  
  
 De forma predeterminada, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utiliza la **localhost** instancia para los nuevos proyectos. Si está utilizando una instancia con nombre o un servidor diferente, debe crear y abrir el proyecto primero y, a continuación, cambiar el nombre de instancia.  
  
 Para obtener más información acerca de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] proyectos, vea [crear un proyecto de Analysis Services](../analysis-services/lesson-1-1-creating-an-analysis-services-project.md).  
  
### <a name="to-create-an-analysis-services-project"></a>Para crear un proyecto de Analysis Services  
  
1.  Abra [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  En el menú **Archivo** , seleccione **Nuevo**y haga clic en **Proyecto**.  
  
3.  Compruebe que la opción **Proyectos de Business Intelligence** esté seleccionada en el panel **Tipos de proyecto** .  
  
4.  En el panel **Plantillas** , seleccione **Proyecto multidimensional y de minería de datos de Analysis Services**.  
  
5.  En el **nombre** cuadro, asigne al nuevo proyecto `BasicDataMining`.  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-change-the-instance-where-data-mining-objects-are-stored"></a>Para cambiar la instancia donde se almacenan los objetos de minería de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], en la **proyecto** menú, seleccione **propiedades**.  
  
2.  En el lado izquierdo del panel **Páginas de propiedades** , en **Propiedades de configuración**, haga clic en **Implementación**.  
  
3.  En el lado derecho del panel **Páginas de propiedades** , en **Destino**, compruebe que el nombre de **Servidor** es **localhost**. Si usa una instancia diferente, escriba el nombre de la instancia. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Crear un origen de datos &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/creating-a-data-source-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Compilar proyectos de Analysis Services &#40;SSDT&#41;](../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)   
 [Crear un proyecto de Analysis Services &#40;SSDT&#41;](../analysis-services/multidimensional-models/create-an-analysis-services-project-ssdt.md)  
  
  