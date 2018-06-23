---
title: Deshacer desprotecciones | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VisualStudio.SourcControl.UndoCheckDialog
helpviewer_keywords:
- checking out files
- checkout source controls [SQL Server]
- undoing checkouts
ms.assetid: a6596b20-3aa5-4dc4-a4c5-3649f1f5a20e
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 84fe5f531edfa8f122dea1b021aa4534b7c2a1f6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104105"
---
# <a name="undo-checkouts"></a>Deshacer desprotecciones
  El comando **Deshacer desprotección** se puede utilizar para cancelar una desprotección existente. Resulta muy útil cuando se ha modificado y guardado un archivo y, posteriormente, es necesario revertir los cambios.  
  
 Según las opciones establecidas en el cuadro de diálogo **Opciones avanzadas de Deshacer desprotección** , el entorno de Studio deja la copia de trabajo del elemento en el disco local o la reemplaza por la última versión controlada por código fuente. Si alguien ha modificado el elemento fuera del contexto del sistema de control de código fuente, puede que la versión recuperada no sea la más reciente.  
  
### <a name="to-undo-a-checkout"></a>Para deshacer una desprotección  
  
1.  En el Explorador de soluciones, seleccione el proyecto.  
  
2.  En el menú **Archivo** , seleccione **Control de código fuente**y haga clic en **Deshacer desprotección**.  
  
3.  En el cuadro de diálogo **Deshacer desprotección** , seleccione las opciones adecuadas y haga clic en el botón **Deshacer desprotección** .  
  
     **Columnas**  
     Identifique las columnas que se van a mostrar y el orden en que lo hacen.  
  
     **Vista plana**  
     Muestra los elementos como listas planas en su conexión de control de código fuente.  
  
     **Nombre**  
     Muestra los nombres de los elementos en los que se deshará la desprotección. Los elementos aparecen con las casillas que se encuentran junto a ellos activadas. Si no desea deshacer la desprotección de un elemento, desactive su casilla.  
  
     **Opciones**  
     Si hace clic en la flecha situada a la derecha del botón, se mostrarán opciones de deshacer desprotección específicas del complemento de control de código fuente.  
  
     **Sort**  
     Ordena la visualización de columnas.  
  
     **Vista de árbol**  
     Muestra la jerarquía de elementos y carpetas de los objetos en los que se anula la desprotección.  
  
     **Deshacer desprotección**  
     Anula la desprotección y descarta los cambios en el archivo desprotegido.  
  
## <a name="see-also"></a>Vea también  
 [Desproteger archivos](../../2014/database-engine/check-out-files.md)   
 [Administrar desprotecciones](../../2014/database-engine/manage-checkouts.md)  
  
  