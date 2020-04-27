---
title: Realización de operaciones de índice en línea | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index online operations [SQL Server]
- online index operations
- ONLINE option
ms.assetid: 1e43537c-bf67-4db3-9908-3cb45c6fdaa1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b9eceaff8ea7fee16eac3afef8bdc560d7fb1642
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63036227"
---
# <a name="perform-index-operations-online"></a>Realizar operaciones de índice en línea
  En este tema se describe cómo crear, volver a generar o quitar índices en línea en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Gracias a la opción ONLINE, es posible que usuarios simultáneos obtengan acceso a los datos de la tabla subyacente o del índice clúster, así como a los índices no clúster asociados durante estas operaciones de índices. Por ejemplo, cuando un usuario vuelve a generar un índice clúster, dicho usuario y los demás pueden seguir actualizando los datos subyacentes y realizando consultas sobre los mismos. Al realizar operaciones DDL (lenguaje de definición de datos) sin conexión, como generar o volver a generar un índice clúster, estas operaciones mantienen bloqueos exclusivos de los datos subyacentes y los índices asociados. Es un modo de evitar modificaciones de los datos subyacentes y consultas sobre los mismos hasta que no finalice la operación de índice.  
  
> [!NOTE]  
>  Las operaciones de índices en línea no están disponibles en todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, vea [características compatibles con las ediciones de SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para volver a generar un índice en línea, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Se recomienda realizar operaciones de índices en línea en entornos empresariales que funcionan 24 horas al día, siete días a la semana, y en los que resulta fundamental la actividad simultánea de los usuarios durante las operaciones de índices.  
  
-   La opción ONLINE está disponible en las siguientes instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
    -   [CREATE INDEX](/sql/t-sql/statements/create-index-transact-sql)  
  
    -   [ALTER INDEX](/sql/t-sql/statements/alter-index-transact-sql)  
  
    -   [DROP INDEX](/sql/t-sql/statements/drop-index-transact-sql)  
  
    -   [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql) (para agregar o quitar restricciones UNIQUE o PRIMARY KEY con la opción de índice CLUSTERED)  
  
-   Para conocer más limitaciones y restricciones relacionadas con la creación, nueva generación o eliminación de índices en línea, vea [Directrices para operaciones de índices en línea](guidelines-for-online-index-operations.md).  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la tabla o la vista.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-rebuild-an-index-online"></a>Para volver a generar un índice en línea  
  
1.  En el Explorador de objetos, haga clic en el signo más para expandir la base de datos que contiene la tabla en la que desea volver a generar un índice en línea.  
  
2.  Expanda la carpeta **Tablas** .  
  
3.  Haga clic en el signo más para expandir la tabla en la que desea volver a generar un índice en línea.  
  
4.  Expanda la carpeta **Índices** .  
  
5.  Haga clic con el botón derecho en el índice que quiere volver a generar en línea y seleccione **Propiedades**.  
  
6.  Debajo de **Seleccionar una página**, seleccione **Opciones**.  
  
7.  Seleccione **Permitir procesamiento DML en línea**y, a continuación, seleccione **True** en la lista.  
  
8.  Haga clic en **OK**.  
  
9. Haga clic con el botón derecho en el índice que quiere volver a generar en línea y seleccione **Volver a generar**.  
  
10. En el cuadro de diálogo **Volver a generar índices** , compruebe que el índice correcto se encuentra en la cuadrícula **Índices que se volverán a generar** y haga clic en **Aceptar**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-create-rebuild-or-drop-an-index-online"></a>Para crear, volver a generar o quitar un índice en línea  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En el ejemplo se vuelve a generar un índice en línea existente.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER INDEX AK_Employee_NationalIDNumber ON HumanResources.Employee  
    REBUILD WITH (ONLINE = ON);  
    GO  
    ```  
  
     En el ejemplo siguiente se elimina un índice clúster en línea y se mueve la tabla resultante (montón) al grupo de archivos `NewGroup` mediante la cláusula `MOVE TO` . Las vistas de catálogo `sys.indexes`, `sys.tables`y `sys.filegroups` se consultan para comprobar la ubicación del índice y la tabla en los grupos de archivos antes y después del desplazamiento.  
  
     [!code-sql[IndexDDL#DropIndex4](../../snippets/tsql/SQL14/tsql/indexddl/transact-sql/dropindex.sql#dropindex4)]  
  
 Para obtener más información, vea [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql).  
  
  
