---
title: Cambiar el nombre de una base de datos Multidimensional (Analysis Services) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: renaming databases
ms.assetid: 15fdaec7-f3e4-44d9-9b78-1a1d78c484e0
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 98a777845371724e215ac0cf58fa5d1ec916f7c9
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
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
 [Configurar las propiedades de servidor en Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Establecer propiedades de la base de datos Multidimensional &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/set-multidimensional-database-properties-analysis-services.md)   
 [Configurar las propiedades de un proyecto de Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md)   
 [Implementar proyectos de Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
  
