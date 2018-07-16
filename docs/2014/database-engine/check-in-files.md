---
title: Proteger los archivos | Microsoft Docs
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
- VisualStudio.SourceControl.CheckInDialog
helpviewer_keywords:
- checking in files
ms.assetid: 0657a387-8411-4406-bef9-d262a5bfa269
caps.latest.revision: 22
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b657d02a06d76645fce350e1f6ba82523e69ff37
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37222655"
---
# <a name="check-in-files"></a>Proteger archivos
  Para poner los archivos controlados por código fuente a disposición de otros usuarios, es necesario proteger esos archivos en el control de código fuente. Al proteger un archivo, la versión que se protege se escribe en el proveedor de control de código fuente y se convierte en la última versión del archivo.  
  
 Para proteger los archivos se puede utilizar el comando **Proteger** . Si usa este comando para proteger una solución o un proyecto, todos los archivos de la solución o el proyecto también se protegen. No obstante, el hecho de proteger un archivo de código fuente individual no da lugar a la protección del proyecto o la solución a los que pertenece.  
  
### <a name="to-check-in-a-file"></a>Para proteger un archivo  
  
1.  En el Explorador de soluciones, haga clic con el botón secundario en el archivo que desea proteger y, a continuación, haga clic en **Proteger**.  
  
2.  Si aparece el cuadro de diálogo **Proteger** , seleccione las opciones adecuadas y, a continuación, haga clic en **Aceptar**.  
  
     **Check-in**  
     Protege todos los elementos seleccionados.  
  
     **Columnas**  
     Identifique las columnas que se van a mostrar y el orden en que lo hacen.  
  
     **Comentarios**  
     Agregue un comentario para asociarlo a la operación de protección.  
  
     **No mostrar en el cuadro de diálogo de comprobación al proteger elementos**  
     Suprime el cuadro de diálogo en las operaciones de protección.  
  
     **Vista plana**  
     Muestra los archivos que protege como listas planas en su conexión de control de código fuente.  
  
     **Nombre**  
     Muestra los nombres de los elementos que se protegen. Los elementos aparecen con las casillas que se encuentran junto a ellos activadas. Si no desea proteger un elemento determinado, desactive su casilla.  
  
     **Opciones**  
     Si hace clic en la flecha situada a la derecha del botón, se mostrarán opciones de protección específicas del complemento de control de código fuente.  
  
     **Sort**  
     Ordena la visualización de columnas.  
  
     **Vista de árbol**  
     Muestra la jerarquía de carpeta y archivo de los elementos que se protegen.  
  
 Si el archivo que ha protegido no forma parte de una desprotección compartida, el entorno de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] lo protege inmediatamente. De lo contrario, es posible que se le pida que combine su versión con las versiones creadas por otros usuarios.  
  
## <a name="see-also"></a>Vea también  
 [Ver una lista de archivos modificados](../../2014/database-engine/view-a-list-of-modified-files.md)   
 [Administrar protecciones](../../2014/database-engine/manage-checkins.md)  
  
  
