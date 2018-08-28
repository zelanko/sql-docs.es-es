---
title: Ver las dependencias de una tabla | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- table dependencies [SQL Server]
- dependencies [SQL Server], tables
- displaying dependences
- viewing dependencies
ms.assetid: c4351ef5-e7d0-46e7-8367-88695e9974f8
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1e2e0ad779b9299538e99d16b6f91c6b668bebfe
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43099602"
---
# <a name="view-the-dependencies-of-a-table"></a>Ver las dependencias de una tabla
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Puede ver las dependencias de una tabla en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para ver las dependencias de una tabla con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Necesita el permiso VIEW DEFINITION en la base de datos y el permiso SELECT en sys.sql_expression_dependencies para la base de datos. De forma predeterminada, solo se permite el permiso SELECT a los miembros del rol fijo de base de datos db_owner. Si se conceden los permisos SELECT y VIEW DEFINITION a otro usuario, el receptor puede ver todas las dependencias de la base de datos.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-view-the-dependencies-of-a-table"></a>Para ver las dependencias de una tabla  
  
1.  En el **Explorador de objetos**, expanda **Bases de datos**, expanda una base de datos y, a continuación, **Tablas**.  
  
2.  Haga clic con el botón derecho en una tabla y, después, haga clic en **Ver dependencias**.  
  
3.  En el cuadro de diálogo **Dependencias del objeto ***\<nombre del objeto>*, seleccione **Objetos que dependen de** *\<nombre del objeto>* u **Objetos de los que depende ***\<nombre del objeto>*****.  
  
4.  Seleccione un objeto en la cuadrícula **Dependencias** . El tipo de objeto (por ejemplo, "Desencadenador" o "Procedimiento almacenado"), aparece en el cuadro **Tipo** .  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-view-the-objects-that-depend-on-a-table"></a>Para ver los objetos que dependen de una tabla  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT * FROM sys.sql_expression_dependencies  
    WHERE referencing_id = OBJECT_ID(N'Production.vProductAndDescription');   
    GO  
  
    ```  
  
#### <a name="to-view-the-objects-on-which-a-table-depends"></a>Para ver los objetos de los que depende una tabla  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  El ejemplo siguiente devuelve los objetos que dependen de la tabla `Production.Product`. Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    SELECT * FROM sys.sql_expression_dependencies  
    WHERE referenced_id = OBJECT_ID(N'Production.Product');   
    GO  
  
    ```  
  
 Para obtener más información, vea [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md).  
  
  
