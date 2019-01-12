---
title: Cambio de nombre de las columnas (motor de base de datos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- columns [SQL Server], names
- renaming columns
- column names [SQL Server]
ms.assetid: 7c71ec9f-0180-4398-b32a-4bfb7592e75d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f5fca9032df4f1327933580a306215fd2fd47854
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54135975"
---
# <a name="rename-columns-database-engine"></a>Cambiar el nombre a las columnas (motor de base de datos)
  Puede cambiar una columna de la tabla en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para cambiar el nombre de las columnas, utilizando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
 Cambiar el nombre de una columna automáticamente no cambiará las referencias a esa columna. Es necesario modificar de forma manual los objetos que hacen referencia a la columna cuyo nombre se ha cambiado. Por ejemplo, si se cambia el nombre de una columna de una tabla y en un desencadenador existe una referencia a esa columna, es necesario modificar el desencadenador para reflejar el nuevo nombre de la columna. Use [sys.sql_expression_dependencies](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql) para ver las dependencias del objeto antes de cambiarle el nombre.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere el permiso ALTER en el objeto.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-rename-a-column-using-object-explorer"></a>Para cambiar el nombre de una columna mediante el Explorador de objetos  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En el **Explorador de objetos**, haga clic con el botón derecho en la tabla en la que quiere cambiar nombres de columnas y elija **Cambiar nombre**.  
  
3.  Escriba un nuevo nombre de columna.  
  
#### <a name="to-rename-a-column-using-table-designer"></a>Para cambiar el nombre de una columna mediante el Diseñador de tablas  
  
1.  En el **Explorador de objetos**, haga clic con el botón derecho en la tabla en la que quiere cambiar nombres de columnas y elija **Diseño**.  
  
2.  En **Nombre de columna**, seleccione el nombre que desea cambiar y escriba uno nuevo.  
  
3.  En el menú **Archivo** , haga clic en **Guardar**_table name_.  
  
> [!NOTE]  
>  También puede cambiar el nombre de una columna en la pestaña **Propiedades de columna** . Seleccione la columna cuyo nombre desea cambiar y escriba un nuevo valor en **Nombre**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para cambiar el nombre de una columna**  
  
#### <a name="to-rename-a-column"></a>Para cambiar el nombre de una columna  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  En el siguiente ejemplo se cambia el nombre de la columna `TerritoryID` de la tabla `Sales.SalesTerritory` por `TerrID`. Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    EXEC sp_rename 'Sales.SalesTerritory.TerritoryID', 'TerrID', 'COLUMN';  
    GO  
    ```  
  
 Para obtener más información, vea [sp_rename &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-rename-transact-sql).  
  
  
