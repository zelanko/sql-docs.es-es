---
title: Actualizar estadísticas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- updating statistics
- statistics [SQL Server], updating
ms.assetid: 4b97c0b4-03ff-4cfb-9c3f-3b33290b7a2c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7c9a628f912f382f3ee8a87276aa34d0e54e37ba
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63033675"
---
# <a name="update-statistics"></a>Actualizar estadísticas
  Puede actualizar las estadísticas de optimización de consultas en una tabla o en una vista indizada de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. De forma predeterminada, el optimizador de consultas ya actualiza las estadísticas como requisito para mejorar el plan de consulta; en algunos casos puede mejorar el rendimiento de las consultas utilizando UPDATE STATISTICS o el procedimiento almacenado `sp_updatestats` para actualizar las estadísticas con más frecuencia que la de las actualizaciones predeterminadas.  
  
 La actualización de las estadísticas asegura que las consultas se compilan con estadísticas actualizadas. Sin embargo, la actualización de las estadísticas hace que las consultas se vuelvan a compilar. Recomendamos no actualizar las estadísticas con demasiada frecuencia, porque hay que elegir el punto válido entre la mejora de los planes de consulta y el tiempo empleado en volver a compilar las consultas. Las compensaciones específicas dependen de su aplicación. UPDATE STATISTICS puede usar tempdb para ordenar la muestra de filas con fines de creación de estadísticas.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para actualizar un objeto de estadísticas, con:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Si usa UPDATE STATISTICS o realiza cambios con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], es necesario el permiso ALTER en la tabla o vista. Si usa `sp_updatestats`, necesita pertenecer al rol fijo de servidor **sysadmin** o ser propietario de la base de datos (**dbo**).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-update-a-statistics-object"></a>Para actualizar un objeto de estadísticas  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir la base de datos en la que desea actualizar la estadística.  
  
2.  Haga clic en el signo más para expandir la carpeta **Tablas** .  
  
3.  Haga clic en el signo más para expandir la tabla en la que desea actualizar la estadística.  
  
4.  Haga clic en el signo más para expandir la carpeta **Estadísticas** .  
  
5.  Haga clic con el botón derecho en el objeto de estadísticas que quiere actualizar y seleccione **Propiedades**.  
  
6.  En el cuadro de diálogo **propiedades de estadísticas-**_statistics_name_ , active la casilla **actualizar estadísticas de estas columnas** y, a continuación, haga clic en **Aceptar**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-update-a-specific-statistics-object"></a>Para actualizar un objeto concreto de estadísticas  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- The following example updates the statistics for the AK_SalesOrderDetail_rowguid index of the SalesOrderDetail table.   
    UPDATE STATISTICS Sales.SalesOrderDetail AK_SalesOrderDetail_rowguid;   
    GO  
    ```  
  
#### <a name="to-update-all-statistics-in-a-table"></a>Para actualizar todas las estadísticas en una tabla  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- The following example updates the statistics for all indexes on the SalesOrderDetail table.   
    UPDATE STATISTICS Sales.SalesOrderDetail;   
    GO  
    ```  
  
 Para obtener más información, vea [UPDATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql).  
  
#### <a name="to-update-all-statistics-in-a-database"></a>Para actualizar todas las estadísticas de una base de datos  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- The following example updates the statistics for all tables in the database.   
    EXEC sp_updatestats;  
    ```  
  
 Para obtener más información, vea [sp_updatestats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql).  
  
  
