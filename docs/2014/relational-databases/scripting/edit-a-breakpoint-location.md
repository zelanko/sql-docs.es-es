---
title: Modificar la ubicación de un punto de interrupción
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoint location
ms.assetid: 5c28e411-0377-4210-a7ce-2a5c13dcdf74
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f2b5bb55452333014aa3ccf5a797d19667dca753
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244887"
---
# <a name="edit-a-breakpoint-location"></a>Modificar la ubicación de un punto de interrupción
  La ubicación del punto de interrupción especifica la línea y el carácter en el que el punto de interrupción reside en un archivo de script de [!INCLUDE[tsql](../../includes/tsql-md.md)] . Puede modificar la ubicación del punto de interrupción para moverlo a otra ubicación en el script o a un script diferente.  
  
## <a name="editing-a-location"></a>Modificar una ubicación  
 Al modificar una ubicación de un punto de interrupción, este se pasa a la nueva ubicación y se lleva con él todas las propiedades existentes, como el número de llamadas o la condición.  
  
#### <a name="to-edit-a-breakpoint-location"></a>Para modificar la ubicación de un punto de interrupción  
  
1.  En la ventana del editor, haga clic con el botón derecho en el glifo de punto de interrupción y, después, en el menú contextual, haga clic en **Ubicación** .  
  
     O bien:  
  
     En la ventana **Puntos de interrupción** , haga clic con el botón derecho en el glifo de punto de interrupción y, después, en el menú contextual, haga clic en **Ubicación** .  
  
2.  En el cuadro de diálogo **Punto de interrupción de archivo** , modifique **Archivo** para especificar un nuevo archivo, **Línea** para especificar una nueva línea o **Carácter** para especificar una nueva ubicación dentro de la línea. Si el nuevo archivo que especifica ya está abierto en una ventana del editor de consultas, el punto de interrupción se mueve a esa ventana del editor. Si el archivo no se abre, se abre una nueva ventana del editor, el archivo se carga y el punto de interrupción se mueve a la nueva ubicación.  
  
     La opción para **Permitir que el código fuente sea diferente al de la versión original** no tiene ningún efecto al depurar [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="see-also"></a>Véase también  
 [Especificar un número de llamadas](specify-a-hit-count.md)   
 [Especificar una acción de punto de interrupción](specify-a-breakpoint-action.md)   
 [Especificar una condición de punto de interrupción](specify-a-breakpoint-condition.md)   
 [Especificar un filtro del punto de interrupción](specify-a-breakpoint-filter.md)  
