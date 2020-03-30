---
title: Funciones definidas por el usuario | Microsoft Docs
ms.custom: ''
ms.date: 08/05/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- user-defined functions [SQL Server], components
- user-defined functions [SQL Server], about user-defined functions
- UDF
- TVF
ms.assetid: d7ddafab-f5a6-44b0-81d5-ba96425aada4
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 09fb423dc4d3685b22c67b2a86a74443633ba74a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "78370548"
---
# <a name="user-defined-functions"></a>Funciones definidas por el usuario
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  Al igual que las funciones de los lenguajes de programación, las funciones definidas por el usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son rutinas que aceptan parámetros, realizan una acción, como un cálculo complejo, y devuelven el resultado de esa acción como un valor. El valor devuelto puede ser un valor escalar único o un conjunto de resultados.  
   
##  <a name="user-defined-functions"></a><a name="Benefits"></a> Funciones definidas por el usuario  
¿Por qué usar funciones definidas por el usuario (UDF)? 
  
-   Permiten una programación modular.  
  
     Puede crear la función una vez, almacenarla en la base de datos y llamarla desde el programa tantas veces como desee. Las funciones definidas por el usuario se pueden modificar, independientemente del código de origen del programa.  
  
-   Permiten una ejecución más rápida.  
  
     Al igual que los procedimientos almacenados, las funciones definidas por el usuario [!INCLUDE[tsql](../../includes/tsql-md.md)] reducen el costo de compilación del código [!INCLUDE[tsql](../../includes/tsql-md.md)] almacenando los planes en la caché y reutilizándolos para ejecuciones repetidas. Esto significa que no es necesario volver a analizar y optimizar la función definida por el usuario con cada uso, lo que permite obtener tiempos de ejecución mucho más rápidos.  
  
     Las funciones CLR ofrecen una ventaja de rendimiento importante sobre las funciones [!INCLUDE[tsql](../../includes/tsql-md.md)] para tareas de cálculo, manipulación de cadenas y lógica empresarial. [!INCLUDE[tsql](../../includes/tsql-md.md)] se adecuan mejor a la lógica intensiva del acceso a datos.  
  
-   Pueden reducir el tráfico de red.  
  
     Una operación que filtra datos basándose en restricciones complejas que no se puede expresar en una sola expresión escalar se puede expresar como una función. La función se puede invocar luego en la cláusula WHERE para reducir el número de filas que se envían al cliente.  
  
> [!IMPORTANT]
> Las funciones definidas por el usuario de [!INCLUDE[tsql](../../includes/tsql-md.md)] en consultas solo se pueden ejecutar en un único subproceso (plan de ejecución en serie). Por tanto, el uso de UDF impide el procesamiento de consultas en paralelo. Para obtener más información sobre el procesamiento de consultas en paralelo, vea la [Guía de arquitectura de procesamiento de consultas](../../relational-databases/query-processing-architecture-guide.md#parallel-query-processing).
  
##  <a name="types-of-functions"></a><a name="FunctionTypes"></a> Tipos de funciones  
**Función escalar**  
 Las funciones escalares definidas por el usuario devuelven un único valor de datos del tipo definido en la cláusula RETURNS. En una función escalar insertada, el valor escalar es el resultado de una sola instrucción. Para una función escalar de varias instrucciones, el cuerpo de la función puede contener una serie de instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] que devuelven el único valor. El tipo devuelto puede ser de cualquier tipo de datos excepto **text**, **ntext**, **image**, **cursor**y **timestamp**. 
 **[Ejemplos.](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#Scalar)**
  
**Funciones con valores de tabla**  
 Las funciones con valores de tabla definidas por el usuario devuelven un tipo de datos **table** . Las funciones insertada con valores de tabla no tienen cuerpo; la tabla es el conjunto de resultados de una sola instrucción SELECT. **[Ejemplos.](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF)**
  
**Funciones del sistema**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona numerosas funciones del sistema que se pueden usar para realizar diversas operaciones. No se pueden modificar. Para obtener más información, vea [Funciones integradas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md), [Funciones almacenadas del sistema &#40;Transact-SQL&#41;](~/relational-databases/system-functions/system-functions-category-transact-sql.md) y [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
##  <a name="guidelines"></a><a name="Guidelines"></a> Instrucciones  
 Los errores de [!INCLUDE[tsql](../../includes/tsql-md.md)] que producen la cancelación de una instrucción y continúan con la siguiente instrucción del módulo (como desencadenadores o procedimientos almacenados) se tratan de forma distinta dentro de una función. En las funciones, estos errores hacen que se detenga la ejecución de la función. Esto hace que se cancele la función que invocó la instrucción.  
  
 Las instrucciones de un bloque `BEGIN...END` no pueden producir efectos secundarios. Los efectos secundarios de una función son cambios definitivos del estado de un recurso que está fuera del ámbito de la función, como una modificación de una tabla de base de datos. Los únicos cambios que pueden realizar las instrucciones de la función son cambios en objetos locales de la función, como cursores o variables locales. En una función no se pueden llevar a cabo algunas acciones como, por ejemplo, modificar tablas de base de datos, realizar operaciones en cursores no locales de la función, enviar correo electrónico, intentar modificar un catálogo o generar un conjunto de resultados que se devuelve al usuario.  
  
> [!NOTE]
> Si una instrucción `CREATE FUNCTION` genera efectos secundarios sobre recursos que no existen en el momento que se emite la instrucción `CREATE FUNCTION`, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ejecuta la instrucción. Sin embargo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no ejecuta la función cuando ésta se invoca.  
  
 El número de veces que se ejecuta realmente una función especificada en una consulta puede variar entre los planes de ejecución generados por el optimizador. Un ejemplo es una función invocada por una subconsulta en una cláusula `WHERE`. El número de veces que se ejecuta la subconsulta y su función puede variar con diferentes rutas de acceso seleccionadas por el optimizador.  
 
> [!IMPORTANT]   
> Para obtener más información y consideraciones de rendimiento sobre las funciones definidas por el usuario, vea [Crear funciones definidas por el usuario &#40;motor de base de datos&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md). 
  
##  <a name="valid-statements-in-a-function"></a><a name="ValidStatements"></a> Instrucciones válidas en una función  
Entre los tipos de instrucciones válidos en una función se incluyen:  
  
-   Las instrucciones `DECLARE` se pueden usar para definir variables y cursores de datos locales de la función.  
  
-   La asignación de valores a objetos locales de la función, como el uso de `SET` para asignar valores a variables locales escalares y de tabla.  
  
-   Las operaciones de cursores que hacen referencia a cursores locales que están declarados, abiertos, cerrados y no asignados en la función. No se admiten las instrucciones `FETCH` que devuelven datos al cliente. Solo se permiten las instrucciones FETCH que asignan valores a variables locales mediante la cláusula `INTO`.  
  
-   Instrucciones de control de flujo excepto instrucciones `TRY...CATCH`.  
  
-   Instrucciones `SELECT` que contienen listas de selección con expresiones que asignan valores a las variables locales para la función.  
  
-   Instrucciones `UPDATE`, `INSERT` y `DELETE` que modifican las variables de tabla locales de la función.  
  
-   Instrucciones `EXECUTE` que llaman a un procedimiento almacenado extendido.  
  
### <a name="built-in-system-functions"></a>Funciones del sistema integradas  
 Las siguientes funciones integradas no deterministas se pueden usar en funciones Transact-SQL definidas por el usuario.  
  
|||  
|-|-|  
|CURRENT_TIMESTAMP|@@MAX_CONNECTIONS|  
|GET_TRANSMISSION_STATUS|@@PACK_RECEIVED|  
|GETDATE|@@PACK_SENT|  
|GETUTCDATE|@@PACKET_ERRORS|  
|@@CONNECTIONS|@@TIMETICKS|  
|@@CPU_BUSY|@@TOTAL_ERRORS|  
|@@DBTS|@@TOTAL_READ|  
|@@IDLE|@@TOTAL_WRITE|  
|@@IO_BUSY||  
  
 Las siguientes funciones integradas no deterministas **no** se pueden usar en funciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] definidas por el usuario.  
  
|||  
|-|-|  
|NEWID|RAND|  
|NEWSEQUENTIALID|TEXTPTR|  
  
 Para consultar una lista de las funciones de sistema integradas deterministas y no deterministas, vea [Funciones deterministas y no deterministas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
##  <a name="schema-bound-functions"></a><a name="SchemaBound"></a> Funciones enlazadas a esquema  
 `CREATE FUNCTION` admite una cláusula `SCHEMABINDING` que enlaza la función con el esquema de cualquier objeto al que haga referencia, como tablas, vistas y otras funciones definidas por el usuario. Se producen errores al intentar modificar o quitar objetos a los que hace referencia una función enlazada con un esquema.  
  
 Para poder especificar `SCHEMABINDING` en [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md) se deben cumplir estas condiciones:  
  
-   Todas las vistas y las funciones definidas por el usuario a las que hace referencia la función deben estar enlazadas con un esquema.  
  
-   Todos los objetos a los que hace referencia la función deben encontrarse en la misma base de datos que la función. Se debe hacer referencia a los objetos mediante nombres de una o dos partes.  
  
-   Se debe disponer de permisos `REFERENCES` en todos los objetos (tablas, vistas y funciones definidas por el usuario) a los que hace referencia la función.  
  
 Se puede usar `ALTER FUNCTION` para quitar el enlace con el esquema. La instrucción `ALTER FUNCTION` debe volver a definir la función sin especificar `WITH SCHEMABINDING`.  
  
##  <a name="specifying-parameters"></a><a name="Parameters"></a> Especificar parámetros  
 Una función definida por el usuario tiene de cero a varios parámetros de entrada y devuelve un valor escalar o una tabla. Una función puede tener un máximo de 1024 parámetros de entrada. Cuando un parámetro de la función tiene un valor predeterminado, debe especificarse la palabra clave DEFAULT al llamar a la función para poder obtener el valor predeterminado. Este comportamiento es diferente del de los parámetros con valores predeterminados de procedimientos almacenados definidos por el usuario, para los cuales omitir el parámetro implica especificar el valor predeterminado. Las funciones definidas por el usuario no admiten parámetros de salida.  
  
##  <a name="more-examples"></a><a name="Tasks"></a> Más ejemplos  
  
|||  
|-|-|  
|**Descripción de la tarea**|**Tema.**|  
|Describe cómo se crea una función Transact-SQL definida por el usuario.|[Crear funciones definidas por el usuario &#40;motor de base de datos&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)|  
|Describe cómo se crea una función CLR.|[Crear funciones CLR](../../relational-databases/user-defined-functions/create-clr-functions.md)|  
|Describe cómo se crea una función de agregado definida por el usuario|[Crear funciones de agregado definidas por el usuario](../../relational-databases/user-defined-functions/create-user-defined-aggregates.md)|  
|Describe cómo se modifica una función Transact-SQL definida por el usuario.|[Modificar funciones definidas por el usuario](../../relational-databases/user-defined-functions/modify-user-defined-functions.md)|  
|Describe cómo se elimina una función definida por el usuario.|[Eliminar funciones definidas por el usuario](../../relational-databases/user-defined-functions/delete-user-defined-functions.md)|  
|Describe cómo se ejecuta una función definida por el usuario.|[Ejecutar funciones definidas por el usuario](../../relational-databases/user-defined-functions/execute-user-defined-functions.md)|  
|Describe cómo se cambia el nombre de una función definida por el usuario.|[Cambiar el nombre de las funciones definidas por el usuario](../../relational-databases/user-defined-functions/rename-user-defined-functions.md)|  
|Describe cómo puede ver la definición de una función definida por el usuario.|[Ver funciones definidas por el usuario](../../relational-databases/user-defined-functions/view-user-defined-functions.md)|  
  
  
