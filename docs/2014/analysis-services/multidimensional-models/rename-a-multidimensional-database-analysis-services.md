---
title: Cambiar el nombre de una base de datos Multidimensional (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- renaming databases
ms.assetid: 15fdaec7-f3e4-44d9-9b78-1a1d78c484e0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b6b27b086e84f173e72a61cf01341d5d01ec7ea9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48168225"
---
# <a name="rename-a-multidimensional-database-analysis-services"></a>Cambie el nombre de una base de datos multidimensional (Analysis Services)
  La forma de cambiar el nombre de una base de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] depende de cómo se conecte a la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para cambiar el nombre de una base de datos existente, debe conectarse en el modo en línea. Para cambiar el nombre de la base de datos a la que se conectan los objetos de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , debe conectarse en el modo de proyecto.  
  
### <a name="to-change-the-database-name-in-online-mode"></a>Para cambiar el nombre de la base de datos en el modo en línea  
  
1.  Con [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], conéctese directamente a la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
2.  En el Explorador de soluciones, haga clic con el botón derecho en la base de datos y, después, haga clic en **Editar base de datos**.  
  
3.  En el cuadro de texto **Nombre de la base de datos** , cambie el nombre de la base de datos.  
  
4.  Haga clic en **Guardar** o en **Guardar todo** en la barra de herramientas, haga clic en **Guardar los elementos seleccionados** o en **Guardar todo** en el menú **Archivo** , o cierre el **Diseñador de bases de datos** y, a continuación, haga clic en **Guardar** cuando se le solicite.  
  
     El nombre de la base de datos se actualiza en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y el objeto de base de datos se actualiza en el Explorador de soluciones.  
  
### <a name="to-change-the-database-name-in-project-mode"></a>Para cambiar el nombre de la base de datos en el modo de proyecto  
  
1.  Abra el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
2.  En el Explorador de soluciones, haga clic con el botón derecho en el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y, después, elija **Propiedades**.  
  
3.  En el cuadro de diálogo **Páginas de propiedades** , haga clic en **Implementación** en la sección **Propiedades de configuración** .  
  
4.  Cambie la propiedad **Database** al nuevo nombre de la base de datos.  
  
     La próxima vez que se implemente el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , se hará con este nuevo nombre de base de datos. Si esta base de datos ya existe, se sobrescribirá.  
  
### <a name="to-change-the-database-name-using-sql-server-management-studio"></a>Para cambiar el nombre de la base de datos con SQL Server Management Studio.  
  
-   Haga clic con el botón derecho en la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y edite la propiedad Name.  
  
## <a name="see-also"></a>Vea también  
 [Configurar las propiedades del servidor en Analysis Services](../server-properties/server-properties-in-analysis-services.md)   
 [Establecer las propiedades de la base de datos Multidimensional &#40;Analysis Services&#41;](set-multidimensional-database-properties-analysis-services.md)   
 [Configurar las propiedades de proyecto de Analysis Services &#40;SSDT&#41;](configure-analysis-services-project-properties-ssdt.md)   
 [Implementar proyectos de Analysis Services &#40;SSDT&#41;](deploy-analysis-services-projects-ssdt.md)  
  
  
