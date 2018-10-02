---
title: Edición de una tabla existente mediante consultas | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 58f4de8e-97b4-4bcb-953f-f3d428432491
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b9687226caec47161fb42038994be279a89becc4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47659583"
---
# <a name="how-to-edit-an-existing-table-using-queries"></a>Cómo: Editar una tabla existente mediante consultas
Puede editar la definición de una tabla o sus datos escribiendo una consulta de Transact\-SQL. Para ver o escribir datos en una tabla visualmente, use el Editor de datos como se describe en [Desarrollo de bases de datos conectadas](../ssdt/connected-database-development.md).  
  
> [!WARNING]  
> Los procedimientos siguientes usan entidades creadas en procedimientos anteriores de la sección [Desarrollo de bases de datos conectadas](../ssdt/connected-database-development.md).  
  
### <a name="to-edit-the-definition-of-an-existing-table"></a>Para editar la definición de una tabla existente  
  
1.  Expanda el nodo **Tablas** de la base de datos **Trade** en el **Explorador de objetos de SQL Server** y haga clic con el botón derecho en **dbo.Suppliers**.  
  
2.  Seleccione **Diseñador de vistas** para ver el esquema de tabla en el Diseñador de tablas.  
  
3.  Active la casilla **Permitir valores NULL** para la columna **Address**. Observe que el código correspondiente del panel de scripts cambia a `NULL` inmediatamente.  
  
4.  Actualice la base de datos siguiendo los pasos del tema [Actualización de una base de datos conectada con Power Buffer](../ssdt/how-to-update-a-connected-database-with-power-buffer.md).  
  
### <a name="to-populate-data-in-new-tables-using-a-transact-sql-query"></a>Para rellenar datos de nuevas tablas usando una consulta de Transact\-SQL  
  
1.  Haga clic con el botón derecho en el nodo de la base de datos **Trade** y seleccione **Nueva consulta**.  
  
2.  En el panel de scripts, pegue el código siguiente.  
  
    ```  
    insert into dbo.Suppliers values  
    (1, 'NorthWind Traders', 'Seattle, WA'),  
    (2, 'Contoso', 'Tacoma, WA')  
    GO  
  
    insert dbo.Customer values  
    (1, 'Fourth Coffee')  
    GO  
  
    insert dbo.Products values  
    (1, 'Apples', 0, 1, 1),  
    (2, 'Instant Coffee', 1, 2, 1)  
    GO  
    ```  
  
3.  Haga clic en el botón **Ejecutar consulta** para ejecutar esta consulta. Lo siguiente en el panel **Mensaje** indica que las filas se agregaron correctamente a las tablas.  
  
**(2 filas afectadas)(1 filas afectadas)(2 filas afectadas)**  
  
4.  Reemplace el código del panel de scripts con lo siguiente y ejecute la consulta. Esto intentará agregar una nueva fila a la tabla `Products` con un `ShelfLife` de 6.  
  
    ```  
    insert dbo.Products values  
    (3, 'Potato Chips', 6, 1, 1)  
    GO  
    ```  
  
5.  El panel **Mensaje** indica que la instrucción `INSERT` entra en conflicto con la restricción CHECK existente, que limita el valor de `ShelfLife` a menos de 5. La tabla Products no se actualiza porque la instrucción no cumple una restricción existente.  
  
6.  Cambie el código a lo siguiente y ejecute de nuevo la consulta. Observe que esta vez la fila se actualiza correctamente.  
  
    ```  
    insert dbo.Products values  
    (3, 'Potato Chips', 2, 1, 1)  
    GO  
    ```  
  
## <a name="see-also"></a>Ver también  
[Administrar tablas y relaciones y corregir errores](../ssdt/manage-tables-relationships-and-fix-errors.md)  
[Usar el Editor de Transact-SQL para editar y ejecutar scripts](../ssdt/use-transact-sql-editor-to-edit-and-execute-scripts.md)  
  
