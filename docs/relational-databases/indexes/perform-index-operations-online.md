---
title: "Realización de operaciones de índice en línea | Microsoft Docs"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- index online operations [SQL Server]
- online index operations
- ONLINE option
ms.assetid: 1e43537c-bf67-4db3-9908-3cb45c6fdaa1
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7be8dd139a8c377d67259df538b097f1337821ca
ms.lasthandoff: 04/11/2017

---
# <a name="perform-index-operations-online"></a>Realizar operaciones de índice en línea
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  En este tema se describe cómo crear, volver a generar o quitar índices en línea en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Gracias a la opción ONLINE, es posible que usuarios simultáneos obtengan acceso a los datos de la tabla subyacente o del índice clúster, así como a los índices no clúster asociados durante estas operaciones de índices. Por ejemplo, cuando un usuario vuelve a generar un índice clúster, dicho usuario y los demás pueden seguir actualizando los datos subyacentes y realizando consultas sobre los mismos. Al realizar operaciones DDL (lenguaje de definición de datos) sin conexión, como generar o volver a generar un índice clúster, estas operaciones mantienen bloqueos exclusivos de los datos subyacentes y los índices asociados. Es un modo de evitar modificaciones de los datos subyacentes y consultas sobre los mismos hasta que no finalice la operación de índice.  
  
> [!NOTE]  
>  Las operaciones de índices en línea no están disponibles en todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, vea Características compatibles con las ediciones de SQL Server 2016.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para volver a generar un índice en línea, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Se recomienda realizar operaciones de índices en línea en entornos empresariales que funcionan 24 horas al día, siete días a la semana, y en los que resulta fundamental la actividad simultánea de los usuarios durante las operaciones de índices.  
  
-   La opción ONLINE está disponible en las siguientes instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
    -   [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)  
  
    -   [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)  
  
    -   [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md)  
  
    -   [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) (para agregar o quitar restricciones UNIQUE o PRIMARY KEY con la opción de índice CLUSTERED)  
  
-   Para conocer más limitaciones y restricciones relacionadas con la creación, nueva generación o eliminación de índices en línea, vea [Directrices para operaciones de índices en línea](../../relational-databases/indexes/guidelines-for-online-index-operations.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en la tabla o la vista.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-rebuild-an-index-online"></a>Para volver a generar un índice en línea  
  
1.  En el Explorador de objetos, haga clic en el signo más para expandir la base de datos que contiene la tabla en la que desea volver a generar un índice en línea.  
  
2.  Expanda la carpeta **Tablas** .  
  
3.  Haga clic en el signo más para expandir la tabla en la que desea volver a generar un índice en línea.  
  
4.  Expanda la carpeta **Índices** .  
  
5.  Haga clic con el botón derecho en el índice que quiere volver a generar en línea y seleccione **Propiedades**.  
  
6.  Debajo de **Seleccionar una página**, seleccione **Opciones**.  
  
7.  Seleccione **Permitir procesamiento DML en línea**y, a continuación, seleccione **True** en la lista.  
  
8.  Haga clic en **Aceptar**.  
  
9. Haga clic con el botón derecho en el índice que quiere volver a generar en línea y seleccione **Volver a generar**.  
  
10. En el cuadro de diálogo **Volver a generar índices** , compruebe que el índice correcto se encuentra en la cuadrícula **Índices que se volverán a generar** y haga clic en **Aceptar**.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
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
  
     [!code-sql[IndexDDL#DropIndex4](../../relational-databases/indexes/codesnippet/tsql/perform-index-operations_1.sql)]  
  
 Para obtener más información, vea [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
  

