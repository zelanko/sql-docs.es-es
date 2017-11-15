---
title: "Modificación de datos mediante una vista | Microsoft Docs"
ms.custom: 
ms.date: 10/05/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-views
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data modifications [SQL Server], views
- views [SQL Server], modifying data through
- modifying data [SQL Server], views
ms.assetid: 410e2812-4ebe-48b2-b95f-c7784f1c4336
caps.latest.revision: "35"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: a7ffd77db6d7d3d68e52ce423b206d84d002d0c5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="modify-data-through-a-view"></a>Modificar datos mediante una vista
  Puede modificar los datos de una tabla base subyacente en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Vea la sección ''Vistas actualizables'' de [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md).  
  
  
###  <a name="Permissions"></a> Permisos  
 Requiere los permisos UPDATE, INSERT o DELETE en la tabla de destino, en función de la acción que se realizará.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-modify-table-data-through-a-view"></a>Para modificar los datos de la tabla mediante una vista  
  
1.  En el **Explorador de objetos**, expanda la base de datos que contiene la vista y, a continuación, expanda **Vistas**.  
  
2.  Haga clic con el botón derecho en la vista y seleccione **Editar las primeras 200 filas**.  
  
3.  Quizás necesite modificar la instrucción SELECT en el panel **SQL** para devolver las filas que se modificarán.  
  
4.  En el panel de **Resultados** , busque la fila que se va a cambiar o eliminar. Para eliminar la fila, haga clic con el botón derecho en ella y seleccione **Eliminar**. Para cambiar los datos de una o más columnas, modifique los datos de la columna.  
  
    > **IMPORTANTE:** No se puede eliminar una fila si la vista hace referencia a más de una tabla base. Solo pueden actualizarse las columnas que pertenecen a una única tabla base.  
  
5.  Para insertar una fila, desplácese hasta el final de las filas e inserte los nuevos valores.  
  
    > **IMPORTANTE:** No se puede insertar una fila si la vista hace referencia a más de una tabla base.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-update-table-data-through-a-view"></a>Para actualizar los datos de la tabla mediante una vista  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. Este ejemplo cambia el valor de las columnas `StartDate` y `EndDate` de un empleado concreto mediante referencias a columnas de la vista `HumanResources.vEmployeeDepartmentHistory`. Esta vista devuelve valores de dos tablas. Esta instrucción se realiza correctamente porque las columnas que se modificaron solo provienen de una de las tablas base.  
  
    ```  
    USE AdventureWorks2012 ;   
    GO  
    UPDATE HumanResources.vEmployeeDepartmentHistory  
    SET StartDate = '20110203', EndDate = GETDATE()   
    WHERE LastName = N'Smith' AND FirstName = 'Samantha';   
    GO  
    ```  
  
 Para obtener más información, vea [UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md).  
  
#### <a name="to-insert-table-data-through-a-view"></a>Para insertar datos de tabla mediante una vista  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. El ejemplo especifica las columnas relevantes de la vista `HumanResouces.Department` para insertar una nueva fila en la tabla base `HumanResources.vEmployeeDepartmentHistory`. La instrucción se realiza correctamente porque solo se especifican las columnas de una tabla base y las demás columnas de la tabla base tienen valores predeterminados.  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    INSERT INTO HumanResources.vEmployeeDepartmentHistory (Department, GroupName)   
    VALUES ('MyDepartment', 'MyGroup');   
    GO  
    ```  
  
 Para obtener más información, vea [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md).  
  
  
