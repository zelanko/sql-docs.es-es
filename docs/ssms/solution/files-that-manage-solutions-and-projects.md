---
title: Archivos que administran soluciones y proyectos | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- projects [SQL Server Management Studio], files
- .ssmssln files
- .ssmsmobileproj files
- .ssmsasproj files
- .ssmssqlproj files
- .sqlsuo files
- files [SQL Server Management Studio], projects
ms.assetid: e19d2859-0b97-4727-ac27-c4c226d86b2f
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ae75460f02779117b9c6061ab676795796215c09
ms.lasthandoff: 04/11/2017

---
# <a name="files-that-manage-solutions-and-projects"></a>Archivos que administran soluciones y proyectos
En este tema se describen los tipos de archivos específicos de [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]. De forma predeterminada, todas las soluciones y sus proyectos se crean en \Mis documentos\SQL Server Management Studio Projects.  
  
## <a name="management-studio-solution-files"></a>Archivos de solución de Management Studio  
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] usa tipos de archivos distintos a los de [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] o [!INCLUDE[msCoName](../../includes/msconame_md.md)] Visual Studio. Esto significa que no es posible abrir una solución de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] o en Visual Studio. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] los archivos de solución permiten que el Explorador de soluciones muestre una interfaz gráfica para administrar los archivos.  
  
|Extensión|Tipo de archivo|Description|Creado por|  
|-------------|-------------|---------------|--------------|  
|.ssmssln|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] Objeto de solución|Proporciona al entorno referencias sobre la ubicación en el disco de los proyectos, los elementos de proyecto y las soluciones de [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] |[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)]|  
  
## <a name="management-studio-project-files"></a>Archivos de proyecto de Management Studio  
Del mismo modo que las soluciones contienen archivos de solución que administran objetos de una solución, los proyectos contienen archivos de proyecto. El tipo de archivo de proyecto que crea [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] para un proyecto depende de la plantilla utiliza para crear el proyecto. En la tabla siguiente se describe el tipo de archivo creado para cada proyecto.  
  
|Extensión|Plantilla de proyecto|  
|-------------|--------------------|  
|.ssmssqlproj|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Proyecto de scripts|  
|.ssmsasproj|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] Proyecto de scripts|  
  
## <a name="location-of-solution-level-files"></a>Ubicación de los archivos de la solución  
De forma predeterminada, los archivos de la solución se crean en el directorio físico del primer proyecto creado con la solución. Puede especificar un directorio para la solución al crear una solución. También puede especificar el directorio al crear un proyecto nuevo.  
  
Si tiene una estructura de directorios similar a la estructura lógica que aparece en el Explorador de soluciones, será más fácil encontrar los proyectos y los archivos de la solución y compartirlos con otros programadores de un equipo.  
  
## <a name="see-also"></a>Vea también  
[Administrar archivos con codificación](../../ssms/solution/manage-files-with-encoding.md)  
[Archivos varios](../../ssms/solution/miscellaneous-files.md)  
[Explorador de soluciones](../../ssms/solution/solution-explorer.md)  
[Soluciones &amp;#40;SQL Server Management Studio&amp;#41;](../../ssms/solution/solutions-sql-server-management-studio.md)  
[Proyectos &amp;#40;SQL Server Management Studio&amp;#41;](../../ssms/solution/projects-sql-server-management-studio.md)  
[Control de código fuente del Explorador de soluciones](https://msdn.microsoft.com/en-us/library/ms173879.aspx)  
  

