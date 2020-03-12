---
title: Establecer o cambiar la intercalación de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- collations [SQL Server], database
- database collations [SQL Server]
ms.assetid: 1379605c-1242-4ac8-ab1b-e2a2b5b1f895
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2221d88e5f564b08f993f68f9be4131588aebe2a
ms.sourcegitcommit: 86268d297e049adf454b97858926d8237d97ebe2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/06/2020
ms.locfileid: "78866114"
---
# <a name="set-or-change-the-database-collation"></a>Establecer o cambiar la intercalación de base de datos
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  En este tema se describe cómo establecer y cambiar la intercalación de base de datos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Si no se especifica ninguna intercalación, se utiliza la del servidor.  
  
> [!IMPORTANT]
> La modificación de la intercalación de base de datos no está explícitamente prohibida en Azure SQL Database. Sin embargo, requiere el bloqueo exclusivo en la base de datos, y otros procesos de usuario o en segundo plano (por ejemplo, las copias de seguridad) podrían mantener este bloqueo y evitar el cambio de la intercalación. La instrucción `ALTER DATABASE COLLATE` de Azure SQL Database producirá un error si se ejecuta mientras los procesos en segundo plano acceden a la base de datos. Si recibe un error de tiempo de expiración de bloqueo, debería reintentar la instrucción. 
 
> [!NOTE]
> La intercalación no se puede modificar con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] una vez que se creó la base de datos en [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Solo se puede modificar a través de [!INCLUDE[tsql](../../includes/tsql-md.md)].

 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para establecer o cambiar la intercalación de base de datos, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Las intercalaciones exclusivas de Unicode de Windows solo se pueden usar con la cláusula COLLATE para aplicar intercalaciones a los tipos de datos **nchar**, **nvarchar**y **ntext** de nivel de columna y de nivel de datos de expresión. No se pueden utilizar con la cláusula COLLATE para cambiar la intercalación de una instancia de la base de datos o del servidor.  
  
-   Si la intercalación especificada o la intercalación usada por el objeto al que se hace referencia utiliza una página de códigos no admitida por Windows, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] muestra un error.  

-   La intercalación no se puede modificar con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] una vez que se creó la base de datos en [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Solo se puede modificar a través de [!INCLUDE[tsql](../../includes/tsql-md.md)].
  
###  <a name="Recommendations"></a> Recomendaciones  
  
Puede buscar los nombres de intercalación admitidos en [Nombre de intercalación de Windows &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md) y [Nombre de intercalación de SQL Server &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md), o puede usar la función del sistema [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) .  
  
Al modificar la intercalación de la base de datos también se cambian los siguientes elementos:  
  
-   Todas las columnas **char**, **varchar**, **text**, **nchar**, **nvarchar**o **ntext** de las tablas del sistema se cambian a la nueva intercalación.  
  
-   Todos los valores devueltos escalares y parámetros **char**, **varchar**, **text**, **nchar**, **nvarchar**o **ntext** existentes para los procedimientos almacenados y las funciones definidas por el usuario se cambian a la nueva intercalación.  
  
-   Los tipos de datos del sistema **char**, **varchar**, **text**, **nchar**, **nvarchar**o **ntext** y todos los tipos de datos definidos por el usuario basados en estos tipos de datos del sistema se cambian a la nueva intercalación predeterminada.  
  
Para cambiar la intercalación de cualquier objeto nuevo creado en una base de datos de usuario, utilice la cláusula `COLLATE` de la instrucción [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md). Esta instrucción **no modifica** la intercalación de las columnas de ninguna de las tablas definidas por el usuario existentes. Para modificarlas, use la cláusula `COLLATE` de [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Para crear una base de datos, requiere el permiso `CREATE DATABASE` en la base de datos **maestra**, o bien requiere `CREATE ANY DATABASE` o el permiso `ALTER ANY DATABASE`.  
  
 Para cambiar la intercalación de una base de datos existente, requiere el permiso `ALTER` en la base de datos.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-set-or-change-the-database-collation"></a>Para establecer o cambiar la intercalación de base de datos  
  
1.  En el **Explorador de objetos**, conéctese a una instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], expándala y, a continuación, expanda **Bases de datos**.  
  
2.  Si está creando una base de datos, haga clic con el botón derecho en **Bases de datos** y haga clic en **Nueva base de datos**. Si no quiere la intercalación predeterminada, haga clic en la página **Opciones** y seleccione una intercalación en la lista desplegable **Intercalación** .  
  
     Como alternativa, si la base de datos ya existe, haga clic con el botón derecho en la base de datos que quiera y haga clic en **Propiedades**. Haga clic en la página **Opciones** y seleccione una intercalación en la lista desplegable **Intercalación** .  
  
3.  Cuando haya terminado, haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-set-the-database-collation"></a>Para establecer la intercalación de base de datos  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se muestra cómo usar la cláusula [COLLATE](~/t-sql/statements/collations.md) para especificar un nombre de intercalación. En el ejemplo de crea la base de datos `MyOptionsTest` que utiliza la intercalación `Latin1_General_100_CS_AS_SC` . Después de crear la base de datos, ejecute la instrucción `SELECT` para comprobar la configuración.  
  
```sql  
USE master;  
GO  
IF DB_ID (N'MyOptionsTest') IS NOT NULL  
DROP DATABASE MyOptionsTest;  
GO  
CREATE DATABASE MyOptionsTest  
COLLATE Latin1_General_100_CS_AS_SC;  
GO  
  
--Verify the collation setting.  
SELECT name, collation_name  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
```  
  
#### <a name="to-change-the-database-collation"></a>Para cambiar la intercalación de base de datos  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se muestra cómo usar la cláusula [COLLATE](~/t-sql/statements/collations.md) en una instrucción [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) para cambiar el nombre de la intercalación. Ejecute la instrucción `SELECT` para comprobar el cambio.  
  
```sql  
USE master;  
GO  
ALTER DATABASE MyOptionsTest  
COLLATE French_CI_AS ;  
GO  
  
--Verify the collation setting.  
SELECT name, collation_name  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Compatibilidad con la intercalación y Unicode](../../relational-databases/collations/collation-and-unicode-support.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Nombre de intercalación de SQL Server &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md)   
 [Nombre de intercalación de Windows &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)   
 [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)   
 [Prioridad de intercalación &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
  
