---
title: "Eliminación de claves principales | Microsoft Docs"
ms.custom: 
ms.date: 07/25/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing primary keys
- deleting primary keys
- primary keys [SQL Server], deleting
ms.assetid: c472e465-7bdd-4d74-8fc9-e47fca007ccb
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 185ab2d26ef049e211ae42624dae3e1517361cca
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="delete-primary-keys"></a>Eliminar claves principales
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Puede eliminar (quitar) una clave principal en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Cuando se elimina la clave principal, se elimina el índice correspondiente.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para eliminar una clave principal con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Requiere el permiso ALTER en la tabla.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-delete-a-primary-key-constraint-using-object-explorer"></a>Para eliminar una restricción de clave principal mediante el Explorador de objetos  
  
1.  En el Explorador de objetos, expanda la tabla que contiene la clave principal y, a continuación, expanda **Claves**.  
  
2.  Haga clic con el botón derecho en la clave y seleccione **Eliminar**.  
  
3.  En el cuadro de diálogo **Eliminar objeto** , compruebe que se ha especificado la clave correcta y haga clic en **Aceptar**.  
  
#### <a name="to-delete-a-primary-key-constraint-using-table-designer"></a>Para eliminar una restricción de clave principal mediante el Diseñador de tablas  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en la tabla con la clave principal y, después, haga clic en **Diseño**.  
  
2.  En la cuadrícula de la tabla, haga clic con el botón derecho en la fila que contiene la clave principal y elija **Quitar clave principal** para desactivar el valor.  
  
    > [!NOTE]  
    >  Para deshacer esta acción, cierre la tabla sin guardar los cambios. Si se elimina una clave principal, no se podrá deshacer la acción sin perder todos los demás cambios realizados en la tabla.  
  
3.  En el menú **Archivo**, haga clic en **Guardar***nombre de tabla*.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-delete-a-primary-key-constraint"></a>Para eliminar una restricción PRIMARY KEY  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. El ejemplo primero identifica el nombre de la restricción de clave principal y luego elimina la restricción.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Return the name of primary key.  
    SELECT name  
    FROM sys.key_constraints  
    WHERE type = 'PK' AND OBJECT_NAME(parent_object_id) = N'TransactionHistoryArchive';  
    GO  
    -- Delete the primary key constraint.  
    ALTER TABLE Production.TransactionHistoryArchive  
    DROP CONSTRAINT PK_TransactionHistoryArchive_TransactionID;   
    GO  
    ```  
  
 Para obtener más información, vea [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md) y [sys.key_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md).  
  
###  <a name="TsqlExample"></a>  
