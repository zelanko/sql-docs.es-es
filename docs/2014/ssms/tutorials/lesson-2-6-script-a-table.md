---
title: Incluir una tabla en un script | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ea88d736-849e-4368-b55d-06aeee097bf3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7808c9270e0085c2f8fafb5262d6356f8c8d1e08
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37196715"
---
# <a name="script-a-table"></a>Incluir una tabla en un script
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] puede crear scripts para seleccionar, insertar, actualizar y eliminar tablas, y para crear, modificar, quitar o ejecutar procedimientos almacenados.  
  
 En ocasiones, necesitará un script que ofrezca varias opciones como, por ejemplo, quitar un procedimiento y, a continuación, crear otro, o bien crear una tabla y modificarla posteriormente. Para crear scripts combinados, guarde el primer script en una ventana del Editor de consultas y el segundo en el Portapapeles para poder pegarlo en la ventana a continuación del primero.  
  
## <a name="creating-an-update-script"></a>Crear un script de actualización  
  
#### <a name="to-create-the-insert-script-for-a-table"></a>Para crear un script de inserción para una tabla  
  
1.  En el Explorador de objetos, expanda el servidor, **Bases de datos**, [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] y **Tablas**; haga clic con el botón derecho en **HumanResources.Employee** y, después, señale **Incluir tabla como**.  
  
2.  El menú contextual tiene siete opciones de scripting disponibles: **CREATE To**, **DROP To**, **DROP y CREATE To**, **SELECT To**, **INSERT To**, **UPDATE To**y **DELETE To**. Seleccione **UPDATE To**y haga clic en **Nueva ventana del Editor de consultas**.  
  
3.  Se abre una ventana nueva del Editor de consultas que establece una conexión y presenta la instrucción completa actualizada.  
  
     Este ejercicio muestra cómo la característica de scripting puede hacer mucho más que crear un script para una tabla o un procedimiento almacenado. Esta nueva función puede ayudarle a agregar scripts de manipulación de datos a su proyecto y a crear fácilmente script para la ejecución de procedimientos almacenados. Esto puede ahorrarle mucho tiempo en el caso de tablas y procedimientos con muchos campos.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Resumen: Escribir Transact-SQL](../../tutorials/summary-writing-transact-sql.md)  
  
  
