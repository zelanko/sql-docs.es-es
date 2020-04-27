---
title: Explorador de soluciones control de código fuente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Visual SourceSafe
- SQL Server Management Studio [SQL Server], source control services
- source-controlled files [SQL Server]
- source controls [SQL Server Management Studio], services
- version control services [SQL Server]
- file source control services [SQL Server]
- VSS [Visual SourceSafe]
ms.assetid: 6373adb8-3d81-4945-a9fc-1d0d5799d29a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 788ce615f914dcc8a2a49fba7575061fff0df870
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62843117"
---
# <a name="solution-explorer-source-control"></a>Control de código fuente del Explorador de soluciones
  [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] Explorador de soluciones puede integrarse en un sistema de control de código fuente independiente. Una vez que una solución o un proyecto se integra en un sistema de control de código fuente, se pueden controlar el acceso de archivos y las versiones de los scripts y las consultas en los proyectos.  
  
## <a name="solution-and-project-source-control"></a>Control de código fuente de soluciones y proyectos  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../includes/ssnotedepfutureavoid-md.md)]  
  
 El control de código fuente hace referencia a un sistema en el que una pieza central de software del servidor almacena y realiza un seguimiento de las versiones de los archivos, además de controlar el acceso a esos archivos. Un sistema típico de control de código fuente incluye un proveedor de control de código fuente y dos o más clientes de control de código fuente. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] se puede integrar con un servicio de control de código fuente. Esto significa que puede usar la herramienta como cliente del proveedor de control de código fuente. Es posible administrar fácilmente los proyectos individuales y de equipo sin salir del entorno. El proveedor de control de código fuente no se incluye con [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
#### <a name="to-select-a-source-control-provider"></a>Para seleccionar un proveedor de control de código fuente  
  
1.  Instale la parte de cliente del proveedor de control de código fuente.  
  
2.  En [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], en el menú **Herramientas** , haga clic en **Opciones**.  
  
3.  En el cuadro de diálogo **Opciones** , expanda **control de código fuente**y, a continuación, haga clic en la página **selección de complemento** .  
  
4.  En el cuadro **complemento de control de código fuente actual** , seleccione el complemento de control de código fuente.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Fundamentos del control de código fuente](../../2014/database-engine/source-control-basics.md)|Define la terminología básica de control de código fuente y explica los beneficios que supone para un proyecto el uso de los servicios de control de código fuente.|  
|[Agregar soluciones y proyectos al control de código fuente](../../2014/database-engine/add-solutions-and-projects-to-source-control.md)|Explica cómo utilizar el entorno de [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] para agregar soluciones y proyectos al control de código fuente.|  
|[Abrir soluciones y proyectos desde el control de código fuente](../../2014/database-engine/open-solutions-and-projects-from-source-control.md)|Explica cómo utilizar el entorno de [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] para abrir soluciones y proyectos controlados por código fuente.|  
|[Administrar desprotecciones](../../2014/database-engine/manage-checkouts.md)|Explica cómo desproteger soluciones y archivos desde el control de código fuente.|  
|[Administrar protecciones](../../2014/database-engine/manage-checkins.md)|Explica cómo proteger soluciones y archivos en el control de código fuente.|  
|[Establecer y recuperar información de versión](../../2014/database-engine/set-and-retrieve-version-information.md)|Explica cómo recuperar el historial de un proyecto o elemento, cómo recuperar una copia local de un elemento o cómo comparar dos versiones de un elemento.|  
|||  
  
## <a name="see-also"></a>Consulte también  
 [Explorador de soluciones](../ssms/solution/solution-explorer.md)   
 [Soluciones &#40;SQL Server Management Studio&#41;](../ssms/sql-server-management-studio-ssms.md)   
 [Proyectos &#40;SQL Server Management Studio&#41;](../ssms/solution/projects-sql-server-management-studio.md)   
 [Archivos que administran soluciones y proyectos](../ssms/solution/files-that-manage-solutions-and-projects.md)  
  
  
