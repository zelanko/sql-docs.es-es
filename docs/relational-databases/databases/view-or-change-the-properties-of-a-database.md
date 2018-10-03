---
title: Ver o cambiar las propiedades de una base de datos | Microsoft Docs
ms.custom: ''
ms.date: 01/05/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- displaying databases
- database viewing [SQL Server]
- databases [SQL Server], viewing
- viewing databases
ms.assetid: 9e8ac097-84b7-46c7-85e3-c1e79f94d747
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0c0ae0a9be78f4263ae084c8455a480e2140a528
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47686084"
---
# <a name="view-or-change-the-properties-of-a-database"></a>Ver o cambiar las propiedades de una base de datos
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  En este tema se describe cómo ver o cambiar las propiedades de una base de datos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Después de cambiar una propiedad de la base de datos, la modificación surte efecto de inmediato.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para ver o cambiar las propiedades de una base de datos, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Si AUTO_CLOSE es ON, algunas columnas de la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) y de la función DATABASEPROPERTYEX devuelven NULL porque la base de datos no está disponible para recuperar los datos. Para resolver este problema, abra la base de datos.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Se requiere el permiso ALTER en la base de datos para cambiar las propiedades de una base de datos. Se requiere como mínimo pertenecer al rol de base de datos Public para ver las propiedades de una base de datos.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-view-or-change-the-properties-of-a-database"></a>Para ver o cambiar las propiedades de una base de datos  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]y, a continuación, expándala.  
  
2.  Expanda **Bases de datos**, haga clic con el botón derecho en la base de datos que quiera ver y, después, haga clic en **Propiedades**.  
  
3.  En el cuadro de diálogo **Propiedades de la base de datos** , seleccione una página para ver la información correspondiente. Por ejemplo, seleccione la página **Archivos** para ver información acerca de los archivos de datos y de registro.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 Transact-SQL proporciona una serie de métodos diferentes para ver y cambiar las propiedades de una base de datos. Para ver las propiedades de una base de datos, puede usar la función [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md) y la vista de catálogo [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) . Para cambiar las propiedades de una base de datos, puede usar la versión de la instrucción ALTER DATABASE para su entorno: [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md) o [ALTER DATABASE (Azure SQL Database)](../../t-sql/statements/alter-database-azure-sql-database.md). Para ver las propiedades de ámbito de base de datos, use la vista de catálogo [sys.database_scoped_configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) . Para modificar dichas propiedades, use la instrucción [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) .  
  
#### <a name="to-view-a-property-of-a-database-by-using-the-databasepropertyex-function"></a>Para ver una propiedad de una base de datos con la función DATABASEPROPERTYEX  
  
1.  Conéctese al [!INCLUDE[ssDE](../../includes/ssde-md.md)] y luego a la base de datos cuyas propiedades desea ver.  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. Este ejemplo usa la función de sistema [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) para devolver el estado de la opción de base de datos AUTO_SHRINK en la base de datos de [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Un valor devuelto de 1 significa que la opción está establecida en ON y un valor devuelto de 0 significa que la opción está establecida en OFF.  
  
    ```sql  
    SELECT DATABASEPROPERTYEX('AdventureWorks2012', 'IsAutoShrink');  
    ```  
  
#### <a name="to-view-the-properties-of-a-database-by-querying-sysdatabases"></a>Para ver las propiedades de una base de datos consultando sys.databases  
  
1.  Conéctese al [!INCLUDE[ssDE](../../includes/ssde-md.md)] y luego a la base de datos cuyas propiedades desea ver.  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se consulta la vista de catálogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) para ver varias propiedades de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Este ejemplo devuelve el número de id. de base de datos (`database_id`), un valor que indica si la base de datos es de solo lectura o de lectura y escritura (`is_read_only`), la intercalación de la base de datos (`collation_name`) y el nivel de compatibilidad de la base de datos (`compatibility_level`).  
  
    ```sql  
    SELECT database_id, is_read_only, collation_name, compatibility_level  
    FROM sys.databases WHERE name = 'AdventureWorks2012';  
    ```  
  
#### <a name="to-view-the-properties-of-a-database-scoped-configuration-by-querying-sysdatabasesscopedconfiguration"></a>Para ver las propiedades de una configuración de ámbito de base de datos mediante una consulta sys.databases_scoped_configuration  
  
1.  Conéctese al [!INCLUDE[ssDE](../../includes/ssde-md.md)] y luego a la base de datos cuyas propiedades desea ver.  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se consulta la vista de catálogo [sys.database_scoped_configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) para ver varias propiedades de la base de datos actual.  
  
    ```sql  
    SELECT configuration_id, name, value, value_for_secondary  
    FROM sys.database_scoped_configurations;  
    ```  
  
     Para ver más ejemplos, vea [sys.database_scoped_configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)  
  
#### <a name="to-change-the-properties-of-a-sql-server-2016-database-using-alter-database"></a>Para cambiar las propiedades de una base de datos de SQL Server 2016 mediante ALTER DATABASE  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el ejemplo siguiente en la ventana de consulta. El ejemplo determina el estado de aislamiento de instantánea en la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] , cambia el estado de la propiedad y comprueba el cambio.  
  
     Para determinar el estado de aislamiento de instantánea, seleccione la primera instrucción `SELECT` y haga clic en **Ejecutar**.  
  
     Para cambiar el estado de aislamiento de instantánea, seleccione la instrucción `ALTER DATABASE` y haga clic en **Ejecutar**de.  
  
     Para comprobar el cambio, seleccione la segunda instrucción `SELECT` y haga clic en **Ejecutar**.  
  
     [!code-sql[DatabaseDDL#AlterDatabase9](../../relational-databases/databases/codesnippet/tsql/view-or-change-the-prope_1.sql)]  
  
#### <a name="to-change-the-database-scoped-properties-using-alter-database-scoped-configuration"></a>Para cambiar las propiedades de ámbito de la base de datos mediante ALTER DATABASE SCOPED CONFIGURATION  
  
1.  Conéctese a una base de datos en la instancia de SQL Server.  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el ejemplo siguiente en la ventana de consulta. En el ejemplo siguiente se establece MAXDOP de una base de datos secundaria con el valor de la base de datos principal.  
  
    ```sql  
    ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP = PRIMARY   
    ```  
  
## <a name="see-also"></a>Ver también  
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [ALTER DATABASE (Azure SQL Database)](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)   
 [sys.database_scoped_configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)  

  
  
