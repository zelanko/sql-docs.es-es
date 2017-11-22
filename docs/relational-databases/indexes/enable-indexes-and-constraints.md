---
title: "Habilitar índices y restricciones | Microsoft Docs"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: indexes
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- indexes [SQL Server], enabling
- nonclustered indexes [SQL Server], enabling a disabled index
- index enabling [SQL Server]
- disabled indexes [SQL Server], how to enable
- constraints [SQL Server], enabling
- clustered indexes, enabling disabled indexes
ms.assetid: c55c8865-322e-4ab0-ba04-ea1f56735353
caps.latest.revision: "27"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 05993c2ce383b65938712557cd82db47aaaf28bb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="enable-indexes-and-constraints"></a>Habilitar índices y restricciones
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  En este tema se describe cómo habilitar un índice deshabilitado en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Cuando se deshabilita un índice, sigue deshabilitado hasta que se vuelve a generar o se quita.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para habilitar un índice deshabilitado, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Después de volver a generar el índice, deben volver a habilitarse manualmente las restricciones deshabilitadas debido a la deshabilitación del índice. Las restricciones PRIMARY KEY y UNIQUE se habilitan cuando se regenera el índice asociado. Este índice debe volver a generarse (habilitarse) para poder habilitar las restricciones FOREIGN KEY que hacen referencia a la restricción PRIMARY KEY o UNIQUE. Las restricciones FOREIGN KEY se habilitan con la instrucción ALTER TABLE CHECK CONSTRAINT.  
  
-   No es posible volver a generar un índice clúster deshabilitado si la opción ONLINE está establecida en ON.  
  
-   Si el índice clúster está deshabilitado o habilitado y el índice no clúster está deshabilitado, la acción del índice clúster tiene los siguientes resultados en el índice no clúster deshabilitado.  
  
    |Acción del índice clúster|Índice no clúster deshabilitado…|  
    |----------------------------|-----------------------------------|  
    |ALTER INDEX REBUILD.|Sigue deshabilitado.|  
    |ALTER INDEX ALL REBUILD.|Se vuelve a generar y se habilita.|  
    |DROP INDEX.|Sigue deshabilitado.|  
    |CREATE INDEX WITH DROP_EXISTING.|Sigue deshabilitado.|  
  
     La creación de un índice clúster se comporta igual que ALTER INDEX ALL REBUILD.  
  
-   Las acciones permitidas en índices no clúster asociados con un índice clúster dependen del estado, deshabilitado o habilitado, de ambos tipos de índice. La tabla siguiente resume las acciones permitidas en índices no clúster.  
  
    |Acción del índice no clúster|Cuando los índices clúster y no clúster están deshabilitados.|Cuando el índice clúster está habilitado y el índice no clúster está deshabilitado o habilitado.|  
    |-------------------------------|--------------------------------------------------------------------|----------------------------------------------------------------------------------------|  
    |ALTER INDEX REBUILD.|Se produce un error en la acción.|La acción se realiza correctamente.|  
    |DROP INDEX.|La acción se realiza correctamente.|La acción se realiza correctamente.|  
    |CREATE INDEX WITH DROP_EXISTING.|Se produce un error en la acción.|La acción se realiza correctamente.|  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la tabla o la vista. Si se usa DBCC DBREINDEX, el usuario debe ser el propietario de la tabla o debe ser miembro del rol fijo de servidor **sysadmin** , o de los roles fijos de base de datos **db_ddladmin** y **db_owner** .  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-enable-a-disabled-index"></a>Para habilitar un índice deshabilitado  
  
1.  En el Explorador de objetos, haga clic en el signo más para expandir la base de datos que contiene la tabla en la que desea habilitar un índice.  
  
2.  Haga clic en el signo más para expandir la carpeta **Tablas** .  
  
3.  Haga clic en el signo más para expandir la tabla en la que desea habilitar un índice.  
  
4.  Haga clic en el signo más para expandir la carpeta **Índices** .  
  
5.  Haga clic con el botón derecho en el índice que quiera habilitar y seleccione **Volver a generar**.  
  
6.  En el cuadro de diálogo **Volver a generar índices** , compruebe que el índice correcto se encuentra en la cuadrícula **Índices que se volverán a generar** y haga clic en **Aceptar**.  
  
#### <a name="to-enable-all-indexes-on-a-table"></a>Para habilitar todos los índices de una tabla  
  
1.  En el Explorador de objetos, haga clic en el signo más para expandir la base de datos que contiene la tabla en la que desea habilitar los índices.  
  
2.  Haga clic en el signo más para expandir la carpeta **Tablas** .  
  
3.  Haga clic en el signo más para expandir la tabla en la que desea habilitar los índices.  
  
4.  Haga clic con el botón derecho en la carpeta **Índices** y seleccione **Volver a generar todo**.  
  
5.  En el cuadro de diálogo **Volver a generar índices** , compruebe que los índices correctos se encuentran en la cuadrícula **Índices que se volverán a generar** y haga clic en **Aceptar**. Para quitar un índice de la cuadrícula **Índices que se volverán a generar** , seleccione el índice y, a continuación, presione la tecla SUPRIMIR.  
  
 La siguiente información está disponible en el cuadro de diálogo **Volver a generar índices** :  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-enable-a-disabled-index-using-alter-index"></a>Para habilitar un índice deshabilitado mediante ALTER INDEX  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- Enables the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table.  
  
    ALTER INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
    REBUILD;   
    GO  
    ```  
  
#### <a name="to-enable-a-disabled-index-using-create-index"></a>Para habilitar un índice deshabilitado mediante CREATE INDEX  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- re-creates the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table  
    -- using the OrganizationLevel and OrganizationNode columns  
    -- and then deletes the existing IX_Employee_OrganizationLevel_OrganizationNode index  
    CREATE INDEX IX_Employee_OrganizationLevel_OrganizationNode ON HumanResources.Employee  
       (OrganizationLevel, OrganizationNode)  
    WITH (DROP_EXISTING = ON);  
    GO  
    ```  
  
#### <a name="to-enable-a-disabled-index-using-dbcc-dbreindex"></a>Para habilitar un índice deshabilitado mediante DBCC DBREINDEX  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- enables the IX_Employee_OrganizationLevel_OrganizationNode index  
    -- on the HumanResources.Employee table  
    DBCC DBREINDEX ("HumanResources.Employee", IX_Employee_OrganizationLevel_OrganizationNode);  
    GO  
    ```  
  
#### <a name="to-enable-all-indexes-on-a-table-using-alter-index"></a>Para habilitar todos los índices de una tabla mediante ALTER INDEX  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- enables all indexes  
    -- on the HumanResources.Employee table  
    ALTER INDEX ALL ON HumanResources.Employee  
    REBUILD;  
    GO  
    ```  
  
#### <a name="to-enable-all-indexes-on-a-table-using-dbcc-dbreindex"></a>Para habilitar todos los índices de una tabla mediante DBCC DBREINDEX  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    -- enables all indexes  
    -- on the HumanResources.Employee table  
    DBCC DBREINDEX ("HumanResources.Employee", " ");  
    GO  
    ```  
  
 Para obtener más información, vea [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md), [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md), y [DBCC DBREINDEX &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md).  
  
  
