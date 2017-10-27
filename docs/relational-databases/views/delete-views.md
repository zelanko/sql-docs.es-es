---
title: "Eliminación de vistas | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-views
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- dropping views
- deleting views
- views [SQL Server], deleting
- removing views
ms.assetid: 6823c7f8-06ca-4bda-8482-7092f03d52a0
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1c869b1e4ba7cc992687baa3236c96d25b0e63e8
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="delete-views"></a>Eliminar vistas
  Puede eliminar (quitar) vistas de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para eliminar una vista de una base de datos, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Cuando se quita una vista, la definición y otra información de la vista se elimina del catálogo del sistema. También se eliminan todos los permisos de la vista.  
  
-   Las vistas de una tabla que se ha quitado mediante `DROP TABLE` se deben quitar explícitamente con `DROP VIEW`.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Se necesita el permiso ALTER en SCHEMA o el permiso CONTROL en OBJECT.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-delete-a-view-from-a-database"></a>Para eliminar una vista de una base de datos  
  
1.  En el **Explorador de objetos**, expanda la base de datos que contiene la vista que desea eliminar y, a continuación, expanda la carpeta **Vistas** .  
  
2.  Haga clic con el botón derecho en la vista que quiere eliminar y haga clic en **Eliminar**.  
  
3.  En el cuadro de diálogo **Eliminar objeto** , haga clic en **Aceptar**.  
  
    > [!IMPORTANT]  
    >  Haga clic en **Mostrar dependencias** en el cuadro de diálogo **Eliminar objeto** para abrir el cuadro de diálogo **Dependencias de *view_name***. Esto mostrará todos los objetos que dependen de la vista y todos los objetos de los que depende la vista.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-delete-a-view-from-a-database"></a>Para eliminar una vista de una base de datos  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. El ejemplo elimina la vista especificada solo si la vista ya existe.  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    IF OBJECT_ID ('HumanResources.EmployeeHireDate', 'V') IS NOT NULL  
    DROP VIEW HumanResources.EmployeeHireDate;  
    GO  
    ```  
  
 Para obtener más información, vea [DROP VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/drop-view-transact-sql.md).  
  
  

