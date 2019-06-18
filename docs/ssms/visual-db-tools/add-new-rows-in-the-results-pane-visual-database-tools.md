---
title: Agregar nuevas filas en el panel Resultados (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
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
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 70faae781da3e9ab78777e0e893a379b64f89949
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65088919"
---
# <a name="add-new-rows-in-the-results-pane-visual-database-tools"></a>Agregar nuevas filas en el panel Resultados (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Puede agregar datos nuevos escribiéndolos manualmente o pegándolos desde otro programa, como el Bloc de notas o Excel. La fila que se vaya a pegar deberá tener exactamente el mismo número y tipos de columnas que la tabla en la que se pegue. Puede pegar varias filas en el panel Resultados de una vez.  
  
Para más información sobre cómo ingresar los datos, consulte [Reglas para actualizar resultados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/rules-for-updating-results-visual-database-tools.md).  
  
### <a name="to-add-a-new-data-row"></a>Para agregar una nueva fila de datos  
  
1.  Navegue a la parte inferior del panel Resultados, donde hay una fila en blanco disponible para agregar una nueva fila de datos.  
  
    Los valores iniciales de todas las columnas serán *NULL*.  
  
    > [!TIP]  
    > Para ir directamente a la primera fila vacía, utilice la barra de navegación situada en el parte inferior del panel Resultados.  
  
2.  Si pega filas desde el Portapapeles, seleccione la nueva fila haciendo clic en el botón que está situado a la izquierda de la fila.  
  
    > [!NOTE]  
    > Si una o varias de las filas que va a pegar no se pueden confirmar en la base de datos, aparecerá un mensaje en el que se indicarán las filas que no se han podido confirmar.  
  
3.  Escriba los datos de la nueva fila. Si va a pegar, elija **Pegar** en el menú **Editar** .  
  
4.  Deje esa fila para confirmarla en la base de datos.  
  
Si al guardar la fila se produce un error, el Diseñador de consultas y vistas mostrará un mensaje y, a continuación, le devolverá a la fila que estaba editando. Seguidamente, puede:  
  
-   Resolver el error realizando modificaciones adicionales en la fila.  
  
-   Cancelar la modificación presionando la tecla ESC. Si presiona ESC cuando está en una celda que ha cambiado, se cancelan los cambios de esa celda. Si presiona ESC cuando está en una celda que no ha cambiado, se cancelan los cambios de toda la celda.  
  
## <a name="see-also"></a>Consulte también  
[Trabajar con datos en el panel Resultados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-data-in-the-results-pane-visual-database-tools.md)  
[Realizar operaciones básicas con consultas (Visual Database Tools)](../../ssms/visual-db-tools/perform-basic-operations-with-queries-visual-database-tools.md)  
  
