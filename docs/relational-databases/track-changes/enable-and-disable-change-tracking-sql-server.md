---
title: Habilitar y deshabilitar el seguimiento de cambios (SQL Server) | Microsoft Docs
ms.custom: 
ms.date: 08/08/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: track-changes
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- change tracking [SQL Server], disabling
- data changes [SQL Server]
- change tracking [SQL Server], enabling
- tracking data changes [SQL Server]
- change tracking [SQL Server], configuring
- data [SQL Server], changing
ms.assetid: 1c92ec7e-ae53-4498-8bfd-c66a42a24d54
caps.latest.revision: "34"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 41bac509d07c7aaeea93ab34ee19aecf653fa2e6
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="enable-and-disable-change-tracking-sql-server"></a>Habilitar y deshabilitar el seguimiento de cambios (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  En este tema se describe cómo habilitar y deshabilitar el seguimiento de cambios para una tabla y una base de datos.  
  
## <a name="enable-change-tracking-for-a-database"></a>Habilitar el seguimiento de cambios para una base de datos  
 Para poder utilizarlo, el seguimiento de cambios se debe habilitar previamente en el nivel de la base de datos. En el ejemplo siguiente se muestra cómo habilitar el seguimiento de cambios mediante [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = ON  
(CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON)  
```  
  
 También puede habilitar el seguimiento de cambios en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] mediante el cuadro de diálogo [Propiedades de la base de datos &#40;página ChangeTracking&#41;](../../relational-databases/databases/database-properties-changetracking-page.md) .  
  
 Puede especificar las opciones CHANGE_RETENTION y AUTO_CLEANUP al habilitar el seguimiento de cambios, y puede cambiar los valores en cualquier momento una vez que esté habilitado.  
  
 El valor de retención de los cambios especifica el período de tiempo para el cual se conserva la información del seguimiento de cambios. La información del seguimiento de cambios anterior a este período de tiempo se quita periódicamente. A la hora de establecer este valor, debería tener en cuenta la frecuencia con que las aplicaciones se sincronizarán con las tablas en la base de datos. El período de retención especificado debe ser como mínimo igual al período máximo de tiempo entre sincronizaciones. Si una aplicación obtiene los cambios en intervalos más prolongados, los resultados que se devuelven podrían ser incorrectos, puesto que es posible que parte de la información de los cambios se haya quitado. Para evitar obtener resultados incorrectos, una aplicación puede utilizar la función del sistema CHANGE_TRACKING_MIN_VALID_VERSION con el fin de determinar si el intervalo entre las sincronizaciones ha sido demasiado largo.  
  
 Puede usar la opción AUTO_CLEANUP para habilitar o deshabilitar la tarea de limpieza que quita la información de seguimiento de cambios antigua. Se trata de algo que puede ser útil en los casos en que haya un problema temporal que evite que las aplicaciones se sincronicen y sea necesario paralizar el proceso de eliminación de información del seguimiento de cambios anterior al período de retención hasta que se resuelva el problema.  
  
 Tenga en cuenta lo siguiente para cualquier base de datos que utilice seguimiento de cambios:  
  
-   Para utilizar el seguimiento de cambios, el nivel de compatibilidad de la base de datos debe establecerse en 90 o mayor. Si una base de datos tiene un nivel de compatibilidad menor que 90, puede configurar el seguimiento de cambios. Sin embargo, la función CHANGETABLE, que se utiliza para obtener información del seguimiento de cambios, devolverá un error.  
  
-   El uso del aislamiento de instantánea es la manera más fácil de ayudarle a asegurarse de que toda la información del seguimiento de cambios es coherente. Por esta razón, recomendamos encarecidamente activar el aislamiento de instantánea para la base de datos. Para obtener más información, vea [Trabajar con el seguimiento de cambios &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-tracking-sql-server.md).  
  
## <a name="enable-change-tracking-for-a-table"></a>Habilitar el seguimiento de cambios para una tabla  
 El seguimiento de cambios debe estar habilitado para cada tabla en la que desea realizar el seguimiento. Cuando el seguimiento de cambios se habilita, su información correspondiente se mantiene para todas las filas de la tabla a las que afecta una operación DML.  
  
 En el ejemplo siguiente se muestra cómo habilitar el seguimiento de cambios para una tabla utilizando [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
```sql  
ALTER TABLE Person.Contact  
ENABLE CHANGE_TRACKING  
WITH (TRACK_COLUMNS_UPDATED = ON)  
```  
  
 También puede habilitar el seguimiento de cambios para una tabla en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] mediante el cuadro de diálogo [Propiedades de la base de datos &#40;página ChangeTracking&#41;](../../relational-databases/databases/database-properties-changetracking-page.md) .  
  
 Cuando la opción TRACK_COLUMNS_UPDATED se activa, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] almacena información adicional sobre las columnas que se actualizaron en la tabla de seguimiento de cambios interna. El seguimiento de columnas puede permitir a una aplicación sincronizar solo las columnas que fueron actualizadas, lo cual puede mejorar la eficacia y el rendimiento. Sin embargo, dado que el mantenimiento de la información de seguimiento de las columnas agrega una sobrecarga adicional de almacenamiento, esta opción está desactivada de forma predeterminada.  
  
## <a name="disable-change-tracking-for-a-database-or-table"></a>Deshabilitar el seguimiento de cambios para una base de datos o una tabla  
 El seguimiento de cambios para todas las tablas sometidas al seguimiento de cambios debe deshabilitarse antes de poder deshabilitar el seguimiento de cambios para toda la base de datos. Para determinar qué tablas de una base de datos tienen habilitado el seguimiento de cambios, use la vista de catálogo [sys.change_tracking_tables](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables.md) .  
  
 Cuando ninguna de las tablas de una base de datos está sometida a seguimiento de cambios, es posible deshabilitar el seguimiento de cambios para la base de datos. En el ejemplo siguiente se muestra cómo deshabilitar el seguimiento de cambios para una base de datos mediante [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET CHANGE_TRACKING = OFF  
```  
  
 En el siguiente ejemplo se muestra cómo deshabilitar el seguimiento de cambios para una tabla utilizando [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
```sql  
ALTER TABLE Person.Contact  
DISABLE CHANGE_TRACKING;  
```  
  
## <a name="see-also"></a>Ver también  
 [Propiedades de la base de datos &#40;página ChangeTracking&#41;](../../relational-databases/databases/database-properties-changetracking-page.md)   
 [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.change_tracking_databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-databases.md)   
 [sys.change_tracking_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/change-tracking-catalog-views-sys-change-tracking-tables.md)   
 [Seguimiento de cambios de datos &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [Acerca del seguimiento de cambios &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md)   
 [Trabajar con datos modificados &#40;SQL Server&#41;](../../relational-databases/track-changes/work-with-change-data-sql-server.md)   
 [Administrar el seguimiento de cambios &#40;SQL Server&#41;](../../relational-databases/track-changes/manage-change-tracking-sql-server.md)  
  
  
