---
title: Revertir una base de datos a una instantánea de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], reverting to
- reverting databases
ms.assetid: 8f74dd31-c9ca-4537-8760-0c7648f0787d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ef9bda4b8eeff394e44ba696e228b121015960b9
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52774357"
---
# <a name="revert-a-database-to-a-database-snapshot"></a>Revertir una base de datos a una instantánea de base de datos
  Si se dañan los datos de una base de datos en línea, revertir la base de datos a una instantánea de base de datos anterior puede ser, en algunos casos, ser una alternativa adecuada a restaurar la base de datos a partir de una copia de seguridad. Por ejemplo, revertir una base de datos puede resultar útil para revertir un error grave del usuario que sea reciente, por ejemplo la eliminación de una tabla. Tenga en cuenta que se pierden todos los cambios realizados después de que se creara la instantánea.  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Requisitos previos](#Prerequisites)  
  
     [Seguridad](#Security)  
  
-   **Para revertir una base de datos a una instantánea de base de datos, utilizando:**  [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
 La reversión no se admite en las siguientes condiciones:  
  
-   La base de datos debe tener en ese momento solo una instantánea de base de datos, a la que se va a revertir.  
  
-   La base de datos contiene grupos de archivos de solo lectura o comprimidos.  
  
-   Algunos archivos que están ahora sin conexión estaban en línea cuando se creó la instantánea.  
  
 Antes de revertir a una base de datos, debe tener en cuenta los siguientes limitaciones:  
  
-   La reversión no se utiliza para la recuperación de medios. . Una instantánea de base de datos es una copia incompleta de los archivos de base de datos, de modo que si se daña la base de datos o la instantánea de base de datos, es probable que no se pueda revertir a partir de una instantánea. Además, aunque sea posible, no es probable que la reversión corrija el problema si se produjesen daños. Por lo tanto, para proteger una base de datos es esencial hacer copias de seguridad con regularidad y probar el plan de restauración. Para obtener más información, consulte [Back Up and Restore of SQL Server Databases](../backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
    > [!NOTE]  
    >  Si tiene que restaurar la base de datos de origen al momento en que creó una instantánea de base de datos, use el modelo de recuperación completa e implemente una directiva de copia de seguridad que le habilite para ello.  
  
-   La base de datos revertida sobrescribe la base de datos de origen original, de modo que se pierden todos los cambios realizados en la base de datos desde que se creó la instantánea.  
  
-   La operación de reversión sobrescribe también el archivo de registro antiguo y lo vuelve a crear. Por consiguiente, la base de datos revertida no se puede poner al día en el punto de error del usuario. Por esta razón, recomendamos realizar una copia de seguridad del registro antes de revertir una base de datos.  
  
    > [!NOTE]  
    >  Aunque no puede restaurar el registro original para poner al día la base de datos, la información del archivo de registro original puede ser útil para reconstruir los datos perdidos.  
  
-   La reversión interrumpe la cadena de copias de seguridad del registro. Así pues, antes de utilizar copias de seguridad de registros de la base de datos revertida, primero deberá realizar una copia de seguridad completa de la base de datos o una copia de seguridad de los archivos. Recomendamos realizar una copia de seguridad completa de la base de datos.  
  
-   Durante una operación de reversión, tanto la instantánea como la base de datos de origen no están disponibles. La base de datos de origen y la instantánea se marcan como "En restauración". Si se produce un error durante la operación de reversión, cuando la base de datos se inicie de nuevo, la operación de reversión intentará finalizar la reversión.  
  
-   Los metadatos de una base de datos revertida son los mismos que los metadatos del momento de realizar la instantánea.  
  
-   Al revertir se quitan todos los catálogos de texto completo.  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Asegúrese de que la base de datos de origen y la instantánea de base de datos cumplen los siguientes requisitos previos:  
  
-   Compruebe que no se ha dañado la base de datos.  
  
    > [!NOTE]  
    >  Si se ha dañado la base de datos, tendrá que restaurarla a partir de copias de seguridad. Para obtener más información, vea [Restauraciones de base de datos completas &#40;modelo de recuperación simple&#41;](../backup-restore/complete-database-restores-simple-recovery-model.md) o [Restauraciones de base de datos completas &#40;modelo de recuperación completa&#41;](../backup-restore/complete-database-restores-full-recovery-model.md).  
  
-   Identifique una instantánea reciente creada antes del error. Para obtener más información, consulte [Ver una instantánea de base de datos &#40;SQL Server&#41;](view-a-database-snapshot-sql-server.md).  
  
-   Quite cualquier otra instantánea que exista actualmente en la base de datos. Para obtener más información, consulte [Eliminar una instantánea de base de datos &#40;Transact-SQL&#41;](drop-a-database-snapshot-transact-sql.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Cualquier usuario que tenga permisos de RESTORE DATABASE en la base de datos de origen puede revertirla a su estado cuando se creó una instantánea de base de datos.  
  
##  <a name="TsqlProcedure"></a> Revertir una base de datos a una instantánea de base de datos (utilizando Transact-SQL)  
 **Para revertir una base de datos a una instantánea de base de datos**  
  
> [!NOTE]  
>  Para obtener un ejemplo de este procedimiento, vea [Ejemplos (Transact-SQL)](#TsqlExample), más adelante en esta sección.  
  
1.  Identifique la instantánea de base de datos a la que desea revertir la base de datos. Puede ver las instantáneas en una base de datos en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (vea [Ver una instantánea de base de datos &#40;SQL Server&#41;](view-a-database-snapshot-sql-server.md)). Además, puede identificar la base de datos de origen de una vista a partir de la columna **source_database_id** de la vista de catálogo [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) .  
  
2.  Quita cualquier otra instantánea de base de datos.  
  
     Para obtener información sobre cómo quitar instantáneas, vea [Eliminar una instantánea de base de datos &#40;Transact-SQL&#41;](drop-a-database-snapshot-transact-sql.md). Si la base de datos utiliza el modelo de recuperación completa, antes de revertir, se debe hacer una copia de seguridad del registro. Para obtener más información, vea [Realizar copia de seguridad de un registro de transacciones &#40;SQL Server&#41;](../backup-restore/back-up-a-transaction-log-sql-server.md) o [Realizar una copia de seguridad del registro de transacciones cuando la base de datos está dañada &#40;SQL Server&#41;](../backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md).  
  
3.  Realice la operación de reversión.  
  
     Para realizar una operación de reversión es necesario disponer de permisos RESTORE DATABASE en la base de datos de origen. Para revertir la base de datos, use la siguiente instrucción Transact-SQL:  
  
     RESTORE DATABASE *nombre_base_de_datos* FROM DATABASE_SNAPSHOT **=***nombre_de_base_de_datos_de_instantánea*  
  
     Donde *nombre_base_de_datos* es la base de datos de origen y *nombre_base_de_datos_de_instantánea* equivale al nombre de la instantánea a la que quiere revertir la base de datos. Tenga en cuenta que en esta instrucción debe especificar un nombre de instantánea y no un dispositivo de copia de seguridad.  
  
     Para obtener más información, consulte [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql).  
  
    > [!NOTE]  
    >  Durante la operación de reversión, la instantánea y la base de datos de origen no están disponibles. La base de datos de origen y la instantánea están marcadas como "en restauración". Si se produce un error durante la operación de reversión, se intentará finalizar la reversión cuando se vuelva a iniciar la base de datos.  
  
4.  Si el propietario de la base de datos ha cambiado desde la creación de la instantánea, se recomienda actualizar el propietario de la base de datos revertida.  
  
    > [!NOTE]  
    >  La base de datos revertida conserva los permisos y la configuración (por ejemplo, el propietario de la base de datos y el modelo de recuperación) de la instantánea de base de datos.  
  
5.  Inicie la base de datos.  
  
6.  De manera opcional, realice una copia de seguridad de la base de datos revertida, especialmente si utiliza el modelo de recuperación completa (o por medio de registros de operaciones masivas). Para realizar una copia de seguridad de una base de datos, vea [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](../backup-restore/create-a-full-database-backup-sql-server.md).  
  
###  <a name="TsqlExample"></a> Ejemplos (Transact-SQL)  
 Esta sección contiene los siguientes ejemplos de reversión de una base de datos a una instantánea de base de datos:  
  
-   A. [Revertir una instantánea en la base de datos AdventureWorks](#Reverting_AW)  
  
-   b. [Revertir una instantánea en la base de datos Sales](#Reverting_Sales)  
  
####  <a name="Reverting_AW"></a> A. Revertir una instantánea en la base de datos AdventureWorks  
 En este ejemplo se considera que solo existe una instantánea en la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Para ver el ejemplo que crea la instantánea a la que se revierte la base de datos, vea [Crear una instantánea de base de datos &#40;Transact-SQL&#41;](create-a-database-snapshot-transact-sql.md).  
  
```  
USE master;  
-- Reverting AdventureWorks to AdventureWorks_dbss1800  
RESTORE DATABASE AdventureWorks from   
DATABASE_SNAPSHOT = 'AdventureWorks_dbss1800';  
GO  
```  
  
####  <a name="Reverting_Sales"></a> B. Revertir una instantánea en la base de datos Sales  
 En este ejemplo se considera que hay dos instantáneas en la base de datos **Sales** : **sales_snapshot0600** y **sales_snapshot1200**. En el ejemplo, se elimina la instantánea más antigua y se revierte la base de datos a la instantánea más reciente.  
  
 Para ver el código para crear la base de datos de ejemplo y las instantáneas de las que depende este ejemplo, vea:  
  
-   Para la base de datos **Sales** y la instantánea **sales_snapshot0600**, vea las secciones "Crear una base de datos con grupos de archivos" y "Crear una instantánea de base de datos" en [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql).  
  
-   Para la base de datos **sales_snapshot1200** , vea "Crear una instantánea de la base datos Sales" en [Crear una instantánea de base de datos &#40;Transact-SQL&#41;](create-a-database-snapshot-transact-sql.md).  
  
```  
--Test to see if sales_snapshot0600 exists and if it   
-- does, delete it.  
IF EXISTS (SELECT dbid FROM sys.databases  
    WHERE NAME='sales_snapshot0600')  
    DROP DATABASE SalesSnapshot0600;  
GO  
-- Reverting Sales to sales_snapshot1200  
USE master;  
RESTORE DATABASE Sales FROM DATABASE_SNAPSHOT = 'sales_snapshot1200';  
GO  
```  
  
##  <a name="RelatedTasks"></a> Tareas relacionadas  
  
-   [Crear una instantánea de base de datos &#40;Transact-SQL&#41;](create-a-database-snapshot-transact-sql.md)  
  
-   [Ver una instantánea de base de datos &#40;SQL Server&#41;](view-a-database-snapshot-sql-server.md)  
  
-   [Eliminar una instantánea de base de datos &#40;Transact-SQL&#41;](drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>Vea también  
 [Instantáneas de base de datos &#40;SQL Server&#41;](database-snapshots-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [Reflejo e instantáneas de base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-and-database-snapshots-sql-server.md)  
  
  
