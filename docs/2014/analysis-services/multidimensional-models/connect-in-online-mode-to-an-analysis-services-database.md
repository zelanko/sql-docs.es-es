---
title: Conectarse en modo con conexión a una base de datos de Analysis Services | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Analysis Services, connecting
ms.assetid: 33041234-7106-404f-a289-8e904f32aff2
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4233f9d50cb64bb3827e4dec49251e382ca3c4b3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36108693"
---
# <a name="connect-in-online-mode-to-an-analysis-services-database"></a>Conectar con una base de datos de Analysis Services en modo en línea
  Puede conectar directamente con una base de datos existente de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y modificar directamente los objetos que contiene. Si se conecta directamente con una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , los cambios realizados en los objetos tienen lugar inmediatamente y no se crea un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
### <a name="to-connect-directly-to-an-analysis-services-database-by-using-sql-server-data-tools"></a>Para conectarse directamente a una base de datos de Analysis Services mediante las Herramientas de datos de SQL Server  
  
1.  Abra [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  En el menú **Archivo** , seleccione **Abrir** y haga clic en **Base de datos de Analysis Services**.  
  
3.  Seleccione **Conectar con base de datos existente**.  
  
4.  Especifique el nombre del servidor y el de la base de datos.  
  
     Puede escribir el nombre de la base de datos o hacer una consulta en el servidor para ver las bases de datos que contiene.  
  
5.  Haga clic en **Aceptar**.  
  
     En ese momento, puede editar directamente los objetos de la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con Analysis Services proyectos y bases de datos durante la fase de desarrollo](work-with-analysis-services-projects-and-databases-in-development.md)   
 [Crear multidimensionales modelos mediante las herramientas de datos SQL Server &#40;SSDT&#41;](creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)  
  
  