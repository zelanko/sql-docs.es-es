---
title: Ver una lista de archivos modificados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- VisualStudio.SourceControl.CheckinWindow
helpviewer_keywords:
- listing modified files
- modified files list [SQL Server]
- checking in files
ms.assetid: 1b053719-8500-4300-a169-fffca5801dd0
caps.latest.revision: 24
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 22309ba15a3df2ed65fd27a002000e58f4beca36
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37228245"
---
# <a name="view-a-list-of-modified-files"></a>Ver una lista de archivos modificados
  Puede usar el **protecciones pendientes** ventana para mostrar en todo momento una lista de los archivos desprotegidos en la solución actual y para proteger estos archivos con un solo botón, haga clic en.  
  
### <a name="to-view-a-list-of-modified-files"></a>Para ver una lista de los archivos modificados  
  
1.  En el **vista** menú, haga clic en **protecciones pendientes**.  
  
2.  Para proteger los archivos seleccionados, haga clic en **proteger**. Como alternativa, puede acoplar el **protecciones pendientes** ventana en el lado derecho de la [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] entorno para que pueda comprobar en los archivos cuando haya terminado de trabajar.  
  
     **Check-in**  
     Protege la solución.  
  
     **Comentarios**  
     Asocia un comentario de texto simple a la protección pendiente. Con cada versión del proyecto se crea un comentario, que se almacena en la base de datos de control de código fuente.  
  
     **Opciones**  
     Especifica las acciones que debe tomar el control de código fuente al hacer clic en el **proteger** botón.  
  
    -   **Mantener todo desprotegido**  
  
         Especifica que los cambios deben escribirse en el proveedor de control de código fuente, pero los archivos deben permanecer desprotegidos.  
  
     **Sort**  
     Especifica el orden de las columnas que aparecen en la lista Elementos.  
  
     **Columnas**  
     Muestra una lista de las columnas que puede agregar a la lista Elementos de la ventana.  
  
     **Vista de árbol**  
     Muestra la carpeta y la jerarquía de archivos de la solución o del proyecto que se protege.  
  
     **Vista plana**  
     Muestra los archivos que se protegen como listas planas, bajo su conexión de control de código fuente.  
  
     **Comparar versiones**  
     Se abre Visual SourceSafe **opciones de diferencia** cuadro de diálogo, que compara un archivo seleccionado en el entorno de desarrollo para cualquier otro archivo seleccionado y se muestra las diferencias, si existe.  
  
     **Deshacer desprotección**  
     Revierte la desprotección de todos los elementos seleccionados en el **protecciones pendientes** ventana.  
  
     **Nombre**  
     Muestra una lista de elementos disponibles para la protección. Los elementos aparecen con la casilla que se encuentra junto a ellos activada. Si no desea proteger un elemento determinado, desactive la casilla adyacente.  
  
## <a name="see-also"></a>Vea también  
 [Administrar protecciones](../../2014/database-engine/manage-checkins.md)   
 [Administrar desprotecciones](../../2014/database-engine/manage-checkouts.md)  
  
  
