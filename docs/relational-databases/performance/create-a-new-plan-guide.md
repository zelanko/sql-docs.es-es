---
title: "Creación de una nueva guía de plan | Microsoft Docs"
ms.custom: 
ms.date: 08/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-plan-guides
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.designer.newplanguide.f1
helpviewer_keywords:
- creating plan guides
- plan guides [SQL Server]. creating
ms.assetid: e1ad78bb-4857-40ea-a0c6-dcf5c28aef2f
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c0cc530e59007070fba228c06a4f8f2983faa3f3
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="create-a-new-plan-guide"></a>Crear una nueva guía de plan
Las guías de plan influyen en la optimización de las consultas adjuntando sugerencias de consulta o un plan de consulta fijo. En la guía de plan, se especifica la instrucción que se desea optimizar y una cláusula OPTION que contiene sugerencias de consulta que desea utilizar. o un plan de consulta específico que desea usar para optimizar la consulta. Cuando la consulta se ejecuta, el optimizador de consultas hace coincidir la instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] con la guía de plan y además asocia en tiempo de ejecución la cláusula OPTION a la consulta o utiliza el plan de consulta especificado.  

Una guía de plan aplica un plan de consulta fijo, y/o sugerencias de consulta, a una consulta.
  
##  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Los argumentos de sp_create_plan_guide deben indicarse en el orden que se muestra. Cuando se incluyen valores para los parámetros de **sp_create_plan_guide**, deben especificarse todos los nombres de parámetro de forma explícita, o bien no especificarse ninguno. Por ejemplo, si se especifica **@name =**, también deben especificarse **@stmt =** , **@type =**, etc. Del mismo modo, si se omite **@name =** y solo se indica el valor del parámetro, también deben omitirse los demás nombres de parámetro y solo se indicará su valor. Los nombres de argumento solo se incluyen con fines de descripción, para ayudar a entender la sintaxis. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no comprueba si el nombre del parámetro especificado coincide con el nombre del parámetro en la posición donde se utiliza.  
  
-   Puede crearse más de una guía de plan OBJECT o SQL para la misma consulta y lote o módulo. Sin embargo, en un momento dado, solo puede estar habilitada una guía de plan.  
  
-   No se pueden crear guías de plan de tipo OBJECT para un valor @module_or_batch que hace referencia a un procedimiento almacenado, una función o un desencadenador DML que especifica la cláusula WITH ENCRYPTION o que es temporal.  
  
-   Se producirá un error si se intenta quitar o modificar una función, procedimiento almacenado o desencadenador DML al que una guía de plan, habilitada o deshabilitada, haga referencia. También se producirá un error si se intenta quitar una tabla que tenga definido un desencadenador al que haga referencia una guía de plan.  
 
  
##  <a name="Permissions"></a> Permissions  
 Para crear una guía de plan de tipo OBJECT necesita el permiso ALTER en el objeto al que se hace referencia. Para crear una guía de plan de tipo SQL o TEMPLATE necesita el permiso ALTER en la base de datos actual.  
  
##  <a name="SSMSProcedure"></a> Creación de una guía de plan mediante SSMS  

 
1.  Haga clic en el signo más para expandir la base de datos en la que desea crear una guía de plan y, a continuación, haga clic en el signo más para expandir la carpeta **Programación** .  
  
2.  Haga clic con el botón derecho en la carpeta **Guías de plan** y seleccione **Nueva guía de plan…**.
![select_plan_guide](../../relational-databases/performance/media/select-plan-guide.png)
  
3.  En el cuadro de diálogo **Nueva guía de plan** , en el cuadro **Nombre** , escriba el nombre de la guía de plan.  
  
4.  En el cuadro **Instrucción** , escriba la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] con la que se aplicará la guía de plan.  
  
5.  En la lista **Tipo de ámbito** , seleccione el tipo de entidad en el que aparecerá la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] . Así se especifica el contexto para hacer coincidir la instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] con la guía de plan. Los valores posibles son **OBJECT**, **SQL**y **TEMPLATE**.  
  
6.  En el cuadro **Lote de ámbito** , escriba el texto del lote en el que aparecerá la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] . El texto del lote no puede incluir una instrucción USE``*database* . El cuadro **Lote de ámbito** solo está disponible cuando **SQL** se ha seleccionado como tipo de ámbito. Si no escribe nada en el cuadro Lote de ámbito cuando SQL es el tipo de ámbito, el valor del texto del lote se establece en el mismo valor que está en el cuadro **Instrucción** .  
  
7.  En la lista **Nombre de esquema de ámbito** , escriba el nombre del esquema en el que está contenido el objeto. El cuadro **Nombre de esquema de ámbito** solo está disponible cuando se ha seleccionado **Objeto** como tipo de ámbito.  
  
8.  En el cuadro **Nombre de objeto de ámbito** , escriba el nombre del procedimiento almacenado [!INCLUDE[tsql](../../includes/tsql-md.md)] , la función escalar definida por el usuario, la función con valores de tabla de múltiples instrucciones o el desencadenador DML en el que aparece la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] . El cuadro **Nombre de objeto de ámbito** solo está disponible cuando se ha seleccionado **Objeto** como tipo de ámbito.  
  
9. En el cuadro **Parámetros** , escriba el nombre de parámetro y el tipo de datos de todos los parámetros incrustados en la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
     Solo se aplican los parámetros si se da una de las dos siguientes condiciones:  
  
    -   El tipo de ámbito es **SQL** o **TEMPLATE**. Si es **TEMPLATE**, los parámetros no deben ser NULL.  
  
    -   La instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] se envía mediante sp_executesql y se especifica un valor para el parámetro, o bien [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] envía internamente una instrucción después del proceso de parametrización.  
  
10. En el cuadro **Sugerencias** , escriba las sugerencias de consulta o el plan de consulta que se va a aplicar a la instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] . Para especificar una o varias sugerencias de consulta, escriba una cláusula OPTION válida.  
  
11. Haga clic en **Aceptar**.  

![plan_guide](../../relational-databases/performance/media/plan-guide.png)  

  
##  <a name="TsqlProcedure"></a> Creación de una guía de plan mediante T-SQL  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**.  
  
    ```  
    -- creates a plan guide named Guide1 based on a SQL statement  
    EXEC sp_create_plan_guide   
        @name = N'Guide1',   
        @stmt = N'SELECT TOP 1 *   
                  FROM Sales.SalesOrderHeader   
                  ORDER BY OrderDate DESC',   
        @type = N'SQL',  
        @module_or_batch = NULL,   
        @params = NULL,   
        @hints = N'OPTION (MAXDOP 1)';  
  
    ```  
  
 Para obtener más información, vea [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md).  
  
  

