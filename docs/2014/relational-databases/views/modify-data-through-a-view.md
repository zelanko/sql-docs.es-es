---
title: Modificación de datos mediante una vista | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- data modifications [SQL Server], views
- views [SQL Server], modifying data through
- modifying data [SQL Server], views
ms.assetid: 410e2812-4ebe-48b2-b95f-c7784f1c4336
author: stevestein
ms.author: sstein
ms.openlocfilehash: df1eb4a33d1d10e63363e52760dad805b20c0a8f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85014225"
---
# <a name="modify-data-through-a-view"></a>Modificar datos mediante una vista
  Puede modificar los datos de una tabla base subyacente en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para modificar los datos de la tabla mediante una vista, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Vea la sección ''Vistas actualizables'' de [CREATE VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql).  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Requiere los permisos UPDATE, INSERT o DELETE en la tabla de destino, en función de la acción que se realizará.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-modify-table-data-through-a-view"></a>Para modificar los datos de la tabla mediante una vista  
  
1.  En el **Explorador de objetos**, expanda la base de datos que contiene la vista y, a continuación, expanda **Vistas**.  
  
2.  Haga clic con el botón derecho en la vista y seleccione **Editar las primeras 200 filas**.  
  
3.  Quizás necesite modificar la instrucción SELECT en el panel **SQL** para devolver las filas que se modificarán.  
  
4.  En el panel de **Resultados** , busque la fila que se va a cambiar o eliminar. Para eliminar la fila, haga clic con el botón derecho en ella y seleccione **Eliminar**. Para cambiar los datos de una o más columnas, modifique los datos de la columna.  
  
    > [!IMPORTANT]  
    >  No se puede eliminar una fila si la vista hace referencia a más de una tabla base. Solo pueden actualizarse las columnas que pertenecen a una única tabla base.  
  
5.  Para insertar una fila, desplácese hasta el final de las filas e inserte los nuevos valores.  
  
    > [!IMPORTANT]  
    >  No se puede insertar una fila si la vista hace referencia a más de una tabla base.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-update-table-data-through-a-view"></a>Para actualizar los datos de la tabla mediante una vista  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
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
  
 Para obtener más información, vea [UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql).  
  
#### <a name="to-insert-table-data-through-a-view"></a>Para insertar datos de tabla mediante una vista  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. El ejemplo especifica las columnas relevantes de la vista `HumanResouces.Department` para insertar una nueva fila en la tabla base `HumanResources.vEmployeeDepartmentHistory`. La instrucción se realiza correctamente porque solo se especifican las columnas de una tabla base y las demás columnas de la tabla base tienen valores predeterminados.  
  
    ```  
    USE AdventureWorks2012 ;  
    GO  
    INSERT INTO HumanResources.vEmployeeDepartmentHistory (Department, GroupName)   
    VALUES ('MyDepartment', 'MyGroup');   
    GO  
    ```  
  
 Para obtener más información, vea [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql).  
  
  
