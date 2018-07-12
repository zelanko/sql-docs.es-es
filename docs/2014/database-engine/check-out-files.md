---
title: Desproteger los archivos | Microsoft Docs
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
- Visual Studio.SourceControl.CheckOutDialog
helpviewer_keywords:
- checking out files
ms.assetid: cc033727-51bb-4b58-a12b-8977ce61ff56
caps.latest.revision: 22
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 319555e7a87922b65ff4846b8b5830041893d3c8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37167176"
---
# <a name="check-out-files"></a>Desproteger archivos
  A menos que se haya configurado el entorno de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para que se permita modificar los archivos protegidos, es necesario desproteger un archivo antes de poder modificarlo. Al desproteger un archivo, una copia de la versión de ese archivo se copia en el disco local y se quita el atributo de solo lectura del mismo.  
  
 Es posible desproteger archivos en modo exclusivo o compartido. Si desprotege un archivo en modo exclusivo, ningún otro usuario podrá desprotegerlo hasta que usted lo vuelva a proteger. Si desprotege un archivo en modo compartido, otros usuarios pueden desprotegerlo y modificarlo, así que cuando vaya a protegerlo, puede que tenga que combinar la versión que ha desprotegido con las versiones creadas por los otros usuarios.  
  
 Utilice el comando **Desproteger** para desproteger proyectos y archivos controlados por código fuente. Si utiliza este comando para desproteger una solución o un proyecto, todos los archivos de la solución o el proyecto también se desprotegen. No obstante, el hecho de desproteger un archivo de código fuente individual no da lugar a la desprotección del proyecto o la solución a los que pertenece.  
  
> [!NOTE]  
>  Si el [!INCLUDE[msCoName](../includes/msconame-md.md)] base de datos de Visual SourceSafe para el proyecto está configurado para permitir varias desprotecciones y desea desproteger un archivo de modo exclusivo, debe borrar el **permitir varias desprotecciones** opción el  **Avanzadas opciones de desprotección** cuadro de diálogo antes de desproteger el archivo. Para que se aplique esta configuración, debe reiniciar [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
### <a name="to-check-out-a-file"></a>Para desproteger un archivo  
  
1.  En el Explorador de soluciones, seleccione el proyecto o el archivo.  
  
2.  En el menú **Archivo** , seleccione **Control de código fuente**y haga clic en **Desproteger para editar**.  
  
3.  Si aparece el cuadro de diálogo **Desproteger para editar** , seleccione los elementos que desee y haga clic en **Desproteger**. Si ha configurado el [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] entorno no se muestre el **desproteger** cuadro de diálogo, los elementos seleccionados en el Explorador de soluciones y los elementos secundarios que puedan tener se desprotegen inmediatamente.  
  
     **Check-out**  
     Desprotege todos los elementos seleccionados.  
  
     **Columnas**  
     Identifique las columnas que se van a mostrar y el orden en que lo hacen.  
  
     **Comentarios**  
     Especifique un comentario que se asociará a la operación de desprotección.  
  
     **No mostrar el cuadro de diálogo al desproteger elementos**  
     Suprime el cuadro de diálogo durante las operaciones de desprotección.  
  
     **Vista plana**  
     Muestra los elementos que va a desproteger como listas planas en su conexión de control de código fuente.  
  
     **Editar**  
     Modifique un elemento sin desprotegerlo. El **editar** botón solo aparece si tiene [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] configurado para admitir la edición de archivos protegidos.  
  
     **Nombre**  
     Muestra los nombres de los elementos disponibles para su desprotección. Los elementos seleccionados aparecen con casillas junto a ellos. Si no desea desproteger un elemento determinado, desactive su casilla.  
  
     **Opciones**  
     Si hace clic en la flecha situada a la derecha del botón, se mostrarán opciones de desprotección específicas del complemento de control de código fuente.  
  
     **Sort**  
     Ordena las columnas mostradas.  
  
     **Vista de árbol**  
     Muestra la jerarquía de carpetas y archivos del elemento que va a desproteger.  
  
## <a name="see-also"></a>Vea también  
 [Editar archivos protegidos](../../2014/database-engine/edit-checked-in-files.md)   
 [Desproteger automáticamente los archivos durante la modificación](../../2014/database-engine/automatically-check-out-files-upon-edit.md)   
 [Deshacer desprotecciones](../../2014/database-engine/undo-checkouts.md)   
 [Administrar desprotecciones](../../2014/database-engine/manage-checkouts.md)  
  
  
