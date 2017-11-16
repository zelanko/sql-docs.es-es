---
title: Seguridad de nivel de fila | Microsoft Docs
ms.custom: SQL2016_New_Updated
ms.date: 03/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- access control predicates
- row level security
- security [SQL Server], predicate based access control
- row level security described
- predicate based security
ms.assetid: 7221fa4e-ca4a-4d5c-9f93-1b8a4af7b9e8
caps.latest.revision: "47"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.openlocfilehash: 809eed1ae84297eb6c8bd04716054660f70a0ee3
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="row-level-security"></a>Seguridad de nivel de fila
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  ![Gráfico de seguridad de nivel de fila](../../relational-databases/security/media/row-level-security-graphic.png "Gráfico de seguridad de nivel de fila")  
  
 La seguridad de nivel de fila permite a los clientes controlar el acceso a las filas de una tabla de base de datos según las características del usuario que ejecuta una consulta (por ejemplo, pertenencia a grupos o contexto de ejecución).  
  
 La seguridad de nivel de fila (RLS) simplifica el diseño y la codificación de la seguridad de la aplicación. RLS permite implementar restricciones en el acceso a las filas de datos. Por ejemplo, garantizar que los trabajadores puedan acceder solo a las filas de datos pertinentes para su departamento o restringir el acceso a los datos de un cliente solo a los datos relevantes para su empresa.  
  
 La lógica de la restricción de acceso está ubicada en el nivel de base de datos en lugar de estar alejado de los datos en otro nivel de aplicación. El sistema de base de datos aplica las restricciones de acceso cada vez que se intenta acceder a los datos desde cualquier nivel. Esto hace que el sistema de seguridad sea más sólido y confiable ya que reduce la superficie del sistema de seguridad.  
  
 Implementar RLS con la instrucción de [CREATE SECURITY POLICY](../../t-sql/statements/create-security-policy-transact-sql.md)[!INCLUDE[tsql](../../includes/tsql-md.md)] y los predicados creados como [funciones Inline con valores de tabla](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md).  
  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([Obtenerla](http://azure.micosoft.com/documentation/articles/sql-database-preview-whats-new/?WT.mc_id=TSQL_GetItTag)).  
  

##  <a name="Description"></a> Descripción  
 RLS admite dos tipos de predicados de seguridad.  
  
-   Los predicados de filtro filtran en modo silencioso las filas disponibles para leer operaciones (SELECT, UPDATE y DELETE).  
  
-   Los predicados de bloqueo bloquean explícitamente las operaciones de escritura (AFTER INSERT, AFTER UPDATE, BEFORE UPDATE, BEFORE DELETE) que infringen el predicado.  
  
 El acceso a los datos de nivel de fila de una tabla está restringido por un predicado de seguridad que se define como una función con valores de tabla insertada. Luego, la función se invoca y una directiva de seguridad la aplica. En el caso de los predicados de filtro, no hay ninguna indicación para la aplicación de que se han filtrado filas del conjunto de resultados; si se filtran todas las filas, se devolverá un conjunto nulo. En el caso de los predicados de bloqueo, las operaciones que infrinjan el predicado generarán un error.  
  
 Los predicados de filtro se aplican al leer los datos de la tabla base y afectan a todas las operaciones get: **SELECT**, **DELETE** (por ejemplo, el usuario no puede eliminar las filas filtradas) y **UPDATE** (por ejemplo, el usuario no puede actualizar las filas filtradas, aunque es posible actualizar las filas de modo que se filtren posteriormente). Los predicados de bloqueo afectan a todas las operaciones de escritura.  
  
-   Los predicados AFTER INSERT y AFTER UPDATE pueden impedir que los usuarios actualicen las filas con valores que infrinjan el predicado.  
  
-   Los predicados BEFORE UPDATE pueden impedir que los usuarios actualicen las filas que actualmente infrinjan el predicado.  
  
-   Los predicados BEFORE DELETE pueden bloquear las operaciones de eliminación.  
  
 Los predicados de filtro y de bloqueo y las directivas de seguridad tienen el siguiente comportamiento:  
  
-   Puede definir una función de predicado que se combine con otra tabla o invoque una función. Si la directiva de seguridad se crea con `SCHEMABINDING = ON`, entonces se puede acceder a la función o combinación desde la consulta y funciona como se espera sin comprobaciones de permisos adicionales. Si la directiva de seguridad se crea con `SCHEMABINDING = OFF`, entonces los usuarios necesitarán los permisos **SELECT** o **EXECUTE** en estas funciones y tablas adicionales para consultar la tabla de destino.
  
-   Puede emitir una consulta a una tabla que tenga un predicado de seguridad definido pero deshabilitado. Todas las filas que se habrían filtrado o bloqueado no se ven afectadas.  
  
-   Si el usuario dbo, un miembro del rol **db_owner** o las consultas del propietario de la tabla en una tabla que tiene una directiva de seguridad definida y habilitada, las filas se filtran o bloquean según indique la directiva de seguridad.  
  
-   Los intentos de modificar el esquema de una tabla enlazada por una directiva de seguridad enlazada a un esquema producirán un error. Sin embargo, se pueden modificar las columnas a las que el predicado no hace referencia.  
  
-   Los intentos de agregar un predicado a una tabla que ya tiene uno definido para la operación especificada (independientemente de si está habilitado o deshabilitado) producen un error.  
  
-   En el caso de las directivas de seguridad enlazadas a un esquema, los intentos de modificar una función que se usa como predicado en una tabla dentro de los resultados de la directiva de seguridad producen un error.  
  
-   Definir varias directivas de seguridad activas que contienen predicados no superpuestos, será correcto.  
  
 Los predicados de filtro tienen el siguiente comportamiento:  
  
-   Definir una directiva de seguridad que filtre las filas de una tabla. La aplicación no es consciente de que las filas se han filtrado para las operaciones **SELECT**, **UPDATE**y **DELETE** , incluidas las situaciones en las que se han filtrado todas las filas. La aplicación puede **INSERT** cualquier fila, independientemente de si se filtrarán o no durante cualquier otra operación.  
  
 Los predicados de bloqueo tienen el siguiente comportamiento:  
  
-   Los predicados de bloqueo para UPDATE se dividen en operaciones independientes para BEFORE y AFTER. En consecuencia no puede, por ejemplo, bloquear a los usuarios para que no actualicen una fila con un valor mayor que el actual. Si se requiere este tipo de lógica, debe usar desencadenadores con las tablas intermedias DELETED e INSERTED para hacer referencia a los valores antiguos y nuevos juntos.  
  
-   El optimizador no comprobará un predicado de bloqueo AFTER UPDATE si no se ha cambiado ninguna de las columnas usadas por la función de predicado. Por ejemplo: Alice no debería poder cambiar un salario para que sea superior a 100 000, pero debería poder cambiar la dirección de un empleado cuyo salario ya sea superior a 100 000 (y, por tanto, ya infringe el predicado).  
  
-   No se han realizado cambios en las API masivas, incluida BULK INSERT. Esto significa que los predicados de bloqueo AFTER INSERT se aplicarán a las operaciones de inserción masivas como si fueran operaciones de inserción normales.  
  
  
##  <a name="UseCases"></a> Casos de uso  
 Estos son ejemplos de diseño de cómo se puede usar RLS:  
  
-   Un hospital puede crear una directiva de seguridad que permita a las enfermeras ver solo las filas de datos de sus pacientes.  
  
-   Un banco puede crear una directiva para restringir el acceso a las filas de datos financieros según la división de negocio del empleado, o según el rol del empleado dentro de la empresa.  
  
-   Una aplicación multiinquilino puede crear una directiva para aplicar una separación lógica de cada fila de datos del inquilino de las filas de otros inquilinos. Las eficiencias se obtienen con el almacenamiento de datos para varios inquilinos en una sola tabla. Por supuesto, cada inquilino solo puede ver sus filas de datos.  
  
 Los predicados de filtro RLS son funcionalmente equivalentes a anexar una cláusula **WHERE** . El predicado puede ser tan sofisticado como dictan las prácticas empresariales o la cláusula puede ser tan simple como `WHERE TenantId = 42`.  
  
 En términos más formales, RLS presenta control de acceso basado en predicado. Ofrece una evaluación flexible, centralizada y basada en predicados que puede tener en cuenta metadatos o cualquier otro criterio que el administrador determine como apropiado. El predicado se usa como un criterio para determinar si el usuario tiene o no el acceso adecuado a los datos según los atributos del usuario. El control de acceso basado en etiquetas se puede implementar con el control de acceso basado en predicados.  
  
  
##  <a name="Permissions"></a> Permisos  
 Crear, modificar o quitar directivas de seguridad necesita el permiso **ALTER ANY SECURITY POLICY** . Crear o quitar una directiva de seguridad necesita el permiso **ALTER** en el esquema.  
  
 Además, son necesarios los siguientes permisos para cada predicado que se agrega:  
  
-   Los permisos**SELECT** y **REFERENCES** de la función que se usa como predicado.  
  
-   El permiso**REFERENCES** de la tabla de destino que se enlaza a la directiva.  
  
-   El permiso**REFERENCES** de cada columna desde la tabla de destino que se usa como argumento.  
  
 Las directivas de seguridad se aplican a todos los usuarios, incluidos los usuarios dbo de la base de datos. Los usuarios dbo pueden modificar o quitar directivas de seguridad, sin embargo, se pueden auditar los cambios en las directivas de seguridad. Si los usuarios con privilegios elevados (como sysadmin o db_owner) necesitan ver todas las filas para solucionar problemas o validar los datos, la directiva de seguridad debe estar escrita de modo que lo permita.  
  
 Si se crea una directiva de seguridad con `SCHEMABINDING = OFF`, los usuarios deben tener el permiso de  **SELECT** o **EXECUTE** en la función de predicado y cualquier función, vista o tabla adicional que se use dentro de la función de predicado para consultar la tabla de destino. Si se crear una directiva de seguridad con `SCHEMABINDING = ON` (el valor predeterminado), entonces estas comprobaciones de permiso se omiten cuando los usuarios consultan la tabla de destino.  
  
  
##  <a name="Best"></a> Procedimientos recomendados  
  
-   Se recomienda crear un esquema independiente para los objetos RLS (directiva de seguridad y función de predicado).  
  
-   El permiso **ALTER ANY SECURITY POLICY** está destinado a los usuarios con privilegios elevados (como un administrador de directivas de seguridad). El administrador de directivas de seguridad necesita el permiso **SELECT** en las tablas que protege.  
  
-   Evite las conversiones de tipos en funciones de predicado para evitar posibles errores en tiempo de ejecución.  
  
-   Evite la recursividad en funciones de predicado siempre que sea posible para evitar la degradación del rendimiento. El optimizador de consultas intentará detectar las recursividades directas pero no garantiza encontrar recursividad indirecta (es decir, donde una segunda función llame a la función de predicado).  
  
-   Evite el uso de combinaciones de tablas de forma excesiva en funciones de predicado para maximizar el rendimiento.  
  
 Evite la lógica del predicado que dependa de [opciones SET](../../t-sql/statements/set-statements-transact-sql.md)específicas de la sesión: aunque es improbable que se usen en aplicaciones prácticas, las funciones de predicado cuya lógica depende de determinadas opciones **SET** específicas de la sesión pueden perder información si los usuarios pueden ejecutar consultas arbitrarias. Por ejemplo, una función de predicado que convierte implícitamente una cadena en **datetime** podría filtrar filas diferentes según la opción **SET DATEFORMAT** de la sesión actual. En general, las funciones de predicado deben cumplir las reglas siguientes:  
  
-   Las funciones de predicado no deben convertir implícitamente cadenas de caracteres en **date**, **smalldatetime**, **datetime**, **datetime2** o **datetimeoffset** o viceversa, ya que estas conversiones se ven afectadas por las opciones [SET DATEFORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/set-dateformat-transact-sql.md) y [SET LANGUAGE &#40;Transact-SQL&#41;](../../t-sql/statements/set-language-transact-sql.md). En su lugar, use la función **CONVERT** y especifique explícitamente el parámetro de estilo.  
  
-   Las funciones de predicado no deben depender del valor del primer día de la semana, ya que este valor se ve afectado por la opción [SET DATEFIRST &#40;Transact-SQL&#41;](../../t-sql/statements/set-datefirst-transact-sql.md).  
  
-   Las funciones de predicado no deben depender de expresiones aritméticas o de agregación que devuelvan **NULL** en caso de error (como desbordamiento o división por cero), ya que este comportamiento se ve afectado por las opciones [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md), [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md) y [SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md).  
  
-   Las funciones de predicado no deben comparar cadenas concatenadas con **NULL**, ya que este comportamiento se ve afectado por la opción [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md).  
   
  
##  <a name="SecNote"></a> Nota de seguridad: ataques del lado de canal  
 **Administrador de directivas de seguridad malintencionado:** es importante observar que un administrador de directivas de seguridad malintencionado, con suficientes permisos para crear una directiva de seguridad en una columna confidencial, y con permisos para crear o modificar funciones con valores de tabla insertadas, puede conspirar con otro usuario que tenga permisos SELECT en una tabla para exfiltrar datos creando malintencionadamente funciones con valores de tabla insertadas diseñadas para usar ataques del lado de canal para inferir los datos. Estos ataques necesitarían una confabulación (o excesivos permisos concedidos a un usuario malintencionado) y es probable que necesiten varias iteraciones de modificación de la directiva (que necesite permisos para quitar el predicado para romper el enlace de esquema), modificación de las funciones con valores de tabla insertada y ejecución repetida de instrucciones SELECT en la tabla de destino. Se recomienda limitar los permisos según sea necesario y supervisar cualquier actividad sospechosa, como cambiar constantemente las directivas y las funciones con valores de tabla insertada relacionadas con la seguridad de nivel de fila.  
  
 **Consultas cuidadosamente diseñadas:** es posible perder información mediante el uso de consultas cuidadosamente diseñadas. Por ejemplo, `SELECT 1/(SALARY-100000) FROM PAYROLL WHERE NAME='John Doe'` permitiría que un usuario malintencionado sepa que el salario de Juan García es 100.000 $. Aunque hay un predicado de seguridad para impedir que un usuario malintencionado consulte directamente el salario de otras personas, el usuario puede determinar el momento en que la consulta devuelve una excepción de división por cero.  
   
  
##  <a name="Limitations"></a> Compatibilidad entre características  
 En general, la seguridad de nivel de fila funcionará como se espera en todas las características. Sin embargo, hay algunas excepciones. En esta sección se describen varias notas y advertencias sobre el uso de la seguridad de nivel de fila con otras características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **DBCC SHOW_STATISTICS** informa de las estadísticas en datos sin filtrar y, por lo tanto, puede perder información si no lo protege una directiva de seguridad. Por esta razón, para ver el objeto de estadísticas de una tabla con una directiva de seguridad de nivel de fila, el usuario debe ser propietario de la tabla o miembro del rol fijo de servidor sysadmin, del rol fijo de base de datos db_owner o del rol fijo de base de datos db_ddladmin.  
  
-   **Filestream:** RLS no es compatible con Filestream.  
  
-   **Polybase:** RLS no es compatible con Polybase.  
  
-   
            **tablas optimizadas para memoria**la función con valores de tabla insertados que se usa como predicado de seguridad en una tabla optimizada para memoria debe definirse mediante la opción `WITH NATIVE_COMPILATION` . Con esta opción, se prohibirán las características del lenguaje incompatibles con las tablas optimizadas para memoria y se emitirá el error adecuado en tiempo de creación. Para obtener más información, vea la sección **Seguridad de nivel de fila en tablas con optimización para memoria** en [Introducción a las tablas con optimización para memoria](../../relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables.md).  
  
-   **Vistas indizadas:** en general, se pueden crear directivas de seguridad sobre las vistas y se pueden crear vistas sobre las tablas que están enlazadas mediante directivas de seguridad. Sin embargo, no se pueden crear vistas indexadas sobre las tablas que tienen una directiva de seguridad, ya que las búsquedas de filas mediante el índice podrían omitir la directiva.  
  
-   **Captura de datos modificados** la captura de datos modificados puede perder filas enteras que se deben filtrar a miembros de **db_owner** o a usuarios que son miembros del rol de "acceso" especificado cuando se habilita CDC para una tabla (Nota: Puede establecerlo explícitamente en **NULL** para permitir que todos los usuarios tengan acceso a los datos modificados). De hecho, **db_owner** y los miembros de este rol de acceso pueden ver todos los cambios en los datos de una tabla, incluso si hay una directiva de seguridad en la tabla.  
  
-   **Seguimiento de cambios:** el seguimiento de cambios puede perder la clave principal de las filas que se deben filtrar a los usuarios con permisos **SELECT** y **VIEW CHANGE TRACKING** . No se pierden los valores de datos reales; solo el hecho de que la columna A se actualizó, se insertó o se eliminó de la fila con la clave principal B. Esto es problemático si la clave principal contiene un elemento confidencial, como un número del seguro social. Sin embargo, en la práctica, **CHANGETABLE** casi siempre se combina con la tabla original para obtener los datos más recientes.  
  
-   **Búsqueda de texto completo** se espera una disminución del rendimiento en las consultas que usan las siguientes funciones de búsqueda de texto completo y búsqueda semántica, debido a una combinación adicional que se ha introducido para aplicar seguridad de nivel de fila y evitar la pérdida de las claves principales de las filas que se deben filtrar: **CONTAINSTABLE**, **FREETEXTTABLE**, semantickeyphrasetable, semanticsimilaritydetailstable, semanticsimilaritytable.  
  
-   **Índices de almacén de columnas** RLS no es compatible con los índices de almacén de columnas en clúster y no clúster. Sin embargo, dado que la seguridad de nivel de fila aplica una función, es posible que el optimizador pueda modificar el plan de consulta para que no use el modo por lotes.  
  
-   **Vistas con particiones:** no se pueden definir predicados de bloqueo en vistas con particiones, y no se pueden crear vistas con particiones sobre tablas que usan predicados de bloqueo. Los predicados de filtro son compatibles con vistas con particiones.  
  
-   **Tablas temporales:** son compatibles con RLS. Sin embargo, los predicados de seguridad en la tabla actual no se replican automáticamente a la tabla del historial. Para aplicar una directiva de seguridad a las tablas actual y del historial, debe agregar individualmente un predicado de seguridad en cada tabla.  
  
  
##  <a name="CodeExamples"></a> Ejemplos  
  
###  <a name="Typical"></a> A. Escenario para los usuarios que se autentican en la base de datos  
 Este pequeño ejemplo crea tres usuarios, crea y llena una tabla con seis filas, y crea una función de valores de tabla insertada y una directiva de seguridad de la tabla. El ejemplo muestra cómo seleccionar instrucciones filtradas para los distintos usuarios.  
  
 Cree tres cuentas de usuario que mostrarán las distintas capacidades de acceso.  
  
```sql  
CREATE USER Manager WITHOUT LOGIN;  
CREATE USER Sales1 WITHOUT LOGIN;  
CREATE USER Sales2 WITHOUT LOGIN;  
```  
  
 Cree una tabla sencilla para almacenar los datos.  
  
```  
CREATE TABLE Sales  
    (  
    OrderID int,  
    SalesRep sysname,  
    Product varchar(10),  
    Qty int  
    );  
```  
  
 Rellene la tabla con seis filas de datos que muestren tres pedidos para cada representante de ventas.  
  
```  
INSERT Sales VALUES   
(1, 'Sales1', 'Valve', 5),   
(2, 'Sales1', 'Wheel', 2),   
(3, 'Sales1', 'Valve', 4),  
(4, 'Sales2', 'Bracket', 2),   
(5, 'Sales2', 'Wheel', 5),   
(6, 'Sales2', 'Seat', 5);  
-- View the 6 rows in the table  
SELECT * FROM Sales;  
```  
  
 Conceda acceso de lectura en la tabla para cada usuario.  
  
```  
GRANT SELECT ON Sales TO Manager;  
GRANT SELECT ON Sales TO Sales1;  
GRANT SELECT ON Sales TO Sales2;  
```  
  
 Cree un nuevo esquema y una función de valores de tabla insertada. La función devuelve 1 cuando una fila de la columna SalesRep es la misma que el usuario que ejecuta la consulta (`@SalesRep = USER_NAME()`) o si el usuario que ejecuta la consulta es el usuario administrador (`USER_NAME() = 'Manager'`).  
  
```  
CREATE SCHEMA Security;  
GO  
  
CREATE FUNCTION Security.fn_securitypredicate(@SalesRep AS sysname)  
    RETURNS TABLE  
WITH SCHEMABINDING  
AS  
    RETURN SELECT 1 AS fn_securitypredicate_result   
WHERE @SalesRep = USER_NAME() OR USER_NAME() = 'Manager';  
```  
  
 Cree una directiva de seguridad agregando la función como un predicado de filtro. El estado se debe configurar en ON para habilitar la directiva.  
  
```  
CREATE SECURITY POLICY SalesFilter  
ADD FILTER PREDICATE Security.fn_securitypredicate(SalesRep)   
ON dbo.Sales  
WITH (STATE = ON);  
```  
  
 Pruebe ahora el predicado de filtrado seleccionando de la tabla Ventas como cada usuario.  
  
```  
EXECUTE AS USER = 'Sales1';  
SELECT * FROM Sales;   
REVERT;  
  
EXECUTE AS USER = 'Sales2';  
SELECT * FROM Sales;   
REVERT;  
  
EXECUTE AS USER = 'Manager';  
SELECT * FROM Sales;   
REVERT;  
```  
  
 El administrador debe ver las 6 filas. Los usuarios Sales1 y Sales2 solo deben ver sus propias ventas.  
  
 Modifique la directiva de seguridad para deshabilitar la directiva.  
  
```  
ALTER SECURITY POLICY SalesFilter  
WITH (STATE = OFF);  
```  
  
 Ahora los usuarios Sales1 y Sales2 pueden ver las 6 filas.  
  
  
###  <a name="MidTier"></a> B. Escenario para los usuarios que se conectan a la base de datos a través de una aplicación de nivel intermedio  
 Este ejemplo muestra cómo una aplicación de nivel intermedio puede implementar el filtrado de conexiones, donde los usuarios de la aplicación (o inquilinos) comparten el mismo usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (la aplicación). La aplicación configura el identificador de usuario de la aplicación actual en [SESSION_CONTEXT &#40;Transact-SQL&#41;](../../t-sql/functions/session-context-transact-sql.md) después de conectarse a la base de datos y, luego, las directivas de seguridad filtran de forma transparente las filas que no deberían ser visibles para este identificador e impiden también que el usuario inserte filas para el identificador de usuario incorrecto. No es necesario ningún otro cambio en la aplicación.  
  
 Cree una tabla sencilla para almacenar los datos.  
  
```  
CREATE TABLE Sales (  
    OrderId int,  
    AppUserId int,  
    Product varchar(10),  
    Qty int  
);  
```  
  
 Rellene la tabla con seis filas de datos que muestren tres pedidos para cada usuario de la aplicación.  
  
```  
INSERT Sales VALUES   
    (1, 1, 'Valve', 5),   
    (2, 1, 'Wheel', 2),   
    (3, 1, 'Valve', 4),  
    (4, 2, 'Bracket', 2),   
    (5, 2, 'Wheel', 5),   
    (6, 2, 'Seat', 5);  
```  
  
 Cree un usuario con pocos privilegios que la aplicación usará para conectarse.  
  
```  
-- Without login only for demo  
CREATE USER AppUser WITHOUT LOGIN;   
GRANT SELECT, INSERT, UPDATE, DELETE ON Sales TO AppUser;  
  
-- Never allow updates on this column  
DENY UPDATE ON Sales(AppUserId) TO AppUser;  
```  
  
 Cree un esquema y una función de predicado nuevos, que usarán el identificador de usuario de la aplicación almacenado en **SESSION_CONTEXT** para filtrar las filas.  
  
```  
CREATE SCHEMA Security;  
GO  
  
CREATE FUNCTION Security.fn_securitypredicate(@AppUserId int)  
    RETURNS TABLE  
    WITH SCHEMABINDING  
AS  
    RETURN SELECT 1 AS fn_securitypredicate_result  
    WHERE  
        DATABASE_PRINCIPAL_ID() = DATABASE_PRINCIPAL_ID('AppUser')    
        AND CAST(SESSION_CONTEXT(N'UserId') AS int) = @AppUserId;   
GO  
```  
  
 Cree una directiva de seguridad que agregue esta función como un predicado de filtro y un predicado de bloqueo en `Sales`. El predicado de bloqueo solo necesita **AFTER INSERT**, ya que **BEFORE UPDATE** y **BEFORE DELETE** ya están filtrados y **AFTER UPDATE** no es necesario porque la columna `AppUserId` no se puede actualizar con otros valores debido al permiso de columna que se ha establecido anteriormente.  
  
```  
CREATE SECURITY POLICY Security.SalesFilter  
    ADD FILTER PREDICATE Security.fn_securitypredicate(AppUserId)   
        ON dbo.Sales,  
    ADD BLOCK PREDICATE Security.fn_securitypredicate(AppUserId)   
        ON dbo.Sales AFTER INSERT   
    WITH (STATE = ON);  
```  
  
 Ahora podemos simular el filtrado de conexiones al seleccionar la tabla `Sales` después de configurar los distintos identificadores de usuario en **SESSION_CONTEXT**. En la práctica, la aplicación es responsable de establecer el identificador de usuario actual en **SESSION_CONTEXT** después de abrir una conexión.  
  
```  
EXECUTE AS USER = 'AppUser';  
EXEC sp_set_session_context @key=N'UserId', @value=1;  
SELECT * FROM Sales;  
GO  
  
--  Note: @read_only prevents the value from changing again   
--  until the connection is closed (returned to the connection pool)  
EXEC sp_set_session_context @key=N'UserId', @value=2, @read_only=1;   
  
SELECT * FROM Sales;  
GO  
  
INSERT INTO Sales VALUES (7, 1, 'Seat', 12); -- error: blocked from inserting row for the wrong user ID  
GO  
  
REVERT;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/create-security-policy-transact-sql.md)   
 [ALTER SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-security-policy-transact-sql.md)   
 [DROP SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-security-policy-transact-sql.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [SESSION_CONTEXT &#40;Transact-SQL&#41;](../../t-sql/functions/session-context-transact-sql.md)   
 [sp_set_session_context &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-set-session-context-transact-sql.md)   
 [sys.security_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [sys.security_predicates &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)   
 [Crear funciones definidas por el usuario &#40;motor de base de datos&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md)  
  
  
