---
title: Eliminación de claves principales | Microsoft Docs
ms.custom: ''
ms.date: 07/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- removing primary keys
- deleting primary keys
- primary keys [SQL Server], deleting
ms.assetid: c472e465-7bdd-4d74-8fc9-e47fca007ccb
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7465a183241211fe4372eea0c57f93f3cfe0aa49
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86002088"
---
# <a name="delete-primary-keys"></a>Eliminar claves principales
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

  Puede eliminar (quitar) una clave principal en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Cuando se elimina la clave principal, se elimina el índice correspondiente.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para eliminar una clave principal con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la tabla.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-delete-a-primary-key-constraint-using-object-explorer"></a>Para eliminar una restricción de clave principal mediante el Explorador de objetos  
  
1.  En el Explorador de objetos, expanda la tabla que contiene la clave principal y, a continuación, expanda **Claves**.  
  
2.  Haga clic con el botón derecho en la clave y seleccione **Eliminar**.  
  
3.  En el cuadro de diálogo **Eliminar objeto** , compruebe que se ha especificado la clave correcta y haga clic en **Aceptar**.  
  
#### <a name="to-delete-a-primary-key-constraint-using-table-designer"></a>Para eliminar una restricción de clave principal mediante el Diseñador de tablas  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en la tabla con la clave principal y, después, haga clic en **Diseño**.  
  
2.  En la cuadrícula de la tabla, haga clic con el botón derecho en la fila que contiene la clave principal y elija **Quitar clave principal** para desactivar el valor.  
  
    > [!NOTE]  
    >  Para deshacer esta acción, cierre la tabla sin guardar los cambios. Si se elimina una clave principal, no se podrá deshacer la acción sin perder todos los demás cambios realizados en la tabla.  
  
3.  En el menú **Archivo** , haga clic en **Guardar**_table name_.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
  
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
