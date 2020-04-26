---
title: Ver una lista de archivos modificados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- VisualStudio.SourceControl.CheckinWindow
helpviewer_keywords:
- listing modified files
- modified files list [SQL Server]
- checking in files
ms.assetid: 1b053719-8500-4300-a169-fffca5801dd0
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c35062e6dfa339d0cd37f3905dc801f0f47becba
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/25/2020
ms.locfileid: "62773436"
---
# <a name="view-a-list-of-modified-files"></a>Ver una lista de archivos modificados
  Puede usar la ventana **protecciones pendientes** para mostrar en todo momento una lista de los archivos desprotegidos de la solución actual y para proteger estos archivos con un solo clic de botón.  
  
### <a name="to-view-a-list-of-modified-files"></a>Para ver una lista de los archivos modificados  
  
1.  En el menú **Ver** , haga clic en **protecciones pendientes**.  
  
2.  Para proteger los archivos seleccionados, haga clic en **proteger**. También puede acoplar la ventana **protecciones pendientes** en el lado derecho del [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] entorno para que pueda proteger los archivos cuando termine de trabajar.  
  
     **Proteger**  
     Protege la solución.  
  
     **Comentarios**  
     Asocia un comentario de texto simple a la protección pendiente. Con cada versión del proyecto se crea un comentario, que se almacena en la base de datos de control de código fuente.  
  
     **Opciones**  
     Especifica las acciones que debe realizar el control de código fuente al hacer clic en el botón **proteger** .  
  
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
     Abre el cuadro de diálogo **Opciones de diferencia** de Visual SourceSafe, que compara un archivo seleccionado en el proyecto del entorno de desarrollo con cualquier otro archivo seleccionado y muestra las diferencias, si existen.  
  
     **Deshacer desprotección**  
     Invierte la desprotección de todos los elementos seleccionados en la ventana **protecciones pendientes** .  
  
     **Nombre**  
     Muestra una lista de elementos disponibles para la protección. Los elementos aparecen con la casilla que se encuentra junto a ellos activada. Si no desea proteger un elemento determinado, desactive la casilla adyacente.  
  
## <a name="see-also"></a>Consulte también  
 [Administrar protecciones](../../2014/database-engine/manage-checkins.md)   
 [Administrar desprotecciones](../../2014/database-engine/manage-checkouts.md)  
  
  
