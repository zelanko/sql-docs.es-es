---
title: Cambio de nombre de los índices | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- renaming indexes
- index names [SQL Server]
- indexes [SQL Server], renaming
ms.assetid: d3d612a1-ea1b-4d99-85d2-0a2ad54f4b0e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 184d6e20f7857c5ea3535e77e21a0630ffc7b678
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049849"
---
# <a name="rename-indexes"></a>Cambiar el nombre a los índices
  En este tema se describe cómo cambiar el nombre de un índice en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Al cambiar el nombre de un índice se reemplaza el nombre de índice actual por el nuevo nombre que se proporciona. El nombre especificado debe ser único en la tabla o en la vista. Por ejemplo, dos tablas pueden tener un índice con el nombre **XPK_1**, pero la misma tabla no puede tener dos índices con el nombre **XPK_1**. No puede crear un índice con el mismo nombre que un índice existente deshabilitado. Al cambiar el nombre de un índice no se hace que se reconstruya el índice.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para cambiar el nombre de un índice, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
 Cuando cree una restricción PRIMARY KEY o UNIQUE en una tabla, se creará automáticamente un índice con el mismo nombre que la restricción para la tabla. Dado que los nombres de índice deben ser únicos en la tabla, no puede crear o cambiar el nombre de un índice para que tenga el mismo nombre que una restricción PRIMARY KEY o UNIQUE que ya existe en la tabla.  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en el índice.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-rename-an-index-by-using-the-table-designer"></a>Para cambiar el nombre de un índice mediante el Diseñador de tablas  
  
1.  En el Explorador de objetos, haga clic en el signo más para expandir la base de datos que contiene la tabla en la que desea cambiar el nombre de un índice.  
  
2.  Haga clic en el signo más para expandir la carpeta **Tablas** .  
  
3.  Haga clic con el botón derecho en la tabla con el índice que quiera cambiar de nombre y seleccione **Diseño**.  
  
4.  En el menú **Diseñador de tablas** , haga clic en **Índices o claves**.  
  
5.  Seleccione el índice que quiera cambiar de nombre en el cuadro de texto **Clave principal o única, o índice seleccionado** .  
  
6.  En la cuadrícula, haga clic en **Nombre** y escriba un nuevo nombre en el cuadro de texto.  
  
7.  Haga clic en **Cerrar**.  
  
8.  En el menú **Archivo** , haga clic en **Guardar**_table_name_.  
  
#### <a name="to-rename-an-index-by-using-object-explorer"></a>Para cambiar el nombre de un índice mediante el Explorador de objetos  
  
1.  En el Explorador de objetos, haga clic en el signo más para expandir la base de datos que contiene la tabla en la que desea cambiar el nombre de un índice.  
  
2.  Haga clic en el signo más para expandir la carpeta **Tablas** .  
  
3.  Haga clic en el signo más para expandir la tabla en la que desea cambiar el nombre de un índice.  
  
4.  Haga clic en el signo más para expandir la carpeta **Índices** .  
  
5.  Haga clic con el botón derecho en el índice que quiera cambiar de nombre y seleccione **Cambiar nombre**.  
  
6.  Escriba el nuevo nombre del índice y presione Entrar.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-rename-an-index"></a>Para cambiar el nombre de un índice  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    --Renames the IX_ProductVendor_VendorID index on the Purchasing.ProductVendor table to IX_VendorID.   
  
    EXEC sp_rename N'Purchasing.ProductVendor.IX_ProductVendor_VendorID', N'IX_VendorID', N'INDEX';   
    GO  
    ```  
  
 Para obtener más información, vea [sp_rename &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-rename-transact-sql).  
  
  
