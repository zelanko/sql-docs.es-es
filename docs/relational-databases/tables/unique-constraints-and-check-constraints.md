---
title: Restricciones UNIQUE y restricciones CHECK | Microsoft Docs
ms.custom: 
ms.date: 06/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-tables
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- constraints [SQL Server], Visual Database Tools
- Visual Database Tools [SQL Server], constraints
ms.assetid: 637098af-2567-48f8-90f4-b41df059833e
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: 42a8cd2f6d94288e5f118b35f3765cd3ad7b63ce
ms.sourcegitcommit: 6b4aae3706247ce9b311682774b13ac067f60a79
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="unique-constraints-and-check-constraints"></a>Restricciones UNIQUE y restricciones CHECK
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Las restricciones UNIQUE y las restricciones CHECK son dos tipos de restricciones que se pueden usar para exigir la integridad de los datos en las tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se trata de objetos de base de datos importantes.  
  
 Este tema contiene las siguientes secciones.  
  
 [Restricciones UNIQUE](#Unique)  
  
 [Restricciones CHECK](#Check)  
  
 [Tareas relacionadas](#Tasks)  
  
##  <a name="Unique"></a> Restricciones UNIQUE  
 Las restricciones son reglas que [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] aplica de forma automática. Por ejemplo, puede usar restricciones UNIQUE para garantizar que no se escriben valores duplicados en columnas específicas que no forman parte de una clave principal. Tanto la restricción UNIQUE como la restricción PRIMARY KEY exigen la unicidad; sin embargo, debe usar la restricción UNIQUE y no PRIMARY KEY si desea exigir la unicidad de una columna o una combinación de columnas que no forman la clave principal.  
  
 A diferencia de las restricciones PRIMARY KEY, las restricciones UNIQUE permiten valores NULL. Sin embargo, de la misma forma que cualquier valor incluido en una restricción UNIQUE, solo se admite un valor NULL por columna. Es posible hacer referencia a una restricción UNIQUE con una restricción FOREIGN KEY.  
  
 Cuando se agrega una restricción UNIQUE a una o varias columnas de la tabla, de forma predeterminada, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] examina los datos existentes en las columnas para garantizar que todos los valores sean únicos. Si se agrega una restricción UNIQUE a una columna que contiene valores duplicados, [!INCLUDE[ssDE](../../includes/ssde-md.md)] devuelve un error y no agrega la restricción.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] crea automáticamente un índice UNIQUE para exigir, de acuerdo con la restricción UNIQUE, que no haya duplicados. Por lo tanto, si se intenta insertar una fila duplicada, [!INCLUDE[ssDE](../../includes/ssde-md.md)] devolverá un mensaje de error para indicar que se ha infringido la restricción UNIQUE y no se agregará la fila a la tabla. A menos que se especifique explícitamente un índice clúster, se creará de forma predeterminada un índice único, no clúster, para exigir la restricción UNIQUE.  
  
##  <a name="Check"></a> Restricciones CHECK  
 Las restricciones CHECK exigen la integridad del dominio mediante la limitación de los valores que puede aceptar una o varias columnas. Puede crear una restricción CHECK con cualquier expresión lógica (booleana) que devuelva TRUE (verdadero) o FALSE (falso) basándose en operadores lógicos. Por ejemplo, es posible limitar el intervalo de valores para una columna **salary** creando una restricción CHECK que solo permita datos entre 15 000 y 100 000 USD. Esto evita que los salarios caigan fuera del intervalo de salario normal. La expresión lógica sería la siguiente: `salary >= 15000 AND salary <= 100000`.  
  
 Puede aplicar varias restricciones CHECK a una sola columna. También puede aplicar una sola restricción CHECK a varias columnas si se crea en el nivel de la tabla. Por ejemplo, una restricción CHECK para varias columnas se podría usar para confirmar que cualquier fila con un valor **USA** en la columna **country_region** tiene también un valor de dos caracteres en la columna **state** . Así se pueden comprobar varias condiciones en un mismo sitio.  
  
 Las restricciones CHECK son similares a las restricciones FOREIGN KEY porque controlan los valores que se colocan en una columna. La diferencia reside en la forma en que determinan qué valores son válidos: las restricciones FOREIGN KEY obtienen la lista de valores válidos de otra tabla, mientras que las restricciones CHECK determinan los valores válidos a partir de una expresión lógica.  
  
> [!CAUTION]  
>  Las restricciones que incluyen la conversión de tipos de datos implícitos o explícitos pueden impedir la correcta ejecución de determinadas operaciones. Por ejemplo, las restricciones definidas en tablas que son orígenes de un cambio de partición pueden impedir que una operación ALTER TABLE...SWITCH se realice correctamente. Evite la conversión de tipos de datos en las definiciones de las restricciones.  
  
### <a name="limitations-of-check-constraints"></a>Limitaciones de las restricciones CHECK  
 Las restricciones CHECK rechazan los valores que se evalúan como FALSE. Puesto que los valores nulos se evalúan como UNKNOWN, su presencia en las expresiones puede reemplazar una restricción. Por ejemplo, supongamos que define una restricción para una columna **int** **MyColumn** , que especifica que **MyColumn** solo puede contener el valor 10 (**MyColumn=10**). Si inserta el valor NULL en **MyColumn**, [!INCLUDE[ssDE](../../includes/ssde-md.md)] inserta NULL y no devuelve un error.  
  
 Una restricción CHECK devuelve TRUE cuando la condición que está comprobando no es FALSE para ninguna fila de la tabla. Una restricción CHECK opera en el nivel de fila. Si una tabla recién creada no tiene filas, cualquier restricción CHECK en esta tabla se considerará válida. Esta situación puede generar resultados inesperados, como en el siguiente ejemplo.  
  
```  
CREATE TABLE CheckTbl (col1 int, col2 int);  
GO  
CREATE FUNCTION CheckFnctn()  
RETURNS int  
AS   
BEGIN  
   DECLARE @retval int  
   SELECT @retval = COUNT(*) FROM CheckTbl  
   RETURN @retval  
END;  
GO  
ALTER TABLE CheckTbl  
ADD CONSTRAINT chkRowCount CHECK (dbo.CheckFnctn() >= 1 );  
GO  
```  
  
 La restricción `CHECK` que se agrega especifica que como mínimo debe existir una fila en la tabla `CheckTbl`. Sin embargo, puesto que no hay filas en la tabla contra la que se comprueba la condición de esta restricción, la instrucción ALTER TABLE será correcta.  
  
 Las restricciones CHECK no se validan durante las instrucciones DELETE. Por lo tanto, la ejecución de instrucciones DELETE en las tablas con ciertos tipos de restricciones CHECK puede generar resultados inesperados. Por ejemplo, imaginemos que las siguientes instrucciones se ejecutan en la tabla `CheckTbl`.  
  
```  
INSERT INTO CheckTbl VALUES (10, 10);  
GO  
DELETE CheckTbl WHERE col1 = 10;  
```  
  
 La instrucción `DELETE` será correcta aunque la restricción `CHECK` especifique que la tabla `CheckTbl` debe tener al menos `1` fila.  
  
##  <a name="Tasks"></a> Tareas relacionadas  
  
> [!NOTE]  
>  Si se publica la tabla para la replicación, debe modificar el esquema mediante la instrucción Transact-SQL [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) o SMO (Objetos de administración de SQL Server). Si se modifica el esquema mediante el Diseñador de tablas o el Diseñador de diagramas de base de datos, se intentará eliminar la tabla y volver a crearla. No se pueden eliminar objetos publicados, por lo que la modificación del esquema generará un error.  
  
|Tarea|Tema|  
|----------|-----------|  
|Describe cómo crear una restricción UNIQUE.|[Crear restricciones UNIQUE](../../relational-databases/tables/create-unique-constraints.md)|  
|Describe cómo modificar una restricción UNIQUE.|[Modificar restricciones UNIQUE](../../relational-databases/tables/modify-unique-constraints.md)|  
|Describe cómo eliminar una restricción UNIQUE.|[Eliminar restricciones UNIQUE](../../relational-databases/tables/delete-unique-constraints.md)|  
|Describe cómo deshabilitar una restricción CHECK cuando un agente de replicación inserta o actualiza datos en una tabla.|[Deshabilitar restricciones CHECK para la replicación](../../relational-databases/tables/disable-check-constraints-for-replication.md)|  
|Describe cómo deshabilitar una restricción CHECK al agregar, actualizar o eliminar datos en una tabla.|[Deshabilitar restricciones CHECK con instrucciones INSERT y UPDATE](../../relational-databases/tables/disable-check-constraints-with-insert-and-update-statements.md)|  
|Describe cómo cambiar la expresión de restricción o las opciones que la habilitan o deshabilitan en condiciones específicas.|[Modificar restricciones CHECK](../../relational-databases/tables/modify-check-constraints.md)|  
|Describe cómo eliminar una restricción CHECK.|[Eliminar restricciones CHECK](../../relational-databases/tables/delete-check-constraints.md)|  
|Describe cómo ver las propiedades de una restricción CHECK.|[Restricciones UNIQUE y restricciones CHECK](../../relational-databases/tables/unique-constraints-and-check-constraints.md)|  
  
  
