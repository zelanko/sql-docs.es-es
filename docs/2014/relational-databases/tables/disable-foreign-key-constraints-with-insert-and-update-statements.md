---
title: Deshabilitar restricciones de clave externa con instrucciones INSERT y UPDATE | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- constraints [SQL Server], foreign keys
- foreign keys [SQL Server], disabling constraints
- disabling constraints
- UPDATE statement [SQL Server], foreign key constraints
- INSERT statement [SQL Server], foreign key constraints
ms.assetid: 029168d7-085e-4b13-9b86-5644b67c6e24
author: stevestein
ms.author: sstein
ms.openlocfilehash: e91328f4f12f2a0a27f397c7bd95390a505f3998
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068117"
---
# <a name="disable-foreign-key-constraints-with-insert-and-update-statements"></a>Deshabilitar restricciones FOREIGN KEY con instrucciones INSERT y UPDATE
  Puede deshabilitar una restricción de clave externa durante las transacciones INSERT y UPDATE en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Use esta opción si sabe que los nuevos datos infringirán la restricción existente o si la restricción solo se aplica a los datos que ya están en la base de datos.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para deshabilitar una restricción de clave externa en las instrucciones INSERT y UPDATE, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
 Después de deshabilitar estas restricciones, las posteriores inserciones o actualizaciones de la columna no se validan con las condiciones de la restricción.  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la tabla.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-disable-a-foreign-key-constraint-for-insert-and-update-statements"></a>Para deshabilitar una restricción FOREIGN KEY de instrucciones INSERT y UPDATE  
  
1.  En el **Explorador de objetos**, expanda la tabla que contiene la restricción y, a continuación, expanda la carpeta **Claves** .  
  
2.  Haga clic con el botón derecho en la restricción y seleccione **Modificar**.  
  
3.  En la cuadrícula situada debajo de **Diseñador de tablas**, haga clic en **Exigir restricción de clave externa** y seleccione **No** en el menú desplegable.  
  
4.  Haga clic en **Cerrar**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-disable-a-foreign-key-constraint-for-insert-and-update-statements"></a>Para deshabilitar una restricción FOREIGN KEY de instrucciones INSERT y UPDATE  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue los ejemplos siguientes en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE Purchasing.PurchaseOrderHeader  
    NOCHECK CONSTRAINT FK_PurchaseOrderHeader_Employee_EmployeeID;  
    GO  
    ```  
  
 Para obtener más información, vea [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).  
  
###  <a name="TsqlExample"></a>  
