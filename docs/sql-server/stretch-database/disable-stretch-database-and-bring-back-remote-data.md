---
title: Deshabilitar Stretch Database y recuperar datos remotos | Microsoft Docs
ms.custom: 
ms.date: 08/05/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: stretch-database
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-stretch
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Stretch Database, disabling
- disabling Stretch Database
ms.assetid: c1bbb24e-47e3-46aa-b786-fcadf9fb65ce
caps.latest.revision: "33"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ff4d72b8809aaeb48429cf4641b9e7f3873dfd7c
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="disable-stretch-database-and-bring-back-remote-data"></a>Deshabilitar Stretch Database y recuperar datos remotos
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  Para deshabilitar Stretch Database para una tabla, seleccione **Stretch** para una tabla en SQL Server Management Studio. Luego seleccione una de las siguientes opciones:  
  
-   **Deshabilitar | Recuperar datos de Azure**. Copie los datos remotos de la tabla de Azure en SQL Server y luego deshabilite Stretch Database para la tabla. Esta operación conlleva gastos de transferencia de datos y no se puede cancelar.  
  
-   **Deshabilitar | Dejar datos en Azure**. Deshabilite Stretch Database para la tabla.  Abandone los datos remotos para la tabla en Azure.  
  
 También puede usar Transact-SQL para deshabilitar Stretch Database para una tabla o una base de datos.  
  
 Después de deshabilitar Stretch Database para una tabla, se detiene la migración de datos y los resultados de la consulta ya no incluyen los resultados de la tabla remota.  
  
 Si solo quiere pausar la migración de datos, vea [Pause and resume data migration &#40;Stretch Database&#41; (Pausar y reanudar la migración de datos &#40;Stretch Database&#41;)](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md).  
  
> [!NOTE]
> Al deshabilitar Stretch Database para una tabla o una base de datos no se elimina el objeto remoto. Si quiere eliminar la tabla o la base de datos remotas, tiene que quitarlas mediante el Portal de administración de Azure. Los objetos remotos siguen acumulando costos de Azure hasta que se eliminan. Para obtener más información, consulte [Precios SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
  
## <a name="disable-stretch-database-for-a-table"></a>Deshabilitar Stretch Database para una tabla  
  
### <a name="use-sql-server-management-studio-to-disable-stretch-database-for-a-table"></a>Para deshabilitar Stretch Database para una tabla, use SQL Server Management Studio.  
  
1.  En SQL Server Management Studio, en el Explorador de objetos, seleccione la tabla para la que quiere deshabilitar Stretch Database.  
  
2.  Haga clic con el botón derecho y seleccione **Stretch**y, luego, seleccione una de las siguientes opciones.  
  
    -   **Deshabilitar | Recuperar datos de Azure**. Copie los datos remotos de la tabla de Azure en SQL Server y luego deshabilite Stretch Database para la tabla. Este comando no se puede cancelar.  
  
        > [!NOTE]
        > La copia de los datos remotos para la tabla de Azure en SQL Server conlleva gastos de transferencia de datos. Para obtener más información, consulte [Detalles de precios de Transferencias de datos](https://azure.microsoft.com/pricing/details/data-transfers/).  
  
         Una vez que todos los datos remotos se han copiado desde Azure en SQL Server, se deshabilita Stretch para la tabla.  
  
    -   **Deshabilitar | Dejar datos en Azure**. Deshabilite Stretch Database para la tabla.  Abandone los datos remotos para la tabla en Azure.  
  
    > [!NOTE]
    > Al deshabilitar Stretch Database para una tabla no se eliminan los datos remotos ni la tabla remota. Si quiere eliminar la tabla remota, tiene que quitarla mediante el Portal de administración de Azure. La tabla remota sigue acumulando costos de Azure hasta que se elimina. Para obtener más información, consulte [Precios SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
  
### <a name="use-transact-sql-to-disable-stretch-database-for-a-table"></a>Usar Transact-SQL para deshabilitar Stretch Database para una tabla  
  
-   Para deshabilitar Stretch para una tabla y copiar los datos remotos de la tabla de Azure en SQL Server, ejecute el siguiente comando. Una vez que todos los datos remotos se han copiado desde Azure en SQL Server, se deshabilita Stretch para la tabla.

    Este comando no se puede cancelar.  
  
    ```sql  
    USE <Stretch-enabled database name>;
    GO
    ALTER TABLE <Stretch-enabled table name>  
       SET ( REMOTE_DATA_ARCHIVE ( MIGRATION_STATE = INBOUND ) ) ; 
    GO 
    ```  
  
    > [!NOTE]
    > La copia de los datos remotos para la tabla de Azure en SQL Server conlleva gastos de transferencia de datos. Para obtener más información, consulte [Detalles de precios de Transferencias de datos](https://azure.microsoft.com/pricing/details/data-transfers/).    
  
-   Para deshabilitar Stretch para una tabla y abandonar los datos remotos, ejecute el siguiente comando.  
  
    ```sql  
    USE <Stretch-enabled database name>;
    GO
    ALTER TABLE <Stretch-enabled table name>  
       SET ( REMOTE_DATA_ARCHIVE = OFF_WITHOUT_DATA_RECOVERY ( MIGRATION_STATE = PAUSED ) ) ; 
    GO
    ```  
  
> [!NOTE]
> Al deshabilitar Stretch Database para una tabla no se eliminan los datos remotos ni la tabla remota. Si quiere eliminar la tabla remota, tiene que quitarla mediante el Portal de administración de Azure. La tabla remota sigue acumulando costos de Azure hasta que se elimina. Para obtener más información, consulte [Precios SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
  
## <a name="disable-stretch-database-for-a-database"></a>Deshabilitar Stretch Database para una base de datos  
 Para poder deshabilitar Stretch Database para una base de datos, tiene que deshabilitar Stretch Database en las tablas individuales habilitadas para Stretch de la base de datos.  
  
### <a name="use-sql-server-management-studio-to-disable-stretch-database-for-a-database"></a>Para deshabilitar Stretch Database para una base de datos, use SQL Server Management Studio.  
  
1.  En SQL Server Management Studio, en el Explorador de objetos, seleccione la base de datos para la que quiere deshabilitar Stretch Database.  
  
2.  Haga clic con el botón derecho y seleccione **Tareas**, luego **Stretch**y, por último, **Deshabilitar**.  
  
> [!NOTE]
> Al deshabilitar Stretch Database para una base de datos no se elimina la base de datos remota. Si quiere eliminar la base de datos remota, tiene que quitarla mediante el Portal de administración de Azure. La base de datos remota sigue acumulando costos de Azure hasta que se elimina. Para obtener más información, consulte [Precios SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
  
### <a name="use-transact-sql-to-disable-stretch-database-for-a-database"></a>Usar Transact-SQL para deshabilitar Stretch Database para una base de datos  
 Ejecute el siguiente comando.  
  
```sql  
ALTER DATABASE <Stretch-enabled database name>  
    SET REMOTE_DATA_ARCHIVE = OFF ;  
GO 
```  
  
> [!NOTE]
> Al deshabilitar Stretch Database para una base de datos no se elimina la base de datos remota. Si quiere eliminar la base de datos remota, tiene que quitarla mediante el Portal de administración de Azure. La base de datos remota sigue acumulando costos de Azure hasta que se elimina. Para obtener más información, consulte [Precios SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/).  
  
## <a name="see-also"></a>Vea también  
 [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [Pause and resume data migration &#40;Stretch Database&#41; (Pausar y reanudar la migración de datos &#40;Stretch Database&#41;)](../../sql-server/stretch-database/pause-and-resume-data-migration-stretch-database.md)  
  
  
