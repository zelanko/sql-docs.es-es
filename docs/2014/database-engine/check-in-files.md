---
title: Proteger archivos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- VisualStudio.SourceControl.CheckInDialog
helpviewer_keywords:
- checking in files
ms.assetid: 0657a387-8411-4406-bef9-d262a5bfa269
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 052859e4605162daa87789b5c61d2ef9d33d4177
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936046"
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
  
     **No mostrar el cuadro de diálogo Proteger al proteger elementos**  
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
  
## <a name="see-also"></a>Consulte también  
 [Ver una lista de archivos modificados](../../2014/database-engine/view-a-list-of-modified-files.md)   
 [Administrar protecciones](../../2014/database-engine/manage-checkins.md)  
  
  
