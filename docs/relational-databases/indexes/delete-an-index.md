---
title: "Eliminar un &#237;ndice | Microsoft Docs"
ms.custom: ""
ms.date: "02/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-indexes"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "índices, quitar"
  - "eliminar índices"
  - "quitar índices"
  - "índices [SQL Server], quitar"
  - "eliminaciones de índices [SQL Server]"
ms.assetid: fd38a0ed-26c4-4c76-9ef7-e0a16147329d
caps.latest.revision: 29
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 29
---
# Eliminar un &#237;ndice
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  En este tema se describe cómo eliminar (quitar) un índice en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para eliminar un índice, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
 Los índices creados como resultado de una restricción PRIMARY KEY o UNIQUE no se pueden eliminar con este método. En su lugar, se debe eliminar la restricción. Para quitar la restricción y el índice correspondiente, use [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) con la cláusula DROP CONSTRAINT en [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para obtener más información, consulte [Delete Primary Keys](../../relational-databases/tables/delete-primary-keys.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la tabla o la vista. Este permiso se concede de forma predeterminada al rol fijo de servidor **sysadmin** y a los roles fijos de base de datos **db_ddladmin** y **db_owner**.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### Para eliminar un índice mediante el Explorador de objetos  
  
1.  En el Explorador de objetos, expanda la base de datos que contiene la tabla en la que desea eliminar un índice.  
  
2.  Expanda la carpeta **Tablas** .  
  
3.  Expanda la tabla que contiene el índice que desee eliminar.  
  
4.  Expanda la carpeta **Índices** .  
  
5.  Haga clic con el botón derecho en el índice que quiere eliminar y seleccione **Eliminar**.  
  
6.  En el cuadro de diálogo **Eliminar objeto** , compruebe que el índice correcto se encuentra en la cuadrícula **Objeto que se va a eliminar** y haga clic en **Aceptar**.  
  
#### Para eliminar un índice mediante el Diseñador de tablas  
  
1.  En el Explorador de objetos, expanda la base de datos que contiene la tabla en la que desea eliminar un índice.  
  
2.  Expanda la carpeta **Tablas** .  
  
3.  Haga clic con el botón secundario en la tabla que contiene el índice que desee eliminar y haga clic en Diseño.  
  
4.  En el menú **Diseñador de tablas**, haga clic en **Índices o claves**.  
  
5.  En el cuadro de diálogo **Índices o claves**, seleccione el índice que quiera eliminar.  
  
6.  Haga clic en **Eliminar**.  
  
7.  Haga clic en **Cerrar**.  
  
8.  En el menú **Archivo**, seleccione **Guardar***nombre_tabla*.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### Para eliminar un índice  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- delete the IX_ProductVendor_BusinessEntityID index  
    -- from the Purchasing.ProductVendor table  
    DROP INDEX IX_ProductVendor_BusinessEntityID   
        ON Purchasing.ProductVendor;  
    GO  
    ```  
  
 Para obtener más información, vea [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md).  
  
  