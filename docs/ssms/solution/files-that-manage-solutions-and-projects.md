---
title: Archivos que administran soluciones y proyectos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
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
ms.openlocfilehash: 3bff8bd75d6852cc978dc63d198479a65f4ede9d
ms.sourcegitcommit: 9f2edcdf958e6afce9a09fb2e572ae36dfe9edb0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/25/2018
ms.locfileid: "50100246"
---
# <a name="files-that-manage-solutions-and-projects"></a>Archivos que administran soluciones y proyectos
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
 En este tema se describen los tipos de archivos específicos de [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. De forma predeterminada, todas las soluciones y sus proyectos se crean en \Mis documentos\SQL Server Management Studio Projects.  


## <a name="management-studio-solution-files"></a>Archivos de solución de Management Studio  
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usa tipos de archivos distintos a los de [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] o [!INCLUDE[msCoName](../../includes/msconame_md.md)] Visual Studio. Esto significa que no es posible abrir una solución de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] o en Visual Studio. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] los archivos de solución permiten que el Explorador de soluciones muestre una interfaz gráfica para administrar los archivos.  
   
|Extensión|Tipo de archivo|Descripción|Creado por|  
|-------------|-------------|---------------|--------------|  
|.ssmssln|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] Objeto de solución|Proporciona al entorno referencias sobre la ubicación en el disco de los proyectos, los elementos de proyecto y las soluciones de [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] |[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
  
## <a name="management-studio-project-files"></a>Archivos de proyecto de Management Studio  
Del mismo modo que las soluciones contienen archivos de solución que administran objetos de una solución, los proyectos contienen archivos de proyecto. El tipo de archivo de proyecto que crea [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para un proyecto depende de la plantilla utiliza para crear el proyecto. En la tabla siguiente se describe el tipo de archivo creado para cada proyecto.  
   
|Extensión|Plantilla de proyecto|  
|-------------|--------------------|  
|.ssmssqlproj|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Proyecto de scripts|  
|.ssmsasproj|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] Proyecto de scripts|  
   
## <a name="location-of-solution-level-files"></a>Ubicación de los archivos de la solución  
De forma predeterminada, los archivos de la solución se crean en el directorio físico del primer proyecto creado con la solución. Puede especificar un directorio para la solución al crear una solución. También puede especificar el directorio al crear un proyecto nuevo.  
 
Si tiene una estructura de directorios similar a la estructura lógica que aparece en el Explorador de soluciones, será más fácil encontrar los proyectos y los archivos de la solución y compartirlos con otros programadores de un equipo.  
   
## <a name="see-also"></a>Ver también  
[Administrar archivos con codificación](../../ssms/solution/manage-files-with-encoding.md)  
[Archivos varios](../../ssms/solution/miscellaneous-files.md)  
[Explorador de soluciones](../../ssms/solution/solution-explorer.md)  
[Soluciones &#40;SQL Server Management Studio&#41;](../../ssms/solution/solutions-sql-server-management-studio.md)  
[Proyectos &#40;SQL Server Management Studio&#41;](../../ssms/solution/projects-sql-server-management-studio.md)  
[Control de código fuente del Explorador de soluciones](https://msdn.microsoft.com/library/ms173879.aspx)  
  
