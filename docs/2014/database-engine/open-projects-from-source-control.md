---
title: Abrir proyectos desde el Control de código fuente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], opening
- opening projects
ms.assetid: 942f93a3-e264-4ec4-ba72-a28e0509a527
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ec14f86b283fa8ccbc037feec4a8a54983126403
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62774959"
---
# <a name="open-projects-from-source-control"></a>Abrir proyectos desde el control de código fuente
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] se puede utilizar para abrir proyectos directamente desde el control de código fuente. Al hacer esto, [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] recupera la última versión del proyecto y la copia en el disco local. El entorno de [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] también crea una solución para el proyecto de forma automática.  
  
 Después de haber abierto un proyecto desde el control de código fuente, es posible desproteger y modificar los archivos de ese proyecto.  
  
> [!NOTE]  
>  El siguiente procedimiento solamente debería utilizarse una vez. Por lo tanto, debe abrir el proyecto como cualquier otro proyecto (haciendo clic en **archivo**, **abrir**y, a continuación, **proyecto**).  
  
### <a name="to-open-a-project-from-source-control"></a>Para abrir un proyecto desde el control de código fuente  
  
1.  En el **archivo** menú, elija **Control de código fuente**y haga clic en **abrir desde el Control de código fuente**.  
  
2.  Si se le pide, inicie sesión en [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual SourceSafe.  
  
3.  En el **crear un proyecto local de SourceSafe** diálogo cuadro, abra la carpeta que contiene el proyecto para abrir.  
  
4.  El **crear un nuevo proyecto en la carpeta** cuadro cambia para identificar el directorio local en el que se creará el proyecto. Si desea colocar el proyecto en un directorio diferente, escriba la ruta de acceso al directorio o use el **examinar** para buscar el directorio en el disco local.  
  
5.  En el **crear un nuevo proyecto en el cuadro carpeta**, compruebe que se muestra la carpeta correcta y, a continuación, haga clic en **Aceptar**.  
  
6.  En el **Abrir solución** cuadro de diálogo, seleccione el proyecto que desea abrir y haga clic en **abrir**.  
  
## <a name="see-also"></a>Vea también  
 [Abrir soluciones y proyectos de Control de código fuente](../../2014/database-engine/open-solutions-and-projects-from-source-control.md)   
 [Abrir soluciones desde el control de código fuente](../../2014/database-engine/open-solutions-from-source-control.md)  
  
  
