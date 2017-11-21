---
title: CREATE PROCEDURE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 09/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PROC
- PROCEDURE
- CREATE PROCEDURE
- CREATE_PROC_TSQL
- PROCEDURE_TSQL
- CREATE PROC
- PROC_TSQL
- CREATE_PROCEDURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- parameters [SQL Server], stored procedures
- table-valued parameters
- SET statement, stored procedures
- stored procedures [SQL Server], creating
- wildcard parameters [SQL Server]
- maximum size of stored procedures
- WITH RECOMPILE clause
- common language runtime [SQL Server], stored procedures
- CREATE PROCEDURE statement
- local temporary procedures [SQL Server]
- WITH ENCRYPTION clause
- output parameters [SQL Server]
- nesting stored procedures
- user-defined stored procedures [SQL Server]
- system stored procedures [SQL Server], creating
- deferred name resolution, stored procedures
- referenced tables [SQL Server]
- global temporary procedures [SQL Server]
- cursor data type
- temporary stored procedures [SQL Server]
- size [SQL Server], stored procedures
- automatic stored procedure execution
- creating stored procedures
ms.assetid: afe3d86d-c9ab-44e4-b74d-4e3dbd9cc58c
caps.latest.revision: 180
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: c2a0a43aefe59bc11f16445b5ee0c781179a33fa
ms.openlocfilehash: 23460288040b37ec6a09293bc02a46e4f9af94fa
ms.contentlocale: es-es
ms.lasthandoff: 09/06/2017

---
# <a name="create-procedure-transact-sql"></a>CREATE PROCEDURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Crea un [!INCLUDE[tsql](../../includes/tsql-md.md)] o common language runtime (CLR) procedimiento almacenado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], almacenamiento de datos de SQL Azure y almacenamiento de datos paralelos. Los procedimientos almacenados son similares a los procedimientos de otros lenguajes de programación en tanto que pueden:  
  
-   Aceptar parámetros de entrada y devolver varios valores en forma de parámetros de salida al lote o al procedimiento que realiza la llamada.  
  
-   Contener instrucciones de programación que realicen operaciones en la base de datos, incluidas las llamadas a otros procedimientos.  
  
-   Devolver un valor de estado a un lote o a un procedimiento que realice una llamada para indicar si la operación se ha realizado correctamente o se han producido errores, y el motivo de estos.  
  
 Use esta instrucción para crear un procedimiento permanente en la base de datos actual o un procedimiento temporal en el **tempdb** base de datos.  
  
> [!NOTE]  
>  La integración de CLR de .NET Framework en SQL Server se describe en este tema. Integración de CLR no se aplica a Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)].

Saltar a [sencillos ejemplos](#Simple) omitir los detalles de la sintaxis y obtener un ejemplo rápido de básico de procedimiento almacenado.
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Transact-SQL Syntax for Stored Procedures in SQL Server and Azure SQL Database  
  
CREATE [ OR ALTER ] { PROC | PROCEDURE } 
    [schema_name.] procedure_name [ ; number ]   
    [ { @parameter [ type_schema_name. ] data_type }  
        [ VARYING ] [ = default ] [ OUT | OUTPUT | [READONLY]  
    ] [ ,...n ]   
[ WITH <procedure_option> [ ,...n ] ]  
[ FOR REPLICATION ]   
AS { [ BEGIN ] sql_statement [;] [ ...n ] [ END ] }  
[;]  
  
<procedure_option> ::=   
    [ ENCRYPTION ]  
    [ RECOMPILE ]  
    [ EXECUTE AS Clause ]  
```  
  
```  
-- Transact-SQL Syntax for CLR Stored Procedures  
  
CREATE [ OR ALTER ] { PROC | PROCEDURE } 
    [schema_name.] procedure_name [ ; number ]   
    [ { @parameter [ type_schema_name. ] data_type }   
        [ = default ] [ OUT | OUTPUT ] [READONLY]  
    ] [ ,...n ]   
[ WITH EXECUTE AS Clause ]  
AS { EXTERNAL NAME assembly_name.class_name.method_name }  
[;]  
```  
  
```  
-- Transact-SQL Syntax for Natively Compiled Stored Procedures  
  
CREATE [ OR ALTER ] { PROC | PROCEDURE } [schema_name.] procedure_name  
    [ { @parameter data_type } [ NULL | NOT NULL ] [ = default ] 
        [ OUT | OUTPUT ] [READONLY] 
    ] [ ,... n ]  
  WITH NATIVE_COMPILATION, SCHEMABINDING [ , EXECUTE AS clause ]  
AS  
{  
  BEGIN ATOMIC WITH (set_option [ ,... n ] )  
sql_statement [;] [ ... n ]  
 [ END ]  
}  
 [;]  
  
<set_option> ::=  
    LANGUAGE =  [ N ] 'language'  
  | TRANSACTION ISOLATION LEVEL =  { SNAPSHOT | REPEATABLE READ | SERIALIZABLE }  
  | [ DATEFIRST = number ]  
  | [ DATEFORMAT = format ]  
  | [ DELAYED_DURABILITY = { OFF | ON } ]  
```  
  
```  
-- Transact-SQL Syntax for Stored Procedures in Azure SQL Data Warehouse
-- and Parallel Data Warehouse  
  
-- Create a stored procedure   
CREATE { PROC | PROCEDURE } [ schema_name.] procedure_name  
    [ { @parameterdata_type } [ OUT | OUTPUT ] ] [ ,...n ]  
AS { [ BEGIN ] sql_statement [;][ ,...n ] [ END ] }  
[;]  
```  
  
## <a name="arguments"></a>Argumentos
O ALTER  
 **Se aplica a**: Azure [!INCLUDE[ssSDS](../../includes/sssds-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1).  
  
 Modifica el procedimiento si ya existe.
 
 *schema_name*  
 El nombre del esquema al que pertenece el procedimiento. Los procedimientos se enlazan a un esquema. Si no se especifica el nombre del esquema cuando se crea el procedimiento, se asigna automáticamente el esquema predeterminado del usuario que crea este procedimiento.  
  
 *procedure_name*  
 El nombre del procedimiento. Nombres de procedimientos deben cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md) y debe ser único dentro del esquema.  
  
 Evite el uso de la **sp_** prefijo cuando asigne nombre a procedimientos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa este prefijo para designar los procedimientos del sistema. Si usa el prefijo, puede provocar la ruptura del código de la aplicación si existe un procedimiento del sistema con el mismo nombre.  
  
 Los procedimientos temporales locales o globales se pueden crear mediante un signo de número (##) antes de *nombre_procedimiento* (*#procedure_name*) para los procedimientos temporales locales y dos signos de número para la cuenta temporal global procedimientos (*## procedure_name*). Solo la conexión que creó un procedimiento temporal local lo ve y se quita cuando se cierra esa conexión. Un procedimiento temporal global está disponible para todas las conexiones y se quita al final de la última sesión que lo use. No se pueden especificar nombres temporales para los procedimientos CLR.  
  
 El nombre completo de un procedimiento o un procedimiento temporal global, incluidos los signos de número ##, no puede superar los 128 caracteres. El nombre completo de un procedimiento temporal local, incluido el signo de número #, no puede superar los 116 caracteres.  
  
 **;**  *número*  
 **Se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Entero opcional que se usa para agrupar procedimientos con el mismo nombre. Estos procedimientos agrupados se pueden quitar juntos mediante una instrucción DROP PROCEDURE.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 No se pueden usar los procedimientos numerados el **xml** o tipos de CLR definidos por el usuario y no se puede usar en una guía de plan.  
  
 **@***parámetro*  
 Parámetro declarado en el procedimiento. Especifique un nombre de parámetro con el signo de arroba (**@**) como primer carácter. El nombre del parámetro debe cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md). Los parámetros son locales respecto al procedimiento; los mismos nombres de parámetro se pueden usar en otros procedimientos.  
  
 Se pueden declarar uno o varios parámetros; el valor máximo es 2.100. El usuario debe proporcionar el valor de cada parámetro declarado cuando se llame al procedimiento, a menos que se haya definido un valor predeterminado para el parámetro o se haya establecido en el mismo valor que el de otro parámetro. Si un procedimiento contiene [parámetros con valores de tabla](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)y el parámetro no está en la llamada, se pasa una tabla vacía. Los parámetros solo pueden ocupar el lugar de expresiones constantes; no se pueden usar en lugar de nombres de tablas, nombres de columnas o nombres de otros objetos de base de datos. Para obtener más información, vea [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md).  
  
 No se pueden declarar los parámetros si se especifica FOR REPLICATION.  
  
 [ *type_schema_name***.** ] *data_type*  
 El tipo de datos del parámetro y el esquema al que pertenece el tipo de datos.  
  
**Directrices para [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimientos**:  
  
-   Todos los [!INCLUDE[tsql](../../includes/tsql-md.md)] tipos de datos se pueden utilizar como parámetros.  
  
-   Puede usar el tipo de tabla definido por el usuario para crear parámetros con valores de tabla. Los parámetros con valores de tabla solo pueden ser parámetros INPUT y deben ir acompañados de la palabra clave READONLY. Para obtener más información, vea [usar parámetros &#40; motor de base de datos &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)  
  
-   **cursor** tipos de datos solo pueden ser parámetros de salida y deben ir acompañados de la palabra clave VARYING.  
  
**Directrices para procedimientos CLR**:  
  
-   Todos los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativos con un equivalente en código administrado se pueden usar como parámetros. Para obtener más información acerca de la correspondencia entre los tipos CLR y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos del sistema, consulte [asignación de datos de parámetro de CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md). Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos del sistema y su sintaxis, vea [tipos de datos &#40; Transact-SQL &#41; ](../../t-sql/data-types/data-types-transact-sql.md).  
  
-   Con valores de tabla o **cursor** tipos de datos no se puede usar como parámetros.  
  
-   Si el tipo de datos del parámetro es un tipo definido por el usuario de CLR, se debe disponer del permiso EXECUTE en el tipo.  
  
VARYING  
 Especifica el conjunto de resultados admitido como parámetro de salida. Este parámetro lo crea de forma dinámica el procedimiento y su contenido puede variar. Solo se aplica a **cursor** parámetros. Esta opción no es válida para los procedimientos CLR.  
  
*valor predeterminado*  
 Valor predeterminado de un parámetro. Si se define un valor predeterminado para un parámetro, el procedimiento se puede ejecutar sin especificar un valor para ese parámetro. El valor predeterminado debe ser una constante o puede ser NULL. El valor constante puede tener el formato de un carácter comodín, lo que permite usar la palabra clave LIKE cuando se pase el parámetro al procedimiento.   
  
 Valores predeterminados se registran en el **sys.parameters.default** columna únicamente para los procedimientos CLR. Esa columna es NULL para [!INCLUDE[tsql](../../includes/tsql-md.md)] parámetros de procedimientos.  
  
OUT | OUTPUT  
 Indica que se trata de un parámetro de salida. Utilice los parámetros OUTPUT para devolver valores al autor de la llamada del procedimiento. **texto**, **ntext**, y **imagen** parámetros no pueden usarse como parámetros de salida, a menos que el procedimiento sea un procedimiento CLR. Un parámetro de salida puede ser un marcador de posición de cursor, a menos que el procedimiento sea un procedimiento CLR. Un tipo de datos con valores de tabla no se puede especificar como parámetro OUTPUT de un procedimiento.  
  
READONLY  
 Indica que el parámetro no se puede actualizar ni modificar en el cuerpo del procedimiento. Si el tipo de parámetro es un tipo con valores de tabla, se debe especificar READONLY.  
  
RECOMPILE  
 Indica que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] no almacena en caché un plan de consulta para este procedimiento, lo que obliga a volver a compilarse cada vez que se ejecuta. Para obtener más información sobre las razones para forzar una nueva compilación, consulte [volver a compilar un procedimiento almacenado](../../relational-databases/stored-procedures/recompile-a-stored-procedure.md). Esta opción no se puede usar cuando se especifica FOR REPLICATION ni para procedimientos CLR.  
  
 Para indicar a la [!INCLUDE[ssDE](../../includes/ssde-md.md)] que descarte planes de consulta para consultas individuales dentro de un procedimiento, utilice la sugerencia de consulta RECOMPILE en la definición de la consulta. Para obtener más información, vea [Sugerencias de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
ENCRYPTION  
 **Se aplica a**: SQL Server ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Indica que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] convierte el texto original de la instrucción CREATE PROCEDURE en un formato confuso. La salida de la protección no es directamente visible en ninguna de las vistas de catálogo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los usuarios que no dispongan de acceso a las tablas del sistema o a los archivos de base de datos no pueden recuperar el texto confuso. Sin embargo, el texto está disponible para los usuarios con privilegios que pueden tener acceso a las tablas del sistema sobre el [puerto DAC](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md) o directamente a los archivos de base de datos. Además, los usuarios que puedan adjuntar un depurador al proceso del servidor pueden recuperar el procedimiento descifrado de la memoria en tiempo de ejecución. Para obtener más información acerca del acceso a los metadatos del sistema, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
 Esta opción no es válida para los procedimientos CLR.  
  
 Los procedimientos creados mediante esta opción no se pueden publicar como parte de la replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
EXECUTE AS *cláusula*  
 Especifica el contexto de seguridad en el que se ejecuta el procedimiento.  
  
 Para los procedimientos almacenados compilados de forma nativa, a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] y en [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], no hay limitaciones en EXECUTE AS cláusula. En [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SELF, OWNER y *'user_name'* cláusulas son compatibles con los procedimientos almacenados compilados de forma nativa.  
  
 Para obtener más información, vea [EXECUTE AS &#40;cláusula de Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
FOR REPLICATION  
 **Se aplica a**: SQL Server ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]), [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Especifica que el procedimiento se crea para replicación. Por consiguiente, no se puede ejecutar en el suscriptor. Se usa un procedimiento creado con la opción FOR REPLICATION como filtro de procedimiento y solo se ejecuta durante la replicación. No se pueden declarar los parámetros si se especifica FOR REPLICATION. No se puede especificar FOR REPLICATION en los procedimientos CLR. La opción RECOMPILE no se tiene en cuenta en el caso de procedimientos creados con FOR REPLICATION.  
  
 A `FOR REPLICATION` procedimiento tiene un tipo de objeto **RF** en **sys.objects** y **sys.procedures**.  
  
 {[BEGIN] *sql_statement* [;] [ ...  *n*  ] [END]}  
 Una o más instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] que comprenden el cuerpo del procedimiento. Puede usar las palabras clave BEGIN y END opcionales para incluir las instrucciones. Para obtener información, vea las secciones Prácticas recomendadas, Comentarios generales, así como Limitaciones y restricciones que aparecen más adelante.  
  
NOMBRE externo *assembly_name***.** *class_name***.** *NombreMétodo*  
 **Se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].  
  
 Especifica el método de un ensamblado de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para un procedimiento CLR al que se va a hacer referencia. *CLASS_NAME* debe ser válido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificador y debe existir como una clase en el ensamblado. Si la clase tiene un nombre calificado de espacio de nombres que utiliza un período (**.**) para separar las partes del espacio de nombres, el nombre de clase debe estar delimitado mediante corchetes (**[]**) o comillas (**""**). El método especificado debe ser un método estático de la clase.  
  
 De manera predeterminada, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede ejecutar código CLR. Puede crear, modificar y quitar objetos de base de datos que hagan referencia a common language runtime módulos; Sin embargo, no se puede ejecutar estas referencias en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hasta que habilite la [opción clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md). Para habilitar la opción, utilice [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
> [!NOTE]  
>  Los procedimientos CLR no se admiten en las bases de datos independientes.  
  
ATOMIC WITH  
 **Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Indica la ejecución automática de procedimientos almacenados. Los cambios se confirman o todos se revierten iniciando una excepción. El bloqueo ATOMIC WITH se requiere para los procedimientos almacenados compilados de forma nativa.  
  
 Si el procedimiento vuelve (explícitamente mediante la instrucción RETURN o implícitamente completando su ejecución), el trabajo que realiza el procedimiento se confirma. Si se inicia el procedimiento, el trabajo que realiza se revierte.  
  
 XACT_ABORT es ON de forma predeterminada en un bloque atómico y no se puede cambiar. XACT_ABORT especifica si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] revierte automáticamente la transacción actual cuando una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] genera un error en tiempo de ejecución.  
  
 Las siguientes opciones SET son siempre ON en el bloqueo ATOMIC; las opciones no se pueden cambiar.  
-   CONCAT_NULL_YIELDS_NULL  
-   QUOTED_IDENTIFIER, ARITHABORT  
-   NOCOUNT  
-   ANSI_NULLS  
-   ANSI_WARNINGS  
  
Las opciones SET no pueden cambiarse dentro de bloques ATOMIC. Las opciones SET de la sesión de usuario no se utilizan en el ámbito de los procedimientos almacenados compilados de forma nativa. Estas opciones se corrigen en tiempo de compilación.  
  
Las operaciones BEGIN, ROLLBACK y COMMIT no se pueden utilizar dentro de un bloque atómico.  
  
 Hay un bloqueo ATOMIC por cada procedimiento almacenado compilado de forma nativa, en el ámbito externo del procedimiento. Los bloqueos no se pueden anidar. Para obtener más información acerca de los bloques atomic, vea [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
  
**NULL** | NO ES NULL  
 Determina si se permiten valores NULL en un parámetro. NULL es el valor predeterminado.  
  
NATIVE_COMPILATION  
 **Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Indica que el procedimiento está compilado de forma nativa. NATIVE_COMPILATION, SCHEMABINDING, y EXECUTE AS se pueden especificar en cualquier orden. Para obtener más información, consulte [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
  
SCHEMABINDING  
 **Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Se garantiza que las tablas a las que un procedimiento hace referencia no se pueden quitar o modificar. SCHEMABINDING se requiere en los procedimientos almacenados compilados de forma nativa (Para obtener más información, consulte [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).) Las restricciones SCHEMABINDING son las mismas que para las funciones definidas por el usuario. Para obtener más información, vea la sección SCHEMABINDING en [CREATE FUNCTION &#40; Transact-SQL &#41; ](../../t-sql/statements/create-function-transact-sql.md).  
  
LANGUAGE = [N] 'idioma'  
 **Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Equivalente a [Establecer idioma &#40; Transact-SQL &#41; ](../../t-sql/statements/set-language-transact-sql.md) opción de sesión. LANGUAGE = [N] 'language' es necesaria.  
  
NIVEL DE AISLAMIENTO DE TRANSACCIÓN  
 **Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Se requiere para los procedimientos almacenados compilados de forma nativa. Especifica el nivel de aislamiento de la transacción para el procedimiento almacenado. Las opciones son las siguientes:  
  
 Para obtener más información acerca de estas opciones, consulte [SET TRANSACTION ISOLATION LEVEL &#40; Transact-SQL &#41; ](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
REPEATABLE READ  
 Especifica que las instrucciones no pueden leer datos que otras transacciones hayan modificado, pero aún no hayan confirmado. Si otra transacción modifica los datos que se ha leído la transacción actual, se produce un error en la transacción actual.  
  
SERIALIZABLE  
 Especifica lo siguiente:  
-   Las instrucciones no pueden leer datos que hayan sido modificados, pero aún no confirmados, por otras transacciones.  
-   Si otra transacción modifica los datos que se ha leído la transacción actual, se produce un error en la transacción actual.  
-   Si otra transacción inserta nuevas filas con valores de clave que pudieran estar incluidos en el intervalo de claves leído por las instrucciones de la transacción actual, se produce un error en la transacción actual.  
  
SNAPSHOT  
 Especifica que los datos leídos por cualquier instrucción de una transacción están la versión transaccionalmente coherente de los datos existentes al comienzo de la transacción.  
  
DATEFIRST = *número*  
 **Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Especifica el primer día de la semana en un número del 1 al 7. DATEFIRST es opcional. Si no se especifica, el valor se deduce del idioma especificado.  
  
 Para obtener más información, vea [SET DATEFIRST &#40; Transact-SQL &#41; ](../../t-sql/statements/set-datefirst-transact-sql.md).  
  
DATEFORMAT = *formato*  
 **Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Especifica el orden de las partes correspondientes al mes, día y año de una fecha para interpretar las cadenas de caracteres date, smalldatetime, datetime, datetime2 y datetimeoffset. DATEFORMAT es opcional. Si no se especifica, el valor se deduce del idioma especificado.  
  
 Para obtener más información, vea [SET DATEFORMAT &#40; Transact-SQL &#41; ](../../t-sql/statements/set-dateformat-transact-sql.md).  
  
DELAYED_DURABILITY = { OFF | ON }  
 **Se aplica a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].  
  
 Las confirmaciones de transacciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden ser totalmente durables (el valor predeterminado) o durables diferidas.  
  
 Para obtener más información, consulte [controlar la durabilidad de transacciones](../../relational-databases/logs/control-transaction-durability.md).  

## <a name="Simple"></a>Ejemplos sencillos

Para ayudarle a empezar a trabajar, presentamos dos ejemplos rápidos:  
`SELECT DB_NAME() AS ThisDB;`Devuelve el nombre de la base de datos actual.  
Puede ajustar esa instrucción en un procedimiento almacenado, como:  
```sql  
CREATE PROC What_DB_is_this     
AS   
SELECT DB_NAME() AS ThisDB; 
```   
Llame al procedimiento de almacén con la instrucción:`EXEC What_DB_is_this;`   

Es un poco más complejo proporcionar un parámetro de entrada para hacer que el procedimiento sea más flexible. Por ejemplo:  
```sql   
CREATE PROC What_DB_is_that @ID int   
AS    
SELECT DB_NAME(@ID) AS ThatDB;   
```   
Especifique un número de Id. de base de datos cuando se llama al procedimiento. Por ejemplo, `EXEC What_DB_is_that 2;` devuelve `tempdb`.   

Vea [ejemplos](#Examples) hacia el final de este tema para muchos más ejemplos.     
    
## <a name="best-practices"></a>Procedimientos recomendados  
 Aunque esta no es una lista de prácticas recomendadas exhaustiva, estas sugerencias pueden mejorar el rendimiento de los procedimientos.  
  
-   Use la instrucción SET NOCOUNT ON como la primera instrucción del cuerpo del procedimiento. Es decir, colóquela a continuación de la palabra clave AS. De esta forma, se desactivan los mensajes que devuelve [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al cliente después de que se ejecute cualquier instrucción SELECT, INSERT, UPDATE, MERGE y DELETE. El rendimiento general de la base de datos y de la aplicación mejora si se elimina esta sobrecarga de red innecesaria. Para obtener información, consulte [SET NOCOUNT &#40; Transact-SQL &#41; ](../../t-sql/statements/set-nocount-transact-sql.md).  
  
-   Use nombres de esquemas cuando cree o haga referencia a los objetos de base de datos del procedimiento. Se tarda menos tiempo de procesamiento la [!INCLUDE[ssDE](../../includes/ssde-md.md)] para resolver los nombres de objeto si no tiene que buscar en varios esquemas. También impide que los permisos y problemas de acceso causados por el esquema predeterminado de un usuario que se asigna cuando se crean objetos sin especificar el esquema.  
  
-   Evite las funciones de ajuste en las columnas especificadas en las cláusulas WHERE y JOIN. De esta forma, las columnas no son deterministas y se evita que el procesador de consultas use índices.  
  
-   Evite usar funciones escalares en instrucciones SELECT que devuelvan muchas filas de datos. Dado que la función escalar se debe aplicar a todas las filas, el comportamiento resultante es similar al procesamiento basado en filas y degrada el rendimiento.  
  
-   Evite el uso de `SELECT *`. En su lugar, especifique los nombres de columna necesarios. De esta forma, puede evitar algunos errores de [!INCLUDE[ssDE](../../includes/ssde-md.md)] que detengan la ejecución del procedimiento. Por ejemplo, un `SELECT *` instrucción que devuelve datos de una tabla de 12 columnas y, a continuación, inserta datos en una tabla temporal de 12 columnas correctamente hasta que el número o se cambia el orden de las columnas en ninguna tabla.  
  
-   Evite el procesamiento o la devolución de demasiados datos. Restrinja los resultados lo antes posible en el código del procedimiento para que las operaciones posteriores realizadas por él se lleven a cabo con el menor conjunto de datos posible. Envíe únicamente los datos fundamentales a la aplicación cliente. Es más eficaz que enviar datos adicionales a través de la red y forzar que dicha aplicación trabaje con conjuntos de resultados innecesariamente grandes.  
  
-   Utilizar transacciones explícitas mediante el uso de BEGIN/COMMIT TRANSACTION y mantenga las transacciones lo más cortas posible. Las transacciones más largas significan bloqueos de registro más largos y mayores posibilidades de interbloqueos.  
  
-   Use la característica TRY…CATCH de [!INCLUDE[tsql](../../includes/tsql-md.md)] para el control de errores dentro de un procedimiento. TRY…CATCH puede encapsular todo un bloque de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)]. Esto no solo crea una sobrecarga de rendimiento menor, sino que también hace que los informes de errores sean más precisos con mucha menos programación.  
  
-   Use la palabra clave DEFAULT en todas las columnas de la tabla a las que haga referencia en las instrucciones CREATE TABLE o ALTER TABLE de [!INCLUDE[tsql](../../includes/tsql-md.md)] en el cuerpo del procedimiento. Esto evita pasar NULL a columnas que no permiten valores null.  
  
-   Use NULL o NOT NULL para todas las columnas de una tabla temporal. Las opciones ANSI_DFLT_ON y ANSI_DFLT_OFF controlan la forma en la que [!INCLUDE[ssDE](../../includes/ssde-md.md)] asigna los atributos NULL o NOT NULL a las columnas si no se especifican dichos atributos en una instrucción CREATE TABLE o ALTER TABLE. Si una conexión ejecuta un procedimiento con valores distintos para estas opciones a los que usó la conexión que creó el procedimiento, las columnas de la tabla creada para la segunda conexión pueden tener distinta nulabilidad y exhibir diferentes comportamientos. Si se especifica NULL o NOT NULL explícitamente para todas las columnas, las tablas temporales se crean con la misma nulabilidad para todas las conexiones que ejecuten el procedimiento almacenado.  
  
-   Use instrucciones de modificación que conviertan valores NULL e incluya lógica que elimine las filas con valores NULL de las consultas. Tenga en cuenta que en [!INCLUDE[tsql](../../includes/tsql-md.md)], NULL no está vacío o el valor "". Es un marcador de posición para un valor desconocido y puede provocar un comportamiento inesperado, especialmente cuando se consultan conjuntos de resultados o se usan funciones AGGREGATE.  
  
-   Use el operador UNION ALL en vez de los operadores UNION u OR, a menos que exista una necesidad específica de valores distintos. El operador UNION ALL necesita menos sobrecarga de procesamiento porque no se filtran los duplicados del conjunto de resultados.  
  
## <a name="general-remarks"></a>Notas generales  
 No hay ningún tamaño máximo predefinido para un procedimiento.  
  
 Las variables especificadas en el procedimiento pueden ser definido por el usuario o las variables del sistema, como @@SPID.  
  
 Cuando un procedimiento se ejecuta por primera vez, se compila para determinar que dispone de un plan de acceso óptimo para recuperar los datos. En las siguientes ejecuciones del procedimiento se puede volver a usar el plan ya generado si aún permanece en la memoria caché de planes de [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Cuando se inicia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se pueden ejecutar automáticamente uno o varios procedimientos. Los procedimientos deben crearse mediante el administrador del sistema en el **maestro** la base de datos y se ejecuta en el **sysadmin** rol fijo de servidor como un proceso en segundo plano. Los procedimientos no pueden tener ningún parámetro de entrada o salida. Para obtener más información, consulte [ejecutar un procedimiento almacenado](../../relational-databases/stored-procedures/execute-a-stored-procedure.md).  
  
 Los procedimientos se anidan cuando un procedimiento llama a otro o ejecuta código administrado mediante una referencia a una rutina, tipo o agregado CLR. Los procedimientos y las referencias a código administrado se pueden anidar hasta 32 niveles. El nivel de anidamiento aumenta en uno cuando el procedimiento o la referencia a código administrado a los que se ha llamado empiezan a ejecutarse, y disminuye en uno cuando se completa su ejecución. Los métodos que se invocan desde el código administrado no cuentan para este límite de niveles de anidamiento. Sin embargo, cuando un procedimiento almacenado CLR realiza operaciones de acceso a datos mediante el proveedor administrado de SQL Server, se agrega un nivel de anidamiento adicional en la transición desde código administrado a SQL.  
  
 Si se intenta superar el nivel máximo de anidamiento, se producirá un error en toda la cadena de llamada. Puede usar el @@NESTLEVEL función para devolver el nivel de anidamiento de la ejecución del procedimiento almacenado actual.  
  
## <a name="interoperability"></a>Interoperabilidad  
 El [!INCLUDE[ssDE](../../includes/ssde-md.md)] guarda los valores de SET QUOTED_IDENTIFIER y de SET ANSI_NULLS cuando se crea o modifica un procedimiento de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Estos valores originales se usan cuando se ejecuta el procedimiento. Por tanto, cualquier valor de sesión de cliente de SET QUOTED_IDENTIFIER y SET ANSI_NULLS se ignora durante la ejecución del procedimiento.  
  
 Otras opciones de SET, como SET ARITHABORT, SET ANSI_WARNINGS o SET ANSI_PADDINGS, no se guardan cuando se crea o se modifica un procedimiento. Si la lógica del procedimiento depende de un valor específico, incluya una instrucción SET al inicio del procedimiento para garantizar el valor adecuado. Cuando una instrucción SET se ejecuta desde un procedimiento, el valor permanece en vigor solo hasta que se complete la ejecución del procedimiento. A continuación, el valor se restaura al que tenía cuando se llamó al procedimiento. Esto permite que clientes individuales establezcan las opciones deseadas sin afectar a la lógica del procedimiento.  
  
 En un procedimiento se puede especificar cualquier instrucción SET, excepto SET SHOWPLAN_TEXT y SET SHOWPLAN_ALL. Estas deben ser las únicas instrucciones del lote. La opción SET elegida permanece vigente durante la ejecución del procedimiento y, a continuación, revierte a su valor anterior.  
  
> [!NOTE]  
>  No se respeta SET ANSI_WARNINGS al pasar parámetros de un procedimiento almacenado, una función definida por el usuario o al declarar y establecer variables en una instrucción por lotes. Por ejemplo, si una variable se define como **char**(3) y, a continuación, establece en un valor mayor que tres caracteres, se truncan los datos para el tamaño definido y la INSERCIÓN o instrucción de actualización se realiza correctamente.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 La instrucción CREATE PROCEDURE no se puede combinar con otras instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] en un único lote.  
  
 Las siguientes instrucciones no se pueden usar en ninguna parte del cuerpo de un procedimiento almacenado.  
  
||||  
|-|-|-|  
|CREATE AGGREGATE|CREATE SCHEMA|SET SHOWPLAN_TEXT|  
|CREATE DEFAULT|CREATE o ALTER TRIGGER|SET SHOWPLAN_XML|  
|CREATE o ALTER FUNCTION|CREATE o ALTER VIEW|USE *database_name*|  
|CREATE o ALTER PROCEDURE|SET PARSEONLY||  
|CREATE RULE|SET SHOWPLAN_ALL||  
  
 Un procedimiento puede hacer referencia a tablas que aún no existan. En el momento de la creación, solo se realiza la comprobación de la sintaxis. El procedimiento no se compila hasta que se ejecute por primera vez. Solamente durante la compilación se resuelven todos los objetos a los que se haga referencia en el procedimiento. Por lo tanto, se puede crear un procedimiento sintácticamente correcto que hace referencia a tablas que no existen correctamente; Sin embargo, el procedimiento produce un error en tiempo de ejecución si las tablas que se hace referencia no existen.  
  
 No puede especificar el nombre de una función como valor predeterminado de parámetro o como el valor pasado a un parámetro cuando se ejecute un procedimiento. Sin embargo, puede pasar una función como una variable, como se muestra en el ejemplo siguiente.  
  
```  
-- Passing the function value as a variable.  
DECLARE @CheckDate datetime = GETDATE();  
EXEC dbo.uspGetWhereUsedProductID 819, @CheckDate;   
GO  
```  
  
 Si el procedimiento realiza cambios en una instancia remota de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], dichos cambios no se pueden revertir. Los procedimientos remotos no intervienen en las transacciones.  
  
 Para que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] haga referencia al método correcto cuando está sobrecargado en .NET Framework, el método especificado en la cláusula EXTERNAL NAME debe tener las características siguientes:  
  
-   Ser declarado un método estático.  
  
-   Recibir el mismo número de parámetros que el número de parámetros del procedimiento.  
  
-   Usar tipos de parámetros compatibles con los tipos de datos de los parámetros correspondientes del procedimiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener información acerca de la coincidencia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos a la [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] tipos de datos, consulte [asignación de datos de parámetro de CLR](../../relational-databases/clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md).  
  
## <a name="metadata"></a>Metadatos  
 En la tabla siguiente se enumeran las vistas de catálogo y las vistas de administración dinámica que puede usar para devolver información sobre los procedimientos almacenados.  
  
|Ver|Description|  
|----------|-----------------|  
|[sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)|Devuelve la definición de un procedimiento de [!INCLUDE[tsql](../../includes/tsql-md.md)]. El texto de un procedimiento creado con la opción ENCRYPTION no se pueden ver mediante el uso de la **sys.sql_modules** vista de catálogo.|  
|[Sys.assembly_modules](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)|Devuelve información sobre un procedimiento CLR.|  
|[Sys.Parameters](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)|Devuelve información sobre los parámetros definidos en un procedimiento.|  
|[Sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) [sys.dm_sql_referenced_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md) [sys.dm_sql_referencing_entities](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)|Devuelve los objetos a los que hace referencia un procedimiento.|  
  
 Para calcular el tamaño de un procedimiento compilado, use los siguientes contadores del Monitor de rendimiento.  
  
|Nombre del objeto del Monitor de rendimiento|Nombre del contador del Monitor de rendimiento|  
|-------------------------------------|--------------------------------------|  
|SQLServer: Plan Cache|Frecuencia de aciertos de caché|  
||Páginas de caché|  
||Recuentos de objetos de caché*|  
  
 * Estos contadores están disponibles para varias categorías de objetos de caché, incluidos [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc, [!INCLUDE[tsql](../../includes/tsql-md.md)] preparados, procedimientos, desencadenadores, etc. Para obtener más información, consulte [SQL Server, planear el objeto de caché](../../relational-databases/performance-monitor/sql-server-plan-cache-object.md).  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 Requiere **CREATE PROCEDURE** permiso en la base de datos y **ALTER** permiso en el esquema en el que se va a crear el procedimiento o debe pertenecer a la **db_ddladmin** rol fijo de base de datos.  
  
 Para conocer los procedimientos almacenados de CLR, se necesita la propiedad del ensamblado al que hace referencia en la cláusula EXTERNAL NAME o **referencias** permiso en ese ensamblado.  
  
##  <a name="mot"></a>CREATE PROCEDURE y tablas optimizadas en memoria  
 Pueden tener acceso a tablas optimizadas en memoria mediante procedimientos almacenados compilados de forma nativa y tradicionales. Procedimientos nativos están en la mayoría de los casos la manera más eficaz.
Para obtener más información, consulte [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
  
 El ejemplo siguiente muestra cómo crear un procedimiento almacenado compilado de forma nativa que tiene acceso a una tabla con optimización para memoria `dbo.Departments`:  
  
```sql  
CREATE PROCEDURE dbo.usp_add_kitchen @dept_id int, @kitchen_count int NOT NULL  
WITH EXECUTE AS OWNER, SCHEMABINDING, NATIVE_COMPILATION  
AS  
BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english')  
  
  UPDATE dbo.Departments  
  SET kitchen_count = ISNULL(kitchen_count, 0) + @kitchen_count  
  WHERE id = @dept_id  
END;  
GO  
```  
  
 Un procedimiento creado sin NATIVE_COMPILATION no se puede modificar en un procedimiento almacenado compilado de forma nativa. 
  
 Para obtener una descripción de la programación en procedimientos almacenados compilados de forma nativa, admiten el área expuesta de consulta y operadores, vea [características admitidas para módulos T-SQL compilados forma nativa](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md).  
  
## <a name="Examples"></a> Ejemplos  
  
|Categoría|Elementos de sintaxis ofrecidos|  
|--------------|------------------------------|  
|[Sintaxis básica](#BasicSyntax)|CREATE PROCEDURE|  
|[Pasar parámetros](#Parameters)|@parameter <br> &nbsp;&nbsp;• = valor predeterminado <br> &nbsp;&nbsp;• SALIDA <br> &nbsp;&nbsp;tipo de parámetro con valores de tabla • <br> &nbsp;&nbsp;• CURSOR VARYING|  
|[Modificar datos mediante un procedimiento almacenado](#Modify)|UPDATE|  
|[Control de errores](#Error)|TRY…CATCH|  
|[Ofuscar la definición del procedimiento](#Encrypt)|WITH ENCRYPTION|  
|[Forzar la recompilación del procedimiento](#Recompile)|WITH RECOMPILE|  
|[Establecer el contexto de seguridad](#Security)|EXECUTE AS|  
  
###  <a name="BasicSyntax"></a>Sintaxis básica  
 En los ejemplos de esta sección se muestra la funcionalidad básica de la instrucción CREATE PROCEDURE con la sintaxis mínima necesaria.  
  
#### <a name="a-creating-a-simple-transact-sql-procedure"></a>A. Crear un procedimiento simple Transact-SQL  
 En el ejemplo siguiente se crea un procedimiento almacenado que devuelve todos los empleados (nombre y apellidos), sus puestos y los nombres de sus departamentos a partir de una vista de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Este procedimiento no usa ningún parámetro. En el ejemplo se muestran a continuación tres métodos de ejecutar el procedimiento.  
  
```sql  
CREATE PROCEDURE HumanResources.uspGetAllEmployees  
AS  
    SET NOCOUNT ON;  
    SELECT LastName, FirstName, JobTitle, Department  
    FROM HumanResources.vEmployeeDepartment;  
GO  
  
SELECT * FROM HumanResources.vEmployeeDepartment;  
```  
  
 El `uspGetEmployees` se puede ejecutar el procedimiento de las maneras siguientes:  
  
```sql  
EXECUTE HumanResources.uspGetAllEmployees;  
GO  
-- Or  
EXEC HumanResources.uspGetAllEmployees;  
GO  
-- Or, if this procedure is the first statement within a batch:  
HumanResources.uspGetAllEmployees;  
```  
  
#### <a name="b-returning-more-than-one-result-set"></a>B. Devolver más de un conjunto de resultados  
 El procedimiento siguiente devuelve dos conjuntos de resultados.  
  
```sql  
CREATE PROCEDURE dbo.uspMultipleResults   
AS  
SELECT TOP(10) BusinessEntityID, Lastname, FirstName FROM Person.Person;  
SELECT TOP(10) CustomerID, AccountNumber FROM Sales.Customer;  
GO  
```  
  
#### <a name="c-creating-a-clr-stored-procedure"></a>C. Crear un procedimiento almacenado CLR  
 En el ejemplo siguiente se crea el `GetPhotoFromDB` procedimiento que hace referencia el `GetPhotoFromDB` método de la `LargeObjectBinary` clase en la `HandlingLOBUsingCLR` ensamblado. Antes de crea el procedimiento, el `HandlingLOBUsingCLR` ensamblado se registra en la base de datos local.  
  
**Se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] (si utiliza un ensamblado creado a partir de *assembly_bits.*  
  
```sql  
CREATE ASSEMBLY HandlingLOBUsingCLR  
FROM '\\MachineName\HandlingLOBUsingCLR\bin\Debug\HandlingLOBUsingCLR.dll';  
GO  
CREATE PROCEDURE dbo.GetPhotoFromDB  
(  
    @ProductPhotoID int,  
    @CurrentDirectory nvarchar(1024),  
    @FileName nvarchar(1024)  
)  
AS EXTERNAL NAME HandlingLOBUsingCLR.LargeObjectBinary.GetPhotoFromDB;  
GO  
```  
  
###  <a name="Parameters"></a>Pasar parámetros  
 En los ejemplos de esta sección se muestra cómo usar parámetros de entrada y de salida para pasar valores a y desde un procedimiento almacenado.  
  
#### <a name="d-creating-a-procedure-with-input-parameters"></a>D. Crear un procedimiento con parámetros de entrada  
 En el ejemplo siguiente se crea un procedimiento almacenado que devuelve información sobre un empleado concreto pasando valores para el nombre y los apellidos del empleado. Este procedimiento solo acepta coincidencias exactas de los parámetros pasados.  
  
```sql  
IF OBJECT_ID ( 'HumanResources.uspGetEmployees', 'P' ) IS NOT NULL   
    DROP PROCEDURE HumanResources.uspGetEmployees;  
GO  
CREATE PROCEDURE HumanResources.uspGetEmployees   
    @LastName nvarchar(50),   
    @FirstName nvarchar(50)   
AS   
  
    SET NOCOUNT ON;  
    SELECT FirstName, LastName, JobTitle, Department  
    FROM HumanResources.vEmployeeDepartment  
    WHERE FirstName = @FirstName AND LastName = @LastName;  
GO  
  
```  
  
 El `uspGetEmployees` se puede ejecutar el procedimiento de las maneras siguientes:  
  
```  
EXECUTE HumanResources.uspGetEmployees N'Ackerman', N'Pilar';  
-- Or  
EXEC HumanResources.uspGetEmployees @LastName = N'Ackerman', @FirstName = N'Pilar';  
GO  
-- Or  
EXECUTE HumanResources.uspGetEmployees @FirstName = N'Pilar', @LastName = N'Ackerman';  
GO  
-- Or, if this procedure is the first statement within a batch:  
HumanResources.uspGetEmployees N'Ackerman', N'Pilar';  
  
```  
  
#### <a name="e-using-a-procedure-with-wildcard-parameters"></a>E. Usar un procedimiento con parámetros comodín  
 En el ejemplo siguiente se crea un procedimiento almacenado que devuelve información sobre empleados pasando valores totales o parciales para el nombre y los apellidos de los empleados. Este patrón de procedimiento coincide con los parámetros pasados o, si no se proporcionan, utiliza los valores predeterminados (apellidos que comienzan con la letra `D`).  
  
```sql  
IF OBJECT_ID ( 'HumanResources.uspGetEmployees2', 'P' ) IS NOT NULL   
    DROP PROCEDURE HumanResources.uspGetEmployees2;  
GO  
CREATE PROCEDURE HumanResources.uspGetEmployees2   
    @LastName nvarchar(50) = N'D%',   
    @FirstName nvarchar(50) = N'%'  
AS   
    SET NOCOUNT ON;  
    SELECT FirstName, LastName, JobTitle, Department  
    FROM HumanResources.vEmployeeDepartment  
    WHERE FirstName LIKE @FirstName AND LastName LIKE @LastName;  
```  
  
 El `uspGetEmployees2` procedimiento se puede ejecutar en muchas combinaciones. Aquí se muestran solo algunas combinaciones posibles.  
  
```sql  
EXECUTE HumanResources.uspGetEmployees2;  
-- Or  
EXECUTE HumanResources.uspGetEmployees2 N'Wi%';  
-- Or  
EXECUTE HumanResources.uspGetEmployees2 @FirstName = N'%';  
-- Or  
EXECUTE HumanResources.uspGetEmployees2 N'[CK]ars[OE]n';  
-- Or  
EXECUTE HumanResources.uspGetEmployees2 N'Hesse', N'Stefen';  
-- Or  
EXECUTE HumanResources.uspGetEmployees2 N'H%', N'S%';  
```  
  
#### <a name="f-using-output-parameters"></a>F. Usar parámetros OUTPUT  
 En el ejemplo siguiente se crea el procedimiento `uspGetList`. Este procedimiento devuelve una lista de productos cuyos precios no superan una cantidad especificada. El ejemplo se muestra con varias instrucciones `SELECT` y varios parámetros `OUTPUT`. Los parámetros OUTPUT permiten a un procedimiento externo, un lote o más de una instrucción [!INCLUDE[tsql](../../includes/tsql-md.md)] tener acceso a un conjunto de valores durante la ejecución del procedimiento.  
  
```sql  
IF OBJECT_ID ( 'Production.uspGetList', 'P' ) IS NOT NULL   
    DROP PROCEDURE Production.uspGetList;  
GO  
CREATE PROCEDURE Production.uspGetList @Product varchar(40)   
    , @MaxPrice money   
    , @ComparePrice money OUTPUT  
    , @ListPrice money OUT  
AS  
    SET NOCOUNT ON;  
    SELECT p.[Name] AS Product, p.ListPrice AS 'List Price'  
    FROM Production.Product AS p  
    JOIN Production.ProductSubcategory AS s   
      ON p.ProductSubcategoryID = s.ProductSubcategoryID  
    WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice;  
-- Populate the output variable @ListPprice.  
SET @ListPrice = (SELECT MAX(p.ListPrice)  
        FROM Production.Product AS p  
        JOIN  Production.ProductSubcategory AS s   
          ON p.ProductSubcategoryID = s.ProductSubcategoryID  
        WHERE s.[Name] LIKE @Product AND p.ListPrice < @MaxPrice);  
-- Populate the output variable @compareprice.  
SET @ComparePrice = @MaxPrice;  
GO  
```  
  
 Ejecute `uspGetList` para obtener una lista de los productos de [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] (bicicletas) que cuestan menos de `$700`. El `OUTPUT` parámetros `@Cost` y `@ComparePrices` se utilizan con lenguaje de control de flujo para devolver un mensaje en el **mensajes** ventana.  
  
> [!NOTE]  
>  La variable OUTPUT debe definirse al crear el procedimiento y también al utilizar la variable. El nombre del parámetro y el nombre de la variable no tienen que coincidir; Sin embargo, deben coincidir, a menos que el tipo de datos y la posición de parámetro `@ListPrice`  =  *variable* se utiliza.  
  
```sql  
DECLARE @ComparePrice money, @Cost money ;  
EXECUTE Production.uspGetList '%Bikes%', 700,   
    @ComparePrice OUT,   
    @Cost OUTPUT  
IF @Cost <= @ComparePrice   
BEGIN  
    PRINT 'These products can be purchased for less than   
    $'+RTRIM(CAST(@ComparePrice AS varchar(20)))+'.'  
END  
ELSE  
    PRINT 'The prices for all products in this category exceed   
    $'+ RTRIM(CAST(@ComparePrice AS varchar(20)))+'.';  
```  
  
 Éste es el conjunto de resultados parciales:  
  
 ```   
 Product                     List Price  
 --------------------------  ----------  
 Road-750 Black, 58          539.99  
 Mountain-500 Silver, 40     564.99  
 Mountain-500 Silver, 42     564.99  
 ...  
 Road-750 Black, 48          539.99  
 Road-750 Black, 52          539.99  
   
 (14 row(s) affected)   
  
 These items can be purchased for less than $700.00.
 ```  
  
#### <a name="g-using-a-table-valued-parameter"></a>G. Usar un parámetro con valores de tabla  
 En el ejemplo siguiente se usa un tipo de parámetro con valores de tabla para insertar varias filas en una tabla. En el ejemplo se crea el tipo de parámetro, se declara una variable de tabla para hacer referencia a ella, se rellena la lista de parámetros y, a continuación, se pasan los valores a un procedimiento almacenado. El procedimiento almacenado usa los valores para insertar varias filas en una tabla.  
  
```sql  
/* Create a table type. */  
CREATE TYPE LocationTableType AS TABLE   
( LocationName VARCHAR(50)  
, CostRate INT );  
GO  
  
/* Create a procedure to receive data for the table-valued parameter. */  
CREATE PROCEDURE usp_InsertProductionLocation  
    @TVP LocationTableType READONLY  
    AS   
    SET NOCOUNT ON  
    INSERT INTO [AdventureWorks2012].[Production].[Location]  
           ([Name]  
           ,[CostRate]  
           ,[Availability]  
           ,[ModifiedDate])  
        SELECT *, 0, GETDATE()  
        FROM  @TVP;  
GO  
  
/* Declare a variable that references the type. */  
DECLARE @LocationTVP   
AS LocationTableType;  
  
/* Add data to the table variable. */  
INSERT INTO @LocationTVP (LocationName, CostRate)  
    SELECT [Name], 0.00  
    FROM   
    [AdventureWorks2012].[Person].[StateProvince];  
  
/* Pass the table variable data to a stored procedure. */  
EXEC usp_InsertProductionLocation @LocationTVP;  
GO  
```  
  
##### <a name="h-using-an-output-cursor-parameter"></a>H. Usar un parámetro de cursor OUTPUT  
 En el ejemplo siguiente se usa el parámetro de cursor OUTPUT para devolver un cursor que es local en un procedimiento al lote, procedimiento o desencadenador que llama.  
  
 Primero, crea el procedimiento que declara y, a continuación, abre un cursor en la tabla `Currency`:  
  
```sql  
CREATE PROCEDURE dbo.uspCurrencyCursor   
    @CurrencyCursor CURSOR VARYING OUTPUT  
AS  
    SET NOCOUNT ON;  
    SET @CurrencyCursor = CURSOR  
    FORWARD_ONLY STATIC FOR  
      SELECT CurrencyCode, Name  
      FROM Sales.Currency;  
    OPEN @CurrencyCursor;  
GO  
```  
  
 A continuación, ejecuta un lote que declara una variable local de cursor, ejecuta el procedimiento para asignar el cursor a la variable local y, por último, captura las filas desde el cursor.  
  
```sql  
DECLARE @MyCursor CURSOR;  
EXEC dbo.uspCurrencyCursor @CurrencyCursor = @MyCursor OUTPUT;  
WHILE (@@FETCH_STATUS = 0)  
BEGIN;  
     FETCH NEXT FROM @MyCursor;  
END;  
CLOSE @MyCursor;  
DEALLOCATE @MyCursor;  
GO  
```  
  
###  <a name="Modify"></a>Modificar datos mediante un procedimiento almacenado  
 En los ejemplos de esta sección se muestra cómo insertar o modificar datos de tablas o vistas incluyendo una instrucción del lenguaje de manipulación de datos (DML) en la definición del procedimiento.  
  
#### <a name="i-using-update-in-a-stored-procedure"></a>I. Usar UPDATE en un procedimiento almacenado  
 En el ejemplo siguiente se usa una instrucción UPDATE en un procedimiento almacenado. El procedimiento toma un parámetro de entrada `@NewHours` y un parámetro de salida `@RowCount`. El `@NewHours` el valor del parámetro se utiliza en la instrucción UPDATE para actualizar la columna `VacationHours` en la tabla `HumanResources.Employee`. El parámetro de salida `@RowCount` se usa para devolver el número de filas afectadas a una variable local. Se usa una expresión CASE en la cláusula SET para determinar de forma condicional el valor establecido para `VacationHours`. Cuando se paga al empleado por hora (`SalariedFlag` = 0), `VacationHours` se establece en el número actual de horas más el valor especificado en `@NewHours`; de lo contrario, `VacationHours` se establece en el valor especificado en `@NewHours`.  
  
```sql  
CREATE PROCEDURE HumanResources.Update_VacationHours  
@NewHours smallint  
AS   
SET NOCOUNT ON;  
UPDATE HumanResources.Employee  
SET VacationHours =   
    ( CASE  
         WHEN SalariedFlag = 0 THEN VacationHours + @NewHours  
         ELSE @NewHours  
       END  
    )  
WHERE CurrentFlag = 1;  
GO  
  
EXEC HumanResources.Update_VacationHours 40;  
```  
  
###  <a name="Error"></a>Control de errores  
 En los ejemplos de esta sección se muestran métodos de controlar errores que pueden producirse cuando se ejecuta el procedimiento almacenado.  
  
#### <a name="j-using-trycatch"></a>J. Usar TRY…CATCH  
 En el ejemplo siguiente se usa la construcción TRY…CATCH para devolver información de error capturada durante la ejecución de un procedimiento almacenado.  
  
```sql  
CREATE PROCEDURE Production.uspDeleteWorkOrder ( @WorkOrderID int )  
AS  
SET NOCOUNT ON;  
BEGIN TRY  
   BEGIN TRANSACTION   
   -- Delete rows from the child table, WorkOrderRouting, for the specified work order.  
   DELETE FROM Production.WorkOrderRouting  
   WHERE WorkOrderID = @WorkOrderID;  
  
   -- Delete the rows from the parent table, WorkOrder, for the specified work order.  
   DELETE FROM Production.WorkOrder  
   WHERE WorkOrderID = @WorkOrderID;  
  
   COMMIT  
  
END TRY  
BEGIN CATCH  
  -- Determine if an error occurred.  
  IF @@TRANCOUNT > 0  
     ROLLBACK  
  
  -- Return the error information.  
  DECLARE @ErrorMessage nvarchar(4000),  @ErrorSeverity int;  
  SELECT @ErrorMessage = ERROR_MESSAGE(),@ErrorSeverity = ERROR_SEVERITY();  
  RAISERROR(@ErrorMessage, @ErrorSeverity, 1);  
END CATCH;  
  
GO  
EXEC Production.uspDeleteWorkOrder 13;  
  
/* Intentionally generate an error by reversing the order in which rows 
   are deleted from the parent and child tables. This change does not 
   cause an error when the procedure definition is altered, but produces 
   an error when the procedure is executed.  
*/  
ALTER PROCEDURE Production.uspDeleteWorkOrder ( @WorkOrderID int )  
AS  
  
BEGIN TRY  
   BEGIN TRANSACTION   
      -- Delete the rows from the parent table, WorkOrder, for the specified work order.  
   DELETE FROM Production.WorkOrder  
   WHERE WorkOrderID = @WorkOrderID;  
  
   -- Delete rows from the child table, WorkOrderRouting, for the specified work order.  
   DELETE FROM Production.WorkOrderRouting  
   WHERE WorkOrderID = @WorkOrderID;  
  
   COMMIT TRANSACTION  
  
END TRY  
BEGIN CATCH  
  -- Determine if an error occurred.  
  IF @@TRANCOUNT > 0  
     ROLLBACK TRANSACTION  
  
  -- Return the error information.  
  DECLARE @ErrorMessage nvarchar(4000),  @ErrorSeverity int;  
  SELECT @ErrorMessage = ERROR_MESSAGE(),@ErrorSeverity = ERROR_SEVERITY();  
  RAISERROR(@ErrorMessage, @ErrorSeverity, 1);  
END CATCH;  
GO  
-- Execute the altered procedure.  
EXEC Production.uspDeleteWorkOrder 15;  
  
DROP PROCEDURE Production.uspDeleteWorkOrder;  
```  
  
###  <a name="Encrypt"></a>Ofuscar la definición del procedimiento  
 En los ejemplos de esta sección se muestra cómo ofuscar la definición del procedimiento almacenado.  
  
#### <a name="k-using-the-with-encryption-option"></a>K. Usar la opción WITH ENCRYPTION  
 En el ejemplo siguiente se crea el procedimiento `HumanResources.uspEncryptThis`.  
  
**Se aplica a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], base de datos SQL.  
  
```sql  
CREATE PROCEDURE HumanResources.uspEncryptThis  
WITH ENCRYPTION  
AS  
    SET NOCOUNT ON;  
    SELECT BusinessEntityID, JobTitle, NationalIDNumber, 
        VacationHours, SickLeaveHours   
    FROM HumanResources.Employee;  
GO  
```  
  
 El `WITH ENCRYPTION` opción ofusca la definición del procedimiento al consultar el catálogo del sistema o mediante metadatos de las funciones, como se muestra en los ejemplos siguientes.  
  
 Run `sp_helptext`:  
  
```sql  
EXEC sp_helptext 'HumanResources.uspEncryptThis';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `The text for object 'HumanResources.uspEncryptThis' is encrypted.`  
  
 Consultar directamente la `sys.sql_modules` vista de catálogo:  
  
```sql  
SELECT definition FROM sys.sql_modules  
WHERE object_id = OBJECT_ID('HumanResources.uspEncryptThis');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 definition  
 --------------------------------  
 NULL  
 ```  
  
###  <a name="Recompile"></a>Forzar la recompilación del procedimiento  
 En los ejemplos de esta sección se usa la cláusula WITH RECOMPILE para forzar la recompilación del procedimiento cada vez que se ejecute.  
  
#### <a name="l-using-the-with-recompile-option"></a>L. Usar la opción WITH RECOMPILE  
 El `WITH RECOMPILE` cláusula es útil cuando los parámetros suministrados al procedimiento no son típicos y cuando un nuevo plan de ejecución no se almacena en caché o almacenado en memoria.  
  
```sql  
IF OBJECT_ID ( 'dbo.uspProductByVendor', 'P' ) IS NOT NULL   
    DROP PROCEDURE dbo.uspProductByVendor;  
GO  
CREATE PROCEDURE dbo.uspProductByVendor @Name varchar(30) = '%'  
WITH RECOMPILE  
AS  
    SET NOCOUNT ON;  
    SELECT v.Name AS 'Vendor name', p.Name AS 'Product name'  
    FROM Purchasing.Vendor AS v   
    JOIN Purchasing.ProductVendor AS pv   
      ON v.BusinessEntityID = pv.BusinessEntityID   
    JOIN Production.Product AS p   
      ON pv.ProductID = p.ProductID  
    WHERE v.Name LIKE @Name;  
```  
  
###  <a name="Security"></a>Establecer el contexto de seguridad  
 En los ejemplos de esta sección se usa la cláusula EXECUTE AS para establecer el contexto de seguridad en el que se ejecuta el procedimiento almacenado.  
  
#### <a name="m-using-the-execute-as-clause"></a>M. Usar la cláusula EXECUTE AS  
 En el ejemplo siguiente se muestra el uso del [EXECUTE AS](../../t-sql/statements/execute-as-clause-transact-sql.md) cláusula para especificar el contexto de seguridad en el que se puede ejecutar un procedimiento. En el ejemplo, la opción `CALLER` especifica que el procedimiento puede ejecutarse en el contexto del usuario que lo llama.  
  
```sql  
CREATE PROCEDURE Purchasing.uspVendorAllInfo  
WITH EXECUTE AS CALLER  
AS  
    SET NOCOUNT ON;  
    SELECT v.Name AS Vendor, p.Name AS 'Product name',   
      v.CreditRating AS 'Rating',   
      v.ActiveFlag AS Availability  
    FROM Purchasing.Vendor v   
    INNER JOIN Purchasing.ProductVendor pv  
      ON v.BusinessEntityID = pv.BusinessEntityID   
    INNER JOIN Production.Product p  
      ON pv.ProductID = p.ProductID   
    ORDER BY v.Name ASC;  
GO  
```  
  
#### <a name="n-creating-custom-permission-sets"></a>N. Crear conjuntos de permisos personalizados  
 En el ejemplo siguiente se usa EXECUTE AS para crear permisos personalizados para una operación de base de datos. Algunas operaciones, como TRUNCATE TABLE, no tienen permisos que se puedan conceder. Si se incorpora la instrucción TRUNCATE TABLE en un procedimiento almacenado y se especifica la ejecución del procedimiento como un usuario con permisos para modificar la tabla, se pueden ampliar los permisos para truncar la tabla al usuario al que se concedan permisos EXECUTE en el procedimiento.  
  
```sql  
CREATE PROCEDURE dbo.TruncateMyTable  
WITH EXECUTE AS SELF  
AS TRUNCATE TABLE MyDB..MyTable;  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="o-create-a-stored-procedure-that-runs-a-select-statement"></a>O. Crear un procedimiento almacenado que se ejecuta una instrucción SELECT  
 Este ejemplo muestra la sintaxis básica para crear y ejecutar un procedimiento. Cuando se ejecuta un lote, CREATE PROCEDURE debe ser la primera instrucción. Por ejemplo, cree el siguiente procedimiento almacenado en [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)], establecer el contexto de base de datos en primer lugar y, a continuación, ejecute la instrucción CREATE PROCEDURE.  
  
```sql  
-- Uses AdventureWorksDW database  
  
--Run CREATE PROCEDURE as the first statement in a batch.  
CREATE PROCEDURE Get10TopResellers   
AS   
BEGIN  
    SELECT TOP (10) r.ResellerName, r.AnnualSales  
    FROM DimReseller AS r  
    ORDER BY AnnualSales DESC, ResellerName ASC;  
END  
;  
  
--Show 10 Top Resellers  
EXEC Get10TopResellers;  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [Lenguaje de control de flujo &#40; Transact-SQL &#41;](~/t-sql/language-elements/control-of-flow.md)   
 [Cursores](../../relational-databases/cursors.md)   
 [Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [DROP PROCEDURE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-procedure-transact-sql.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [EJECUTAR AS &#40; Transact-SQL &#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [Procedimientos almacenados &#40;motor de base de datos&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)   
 [sp_procoption &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-procoption-transact-sql.md)   
 [sp_recompile &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.parameters &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-parameters-transact-sql.md)   
 [sys.procedures &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-procedures-transact-sql.md)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-assembly-modules-transact-sql.md)   
 [Sys.numbered_procedures &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-numbered-procedures-transact-sql.md)   
 [Sys.numbered_procedure_parameters &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-numbered-procedure-parameters-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [Crear un procedimiento almacenado](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [Usar con valores de tabla parámetros &#40; motor de base de datos &#41;](../../relational-databases/tables/use-table-valued-parameters-database-engine.md)   
 [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql.md)   
 [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql.md)  
  
  




