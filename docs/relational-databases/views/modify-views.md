---
title: "Modificación de vistas | Microsoft Docs"
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
- views [SQL Server], renaming
- views [SQL Server], modifying
- modifying views
- renaming views
ms.assetid: 2d3c14dc-43e5-4324-b8fb-f2692d330b16
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 242d7b946699560cf24c59a262e3a14a5c08b8d9
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="modify-views"></a>Modificar vistas
  Después de definir una vista, puede cambiar su definición en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] sin tener que quitarla y volverla a crear si usa [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para modificar una vista, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   La modificación de una vista no afecta a los objetos dependientes, como pueden ser los procedimientos almacenados o los desencadenadores, a menos que la definición de la vista cambie de tal modo que el objeto dependiente deje de ser válido.  
  
-   Si una vista que está actualmente en uso se modifica mediante ALTER VIEW, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] impone un bloqueo exclusivo de esquema sobre la vista. Cuando se concede el bloqueo, y no hay usuarios activos de la vista, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] elimina todas las copias de la vista de la caché de procedimientos. Los planes existentes que hacen referencia a la vista permanecen en la caché, pero se vuelven a compilar cuando se llaman.  
  
-   ALTER VIEW se puede aplicar a vistas indizadas; no obstante, quita incondicionalmente todos los índices de la vista.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Para ejecutar ALTER VIEW, como mínimo, se necesita el permiso ALTER en OBJECT.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-modify-a-view"></a>Para modificar una vista  
  
1.  En el **Explorador de objetos**, haga clic en el signo más situado junto a la base de datos donde se encuentra la vista y, a continuación, haga clic en el signo más situado junto a la carpeta **Vistas** .  
  
2.  Haga clic con el botón derecho en la vista que quiere modificar y seleccione **Diseño**.  
  
3.  En el panel de diagrama del Diseñador de consultas, realice los cambios a la vista en una o más de las siguientes maneras:  
  
    1.  Active o desactive las casillas de cualquier elemento que desee agregar o quitar.  
  
    2.  Haga clic con el botón derecho en el panel de diagrama, seleccione **Agregar tabla**y, luego, las columnas adicionales que quiere agregar a la vista del cuadro de diálogo **Agregar tabla** .  
  
    3.  Haga clic con el botón derecho en la barra de título de la tabla que quiere quitar y seleccione **Quitar**.  
  
4.  En el menú **Archivo** , haga clic en **Guardar***view name*.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-modify-a-view"></a>Para modificar una vista  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. El ejemplo crea primero una vista y luego la modifica mediante ALTER VIEW. La cláusula WHERE se agrega a la definición de la vista.  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    -- Create a view.  
    CREATE VIEW HumanResources.EmployeeHireDate  
    AS  
    SELECT p.FirstName, p.LastName, e.HireDate  
    FROM HumanResources.Employee AS e JOIN Person.Person AS  p  
    ON e.BusinessEntityID = p.BusinessEntityID ;   
  
    -- Modify the view by adding a WHERE clause to limit the rows returned.  
    ALTER VIEW HumanResources.EmployeeHireDate  
    AS  
    SELECT p.FirstName, p.LastName, e.HireDate  
    FROM HumanResources.Employee AS e JOIN Person.Person AS  p  
    ON e.BusinessEntityID = p.BusinessEntityID  
    WHERE HireDate < CONVERT(DATETIME,'20020101',101) ;   
    GO  
    ```  
  
 Para obtener más información, vea [ALTER VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/alter-view-transact-sql.md).  
  
  
