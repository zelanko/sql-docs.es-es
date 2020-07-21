---
title: Creación de una nueva guía de plan | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql12.swb.designer.newplanguide.f1
helpviewer_keywords:
- creating plan guides
- plan guides [SQL Server]. creating
ms.assetid: e1ad78bb-4857-40ea-a0c6-dcf5c28aef2f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 60ba31e2a63575a316db5befb397bea59c0ad1e6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066045"
---
# <a name="create-a-new-plan-guide"></a>Crear una nueva guía de plan
  Puede crear una guía de plan en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Las guías de plan influyen en la optimización de las consultas adjuntando sugerencias de consulta o un plan de consulta fijo. En la guía de plan, se especifica la instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] que se desea optimizar y además una cláusula OPTION que incluye las sugerencias de consulta que se desean utilizar o un plan de consulta específico con el que desea optimizar la consulta. Cuando la consulta se ejecuta, el optimizador de consultas hace coincidir la instrucción de [!INCLUDE[tsql](../../includes/tsql-md.md)] con la guía de plan y además asocia en tiempo de ejecución la cláusula OPTION a la consulta o utiliza el plan de consulta especificado.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para crear una guía de plan, use:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Los argumentos de sp_create_plan_guide deben indicarse en el orden que se muestra. Cuando se incluyen valores para los parámetros de `sp_create_plan_guide`, deben especificarse todos los nombres de parámetro de forma explícita, o bien no especificarse ninguno. Por ejemplo, si se especifica `@name =`, también deben especificarse `@stmt =` , `@type =`, etc. Del mismo modo, si se omite `@name =` y solo se indica el valor del parámetro, también deben omitirse los demás nombres de parámetro y solo se indicará su valor. Los nombres de argumento solo se incluyen con fines de descripción, para ayudar a entender la sintaxis. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no comprueba si el nombre del parámetro especificado coincide con el nombre del parámetro en la posición donde se utiliza.  
  
-   Puede crearse más de una guía de plan OBJECT o SQL para la misma consulta y lote o módulo. Sin embargo, en un momento dado, solo puede estar habilitada una guía de plan.  
  
-   No se pueden crear guías de plan de tipo OBJECT para un valor @module_or_batch que hace referencia a un procedimiento almacenado, una función o un desencadenador DML que especifica la cláusula WITH ENCRYPTION o que es temporal.  
  
-   Se producirá un error si se intenta quitar o modificar una función, procedimiento almacenado o desencadenador DML al que una guía de plan, habilitada o deshabilitada, haga referencia. También se producirá un error si se intenta quitar una tabla que tenga definido un desencadenador al que haga referencia una guía de plan.  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Para crear una guía de plan de tipo OBJECT se requiere el permiso ALTER en el objeto al que se hace referencia. Para crear una guía de plan de tipo SQL o TEMPLATE, se requiere el permiso ALTER en la base de datos actual.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-create-a-plan-guide"></a>Para crear una guía de plan  
  
1.  Haga clic en el signo más para expandir la base de datos en la que desea crear una guía de plan y, a continuación, haga clic en el signo más para expandir la carpeta **Programación** .  
  
2.  Haga clic con el botón derecho en la carpeta **guías de plan** y seleccione **nueva guía de plan.**...  
  
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
  
11. Haga clic en **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-create-a-plan-guide"></a>Para crear una guía de plan  
  
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
  
 Para obtener más información, vea [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql).  
  
  
