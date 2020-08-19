---
description: Cambiar el nombre a las tablas (motor de base de datos)
title: Cambio de nombre de las tablas (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 02/23/2018
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- table renaming [SQL Server]
- table names [SQL Server]
- tables [SQL Server], Visual Database Tools
- renaming tables
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 86a6b67d0393c9bac6e5ad3b9713c89796df3db4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427457"
---
# <a name="rename-tables-database-engine"></a>Cambiar el nombre a las tablas (motor de base de datos)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

Cambie el nombre de una tabla en SQL Server o Azure SQL Database.

Para cambiar el nombre de una tabla en Azure SQL Data Warehouse o en Almacenamiento de datos paralelos, use la instrucción [RENAME OBJECT](../../t-sql/statements/rename-transact-sql.md) de Transact-SQL. 
  
> [!CAUTION]  
>  Piénselo bien antes de cambiar el nombre de una tabla. Si las consultas, vistas, funciones definidas por el usuario, procedimientos almacenados o programas existentes hacen referencia a esta tabla, la modificación del nombre hará que estos objetos dejen de ser válidos.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para cambiar el nombre de una tabla con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
 Cambiar el nombre de una tabla automáticamente no cambiará las referencias a esa tabla. Es necesario modificar de forma manual los objetos que hacen referencia a la tabla cuyo nombre se ha cambiado. Por ejemplo, si se cambia el nombre de una tabla y en un desencadenador existe una referencia a esa tabla, es necesario modificar el desencadenador para reflejar el nuevo nombre de la tabla. Use [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) para enumerar las dependencias de la tabla antes de cambiarle el nombre.  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la tabla.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-rename-a-table"></a>Para cambiar el nombre de una tabla  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en la tabla cuyo nombre quiere cambiar y seleccione **Diseño** en el menú contextual.  
  
2.  En el menú **Ver** , elija **Propiedades**.  
  
3.  En el campo del valor **Nombre** de la ventana **Propiedades** , escriba un nuevo nombre para la tabla.  
  
4.  Para cancelar esta acción, presione la tecla ESC antes de salir del campo.  
  
5.  En el menú **Archivo**, seleccione **Guardar** _nombre de tabla_.  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-rename-a-table"></a>Para cambiar el nombre de una tabla  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  En el siguiente ejemplo se cambia el nombre de la tabla `SalesTerritory` por `SalesTerr` en el esquema `Sales` . Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    EXEC sp_rename 'Sales.SalesTerritory', 'SalesTerr';  
    ```  
  
 Para ver otros ejemplos, vea [sp_rename &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-rename-transact-sql.md).  
  
  
