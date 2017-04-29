---
title: Quitar o eliminar un elemento o un proyecto | Microsoft Docs
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
- deleting project items
- projects [SQL Server Management Studio], item removal
- removing project items
ms.assetid: 3fd92434-70f5-466e-bef0-7e0fd73ddb1c
caps.latest.revision: 3
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b09e3ba21b75c91b4ceb5deb70379d60b644e49d
ms.lasthandoff: 04/11/2017

---
# <a name="remove-or-delete-an-item-or-project"></a>Quitar o eliminar un elemento o un proyecto
Los elementos de proyecto en los proyectos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] son las consultas, las conexiones y los archivos varios. Se pueden quitar consultas y archivos varios del proyecto de una solución sin borrar los archivos almacenados. Quite un proyecto o un elemento que no sea útil para la solución actual, pero que desee incluir en otra solución.  
  
### <a name="to-remove-a-project-item"></a>Para quitar un elemento de un proyecto  
  
1.  En el Explorador de soluciones, seleccione el elemento del proyecto que desea quitar.  
  
2.  En el menú **Editar** , haga clic en **Quitar**.  
  
3.  En el cuadro de diálogo de confirmación, haga clic en **Quitar** para quitar el elemento del proyecto.  
  
Un elemento quitado aún se encuentra en el sistema de archivos. Por lo tanto, puede agregar ese elemento quitado a la solución original o a otra solución.  
  
#### <a name="to-remove-a-project"></a>Para quitar un proyecto  
  
1.  En el Explorador de soluciones, seleccione el proyecto que desea quitar.  
  
2.  En el menú **Editar** , haga clic en **Quitar**.  
  
3.  En el cuadro de diálogo de confirmación, haga clic en **Aceptar**para quitar el proyecto de la solución.  
  
Un proyecto se puede eliminar de forma permanente, pero primero es necesario quitar todas las referencias al mismo de las soluciones de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] y, a continuación, utilizar el Explorador de [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows para eliminar de forma permanente los archivos asociados almacenados.  
  
#### <a name="to-delete-a-project"></a>Para eliminar un proyecto  
  
1.  En el Explorador de soluciones, quite el proyecto que desea eliminar de la solución.  
  
2.  En el Explorador de Windows, busque y seleccione los archivos asociados al proyecto o elemento que desea eliminar.  
  
3.  En el menú **Archivo** , haga clic en **Eliminar**.  
  
## <a name="see-also"></a>Vea también  
[Explorador de soluciones](../../ssms/solution/solution-explorer.md)  
[Agregar nuevos elementos a un proyecto](../../ssms/solution/add-new-items-to-a-project.md)  
[Agregar elementos existentes a un proyecto](../../ssms/solution/add-existing-items-to-a-project.md)  
  

