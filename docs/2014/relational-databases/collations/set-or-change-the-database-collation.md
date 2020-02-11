---
title: Establecer o cambiar la intercalación de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- collations [SQL Server], database
- database collations [SQL Server]
ms.assetid: 1379605c-1242-4ac8-ab1b-e2a2b5b1f895
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 38c29f8d70b3cc72baf81e2ae23082fe270ba573
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62874028"
---
# <a name="set-or-change-the-database-collation"></a>Establecer o cambiar la intercalación de base de datos
  En este tema se describe cómo establecer y cambiar la intercalación de base de datos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Si no se especifica ninguna intercalación, se utiliza la del servidor.  
  
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
  
-   Las intercalaciones exclusivas de Unicode de Windows se pueden utilizar únicamente con la cláusula COLLATE para aplicar intercalaciones a los tipos de datos `nchar`, `nvarchar` y `ntext` de nivel de columna y de nivel de datos de expresión. No se pueden utilizar con la cláusula COLLATE para cambiar la intercalación de una instancia de la base de datos o del servidor.  
  
-   Si la intercalación especificada o la intercalación usada por el objeto al que se hace referencia utiliza una página de códigos no admitida por Windows, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] muestra un error.  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Puede buscar los nombres de intercalación admitidos en [Nombre de intercalación de Windows &#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql) y [Nombre de intercalación de SQL Server &#40;Transact-SQL&#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql), o puede usar la función del sistema [sys.fn_helpcollations &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-helpcollations-transact-sql) .  
  
-   Al modificar la intercalación de la base de datos también se cambian los siguientes elementos:  
  
    -   Todas las columnas `char`, `varchar`, `text`, `nchar`, `nvarchar` o `ntext` de las tablas del sistema se cambian a la nueva intercalación.  
  
    -   Todos los parámetros `char`, `varchar`, `text`, `nchar`, `nvarchar` o `ntext` y valores devueltos escalares existentes para los procedimientos almacenados y las funciones definidas por el usuario se cambian a la nueva intercalación.  
  
    -   Los tipos de datos del sistema `char`, `varchar`, `text`, `nchar`, `nvarchar` o `ntext` y todos los tipos de datos definidos por el usuario basados en estos tipos de datos del sistema se cambian a la nueva intercalación predeterminada.  
  
-   Para cambiar la intercalación de cualquier objeto nuevo creado en una base de datos de usuario, utilice la cláusula COLLATE de la instrucción [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) . Esta instrucción no modifica la intercalación de las columnas de ninguna de las tablas definidas por el usuario existentes. Para modificarlas, utilice la cláusula COLLATE de [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 CREATE DATABASE  
 Requiere el permiso CREATE DATABASE en la base de datos **maestra** , o los permisos CREATE ANY DATABASE o ALTER ANY DATABASE.  
  
 ALTER DATABASE  
 Requiere el permiso ALTER en la base de datos.  
  
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
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se muestra cómo usar la cláusula [COLLATE](/sql/t-sql/statements/collations) para especificar un nombre de intercalación. En el ejemplo de crea la base de datos `MyOptionsTest` que utiliza la intercalación `Latin1_General_100_CS_AS_SC` . Después de crear la base de datos, ejecute la instrucción `SELECT` para comprobar la configuración.  
  
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
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se muestra cómo usar la cláusula [COLLATE](/sql/t-sql/statements/collations) en una instrucción [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) para cambiar el nombre de la intercalación. Ejecute la instrucción `SELECT` para comprobar el cambio.  
  
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
 [Compatibilidad con la intercalación y Unicode](collation-and-unicode-support.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-helpcollations-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [Nombre de intercalación de SQL Server &#40;Transact-SQL&#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql)   
 [Nombre de intercalación de Windows &#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql)   
 [COLLATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/collations)   
 [Prioridad de intercalación &#40;Transact-SQL&#41;](/sql/t-sql/statements/collation-precedence-transact-sql)   
 [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)   
 [CREATE DATABASE &#40;Transact-SQL de SQL Server&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
  
