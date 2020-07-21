---
title: Conectar en modo en línea a una base de datos de Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services, connecting
ms.assetid: 33041234-7106-404f-a289-8e904f32aff2
author: minewiskan
ms.author: owend
ms.openlocfilehash: 520bf86abe448b444c653f61849640f0b1a7789f
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84536987"
---
# <a name="connect-in-online-mode-to-an-analysis-services-database"></a>Conectar con una base de datos de Analysis Services en modo en línea
  Puede conectarse directamente a una base de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] datos existente y modificar directamente los objetos de esa base de datos. Si se conecta directamente con una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , los cambios realizados en los objetos tienen lugar inmediatamente y no se crea un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
### <a name="to-connect-directly-to-an-analysis-services-database-by-using-sql-server-data-tools"></a>Para conectarse directamente a una base de datos de Analysis Services mediante las Herramientas de datos de SQL Server  
  
1.  Abra [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  En el menú **Archivo** , seleccione **Abrir** y haga clic en **Base de datos de Analysis Services**.  
  
3.  Seleccione **Conectar con base de datos existente**.  
  
4.  Especifique el nombre del servidor y el de la base de datos.  
  
     Puede escribir el nombre de la base de datos o hacer una consulta en el servidor para ver las bases de datos que contiene.  
  
5.  Haga clic en **OK**.  
  
     En ese momento, puede editar directamente los objetos de la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte también  
 [Trabajar con Analysis Services proyectos y bases de datos durante la fase de desarrollo](work-with-analysis-services-projects-and-databases-in-development.md)   
 [Crear modelos multidimensionales utilizando las herramientas de datos de SQL Server &#40;SSDT&#41;](creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)  
  
  
