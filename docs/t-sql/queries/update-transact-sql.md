---
title: UPDATE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 09/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- UPDATE_TSQL
- UPDATE
dev_langs: TSQL
helpviewer_keywords:
- DML [SQL Server], UPDATE statement
- data updates [SQL Server], UPDATE statement
- updating data [SQL Server]
- TOP clause, UPDATE
- OUTPUT clause
- large value data types
- data manipulation language [SQL Server], UPDATE statement
- user-defined types [SQL Server], modifying
- INSTEAD OF triggers
- modifying data [SQL Server], UPDATE statement
- data modifications [SQL Server], UPDATE statement
- large data, modifying
- .WRITE clause
- table modifications [SQL Server], UPDATE statement
- UDTs [SQL Server], modifying
- UPDATE statement [SQL Server], about UPDATE statement
- LOB data [SQL Server], modifying
- modifying LOB data
- UPDATE statement [SQL Server]
- FROM clause, UPDATE statement
- WHERE clause, UPDATE statement
ms.assetid: 40e63302-0c68-4593-af3e-6d190181fee7
caps.latest.revision: "91"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 671eb95a5c1772ec790886d923112d491bbd2a35
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="update-transact-sql"></a>UPDATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Cambia los datos de una tabla o vista de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener ejemplos, vea [ejemplos](#UpdateExamples).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```tsql  
-- Syntax for SQL Server and Azure SQL Database  

[ WITH <common_table_expression> [...n] ]  
UPDATE   
    [ TOP ( expression ) [ PERCENT ] ]   
    { { table_alias | <object> | rowset_function_limited   
         [ WITH ( <Table_Hint_Limited> [ ...n ] ) ]  
      }  
      | @table_variable      
    }  
    SET  
        { column_name = { expression | DEFAULT | NULL }  
          | { udt_column_name.{ { property_name = expression  
                                | field_name = expression }  
                                | method_name ( argument [ ,...n ] )  
                              }  
          }  
          | column_name { .WRITE ( expression , @Offset , @Length ) }  
          | @variable = expression  
          | @variable = column = expression  
          | column_name { += | -= | *= | /= | %= | &= | ^= | |= } expression  
          | @variable { += | -= | *= | /= | %= | &= | ^= | |= } expression  
          | @variable = column { += | -= | *= | /= | %= | &= | ^= | |= } expression  
        } [ ,...n ]   
  
    [ <OUTPUT Clause> ]  
    [ FROM{ <table_source> } [ ,...n ] ]   
    [ WHERE { <search_condition>   
            | { [ CURRENT OF   
                  { { [ GLOBAL ] cursor_name }   
                      | cursor_variable_name   
                  }   
                ]  
              }  
            }   
    ]   
    [ OPTION ( <query_hint> [ ,...n ] ) ]  
[ ; ]  
  
<object> ::=  
{   
    [ server_name . database_name . schema_name .   
    | database_name .[ schema_name ] .   
    | schema_name .  
    ]  
    table_or_view_name}  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  

UPDATE [ database_name . [ schema_name ] . | schema_name . ] table_name   
SET { column_name = { expression | NULL } } [ ,...n ]  
[ FROM from_clause ]  
[ WHERE <search_condition> ]   
[ OPTION ( LABEL = label_name ) ]  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 CON \<common_table_expression >  
 Especifica la vista o el conjunto de resultados temporal indicado, que también se conoce como expresión de tabla común (CTE), definido en el ámbito de la instrucción UPDATE. El conjunto de resultados CTE se deriva de una consulta simple. La instrucción UPDATE hace referencia al conjunto de resultados.  
  
 Las expresiones de tabla comunes también se pueden utilizar con las instrucciones SELECT, INSERT, DELETE y CREATE VIEW. Para obtener más información, consulte [con common_table_expression &#40; Transact-SQL &#41; ](../../t-sql/queries/with-common-table-expression-transact-sql.md).  
  
 Parte superior **(** *expresión***)** [%]  
 Especifica el número o porcentaje de filas que se actualizan. *expression* puede ser un número o un porcentaje de las filas.  
  
 Las filas a las que se hace referencia en la expresión TOP utilizada con INSERT, UPDATE o DELETE no se ordenan.  
  
 Utilizar paréntesis para delimitar *expresión* en la parte superior se requieren en instrucciones INSERT, UPDATE y DELETE. Para obtener más información, vea [TOP &#40; Transact-SQL &#41; ](../../t-sql/queries/top-transact-sql.md).  
  
 *aliasTabla*  
 Alias especificado en la cláusula FROM que representa la tabla o vista de la que se van a actualizar las filas.  
  
 *nombre_servidor*  
 Es el nombre del servidor (con un nombre de servidor vinculado o [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) funcionar como el nombre del servidor) en el que se encuentra la tabla o vista. Si *nombre_servidor* se especifica, *database_name* y *schema_name* son necesarios.  
  
 *database_name*  
 Es el nombre de la base de datos.  
  
 *schema_name*  
 Es el nombre del esquema al que pertenece la tabla o la vista.  
  
 *view_name table_or*  
 Es el nombre de la tabla o vista cuyas filas se deben actualizar. La vista hace referencia a *nombre_tabla_o_vista* debe ser actualizable y referencia exactamente a una tabla base en la cláusula FROM de la vista. Para obtener más información acerca de las vistas actualizables, vea [CREATE VIEW &#40; Transact-SQL &#41; ](../../t-sql/statements/create-view-transact-sql.md).  
  
 *funciónConjuntoFilasLimitado*  
 Es el [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) o [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) función, dependiendo del proveedor.  
  
 CON **(** \<sugerenciaTablaLimitada > **)**  
 Especifica una o varias sugerencias de tabla que están permitidas en una tabla de destino. La palabra clave WITH y los paréntesis son obligatorios. No se permiten NOLOCK ni READUNCOMMITTED. Para obtener información acerca de las sugerencias de tabla, vea [sugerencias de tabla &#40; Transact-SQL &#41; ](../../t-sql/queries/hints-transact-sql-table.md).  
  
 @*table_variable*  
 Especifica un [tabla](../../t-sql/data-types/table-transact-sql.md) variable como una tabla de origen.  
  
 SET  
 Especifica la lista de nombres de variable o de columna que se van a actualizar.  
  
 *column_name*  
 Es una columna que contiene los datos que se van a cambiar. *column_name* debe existir en *table_or view_name*. Las columnas de identidad no se pueden actualizar.  
  
 *expression*  
 Es una variable, un valor literal, una expresión o una instrucción de subselección entre paréntesis que devuelve un solo valor. El valor devuelto por *expresión* reemplaza al valor existente en *column_name* o  *@variable* .  
  
> [!NOTE]  
>  Al hacer referencia a los tipos de datos de caracteres Unicode **nchar**, **nvarchar**, y **ntext**, 'expression' debe agregarse como prefijo la letra mayúscula ' n '. Si no se especifica 'N', [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] convierte la cadena a la página de códigos que se corresponde con la intercalación predeterminada de la base de datos o columna. Los caracteres que no se encuentren en esta página de códigos se perderán.  
  
 DEFAULT  
 Especifica que el valor predeterminado definido para la columna debe reemplazar al valor existente en esa columna. Esta operación también puede utilizarse para cambiar la columna a NULL si no tiene asignado ningún valor predeterminado y se ha definido para aceptar valores NULL.  
  
 { **+=** | **-=** | **\*=** | **/=** | **%=** | **&=** | **^=** | **|=** }  
 Operador de asignación compuesta:  
 += Sumar y asignar  
 -= Restar y asignar  
 * = Multiplicar y asignar  
 / = Dividir y asignar  
 % = Módulo y asignar  
 & = AND bit a bit y asignar  
 ^ = XOR bit a bit y asignar  
 | = OR bit a bit y asignar  
  
 *udt_column_name*  
 Es una columna de un tipo definido por el usuario.  
  
 *property_name* | *Nombre_de_campo*  
 Es un miembro de propiedad público o un miembro de datos público de un tipo definido por el usuario.  
  
 *NombreMétodo* **(** *argumento* [ **,**... *n*] **)**  
 Es un método mutador público no estático de *udt_column_name* que toma uno o más argumentos.  
  
 **.** Escribir **(***expresión***,***@Offset***,** *@Length***)**  
 Especifica que una sección del valor de *column_name* consiste en modificar. *expresión* reemplaza  *@Length*  unidades desde  *@Offset*  de *column_name*. Solo las columnas de **varchar (max)**, **nvarchar (max)**, o **varbinary (max)** puede especificarse con esta cláusula. *column_name* no puede ser NULL y no se puede calificar con un nombre de tabla o el alias de la tabla.  
  
 *expresión* es el valor que se copia en *column_name*. *expresión* debe evaluar, o que pueda convertirse implícitamente a la *column_name* tipo. Si *expresión* se establece en NULL,  *@Length*  se omite y el valor de *column_name* se trunca en el índice especificado  *@Offset* .  
  
 *@Offset*es el punto inicial en el valor de *column_name* en el que *expresión* se escribe. *@Offset*es una posición ordinal basado en cero, es **bigint**, y no puede ser un número negativo. Si  *@Offset*  es NULL, la operación de actualización anexa *expresión* al final de la existente *column_name* valor y  *@Length*  se omite. Si @Offset es mayor que la longitud de la *column_name* valor, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] devuelve un error. Si  *@Offset*  más  *@Length*  excede el final del valor subyacente de la columna, la eliminación produce hasta hasta el último carácter del valor. Si  *@Offset*  plus LEN (*expresión*) es mayor que subyacente declarado tamaño, se produce un error.  
  
 *@Length*es la longitud de la sección en la columna, a partir de  *@Offset* , que se sustituye por *expresión*. *@Length*es **bigint** y no puede ser un número negativo. Si  *@Length*  es NULL, la operación de actualización quita todos los datos de  *@Offset*  al final de la *column_name* valor.  
  
 Para obtener más información, vea la sección Comentarios.  
  
 **@***variable*  
 Es una variable declarada a la que se establece en el valor devuelto por *expresión*.  
  
 ESTABLECER  **@**  *variable* = *columna* = *expresión* establece la variable a la misma valor que la columna. Esto difiere del conjunto  **@**  *variable* = *columna*, *columna*  =  *expresión*, que establece la variable en el valor anterior a la actualización de la columna.  
  
 \<OUTPUT_Clause >  
 Devuelve datos actualizados o expresiones basadas en ellos como parte de la operación UPDATE. La cláusula OUTPUT no se admite en instrucciones DML dirigidas a tablas o vistas remotas. Para obtener más información, vea [cláusula OUTPUT &#40; Transact-SQL &#41; ](../../t-sql/queries/output-clause-transact-sql.md).  
  
 DESDE \<table_source >  
 Especifica que se utiliza un origen de tabla, vista o tabla derivada para proporcionar los criterios de la operación de actualización. Para obtener más información, vea [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md).  
  
 Si el objeto que se actualiza es el que se indica en la cláusula FROM y solo hay una referencia al objeto en ella, puede especificarse o no un alias de objeto. Si el objeto que se actualiza aparece más de una vez en la cláusula FROM, una única referencia al objeto no debe especificar un alias de tabla. Todas las demás referencias al objeto de la cláusula FROM deben incluir un alias de objeto.  
  
 Una vista con un desencadenador INSTEAD OF UPDATE no puede ser el destino de UPDATE con una cláusula FROM.  
  
> [!NOTE]  
>  Las llamadas a OPENDATASOURCE, OPENQUERY u OPENROWSET en la cláusula FROM se evalúan por separado y de forma independiente de otras llamadas a estas funciones utilizadas como destino de la actualización, incluso si se han suministrado argumentos idénticos a las dos llamadas. En particular, las condiciones de filtro o combinación aplicadas en el resultado de una de esas llamadas no tienen ningún efecto en los resultados de la otra llamada.  
  
 WHERE  
 Especifica las condiciones que limitan las filas que se actualizan. Hay dos modos de actualización, dependiendo del formato de cláusula WHERE que se utilice:  
  
-   Las actualizaciones por búsqueda especifican una condición de búsqueda para calificar las filas que se van a eliminar.  
  
-   Las actualizaciones posicionadas utilizan la cláusula CURRENT OF para especificar un cursor. La operación de actualización se produce en la posición actual del cursor.  
  
\<search_condition >  
 Especifica la condición que debe cumplirse para que se actualicen las filas. La condición de búsqueda también puede ser la condición en la que se basa una combinación. No hay límite en el número de predicados que se pueden incluir en una condición de búsqueda. Para obtener más información sobre predicados y condiciones de búsqueda, vea [condición de búsqueda &#40; Transact-SQL &#41; ](../../t-sql/queries/search-condition-transact-sql.md).  
  
CURRENT OF  
 Indica que la actualización se realice en la posición actual del cursor especificado.  
  
 Una actualización posicionada que utiliza una cláusula WHERE CURRENT OF actualiza la fila que se encuentra en la posición actual del cursor. Esto puede ser más preciso que una actualización por búsqueda que utilice un WHERE \<search_condition > cláusula para calificar las filas que se va a actualizar. Una actualización por búsqueda modifica varias filas cuando la condición de búsqueda no identifica una sola fila de forma exclusiva.  
  
GLOBAL  
 Especifica que *cursor_name* hace referencia a un cursor global.  
  
*cursor_name*  
 Es el nombre del cursor abierto desde el que se debe realizar la captura. Si tanto un cursor global y otro local con el nombre *cursor_name* existe, este argumento hace referencia al cursor global si se especifica GLOBAL; en caso contrario, hace referencia al cursor local. El cursor debe permitir actualizaciones.  
  
*cursor_variable_name*  
 Es el nombre de una variable de cursor. *cursor_variable_name* debe hacer referencia a un cursor que permita realizar actualizaciones.  
  
OPCIÓN **(** \<query_hint > [ **,**... *n* ] **)**  
 Especifica que se utilizan las sugerencias del optimizador para personalizar el modo en que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] procesa la instrucción. Para obtener más información, vea [Sugerencias de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
## <a name="best-practices"></a>Procedimientos recomendados  
 Use el @@ROWCOUNT insertado de función para devolver el número de filas a la aplicación cliente. Para obtener más información, consulte [@@ROWCOUNT &#40; Transact-SQL &#41; ](../../t-sql/functions/rowcount-transact-sql.md).  
  
 Es posible utilizar nombres de variables en las instrucciones UPDATE para mostrar los valores nuevos y antiguos afectados, pero solo se recomienda cuando la instrucción UPDATE afecta a un único registro. Si la instrucción UPDATE afecta a varios registros, para devolver los valores antiguos y nuevos para cada registro, use el [cláusula OUTPUT](../../t-sql/queries/output-clause-transact-sql.md).  
  
 Actúe con precaución al especificar la cláusula FROM para proporcionar los criterios de la operación de actualización. Los resultados de una instrucción UPDATE son indefinidos si la instrucción incluye una cláusula FROM que no se especifica de tal forma que solo un valor está disponible para cada ocurrencia de columna que se actualiza, es decir, si la instrucción UPDATE no determinista. Por ejemplo, en la instrucción UPDATE del siguiente script, las dos filas de `Table1` cumplen los requisitos de la cláusula FROM de la instrucción UPDATE, pero no se define qué fila de `Table1` se utiliza para actualizar la fila de `Table2.`  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ('dbo.Table1', 'U') IS NOT NULL  
    DROP TABLE dbo.Table1;  
GO  
IF OBJECT_ID ('dbo.Table2', 'U') IS NOT NULL  
    DROP TABLE dbo.Table2;  
GO  
CREATE TABLE dbo.Table1   
    (ColA int NOT NULL, ColB decimal(10,3) NOT NULL);  
GO  
CREATE TABLE dbo.Table2   
    (ColA int PRIMARY KEY NOT NULL, ColB decimal(10,3) NOT NULL);  
GO  
INSERT INTO dbo.Table1 VALUES(1, 10.0), (1, 20.0);  
INSERT INTO dbo.Table2 VALUES(1, 0.0);  
GO  
UPDATE dbo.Table2   
SET dbo.Table2.ColB = dbo.Table2.ColB + dbo.Table1.ColB  
FROM dbo.Table2   
    INNER JOIN dbo.Table1   
    ON (dbo.Table2.ColA = dbo.Table1.ColA);  
GO  
SELECT ColA, ColB   
FROM dbo.Table2;  
```  
  
 Puede ocurrir el mismo problema cuando se combinan las cláusulas FROM y WHERE CURRENT OF. En el ejemplo siguiente, las dos filas de `Table2` cumplen los requisitos de la cláusula `FROM` de la instrucción `UPDATE`. No se ha definido qué fila de `Table2` se utilizará para actualizar la fila de `Table1`.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ('dbo.Table1', 'U') IS NOT NULL  
    DROP TABLE dbo.Table1;  
GO  
IF OBJECT_ID ('dbo.Table2', 'U') IS NOT NULL  
    DROP TABLE dbo.Table2;  
GO  
CREATE TABLE dbo.Table1  
    (c1 int PRIMARY KEY NOT NULL, c2 int NOT NULL);  
GO  
CREATE TABLE dbo.Table2  
    (d1 int PRIMARY KEY NOT NULL, d2 int NOT NULL);  
GO  
INSERT INTO dbo.Table1 VALUES (1, 10);  
INSERT INTO dbo.Table2 VALUES (1, 20), (2, 30);  
GO  
DECLARE abc CURSOR LOCAL FOR  
    SELECT c1, c2   
    FROM dbo.Table1;  
OPEN abc;  
FETCH abc;  
UPDATE dbo.Table1   
SET c2 = c2 + d2   
FROM dbo.Table2   
WHERE CURRENT OF abc;  
GO  
SELECT c1, c2 FROM dbo.Table1;  
GO  
```  
  
## <a name="compatibility-support"></a>Soporte de compatibilidad  
 En una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se quitará el uso de las sugerencias READUNCOMMITTED y NOLOCK en la cláusula FROM que se aplican a la tabla de destino de una instrucción UPDATE o DELETE. Evite usar estas sugerencias en este contexto en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que las usan actualmente.  
  
## <a name="data-types"></a>Tipos de datos  
 Todos los **char** y **nchar** columnas son rellenado a la derecha hasta la longitud definida.  
  
 Si ANSI_PADDING se establece en OFF, se quitan todos los espacios finales de los datos insertados en **varchar** y **nvarchar** columnas, excepto en las cadenas que contienen solo espacios. Estas cadenas se truncan en una cadena vacía. Si ANSI_PADDING se establece en ON, se insertan espacios al final. El controlador ODBC de Microsoft SQL Server y el proveedor OLE DB para SQL Server establecen automáticamente SET ANSI_PADDING en ON para cada conexión. Se puede configurar en orígenes de datos ODBC o mediante atributos o propiedades de conexión. Para obtener más información, vea [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md).  
  
### <a name="updating-text-ntext-and-image-columns"></a>Actualizar columnas de tipo text, ntext e image  
 Modificar un **texto**, **ntext**, o **imagen** columna con UPDATE inicializa la columna, le asigna un puntero de texto válido y asigna al menos una página de datos, a menos que el se está actualizando la columna con el valor NULL.  
  
 Para reemplazar o modificar bloques grandes de **texto**, **ntext**, o **imagen** datos, usar [WRITETEXT](../../t-sql/queries/writetext-transact-sql.md) o [UPDATETEXT](../../t-sql/queries/updatetext-transact-sql.md) en lugar de la instrucción UPDATE.  
  
 Si la instrucción UPDATE puede cambiar más de una fila al actualizar la clave de agrupación en clústeres y a uno o varios **texto**, **ntext**, o **imagen** columnas, la actualización parcial Estas columnas se ejecuta como una sustitución completa de los valores.  
  
> [!IMPORTANT]  
>  El **ntext**, **texto**, y **imagen** tipos de datos se quitará en una versión futura de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite su uso en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que los usan actualmente. Use [nvarchar(max)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md), [varchar(max)](../../t-sql/data-types/char-and-varchar-transact-sql.md)y [varbinary(max)](../../t-sql/data-types/binary-and-varbinary-transact-sql.md) en su lugar.  
  
### <a name="updating-large-value-data-types"></a>Actualizar tipos de datos de valores grandes  
 Use la **.** ESCRIBIR (*expresión***,**  *@Offset*  **,***@Length*) cláusula para realizar una actualización parcial o completa de **varchar (max)**, **nvarchar (max)**, y **varbinary (max)** tipos de datos. Por ejemplo, una actualización parcial de un **varchar (max)** columna podría eliminar o modificar solo los primeros 200 caracteres de la columna, mientras que una actualización completa eliminaría o modificaría todos los datos de la columna. **.** WRITE que insertan o anexa datos nuevos se registra mínimamente si el modelo de recuperación de base de datos está establecido para registro masivo o simple. El registro mínimo no se utiliza cuando se actualizan los datos existentes. Para más información, consulte [El registro de transacciones &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md).  
  
 El [!INCLUDE[ssDE](../../includes/ssde-md.md)] convierte una actualización parcial en actualización completa cuando la instrucción UPDATE realiza una de estas acciones:  
-   Cambia una columna de clave de la tabla o vista con particiones.  
-   Modifica más de una fila y también actualiza la clave de un índice clúster no único en un valor no constante.  
  
No se puede utilizar el **.** Cláusula de escritura para actualizar una columna NULL o establecer el valor de *column_name* en NULL.  
  
*@Offset*y  *@Length*  se especifican en bytes para **varbinary** y **varchar** tipos de datos y en caracteres para la **nvarchar**tipo de datos. Se calculan los desplazamientos correspondientes para las intercalaciones del juego de caracteres de doble byte (DBCS).  
  
Para que el rendimiento sea óptimo, se recomienda insertar o actualizar los datos en tamaños de fragmento que sean múltiplos de 8.040 bytes.  
  
Si la columna modificada por la **.** ESCRIBIR la cláusula se hace referencia en una cláusula OUTPUT, el valor completo de la columna, o bien la imagen anterior de **eliminado.** *column_name* o la imagen posterior de **insertado.** *column_name*, se devuelve a la columna especificada en la variable de tabla. Vea el ejemplo R que sigue.  
  
Para lograr la misma funcionalidad de **.** ESCRIBIR por otro carácter o tipos de datos binarios, utilice la [cosas &#40; Transact-SQL &#41; ](../../t-sql/functions/stuff-transact-sql.md).  
  
### <a name="updating-user-defined-type-columns"></a>Actualizar columnas de tipos definidos por el usuario  
 Hay varios métodos para actualizar los valores de columnas de tipos definidos por el usuario:  
  
-   Suministrar un valor de un tipo de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], siempre y cuando el tipo definido por el usuario admita la conversión implícita o explícita desde ese tipo. En el ejemplo siguiente se muestra cómo actualizar un valor de una columna de tipo `Point`, definido por el usuario, mediante la conversión explícita de una cadena.  
  
    ```sql  
    UPDATE Cities  
    SET Location = CONVERT(Point, '12.3:46.2')  
    WHERE Name = 'Anchorage';  
    ```  
  
-   Invocar un método, marcado como mutator, del tipo definido por el usuario, para realizar la actualización. En el ejemplo siguiente se invoca un método mutador de tipo `Point` denominado `SetXY`. Esto actualiza el estado de la instancia del tipo.  
  
    ```sql  
    UPDATE Cities  
    SET Location.SetXY(23.5, 23.5)  
    WHERE Name = 'Anchorage';  
    ```  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve un error si se invoca un método mutador en un valor NULL de [!INCLUDE[tsql](../../includes/tsql-md.md)], o si un nuevo valor producido por un método mutador es NULL.  
  
-   Modificar el valor de un miembro de propiedad registrado o un miembro de datos público del tipo definido por el usuario. La expresión que suministra el valor debe poder convertirse implícitamente al tipo de la propiedad. En el ejemplo siguiente se modifica el valor de la propiedad `X` del tipo `Point` definido por el usuario.  
  
    ```sql  
    UPDATE Cities  
    SET Location.X = 23.5  
    WHERE Name = 'Anchorage';  
    ```  
  
     Para modificar diferentes propiedades de la misma columna de tipo definido por el usuario, emita varias instrucciones UPDATE o invoque un método mutador del tipo.  
  
### <a name="updating-filestream-data"></a>Actualizar datos FILESTREAM  
 Puede utilizar la instrucción UPDATE para actualizar un campo FILESTREAM de forma que tenga un valor nulo, un valor vacío o una cantidad relativamente pequeña de datos insertados. Sin embargo, se envía una gran cantidad de datos de manera más eficaz en un archivo si se utilizan interfaces de Win32. Al actualizar un campo FILESTREAM, modifica los datos de BLOB subyacentes en el sistema de archivos. Cuando un campo FILESTREAM está establecido en NULL, se eliminan los datos de BLOB asociados al campo. No se puede usar. Write() para realizar actualizaciones parciales de los datos de FILESTREAM. Para obtener más información, vea [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
## <a name="error-handling"></a>Tratamiento de errores  
 Si la actualización de una fila infringe una restricción o una regla, infringe la configuración de valores NULL de la columna o, si el nuevo valor es de un tipo de datos incompatible, se cancela la instrucción, se devuelve un error y no se actualiza ningún registro.  
  
 Cuando una instrucción UPDATE encuentra un error aritmético (error de desbordamiento, división por cero o de dominio) durante la evaluación de la expresión, la actualización no se lleva a cabo. El resto del lote no se ejecuta y se devuelve un mensaje de error.  
  
 Si la actualización de una o varias columnas que participan en un índice clúster hace que el tamaño del mismo y de la fila supere 8.060 bytes, la actualización no se produce y se devuelve un mensaje de error.  
  
## <a name="interoperability"></a>Interoperabilidad  
 Se pueden utilizar instrucciones UPDATE en el cuerpo de las funciones definidas por el usuario solamente si la tabla que se modifica es una variable de tabla.  
  
 Cuando se define un desencadenador INSTEAD OF para las acciones UPDATE de una tabla, se ejecuta el desencadenador en lugar de la instrucción UPDATE. En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo se admite la definición de desencadenadores AFTER en instrucciones UPDATE y otras instrucciones de modificación de datos. No se puede especificar la cláusula FROM en una instrucción UPDATE que haga referencia, directa o indirectamente, a una vista que tenga definido un desencadenador INSTEAD OF. Para obtener más información acerca de desencadenadores INSTEAD OF, vea [CREATE TRIGGER &#40; Transact-SQL &#41; ](../../t-sql/statements/create-trigger-transact-sql.md).  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 No se puede especificar la cláusula FROM de una instrucción UPDATE que hace referencia, directa o indirectamente, una vista que tiene un desencadenador INSTEAD OF definido en él. Para obtener más información acerca de desencadenadores INSTEAD OF, vea [CREATE TRIGGER &#40; Transact-SQL &#41; ](../../t-sql/statements/create-trigger-transact-sql.md).  
  
 Cuando una expresión de tabla común (CTE) es el destino de una instrucción UPDATE, todas las referencias a la CTE de la instrucción deben coincidir. Por ejemplo, si la CTE tiene asignado un alias en la cláusula FROM, el alias se debe utilizar para obtener todas las otras referencias a la CTE. Se requieren referencias CTE inequívocas porque una CTE no tiene un objeto ID, que utiliza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para reconocer la relación implícita entre un objeto y su alias. Sin esta relación, el plan de consulta puede producir un comportamiento de la unión inesperado y resultados imprevistos de la consulta. Los ejemplos siguientes muestran métodos correctos e incorrectos de especificar una CTE cuando la CTE es el objeto de destino de la operación de actualización.  
  
```sql  
USE tempdb;  
GO  
-- UPDATE statement with CTE references that are correctly matched.  
DECLARE @x TABLE (ID int, Value int);  
DECLARE @y TABLE (ID int, Value int);  
INSERT @x VALUES (1, 10), (2, 20);  
INSERT @y VALUES (1, 100),(2, 200);  
  
WITH cte AS (SELECT * FROM @x)  
UPDATE x -- cte is referenced by the alias.  
SET Value = y.Value  
FROM cte AS x  -- cte is assigned an alias.  
INNER JOIN @y AS y ON y.ID = x.ID;  
SELECT * FROM @x;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```  
 ID     Value  
 ------ -----  
 1      100  
 2      200  
 (2 row(s) affected)  
```  

Instrucción UPDATE con referencias CTE que se hacen coincidir de forma incorrecta.  
```sql  
USE tempdb;  
GO  
DECLARE @x TABLE (ID int, Value int);  
DECLARE @y TABLE (ID int, Value int);  
INSERT @x VALUES (1, 10), (2, 20);  
INSERT @y VALUES (1, 100),(2, 200);  
  
WITH cte AS (SELECT * FROM @x)  
UPDATE cte   -- cte is not referenced by the alias.  
SET Value = y.Value  
FROM cte AS x  -- cte is assigned an alias.  
INNER JOIN @y AS y ON y.ID = x.ID;   
SELECT * FROM @x;   
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
ID     Value  
------ -----  
1      100  
2      100  
(2 row(s) affected)  
```  

## <a name="locking-behavior"></a>Comportamiento del bloqueo  
 Una instrucción UPDATE siempre adquiere un bloqueo exclusivo (X) en la tabla que modifica y retiene ese bloqueo hasta que se completa la transacción. Con un bloqueo exclusivo, ninguna otra transacción puede modificar los datos. Puede especificar sugerencias de tabla para invalidar este comportamiento predeterminado durante la ejecución de la instrucción UPDATE especificando otro método de bloqueo, sin embargo se recomienda que solo los desarrolladores y administradores de bases de datos experimentados usen las sugerencias y únicamente como último recurso. Para obtener más información, vea [Sugerencias de tabla &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-table.md).  
  
## <a name="logging-behavior"></a>Comportamiento del registro  
 La instrucción UPDATE se registra; Sin embargo, las actualizaciones parciales de tipos de datos de valores grandes mediante la **.** ESCRIBIR la cláusula se registran mínimamente. Para obtener más información, vea "Actualizar tipos de datos de valores grandes" en la sección anterior "Tipos de datos".  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 Se requieren permisos UPDATE en la tabla de destino. Seleccione los permisos también son necesarios para la tabla que se actualiza si la instrucción UPDATE contiene una cláusula WHERE, o si *expresión* en el conjunto de cláusula utiliza una columna en la tabla.  
  
 Actualizar permisos de manera predeterminada a los miembros de la **sysadmin** rol fijo de servidor, el **db_owner** y **db_datawriter** se han corregido los roles de base de datos y el propietario de la tabla. Los miembros de la **sysadmin**, **db_owner**, y **db_securityadmin** roles y el propietario de la tabla pueden transferir permisos a otros usuarios.  
  
##  <a name="UpdateExamples"></a> Ejemplos  
  
|Categoría|Elementos de sintaxis ofrecidos|  
|--------------|------------------------------|  
|[Sintaxis básica](#BasicSyntax)|UPDATE|  
|[Limitar las filas que se actualizan](#LimitingValues)|WHERE • TOP • expresión de tabla común WITH • WHERE CURRENT OF|  
|[Establecer valores de columna](#ColumnValues)|valores calculados • operadores compuestos • valores predeterminados • subconsultas|  
|[Especificar objetos de destino que no sean tablas estándares](#TargetObjects)|vistas • variables de tabla • alias de tabla|  
|[Actualizar los datos basados en datos procedentes de otras tablas](#OtherTables)|FROM|  
|[Actualizar las filas de una tabla remota](#RemoteTables)|servidor vinculado • OPENQUERY • OPENDATASOURCE|  
|[Actualizar tipos de datos de objetos grandes](#LOBValues)|. ESCRIBIR • OPENROWSET|  
|[Actualizar tipos definidos por el usuario](#UDTs)|Tipos definidos por el usuario|  
|[Invalidar el comportamiento predeterminado del optimizador de consultas mediante sugerencias](#TableHints)|sugerencias de tabla • sugerencias de consulta|  
|[Capturar los resultados de la instrucción UPDATE](#CaptureResults)|Cláusula OUTPUT|  
|[Usar UPDATE en otras instrucciones](#Other)|Procedimientos almacenados • TRY…CATCH|  
  
###  <a name="BasicSyntax"></a>Sintaxis básica  
 Los ejemplos de esta sección demuestran la funcionalidad básica de la instrucción UPDATE con la sintaxis mínima requerida.  
  
#### <a name="a-using-a-simple-update-statement"></a>A. Usar una instrucción UPDATE simple  
 En el ejemplo siguiente se actualiza un solo valor de columna para todas las filas de la tabla `Person.Address`.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Person.Address  
SET ModifiedDate = GETDATE();  
```  
  
#### <a name="b-updating-multiple-columns"></a>B. Actualizar varias columnas  
 En el siguiente ejemplo se actualizan los valores de las columnas `Bonus`, `CommissionPct` y `SalesQuota` para todas las filas de la tabla `SalesPerson`.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Sales.SalesPerson  
SET Bonus = 6000, CommissionPct = .10, SalesQuota = NULL;  
GO  
```  
  
###  <a name="LimitingValues"></a>Limitar las filas que se actualizan  
 En los ejemplos de esta sección se muestran varias formas de limitar el número de filas afectadas por la instrucción UPDATE.  
  
#### <a name="c-using-the-where-clause"></a>C. Usar la cláusula WHERE  
 En el ejemplo siguiente se utiliza la cláusula WHERE para especificar las filas que se van a actualizar. La instrucción actualiza el valor de la columna `Color` de la tabla `Production.Product` para todas las filas con un valor existente de 'Red' en la columna `Color` y con un valor que comience por 'Road-250' en la columna `Name`.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.Product  
SET Color = N'Metallic Red'  
WHERE Name LIKE N'Road-250%' AND Color = N'Red';  
GO  
```  
  
#### <a name="d-using-the-top-clause"></a>D. Usar la cláusula TOP  
 En los siguientes ejemplos use la cláusula TOP para limitar el número de filas que se modifican en una instrucción UPDATE. Cuando una parte superior (*n*) se utiliza la cláusula con la actualización, la operación de actualización se realiza en una selección aleatoria de '*n*' número de filas. En el ejemplo siguiente se actualiza un 25 por ciento la columna `VacationHours` en 10 filas aleatorias de la tabla `Employee`.  
  
```sql  
USE AdventureWorks2012;
GO
UPDATE TOP (10) HumanResources.Employee
SET VacationHours = VacationHours * 1.25 ;
GO  
```  
  
 Si debe usar TOP para aplicar actualizaciones por orden cronológico, debe utilizarla junto con ORDER BY en una instrucción de subselección. En el siguiente ejemplo se actualizan las horas de vacaciones de los 10 empleados cuyas fechas de alta son más antiguas.  
  
```sql  
UPDATE HumanResources.Employee  
SET VacationHours = VacationHours + 8  
FROM (SELECT TOP 10 BusinessEntityID FROM HumanResources.Employee  
     ORDER BY HireDate ASC) AS th  
WHERE HumanResources.Employee.BusinessEntityID = th.BusinessEntityID;  
GO  
```  
  
#### <a name="e-using-the-with-commontableexpression-clause"></a>E. Usar la cláusula WITH common_table_expression  
 En el siguiente ejemplo se actualiza el valor `PerAssemnblyQty` para todas las partes y componentes que se utilizan directamente o indirectamente para crear el `ProductAssemblyID 800`. La expresión de tabla común devuelve una lista jerárquica de elementos que suelen usarse directamente para generar `ProductAssemblyID 800` y los elementos que se usan para generar esos componentes y así sucesivamente. Solo se modifican las filas devueltas por la expresión de tabla común.  
  
```sql  
USE AdventureWorks2012;  
GO  
WITH Parts(AssemblyID, ComponentID, PerAssemblyQty, EndDate, ComponentLevel) AS  
(  
    SELECT b.ProductAssemblyID, b.ComponentID, b.PerAssemblyQty,  
        b.EndDate, 0 AS ComponentLevel  
    FROM Production.BillOfMaterials AS b  
    WHERE b.ProductAssemblyID = 800  
          AND b.EndDate IS NULL  
    UNION ALL  
    SELECT bom.ProductAssemblyID, bom.ComponentID, p.PerAssemblyQty,  
        bom.EndDate, ComponentLevel + 1  
    FROM Production.BillOfMaterials AS bom   
        INNER JOIN Parts AS p  
        ON bom.ProductAssemblyID = p.ComponentID  
        AND bom.EndDate IS NULL  
)  
UPDATE Production.BillOfMaterials  
SET PerAssemblyQty = c.PerAssemblyQty * 2  
FROM Production.BillOfMaterials AS c  
JOIN Parts AS d ON c.ProductAssemblyID = d.AssemblyID  
WHERE d.ComponentLevel = 0;  
```  
  
#### <a name="f-using-the-where-current-of-clause"></a>F. Usar la cláusula WHERE CURRENT OF  
 En el siguiente ejemplo se usa la cláusula WHERE CURRENT OF para actualizar solo la fila en la que se coloca el cursor. Cuando un cursor se basa en una combinación, solo se modifica el `table_name` especificado en la instrucción UPDATE. Las demás tablas que participan en el cursor no se ven afectadas.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE complex_cursor CURSOR FOR  
    SELECT a.BusinessEntityID  
    FROM HumanResources.EmployeePayHistory AS a  
    WHERE RateChangeDate <>   
         (SELECT MAX(RateChangeDate)  
          FROM HumanResources.EmployeePayHistory AS b  
          WHERE a.BusinessEntityID = b.BusinessEntityID) ;  
OPEN complex_cursor;  
FETCH FROM complex_cursor;  
UPDATE HumanResources.EmployeePayHistory  
SET PayFrequency = 2   
WHERE CURRENT OF complex_cursor;  
CLOSE complex_cursor;  
DEALLOCATE complex_cursor;  
GO  
```  
  
###  <a name="ColumnValues"></a>Establecer valores de columna  
 En los ejemplos de esta sección se muestra la actualización de columnas mediante valores calculados, subconsultas y valores DEFAULT.  
  
#### <a name="g-specifying-a-computed-value"></a>G. Especificar un valor calculado  
 En los siguientes ejemplos se usan valores calculados en una instrucción UPDATE. En el ejemplo se duplica el valor de la columna `ListPrice` para todas las filas de la tabla `Product`.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
UPDATE Production.Product  
SET ListPrice = ListPrice * 2;  
GO  
```  
  
#### <a name="h-specifying-a-compound-operator"></a>H. Especificar un operador compuesto  
 En el ejemplo siguiente se usa la variable `@NewPrice` para incrementar el precio de todas las bicicletas rojas, tomando como base el precio actual y sumándole 10.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @NewPrice int = 10;  
UPDATE Production.Product  
SET ListPrice += @NewPrice  
WHERE Color = N'Red';  
GO  
```  
  
 En el siguiente ejemplo se usa el operador compuesto += para anexar los datos `' - tool malfunction'` al valor existente de la columna `Name` de las filas que tienen un valor de `ScrapReasonID` comprendido entre 10 y 12.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.ScrapReason   
SET Name += ' - tool malfunction'  
WHERE ScrapReasonID BETWEEN 10 and 12;  
```  
  
#### <a name="i-specifying-a-subquery-in-the-set-clause"></a>I. Especificar una subconsulta en la cláusula SET  
 En el siguiente ejemplo se usa una subconsulta en la cláusula SET para determinar el valor usado para actualizar la columna. La subconsulta debe devolver solo un valor escalar. Es decir, un solo valor por fila. En el ejemplo se modifica la columna `SalesYTD` de la tabla `SalesPerson` para reflejar las ventas más recientes registradas en la tabla `SalesOrderHeader`. La subconsulta suma las ventas de cada vendedor en la instrucción `UPDATE`.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Sales.SalesPerson  
SET SalesYTD = SalesYTD +   
    (SELECT SUM(so.SubTotal)   
     FROM Sales.SalesOrderHeader AS so  
     WHERE so.OrderDate = (SELECT MAX(OrderDate)  
                           FROM Sales.SalesOrderHeader AS so2  
                           WHERE so2.SalesPersonID = so.SalesPersonID)  
     AND Sales.SalesPerson.BusinessEntityID = so.SalesPersonID  
     GROUP BY so.SalesPersonID);  
GO  
```  
  
#### <a name="j-updating-rows-using-default-values"></a>J. Actualizar las filas con valores DEFAULT  
 En el siguiente ejemplo se establece la columna `CostRate` en su valor predeterminado (0.00) para todas las filas que tengan un valor de `CostRate` mayor que `20.00`.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.Location  
SET CostRate = DEFAULT  
WHERE CostRate > 20.00;  
```  
  
###  <a name="TargetObjects"></a>Especificar objetos de destino que no sean tablas estándares  
 En los ejemplos de esta sección se muestra cómo actualizar filas especificando una vista, un alias de tabla o una variable de tabla.  
  
#### <a name="k-specifying-a-view-as-the-target-object"></a>K. Especificar una vista como el objeto de destino  
 En el siguiente ejemplo se actualizan las filas de la tabla especificando una vista como el objeto de destino. La definición de la vista hace referencia a varias tablas, sin embargo, la instrucción UPDATE se ejecuta correctamente porque hace referencia a columnas de una sola de las tablas subyacentes. Se produciría un error en la instrucción UPDATE si se especificaran columnas de ambas tablas. Para obtener más información, consulte [modificar datos mediante una vista](../../relational-databases/views/modify-data-through-a-view.md).  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Person.vStateProvinceCountryRegion  
SET CountryRegionName = 'United States of America'  
WHERE CountryRegionName = 'United States';  
```  
  
#### <a name="l-specifying-a-table-alias-as-the-target-object"></a>L. Especificar un alias de tabla como el objeto de destino  
 En el siguiente ejemplo se actualizan las filas de la tabla `Production.ScrapReason`. El alias de tabla asignado a `ScrapReason` de la cláusula FROM se especifica como el objeto de destino de la cláusula UPDATE.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE sr  
SET sr.Name += ' - tool malfunction'  
FROM Production.ScrapReason AS sr  
JOIN Production.WorkOrder AS wo   
     ON sr.ScrapReasonID = wo.ScrapReasonID  
     AND wo.ScrappedQty > 300;  
```  
  
#### <a name="m-specifying-a-table-variable-as-the-target-object"></a>M. Especificar una variable de tabla como el objeto de destino  
 En el siguiente ejemplo se actualizan las filas de una variable de tabla.  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Create the table variable.  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    NewVacationHours int,  
    ModifiedDate datetime);  
  
-- Populate the table variable with employee ID values from HumanResources.Employee.  
INSERT INTO @MyTableVar (EmpID)  
    SELECT BusinessEntityID FROM HumanResources.Employee;  
  
-- Update columns in the table variable.  
UPDATE @MyTableVar  
SET NewVacationHours = e.VacationHours + 20,  
    ModifiedDate = GETDATE()  
FROM HumanResources.Employee AS e   
WHERE e.BusinessEntityID = EmpID;  
  
-- Display the results of the UPDATE statement.  
SELECT EmpID, NewVacationHours, ModifiedDate FROM @MyTableVar  
ORDER BY EmpID;  
GO  
```  
  
###  <a name="OtherTables"></a>Actualizar los datos basados en datos procedentes de otras tablas  
 En los ejemplos de esta sección se muestran métodos para actualizar las filas de una tabla basada en la información de otra.  
  
#### <a name="n-using-the-update-statement-with-information-from-another-table"></a>N. Usar la instrucción UPDATE con información de otra tabla  
 En este ejemplo se modifica la columna `SalesYTD` de la tabla `SalesPerson` para reflejar las ventas más recientes registradas en la tabla `SalesOrderHeader`.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Sales.SalesPerson  
SET SalesYTD = SalesYTD + SubTotal  
FROM Sales.SalesPerson AS sp  
JOIN Sales.SalesOrderHeader AS so  
    ON sp.BusinessEntityID = so.SalesPersonID  
    AND so.OrderDate = (SELECT MAX(OrderDate)  
                        FROM Sales.SalesOrderHeader  
                        WHERE SalesPersonID = sp.BusinessEntityID);  
GO  
```  
  
 En el ejemplo anterior se asume que solo se registra una venta para un determinado vendedor en una fecha determinada y que las actualizaciones son recientes. Si se puede registrar más de una venta para un vendedor determinado el mismo día, el ejemplo que se muestra no funcionará correctamente. El ejemplo se ejecuta sin errores, pero cada `SalesYTD` valor se actualiza con solo una venta, independientemente de cuántas ventas realmente se ha producido ese día. Esto es debido a que una sola instrucción UPDATE nunca actualiza la misma fila dos veces.  
  
 En el caso de más de una venta para un vendedor especificado puede tener lugar en el mismo día, todas las ventas de cada vendedor deben agregarse juntos en el `UPDATE` instrucción, como se muestra en el ejemplo siguiente:  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Sales.SalesPerson  
SET SalesYTD = SalesYTD +   
    (SELECT SUM(so.SubTotal)   
     FROM Sales.SalesOrderHeader AS so  
     WHERE so.OrderDate = (SELECT MAX(OrderDate)  
                           FROM Sales.SalesOrderHeader AS so2  
                           WHERE so2.SalesPersonID = so.SalesPersonID)  
     AND Sales.SalesPerson.BusinessEntityID = so.SalesPersonID  
     GROUP BY so.SalesPersonID);  
GO  
```  
  
###  <a name="RemoteTables"></a>Actualizar las filas de una tabla remota  
 Ejemplos de esta sección muestra cómo actualizar filas en una tabla de destino remota mediante el uso de un [servidor vinculado](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) o un [función rowset](../../t-sql/functions/rowset-functions-transact-sql.md) para hacer referencia a la tabla remota.  
  
#### <a name="o-updating-data-in-a-remote-table-by-using-a-linked-server"></a>O. Actualizar datos en una tabla remota con un servidor vinculado  
 En el ejemplo siguiente se actualiza una tabla en un servidor remoto. El ejemplo comienza creando un vínculo al origen de datos remoto mediante el uso de [sp_addlinkedserver](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md). El nombre del servidor vinculado, `MyLinkServer`, se especifica después como parte del nombre de objeto de cuatro partes con el formato servidor.catálogo.esquema.objeto. Observe que debe especificar un nombre de servidor válido para `@datasrc`.  
  
```sql  
USE master;  
GO  
-- Create a link to the remote data source.   
-- Specify a valid server name for @datasrc as 'server_name' or 'server_nameinstance_name'.  
  
EXEC sp_addlinkedserver @server = N'MyLinkServer',  
    @srvproduct = N' ',  
    @provider = N'SQLNCLI10',   
    @datasrc = N'<server name>',  
    @catalog = N'AdventureWorks2012';  
GO  
USE AdventureWorks2012;  
GO  
-- Specify the remote data source using a four-part name   
-- in the form linked_server.catalog.schema.object.  
  
UPDATE MyLinkServer.AdventureWorks2012.HumanResources.Department  
SET GroupName = N'Public Relations'  
WHERE DepartmentID = 4;  
```  
  
#### <a name="p-updating-data-in-a-remote-table-by-using-the-openquery-function"></a>P. Actualizar datos en una tabla remota con la función OPENQUERY  
 En el ejemplo siguiente se actualiza una fila en una tabla remota especificando la [OPENQUERY](../../t-sql/functions/openquery-transact-sql.md) función de conjunto de filas. En este ejemplo se usa el nombre del servidor vinculado creado en el ejemplo anterior.  
  
```sql  
UPDATE OPENQUERY (MyLinkServer, 'SELECT GroupName FROM HumanResources.Department WHERE DepartmentID = 4')   
SET GroupName = 'Sales and Marketing';  
```  
  
#### <a name="q-updating-data-in-a-remote-table-by-using-the-opendatasource-function"></a>Q. Actualizar datos en una tabla remota con la función OPENDATASOURCE  
 En el ejemplo siguiente se inserta una fila en una tabla remota especificando la [OPENDATASOURCE](../../t-sql/functions/opendatasource-transact-sql.md) función de conjunto de filas. Especifique un nombre de servidor válido para el origen de datos con el formato *nombre_servidor* o *nombre_servidor ombre_instancia*. Quizá deba configurar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para las consultas distribuidas ad hoc. Para obtener más información, consulte [ad hoc distributed queries (opción) de configuración de servidor](../../database-engine/configure-windows/ad-hoc-distributed-queries-server-configuration-option.md).  
  
```sql  
UPDATE OPENQUERY (MyLinkServer, 'SELECT GroupName FROM HumanResources.Department WHERE DepartmentID = 4')   
SET GroupName = 'Sales and Marketing';  
```  
  
###  <a name="LOBValues"></a>Actualizar tipos de datos de objetos grandes  
 En los ejemplos de esta sección se muestran los métodos de actualización de los valores de columnas definidos con tipos de datos de objetos grandes (LOB).  
  
#### <a name="r-using-update-with-write-to-modify-data-in-an-nvarcharmax-column"></a>R. Usar UPDATE con .WRITE para modificar los datos de una columna de tipo nvarchar(max)  
 En el ejemplo siguiente se usa el. Cláusula de escritura para actualizar un valor parcial de `DocumentSummary`, **nvarchar (max)** columna en el `Production.Document` tabla. La palabra `components` se sustituye por la palabra `features` especificando la palabra sustituta, la ubicación inicial (desplazamiento) de la palabra que se va a sustituir en los datos existentes y el número de caracteres que se va a sustituir (longitud). El ejemplo también utiliza la cláusula OUTPUT para devolver el antes y después de las imágenes de la `DocumentSummary` columna a la `@MyTableVar` variable de tabla.  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table (  
    SummaryBefore nvarchar(max),  
    SummaryAfter nvarchar(max));  
UPDATE Production.Document  
SET DocumentSummary .WRITE (N'features',28,10)  
OUTPUT deleted.DocumentSummary,   
       inserted.DocumentSummary   
    INTO @MyTableVar  
WHERE Title = N'Front Reflector Bracket Installation';  
SELECT SummaryBefore, SummaryAfter   
FROM @MyTableVar;  
GO  
```  
  
#### <a name="s-using-update-with-write-to-add-and-remove-data-in-an-nvarcharmax-column"></a>S. Usar UPDATE con .WRITE para agregar y quitar datos en una columna de tipo nvarchar(max)  
 Los ejemplos siguientes, agregar y quitar datos de un **nvarchar (max)** columna que tiene un valor establecido actualmente en NULL. Dado que el. ESCRIBIR la cláusula no se puede usar para modificar una columna es NULL, la columna en primer lugar se rellena con los datos temporales. Después, estos datos se reemplazan por los datos correctos mediante la cláusula .WRITE. En los demás ejemplos se anexan datos al final del valor de la columna, se quitan (truncan) los datos de la columna y, por último, se quitan los datos parciales de la columna. Las instrucciones SELECT muestran la modificación de datos resultante de cada instrucción UPDATE.  
  
```sql  
USE AdventureWorks2012;  
GO  
-- Replacing NULL value with temporary data.  
UPDATE Production.Document  
SET DocumentSummary = N'Replacing NULL value'  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
-- Replacing temporary data with the correct data. Setting @Length to NULL   
-- truncates all existing data from the @Offset position.  
UPDATE Production.Document  
SET DocumentSummary .WRITE(N'Carefully inspect and maintain the tires and crank arms.',0,NULL)  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
-- Appending additional data to the end of the column by setting   
-- @Offset to NULL.  
UPDATE Production.Document  
SET DocumentSummary .WRITE (N' Appending data to the end of the column.', NULL, 0)  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
-- Removing all data from @Offset to the end of the existing value by   
-- setting expression to NULL.   
UPDATE Production.Document  
SET DocumentSummary .WRITE (NULL, 56, 0)  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
-- Removing partial data beginning at position 9 and ending at   
-- position 21.  
UPDATE Production.Document  
SET DocumentSummary .WRITE ('',9, 12)  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
SELECT DocumentSummary   
FROM Production.Document  
WHERE Title = N'Crank Arm and Tire Maintenance';  
GO  
```  
  
#### <a name="t-using-update-with-openrowset-to-modify-a-varbinarymax-column"></a>T. Usar UPDATE con OPENROWSET para modificar una columna de tipo varbinary(max)  
 En el ejemplo siguiente se reemplaza una imagen almacenada en un **varbinary (max)** columna con una imagen nueva. El [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) función se utiliza con la opción BULK para cargar la imagen en la columna. En este ejemplo se da por supuesto que hay un archivo denominado `Tires.jpg` en la ruta de acceso especificada.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.ProductPhoto  
SET ThumbNailPhoto = (  
    SELECT *  
    FROM OPENROWSET(BULK 'c:Tires.jpg', SINGLE_BLOB) AS x )  
WHERE ProductPhotoID = 1;  
GO  
```  
  
#### <a name="u-using-update-to-modify-filestream-data"></a>U. Usar UPDATE para modificar datos FILESTREAM  
 En el siguiente ejemplo se usa la instrucción UPDATE para modificar los datos del archivo del sistema de archivos. No se recomienda este método para transmitir grandes cantidades de datos a un archivo. Use las interfaces de Win32 adecuadas. En el ejemplo siguiente se reemplaza cualquier texto del registro del archivo por el texto `Xray 1`. Para obtener más información, vea [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
```sql  
UPDATE Archive.dbo.Records  
SET [Chart] = CAST('Xray 1' as varbinary(max))  
WHERE [SerialNumber] = 2;  
```  
  
###  <a name="UDTs"></a>Actualizar tipos definidos por el usuario  
 En los siguientes ejemplos se modifican valores de columnas de tipo definido por el usuario (UDT) CLR. Se muestran tres métodos. Para obtener más información acerca de las columnas definidas por el usuario, consulte [tipos definidos](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  
  
#### <a name="v-using-a-system-data-type"></a>V. Usar un tipo de datos del sistema  
 Puede actualizar un UDT suministrando un valor en un tipo de datos del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], siempre que el tipo definido por el usuario admita la conversión implícita o explícita desde ese tipo. En el ejemplo siguiente se muestra cómo actualizar un valor de una columna de tipo `Point`, definido por el usuario, mediante la conversión explícita de una cadena.  
  
```sql  
UPDATE dbo.Cities  
SET Location = CONVERT(Point, '12.3:46.2')  
WHERE Name = 'Anchorage';  
```  
  
#### <a name="w-invoking-a-method"></a>W. Invocar un método  
 Puede actualizar un UDT invocando un método, marcado como mutador, del tipo definido por el usuario, para realizar la actualización. En el ejemplo siguiente se invoca un método mutador de tipo `Point` denominado `SetXY`. Esto actualiza el estado de la instancia del tipo.  
  
```sql  
UPDATE dbo.Cities  
SET Location.SetXY(23.5, 23.5)  
WHERE Name = 'Anchorage';  
```  
  
#### <a name="x-modifying-the-value-of-a-property-or-data-member"></a>X. Modificar el valor de una propiedad o miembro de datos  
 Puede actualizar un UDT modificando el valor de un miembro de datos público o de un miembro de propiedad registrado del tipo definido por el usuario. La expresión que suministra el valor debe poder convertirse implícitamente al tipo de la propiedad. En el ejemplo siguiente se modifica el valor de la propiedad `X` del tipo `Point` definido por el usuario.  
  
```sql  
UPDATE dbo.Cities  
SET Location.X = 23.5  
WHERE Name = 'Anchorage';  
```  
  
###  <a name="TableHints"></a>Invalidar el comportamiento predeterminado del optimizador de consultas mediante sugerencias  
 En los ejemplos de esta sección se muestra cómo usar sugerencias de tabla y de consulta para invalidar de forma temporal el comportamiento predeterminado del optimizador de consultas cuando se procesa la instrucción UPDATE.  
  
> [!CAUTION]  
>  Como el optimizador de consultas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] suele seleccionar el mejor plan de ejecución de una consulta, se recomienda que únicamente los administradores de bases de datos y desarrolladores experimentados utilicen las sugerencias como último recurso.  
  
#### <a name="y-specifying-a-table-hint"></a>Y. Especificar una sugerencia de tabla  
 En el ejemplo siguiente se especifica la [sugerencia de tabla](../../t-sql/queries/hints-transact-sql-table.md) TABLOCK. Esta sugerencia especifica que se aplique un bloqueo compartido a la tabla `Production.Product` y que se mantenga hasta que finalice la instrucción UPDATE.  
  
```sql  
USE AdventureWorks2012;  
GO  
UPDATE Production.Product  
WITH (TABLOCK)  
SET ListPrice = ListPrice * 1.10  
WHERE ProductNumber LIKE 'BK-%';  
GO  
```  
  
#### <a name="z-specifying-a-query-hint"></a>Z. Especificar una sugerencia de consulta  
 En el ejemplo siguiente se especifica la [sugerencia de consulta](../../t-sql/queries/hints-transact-sql-query.md) `OPTIMIZE FOR (@variable)` en la instrucción UPDATE. Esta sugerencia indica al optimizador de consultas que use un valor concreto para una variable local cuando la consulta se compile y optimice. El valor se utiliza solo durante la optimización de la consulta y no durante la ejecución de la misma.  
  
```sql  
USE AdventureWorks2012;  
GO  
CREATE PROCEDURE Production.uspProductUpdate  
@Product nvarchar(25)  
AS  
SET NOCOUNT ON;  
UPDATE Production.Product  
SET ListPrice = ListPrice * 1.10  
WHERE ProductNumber LIKE @Product  
OPTION (OPTIMIZE FOR (@Product = 'BK-%') );  
GO  
-- Execute the stored procedure   
EXEC Production.uspProductUpdate 'BK-%';  
```  
  
###  <a name="CaptureResults"></a>Capturar los resultados de la instrucción UPDATE  
 Ejemplos de esta sección muestran cómo usar el [cláusula OUTPUT](../../t-sql/queries/output-clause-transact-sql.md) para devolver información de, o en función de las expresiones, cada fila afectada por una instrucción UPDATE. Estos resultados se pueden devolver a la aplicación de procesamiento para que los utilice en mensajes de confirmación, archivado y otros requisitos similares de una aplicación.  
  
#### <a name="aa-using-update-with-the-output-clause"></a>AA. Usar UPDATE con la cláusula OUTPUT  
 En el siguiente ejemplo se actualiza en un 25 por ciento la columna `VacationHours` de las 10 primeras filas de la tabla `Employee` y también se establece el valor de la columna `ModifiedDate` en la fecha actual. La cláusula `OUTPUT` devuelve el valor de `VacationHours` antes de aplicar la instrucción `UPDATE` en la columna `deleted.VacationHours` y el valor actualizado en la columna `inserted.VacationHours` en la variable de tabla `@MyTableVar`.  
  
 Las dos instrucciones `SELECT` que le siguen devuelven los valores en `@MyTableVar` y los resultados de la operación de actualización en la tabla `Employee`. Para obtener más ejemplos usa la cláusula OUTPUT, vea [cláusula OUTPUT &#40; Transact-SQL &#41; ](../../t-sql/queries/output-clause-transact-sql.md).  
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @MyTableVar table(  
    EmpID int NOT NULL,  
    OldVacationHours int,  
    NewVacationHours int,  
    ModifiedDate datetime);  
UPDATE TOP (10) HumanResources.Employee  
SET VacationHours = VacationHours * 1.25,  
    ModifiedDate = GETDATE()   
OUTPUT inserted.BusinessEntityID,  
       deleted.VacationHours,  
       inserted.VacationHours,  
       inserted.ModifiedDate  
INTO @MyTableVar;  
--Display the result set of the table variable.  
SELECT EmpID, OldVacationHours, NewVacationHours, ModifiedDate  
FROM @MyTableVar;  
GO  
--Display the result set of the table.  
SELECT TOP (10) BusinessEntityID, VacationHours, ModifiedDate  
FROM HumanResources.Employee;  
GO  
```  
  
###  <a name="Other"></a>Usar UPDATE en otras instrucciones  
 En los ejemplos de esta sección se muestra cómo usar UPDATE en otras instrucciones.  
  
#### <a name="ab-using-update-in-a-stored-procedure"></a>AB. Usar UPDATE en un procedimiento almacenado  
 En el ejemplo siguiente se usa una instrucción UPDATE en un procedimiento almacenado. El procedimiento toma un parámetro de entrada `@NewHours` y un parámetro de salida `@RowCount`. El `@NewHours` el valor del parámetro se utiliza en la instrucción UPDATE para actualizar la columna `VacationHours` en la tabla `HumanResources.Employee`. El parámetro de salida `@RowCount` se usa para devolver el número de filas afectadas a una variable local. La expresión CASE se utiliza en la cláusula SET para determinar el valor que está establecido para `VacationHours` condicionalmente. Cuando se paga al empleado por hora (`SalariedFlag` = 0), `VacationHours` se establece en el número actual de horas más el valor especificado en `@NewHours`; de lo contrario, `VacationHours` se establece en el valor especificado en `@NewHours`.  
  
```sql  
USE AdventureWorks2012;  
GO  
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
  
#### <a name="ac-using-update-in-a-trycatch-block"></a>CA. Usar UPDATE en un bloque TRY…CATCH  
 En el ejemplo siguiente se usa una instrucción UPDATE en un bloque TRY... Bloque CATCH para controlar los errores de ejecución que podrían producirse durante la operación de actualización.  
  
```sql  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
  
BEGIN TRY  
    -- Intentionally generate a constraint violation error.  
    UPDATE HumanResources.Department  
    SET Name = N'MyNewName'  
    WHERE DepartmentID BETWEEN 1 AND 2;  
END TRY  
BEGIN CATCH  
    SELECT   
         ERROR_NUMBER() AS ErrorNumber  
        ,ERROR_SEVERITY() AS ErrorSeverity  
        ,ERROR_STATE() AS ErrorState  
        ,ERROR_PROCEDURE() AS ErrorProcedure  
        ,ERROR_LINE() AS ErrorLine  
        ,ERROR_MESSAGE() AS ErrorMessage;  
  
    IF @@TRANCOUNT > 0  
        ROLLBACK TRANSACTION;  
END CATCH;  
  
IF @@TRANCOUNT > 0  
    COMMIT TRANSACTION;  
GO  
```  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="ad-using-a-simple-update-statement"></a>AD. Usar una instrucción UPDATE simple  
 Los siguientes ejemplos se muestra cómo pueden verse afectadas todas las filas cuando una cláusula WHERE no se utiliza para especificar la fila (o filas) para actualizar.  
  
 Este ejemplo actualiza los valores de la `EndDate` y `CurrentFlag` columnas para todas las filas de la `DimEmployee` tabla.  
  
```sql  
-- Uses AdventureWorks  
  
UPDATE DimEmployee  
SET EndDate = '2010-12-31', CurrentFlag='False';  
```  
  
 También se pueden utilizar valores calculados en una instrucción UPDATE. En el ejemplo siguiente se duplica el valor de la columna `ListPrice` para todas las filas de la tabla `Product`.  
  
```sql  
-- Uses AdventureWorks  
  
UPDATE DimEmployee  
SET BaseRate = BaseRate * 2;  
```  
  
### <a name="ae-using-the-update-statement-with-a-where-clause"></a>AE. Uso de la instrucción UPDATE con una cláusula WHERE  
 En el ejemplo siguiente se utiliza la cláusula WHERE para especificar las filas que se van a actualizar.  
  
```sql  
-- Uses AdventureWorks  
  
UPDATE DimEmployee  
SET FirstName = 'Gail'  
WHERE EmployeeKey = 500;  
```  
  
### <a name="af-using-the-update-statement-with-label"></a>AF. Mediante la instrucción UPDATE con etiqueta  
 En el ejemplo siguiente se muestra el uso de una etiqueta para la instrucción UPDATE.  
  
```sql  
-- Uses AdventureWorks  
  
UPDATE DimProduct  
SET ProductSubcategoryKey = 2   
WHERE ProductKey = 313  
OPTION (LABEL = N'label1');  
```  
  
### <a name="ag-using-the-update-statement-with-information-from-another-table"></a>AG. Usar la instrucción UPDATE con información de otra tabla  
 Este ejemplo crea una tabla para almacenar el total de ventas por año. Actualiza las ventas totales para el año 2004 mediante la ejecución de una instrucción SELECT en la tabla FactInternetSales.  
  
```sql  
-- Uses AdventureWorks  
  
CREATE TABLE YearlyTotalSales (  
    YearlySalesAmount money NOT NULL,  
    Year smallint NOT NULL )  
WITH ( DISTRIBUTION = REPLICATE );  
  
INSERT INTO YearlyTotalSales VALUES (0, 2004);  
INSERT INTO YearlyTotalSales VALUES (0, 2005);  
INSERT INTO YearlyTotalSales VALUES (0, 2006);  
  
UPDATE YearlyTotalSales  
SET YearlySalesAmount=  
(SELECT SUM(SalesAmount) FROM FactInternetSales WHERE OrderDateKey >=20040000 AND OrderDateKey < 20050000)  
WHERE Year=2004;  
  
SELECT * FROM YearlyTotalSales;   
```  

### <a name="ah-ansi-join-replacement-for-update-statements"></a>AH. Reemplazo de combinación ANSI para instrucciones update
Es posible que tener una actualización compleja que combina más de dos tablas juntos mediante sintaxis de unión de ANSI para realizar la actualización o eliminación.  

Imagine que había que actualizar esta tabla:  

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(   [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,   [CalendarYear]                  SMALLINT        NOT NULL
,   [TotalSalesAmount]              MONEY           NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;  
```

La consulta original podría haber buscando algo parecido a esto:  

```
UPDATE  acs
SET     [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT  [EnglishProductCategoryName]
        ,       [CalendarYear]
        ,       SUM([SalesAmount])              AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]       AS s
        JOIN    [dbo].[DimDate]                 AS d    ON s.[OrderDateKey]             = d.[DateKey]
        JOIN    [dbo].[DimProduct]              AS p    ON s.[ProductKey]               = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]   AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]      AS c    ON u.[ProductCategoryKey]       = c.[ProductCategoryKey]
        WHERE   [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,       [CalendarYear]
        ) AS fis
ON  [acs].[EnglishProductCategoryName]  = [fis].[EnglishProductCategoryName]
AND [acs].[CalendarYear]                = [fis].[CalendarYear]
;  
```

Puesto que [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)] no admite combinaciones ANSI en la cláusula FROM de una instrucción UPDATE, no se puede copiar este código a través sin cambiar ligeramente.  

Puede utilizar una combinación de un CTAS y una combinación implícita para reemplazar este código:  

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT  ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,       ISNULL(CAST([CalendarYear] AS SMALLINT),0)                      AS [CalendarYear]
,       ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                     AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]       AS s
JOIN    [dbo].[DimDate]                 AS d    ON s.[OrderDateKey]             = d.[DateKey]
JOIN    [dbo].[DimProduct]              AS p    ON s.[ProductKey]               = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]   AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]      AS c    ON u.[ProductCategoryKey]       = c.[ProductCategoryKey]
WHERE   [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,       [CalendarYear]
;

-- Use an implicit join to perform the update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop the interim table
DROP TABLE CTAS_acs
;
```
  
## <a name="see-also"></a>Vea también  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [Cursores &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md)   
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [Texto y funciones de imagen &#40; Transact-SQL &#41;](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)   
 [CON common_table_expression &#40; Transact-SQL &#41;](../../t-sql/queries/with-common-table-expression-transact-sql.md)   
 [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md)  
  
  
