---
title: Proyecto de Scripts en SQL Server Management Studio de Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- scripts [Analysis Services]
- scripts [Analysis Services], projects
- projects [Analysis Services], Analysis Server Scripts project
- projects [Analysis Services], creating
- Analysis Server Scripts project
- items [Analysis Services]
ms.assetid: c4f5a06b-e2e4-4660-a3a8-6fd356742c02
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2b262fce9cf83295e8fd06a7abdce1999cc8a95d
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2018
ms.locfileid: "50147050"
---
# <a name="analysis-services-scripts-project-in-sql-server-management-studio"></a>Proyecto de scripts de Analysis Services en SQL Server Management Studio
  En [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], se puede crear un proyecto de scripts de Analysis Server en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para agrupar los scripts relacionados para fines de desarrollo, administración y control de código fuente. Si no hay una solución cargada en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], al crear un nuevo proyecto de scripts de Analysis Server se genera automáticamente una nueva solución. De lo contrario, el nuevo proyecto de scripts de Analysis Server se puede agregar a la solución existente o crear en una nueva solución.  
  
 Puede utilizar los siguientes pasos básicos para crear un proyecto de scripts de Analysis Server en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:  
  
1.  En el menú Archivo, seleccione **Nuevo**y haga clic en **Proyecto**.  
  
     Seleccione la plantilla de proyecto **Scripts de Analysis Server** y después especifique un nombre y una ubicación para el nuevo proyecto.  
  
2.  Haga clic con el botón derecho en **Conexiones** para crear una conexión en la carpeta Conexiones del proyecto de scripts de Analysis Server en el Explorador de soluciones.  
  
     Esta carpeta contiene las cadenas de conexión a las instancias de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en las que se ejecutan los scripts que contiene el proyecto de scripts de Analysis Server. Puede tener varias conexiones en un proyecto de scripts de Analysis Server y, en el momento de la ejecución, puede elegir la conexión donde se va a ejecutar un script que contiene el proyecto.  
  
3.  Haga clic con el botón derecho en **Consultas** para crear scripts MDX (Expresiones multidimensionales), DMX (Extensiones de minería de datos) y XMLA (XML for Analysis) en la carpeta Scripts del proyecto de scripts de Analysis Server en el Explorador de soluciones. Para más información, consulte [Script Administrative Tasks in Analysis Services](../script-administrative-tasks-in-analysis-services.md).  
  
4.  Haga clic con el botón derecho en el proyecto, seleccione **Agregar**y, después, seleccione **Elemento existente** para agregar archivos varios, como archivos de texto que contengan notas del proyecto, en la carpeta **Varios** del proyecto de scripts de Analysis Server en el Explorador de soluciones. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]omite estos archivos.  
  
## <a name="file-types"></a>Tipos de archivo  
 Una solución de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] puede contener varios tipos de archivos, dependiendo de qué proyectos se incluyeron en la solución y qué elementos se incluyeron en cada proyecto. Para obtener más información sobre los tipos de archivos de las soluciones de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], vea [Archivos que administran soluciones y proyectos](../../ssms/solution/files-that-manage-solutions-and-projects.md). Por lo general, los archivos de cada proyecto de una solución de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] se almacenan en la carpeta de la solución, en una carpeta independiente para cada proyecto.  
  
 La carpeta de proyecto de un proyecto de scripts de Analysis Server puede contener los tipos de archivos que aparecen en la siguiente tabla.  
  
|Tipo de archivo|Descripción|  
|---------------|-----------------|  
|Archivo de definición de proyecto de scripts de Analysis Server (.ssmsasproj)|Contiene metadatos acerca de las carpetas que aparecen en el Explorador de soluciones, así como información que indica qué carpetas deben mostrar los archivos que incluye el proyecto.<br /><br /> El archivo de definición del proyecto contiene también los metadatos para las conexiones de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contiene el proyecto, así como los metadatos que asocian las conexiones con los archivos de script que incluye el proyecto.|  
|Archivo de script DMX (.dmx)|Contiene un script DMX incluida en el proyecto.|  
|Archivo de script MDX (.mdx)|Contiene un script MDX incluido en el proyecto.|  
|Archivo de script XMLA (.xmla)|Contiene un script XMLA incluido en el proyecto.|  
  
## <a name="analysis-services-templates"></a>Plantillas de Analysis Services  
 Al agregar nuevos scripts MDX, DMX o XMLA a un proyecto de scripts de Analysis Server, tiene la opción de usar el Explorador de plantillas para buscar plantillas de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , una colección de scripts o instrucciones predefinidos que muestran cómo llevar a cabo una acción especificada. El Explorador de plantillas está disponible en el menú **Ver** y dispone de plantillas para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]y [!INCLUDE[ssEW](../../includes/ssew-md.md)]. Para más información, consulte [Use Analysis Services Templates in SQL Server Management Studio](use-analysis-services-templates-in-sql-server-management-studio.md).  
  
## <a name="see-also"></a>Vea también  
 [Crear modelos multidimensionales utilizando las herramientas de datos de SQL Server &#40;SSDT&#41;](../multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)   
 [Referencia de expresiones multidimensionales &#40;MDX&#41;](/sql/mdx/multidimensional-expressions-mdx-reference)   
 [Referencia de Extensiones de minería de datos &#40;DMX&#41;](/sql/dmx/data-mining-extensions-dmx-reference)   
 [Lenguaje de Scripting de Analysis Services &#40;ASSL&#41; referencia](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)   
 [Lenguaje de Scripting de Analysis Services &#40;ASSL&#41; referencia](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)  
  
  
