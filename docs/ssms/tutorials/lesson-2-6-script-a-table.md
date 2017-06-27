---
title: Incluir una tabla en un script | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ea88d736-849e-4368-b55d-06aeee097bf3
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 5db067d5a2fe5bbf9953484c9a999ed7b1fcddae
ms.openlocfilehash: 422a81da1656b9b5c72fdcf1e71979ff0c8c058f
ms.contentlocale: es-es
ms.lasthandoff: 06/23/2017

---
# <a name="lesson-2-6---script-a-table"></a>Lección 2.6: Incluir una tabla en un script
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] puede crear scripts para seleccionar, insertar, actualizar y eliminar tablas, y para crear, modificar, quitar o ejecutar procedimientos almacenados.  
  
En ocasiones, necesitará un script que ofrezca varias opciones como, por ejemplo, quitar un procedimiento y, a continuación, crear otro, o bien crear una tabla y modificarla posteriormente. Para crear scripts combinados, guarde el primer script en una ventana del Editor de consultas y el segundo en el Portapapeles para poder pegarlo en la ventana a continuación del primero.  
  
 
1.  En el Explorador de objetos, expanda el servidor, **Bases de datos**, [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]y **Tablas**; haga clic con el botón derecho en **HumanResources.Employee**y, después, señale **Incluir tabla como**.  
  
2.  El menú contextual tiene siete opciones de scripting disponibles: **CREATE To**, **DROP To**, **DROP y CREATE To**, **SELECT To**, **INSERT To**, **UPDATE To**y **DELETE To**. Seleccione **UPDATE To**y haga clic en **Nueva ventana del Editor de consultas**.  
  
3.  Se abre una ventana nueva del Editor de consultas que establece una conexión y presenta la instrucción completa actualizada.  
  
    Este ejercicio muestra cómo la característica de scripting puede hacer mucho más que crear un script para una tabla o un procedimiento almacenado. Esta nueva función puede ayudarle a agregar scripts de manipulación de datos a su proyecto y a crear fácilmente script para la ejecución de procedimientos almacenados. Esto puede ahorrarle mucho tiempo en el caso de tablas y procedimientos con muchos campos.  
  
 
  
  
  

