---
title: Archivos que administran soluciones y proyectos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], files
- .ssmssln files
- .ssmsmobileproj files
- .ssmsasproj files
- .ssmssqlproj files
- .sqlsuo files
- files [SQL Server Management Studio], projects
ms.assetid: e19d2859-0b97-4727-ac27-c4c226d86b2f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6e8481c1cce3e43287c04678ddae10ac1b0703af
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63044397"
---
# <a name="files-that-manage-solutions-and-projects"></a>Archivos que administran soluciones y proyectos
  En este tema se describen los tipos de archivo que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]son específicos de. De forma predeterminada, todas las soluciones y sus proyectos se crean en \Mis documentos\SQL Server Management Studio Projects.  
  
## <a name="management-studio-solution-files"></a>Archivos de solución de Management Studio  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]usa tipos de archivo diferentes [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] a [!INCLUDE[msCoName](../../includes/msconame-md.md)] los de o Visual Studio. Esto significa que no es posible abrir una solución de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o en Visual Studio. 
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] los archivos de solución permiten que el Explorador de soluciones muestre una interfaz gráfica para administrar los archivos.  
  
|Extensión|Tipo de archivo|Descripción|Creado por|  
|---------------|---------------|-----------------|----------------|  
|.ssmssln|
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Objeto de solución|Proporciona al entorno referencias a la ubicación en el disco de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los proyectos, los elementos de proyecto y la solución.|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
  
## <a name="management-studio-project-files"></a>Archivos de proyecto de Management Studio  
 Del mismo modo que las soluciones contienen archivos de solución que administran objetos de una solución, los proyectos contienen archivos de proyecto. El tipo de archivo de proyecto que crea [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para un proyecto depende de la plantilla utiliza para crear el proyecto. En la tabla siguiente se describe el tipo de archivo creado para cada proyecto.  
  
|Extensión|Plantilla de proyecto|  
|---------------|----------------------|  
|.ssmssqlproj|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Proyecto de scripts|  
|.ssmsasproj|
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Proyecto de scripts|  
  
## <a name="location-of-solution-level-files"></a>Ubicación de los archivos de la solución  
 De forma predeterminada, los archivos de la solución se crean en el directorio físico del primer proyecto creado con la solución. Puede especificar un directorio para la solución al crear una solución. También puede especificar el directorio al crear un proyecto nuevo.  
  
 Si tiene una estructura de directorios similar a la estructura lógica que aparece en el Explorador de soluciones, será más fácil encontrar los proyectos y los archivos de la solución y compartirlos con otros programadores de un equipo.  
  
## <a name="see-also"></a>Consulte también  
 [Administrar archivos con codificación](manage-files-with-encoding.md)   
 [Archivos varios](miscellaneous-files.md)   
 [Explorador de soluciones](solution-explorer.md)   
 [Soluciones &#40;SQL Server Management Studio&#41;](solutions-sql-server-management-studio.md)   
 [Proyectos &#40;SQL Server Management Studio&#41;](projects-sql-server-management-studio.md)   
 [Control de código fuente del Explorador de soluciones](../../database-engine/solution-explorer-source-control.md)  
  
  
