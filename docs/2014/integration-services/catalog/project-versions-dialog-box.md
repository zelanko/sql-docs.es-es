---
title: Cuadro de diálogo Versiones del proyecto | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.isprojectprop.versions.f1
ms.assetid: a48a387c-2e70-45bc-be2e-26e57a9bb2c4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8aefce0d5afe7bec37c5fe49ba63c3fec61f3747
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62771551"
---
# <a name="project-versions-dialog-box"></a>Cuadro de diálogo Versiones del proyecto
  Use el cuadro de diálogo **Versiones del proyecto** para ver las versiones de un proyecto y restaurar una versión anterior.  
  
 También puede ver las versiones anteriores en la vista [catalog.object_versions &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-object-versions-ssisdb-database) y usar el procedimiento almacenado [catalog.restore_project &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database) para restaurar versiones anteriores.  
  
 **¿Qué desea hacer?**  
  
-   [Abrir el cuadro de diálogo Versiones del proyecto](#open_dialog)  
  
-   [Restaurar una versión del proyecto](#restore)  
  
##  <a name="open-the-project-versions-dialog-box"></a><a name="open_dialog"></a> Abrir el cuadro de diálogo Versiones del proyecto  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese al servidor de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] .  
  
     Es decir, conéctese a la instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda la base de datos de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] .  
  
2.  En el Explorador de objetos, expanda el árbol para que se muestre el nodo **Catálogos de Integration Services** .  
  
3.  Expanda el nodo **Catálogos de Integration Services** para mostrar el nodo de **SSISDB** .  
  
4.  El nodo de **SSISDB** contiene una o varias carpetas y cada una de ellas contiene uno o más proyectos. Expanda la carpeta que contiene el proyecto que le interesa.  
  
5.  Haga clic con el botón derecho en el proyecto y, después, haga clic en **Versiones**.  
  
 En el cuadro de diálogo **Versiones del proyecto** , la tabla **Versiones** muestra la lista de versiones del proyecto que se han implementado en el servidor, con la fecha y hora en que se implementaron, así como la fecha y hora en que se restauraron (en su caso), la descripción de la versión y un identificador de versión. Actualmente la versión activa se indica con una marca de verificación de la columna **Actual** de la tabla.  
  
##  <a name="restore-a-project-version"></a><a name="restore"></a> Restaurar una versión del proyecto  
 Para restaurar una versión anterior de un proyecto, seleccione la versión en la tabla **Versiones** y haga clic en **Restaurar a la versión seleccionada**. El proyecto se restaura a la versión seleccionada y esa versión se indica con una marca de verificación en la columna **Actual** de la tabla **Versiones** .  
  
  
