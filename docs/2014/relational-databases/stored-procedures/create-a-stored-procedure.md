---
title: Creación de un procedimiento almacenado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- new stored procedures
- stored procedures [SQL Server], creating
- creating stored procedures
ms.assetid: 76e8a6ba-1381-4620-b356-4311e1331ca7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9aa5518ee9ebcaca287b76636d6eeea8af2f4ea5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "72796423"
---
# <a name="create-a-stored-procedure"></a>Crear un procedimiento almacenado
  En este tema se describe cómo se crea un procedimiento almacenado de [!INCLUDE[tsql](../../includes/tsql-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y la instrucción CREATE PROCEDURE de [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
##  <a name="Top"></a>   
-   **Antes de empezar:**  [Permisos](#Permissions)  
  
-   **Para crear un procedimiento con:**  [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Requiere el permiso CREATE PROCEDURE en la base de datos y el permiso ALTER en el esquema en el que se va a crear el procedimiento.  
  
##  <a name="how-to-create-a-stored-procedure"></a><a name="Procedures"></a> Crear un procedimiento almacenado  
 Puede usar cualquiera de los siguientes medios:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
 **Para crear un procedimiento en el Explorador de objetos**  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] y expándala.  
  
2.  Expanda **Bases de datos**, la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] y, por último, **Programación**.  
  
3.  Haga clic con el botón derecho en **Procedimientos almacenados**y, después, haga clic en **Nuevo procedimiento almacenado**.  
  
4.  En el menú **Consulta** , haga clic en **Especificar valores para parámetros de plantilla**.  
  
5.  En el cuadro de diálogo **Especificar valores para parámetros de plantilla** , especifique los siguientes valores para los parámetros mostrados.  
  
    |Parámetro|Value|  
    |---------------|-----------|  
    |Autor|*Su nombre.*|  
    |Create Date|*La fecha de hoy.*|  
    |Descripción|Devuelve datos de empleado.|  
    |Procedure_name|HumanResources.uspGetEmployeesTest|  
    |@Param1|@LastName|  
    |@Datatype_For_Param1|`nvarchar`(50)|  
    |Default_Value_For_Param1|NULL|  
    |@Param2|@FirstName|  
    |@Datatype_For_Param2|`nvarchar`(50)|  
    |Default_Value_For_Param2|NULL|  
  
6.  Haga clic en **OK**.  
  
7.  En el **Editor de consultas**, reemplace la instrucción SELECT por la siguiente instrucción:  
  
    ```sql  
    SELECT FirstName, LastName, Department  
    FROM HumanResources.vEmployeeDepartmentHistory  
    WHERE FirstName = @FirstName AND LastName = @LastName  
        AND EndDate IS NULL;  
    ```  
  
8.  Para probar la sintaxis, en el menú **Consulta** , haga clic en **Analizar**. Si se devuelve un mensaje de error, compare las instrucciones con la información anterior y corrija lo que sea necesario.  
  
9. Para crear el procedimiento, en el menú **Consulta** , haga clic en **Ejecutar**. El procedimiento se crea como un objeto de la base de datos.  
  
10. Para ver el procedimiento que aparece en el Explorador de objetos, haga clic con el botón derecho en **Procedimientos almacenados** y seleccione **Actualizar**.  
  
11. Para ejecutar el procedimiento, en el Explorador de objetos, haga clic con el botón derecho en el nombre del procedimiento almacenado **HumanResources.uspGetEmployeesTest** y seleccione **Ejecutar procedimiento almacenado**.  
  
12. En la ventana **Ejecutar procedimiento**, escriba Margheim como valor del parámetro @LastName y Diane como valor del parámetro @FirstName.  
  
> [!WARNING]  
>  Valide todos los datos proporcionados por el usuario. No concatene ninguna entrada de usuario antes de validarla. No ejecute nunca un comando creado a partir de una entrada de usuario no validada.  
  
###  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para crear un procedimiento en el Editor de consultas**  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En el menú **Archivo** , haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se crea el mismo procedimiento almacenado que antes con otro nombre diferente.  
  
    ```sql
    USE AdventureWorks2012;  
    GO  
    CREATE PROCEDURE HumanResources.uspGetEmployeesTest2   
        @LastName nvarchar(50),   
        @FirstName nvarchar(50)   
    AS
  
        SET NOCOUNT ON;  
        SELECT FirstName, LastName, Department  
        FROM HumanResources.vEmployeeDepartmentHistory  
        WHERE FirstName = @FirstName AND LastName = @LastName  
        AND EndDate IS NULL;  
    GO
    ```  
  
4.  Para ejecutar el procedimiento, copie y pegue el ejemplo siguiente en una nueva ventana de consulta y haga clic en **Ejecutar**. Observe que se muestran diferentes métodos para especificar los valores de parámetro.  
  
    ```sql
    EXECUTE HumanResources.uspGetEmployeesTest2 N'Ackerman', N'Pilar';  
    -- Or  
    EXEC HumanResources.uspGetEmployeesTest2 @LastName = N'Ackerman', @FirstName = N'Pilar';  
    GO  
    -- Or  
    EXECUTE HumanResources.uspGetEmployeesTest2 @FirstName = N'Pilar', @LastName = N'Ackerman';  
    GO
    ```  
  
## <a name="see-also"></a>Consulte también  
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)  
  