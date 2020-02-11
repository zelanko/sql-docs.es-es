---
title: Agregar nuevas filas en el panel Resultados (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- inserting rows
- Query Designer [SQL Server], Results pane
- Results pane
- adding rows
- row additions [SQL Server], Results pane
ms.assetid: 59891c84-3f54-4ab9-8b86-72c59627b480
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cda813db916faf4819f85d3d09213679fba2eeec
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63460003"
---
# <a name="add-new-rows-in-the-results-pane-visual-database-tools"></a>Agregar nuevas filas en el panel Resultados (Visual Database Tools)
  Puede agregar datos nuevos escribiéndolos manualmente o pegándolos desde otro programa, como el Bloc de notas o Excel. La fila que se vaya a pegar deberá tener exactamente el mismo número y tipos de columnas que la tabla en la que se pegue. Puede pegar varias filas en el panel Resultados de una vez.  
  
 Para más información sobre cómo ingresar los datos, consulte [Reglas para actualizar resultados &#40;Visual Database Tools&#41;](visual-database-tools.md).  
  
### <a name="to-add-a-new-data-row"></a>Para agregar una nueva fila de datos  
  
1.  Navegue a la parte inferior del panel Resultados, donde hay una fila en blanco disponible para agregar una nueva fila de datos.  
  
     Los valores iniciales de todas las columnas serán *NULL*.  
  
    > [!TIP]  
    >  Para ir directamente a la primera fila vacía, utilice la barra de navegación situada en el parte inferior del panel Resultados.  
  
2.  Si pega filas desde el Portapapeles, seleccione la nueva fila haciendo clic en el botón que está situado a la izquierda de la fila.  
  
    > [!NOTE]  
    >  Si una o varias de las filas que va a pegar no se pueden confirmar en la base de datos, aparecerá un mensaje en el que se indicarán las filas que no se han podido confirmar.  
  
3.  Escriba los datos de la nueva fila. Si va a pegar, elija **Pegar** en el menú **Editar** .  
  
4.  Deje esa fila para confirmarla en la base de datos.  
  
 Si al guardar la fila se produce un error, el Diseñador de consultas y vistas mostrará un mensaje y, a continuación, le devolverá a la fila que estaba editando. Seguidamente, puede:  
  
-   Resolver el error realizando modificaciones adicionales en la fila.  
  
-   Cancelar la modificación presionando la tecla ESC. Si presiona ESC cuando está en una celda que ha cambiado, se cancelan los cambios de esa celda. Si presiona ESC cuando está en una celda que no ha cambiado, se cancelan los cambios de toda la celda.  
  
## <a name="see-also"></a>Consulte también  
 [Trabajar con datos en el panel resultados &#40;Visual Database Tools&#41;](results-pane-visual-database-tools.md)   
 [Realizar operaciones básicas con consultas (Visual Database Tools)](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
