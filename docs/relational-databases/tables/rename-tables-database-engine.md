---
title: Cambio de nombre de las tablas (motor de base de datos) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- table renaming [SQL Server]
- table names [SQL Server]
- tables [SQL Server], Visual Database Tools
- renaming tables
ms.assetid: 2f5c922d-4d71-4694-9fca-28dd99375799
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d65c475509d57577f691e656157c7754c7d8549f
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="rename-tables-database-engine"></a>Cambiar el nombre a las tablas (motor de base de datos)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Puede cambiar el nombre de una tabla en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!CAUTION]  
>  Piénselo bien antes de cambiar el nombre de una tabla. Si las consultas, vistas, funciones definidas por el usuario, procedimientos almacenados o programas existentes hacen referencia a esta tabla, la modificación del nombre hará que estos objetos dejen de ser válidos.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para cambiar el nombre de una tabla con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
 Cambiar el nombre de una tabla automáticamente no cambiará las referencias a esa tabla. Es necesario modificar de forma manual los objetos que hacen referencia a la tabla cuyo nombre se ha cambiado. Por ejemplo, si se cambia el nombre de una tabla y en un desencadenador existe una referencia a esa tabla, es necesario modificar el desencadenador para reflejar el nuevo nombre de la tabla. Use [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) para enumerar las dependencias de la tabla antes de cambiarle el nombre.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la tabla.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-rename-a-table"></a>Para cambiar el nombre de una tabla  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en la tabla cuyo nombre quiere cambiar y seleccione **Diseño** en el menú contextual.  
  
2.  En el menú **Ver** , elija **Propiedades**.  
  
3.  En el campo del valor **Nombre** de la ventana **Propiedades** , escriba un nuevo nombre para la tabla.  
  
4.  Para cancelar esta acción, presione la tecla ESC antes de salir del campo.  
  
5.  En el menú **Archivo** , elija **Guardar***table name*.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
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
  
  

