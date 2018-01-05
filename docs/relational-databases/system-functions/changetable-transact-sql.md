---
title: CHANGETABLE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/08/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHANGETABLE_TSQL
- CHANGETABLE
dev_langs: TSQL
helpviewer_keywords:
- CHANGETABLE
- change tracking [SQL Server], CHANGETABLE
ms.assetid: d405fb8d-3b02-4327-8d45-f643df7f501a
caps.latest.revision: "34"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 233a613024b4e216501ea7baaaf9a363325e5998
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/02/2018
---
# <a name="changetable-transact-sql"></a>CHANGETABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve información de seguimiento de cambios para una tabla. Puede utilizar esta instrucción para devolver todos los cambios de una tabla o información de seguimiento de cambios de una fila concreta.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CHANGETABLE (  
    { CHANGES table , last_sync_version  
    | VERSION table , <primary_key_values> } )  
[AS] table_alias [ ( column_alias [ ,...n ] )  
  
<primary_key_values> ::=  
( column_name [ , ...n ] ) , ( value [ , ...n ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 CAMBIOS *tabla* , *last_sync_version*  
 Devuelve información de seguimiento de todos los cambios a una tabla que se ha producido desde la versión especificada por *last_sync_version*.  
  
 *table*  
 Es la tabla definida por el usuario de la que obtener cambios a los que se ha realizado el seguimiento. El seguimiento de cambios debe estar habilitado en la tabla. Puede utilizarse un nombre de tabla de uno, dos, tres o cuatro partes. El nombre de tabla puede ser un sinónimo de la tabla.  
  
 *last_sync_version*  
 Cuando obtiene cambios, la aplicación que realiza la llamada debe especificar el punto del que se requieren cambios. El parámetro last_sync_version especifica ese punto. La función devuelve de todas las filas que se han cambiado desde esa versión. La aplicación consulta la recepción de cambios con una versión superior a last_sync_version.  
  
 Por lo general, antes de obtener cambios, la aplicación llamará **change_tracking_current_version ()** para obtener la versión que se usarán los cambios de tiempo siguientes son necesarios. Por consiguiente, la aplicación no tiene que interpretar ni conocer el valor real.  
  
 Dado que el valor de last_sync_version lo obtiene la aplicación que realiza la llamada, la aplicación tiene que conservar el valor. Si la aplicación pierde este valor, será necesario reinicializar los datos.  
  
 *last_sync_version* es **bigint**. El valor debe ser escalar. Una expresión producirá un error de sintaxis.  
  
 Si el valor es NULL, se devuelven todos los cambios a los que se ha realizado el seguimiento.  
  
 *last_sync_version* se debe validar para asegurarse de que no es demasiado antigua, porque algunos o todos los de la información de cambio podría haberse limpiada según el período de retención configurado para la base de datos. Para obtener más información, consulte [CHANGE_TRACKING_MIN_VALID_VERSION &#40; Transact-SQL &#41; ](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md) y [modificar opciones de SET de base de datos &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
 VERSIÓN *tabla*, {< primary_key_values >}  
 Devuelve la última información de seguimiento de cambios para una fila especificada. Los valores de clave principal deben identificar la fila. <primary_key_values> identifica las columnas de clave principal y especifica los valores. Los nombres de columna de clave principal se pueden especificar en cualquier orden.  
  
 *Table*  
 Es la tabla definida por el usuario de la que obtener la información de seguimiento de cambios. El seguimiento de cambios debe estar habilitado en la tabla. Puede utilizarse un nombre de tabla de uno, dos, tres o cuatro partes. El nombre de tabla puede ser un sinónimo de la tabla.  
  
 *column_name*  
 Especifica el nombre de la columna o columnas de clave principal. Se pueden especificar varios nombres de columna y en cualquier orden.  
  
 *Value*  
 Es el valor de la clave principal. Si hay varias columnas de clave principales, deben especificarse los valores en el mismo orden que las columnas aparecen en la *column_name* lista.  
  
 [COMO] *aliasTabla* [(*column_alias* [,...*n* ] ) ]  
 Proporciona los nombres de los resultados devueltos por CHANGETABLE.  
  
 *aliasTabla*  
 Es el nombre del alias de la tabla que es devuelta por CHANGETABLE. *aliasTabla* es obligatorio y debe ser válido [identificador](../../relational-databases/databases/database-identifiers.md).  
  
 *usar column_alias*  
 Es un alias de columna opcional o lista de alias de columna para las columnas devueltas por CHANGETABLE. Esto permite personalizar los nombres de columna en caso de que haya nombres duplicados en los resultados.  
  
## <a name="return-types"></a>Tipos devueltos  
 **table**  
  
## <a name="return-values"></a>Valores devueltos  
  
### <a name="changetable-changes"></a>CHANGETABLE CHANGES  
 Si se especifica CHANGES, se devuelven cero o varias filas con las columnas siguientes.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|SYS_CHANGE_VERSION|**bigint**|Valor de versión asociado al último cambio de la fila|  
|SYS_CHANGE_CREATION_VERSION|**bigint**|Valores de versión asociados a la última operación de inserción.|  
|SYS_CHANGE_OPERATION|**nchar (1)**|Especifica el tipo de cambio:<br /><br /> **U** = actualizar<br /><br /> **¿** = Inserción<br /><br /> **D.** = eliminar|  
|SYS_CHANGE_COLUMNS|**varbinary(4100)**|Enumera las columnas que han cambiado desde last_sync_version (la básica). Tenga en cuenta que las columnas calculadas nunca se presentan como cambiadas.<br /><br /> El valor es NULL si se cumple una cualquiera de las siguientes condiciones:<br /><br /> El seguimiento de cambios de columna no está habilitado.<br /><br /> Se trata de una operación de eliminación o de inserción.<br /><br /> Se actualizaron en una única operación todas las columnas de clave no principal. No debería interpretarse directamente este valor binario. En su lugar, para interpretarlo utilice [change_tracking_is_column_in_mask ()](../../relational-databases/system-functions/change-tracking-is-column-in-mask-transact-sql.md).|  
|SYS_CHANGE_CONTEXT|**varbinary(128)**|Cambiar la información de contexto que puede especificar opcionalmente usando la [WITH](../../relational-databases/system-functions/with-change-tracking-context-transact-sql.md) cláusula como parte de una instrucción INSERT, UPDATE o DELETE.|  
|\<valor de columna de clave principal >|Igual que las columnas de tabla de usuario|Los valores de clave principal de la tabla con seguimiento. Estos valores identifican de manera única cada fila en la tabla de usuario.|  
  
### <a name="changetable-version"></a>CHANGETABLE VERSION  
 Si se especifica VERSION, se devuelve una fila con las siguientes columnas.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|SYS_CHANGE_VERSION|**bigint**|Valor de versión de cambios actual asociado a la fila.<br /><br /> El valor es NULL si no se ha realizado ningún cambio durante un periodo más largo que el periodo de retención del seguimiento de cambios, o no se ha cambiado la fila desde que se habilitó el seguimiento de cambios.|  
|SYS_CHANGE_CONTEXT|**varbinary(128)**|Cambie la información de contexto que se puede especificar opcionalmente usando la cláusula WITH como parte de una instrucción INSERT, UPDATE o DELETE.|  
|\<valor de columna de clave principal >|Igual que las columnas de tabla de usuario|Los valores de clave principal de la tabla con seguimiento. Estos valores identifican de manera única cada fila en la tabla de usuario.|  
  
## <a name="remarks"></a>Comentarios  
 Normalmente, la función CHANGETABLE se utiliza en la cláusula FROM de una consulta como si fuera una tabla.  
  
## <a name="changetablechanges"></a>CHANGETABLE(CHANGES...)  
 Para obtener los datos de fila para las filas nuevas o modificadas, una el conjunto de resultados a la tabla de usuario mediante las columnas de clave principal. Se devuelve solo una fila para cada fila de la tabla de usuario que ha cambiado, incluso si ha habido varios cambios en la misma fila desde la *last_sync_version* valor.  
  
 Los cambios de la columna de clave principal nunca se marcan como actualizaciones. Si un valor de clave principal cambia, se considera que es una eliminación del valor anterior y una inserción del valor nuevo.  
  
 Si elimina una fila y, a continuación, inserta una fila con la clave principal anterior, el cambio se considera una actualización para todas las columnas de la fila.  
  
 Los valores devueltos para las columnas SYS_CHANGE_OPERATION y SYS_CHANGE_COLUMNS son con respecto a la línea de base (last_sync_version) especificada. Por ejemplo, si se realiza una operación de inserción en la versión 10 y una operación de actualización en la versión 15 y si la línea de base *last_sync_version* es 12, se notificará una actualización. Si el *last_sync_version* valor es 8, se notificará una inserción. SYS_CHANGE_COLUMNS nunca notificará columnas calculadas como si hubieran sido actualizadas.  
  
 Generalmente, se someten a seguimiento todas las operaciones que insertan, actualizan o eliminan datos en tablas de usuario, incluida la instrucción MERGE.  
  
 Las siguientes operaciones, que afectan a datos de tablas de usuario, no se someten a seguimiento:  
  
-   Ejecutar la instrucción UPDATETEXT  
  
     Esta instrucción ha quedado desusada y no estará presente en una versión futura de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sin embargo, sí se realiza el seguimiento de los cambios realizados mediante la cláusula  .WRITE de la instrucción UPDATE.  
  
-   Eliminar filas mediante TRUNCATE TABLE  
  
     Cuando se trunca una tabla, la información de versión del seguimiento de cambios asociada a la tabla se restablece como si el seguimiento de cambios se hubiera habilitado recientemente en la tabla. Una aplicación cliente debe validar siempre su última versión sincronizada. Se producirá un error en la validación si se ha truncado la tabla.  
  
## <a name="changetableversion"></a>CHANGETABLE(VERSION...)  
 Se devuelve un conjunto de resultados vacío si se especifica una clave principal inexistente.  
  
 El valor de SYS_CHANGE_VERSION podría ser NULL si lleva sin realizarse un cambio más tiempo del correspondiente al período de retención (por ejemplo, la limpieza ha quitado la información de los cambios) o si la fila nunca ha cambiado desde que el seguimiento de cambios se habilitó en la tabla.  
  
## <a name="permissions"></a>Permissions  
 Requiere los siguientes permisos en la tabla que se especifica mediante la *tabla* valor para obtener información de seguimiento de cambios:  
  
-   Permiso SELECT en las columnas de clave principal  
  
-   VIEW CHANGE TRACKING  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-rows-for-an-initial-synchronization-of-data"></a>A. Devolver las filas de una sincronización inicial de los datos  
 El ejemplo siguiente obtiene los datos para una sincronización inicial de los datos de la tabla. La consulta devuelve todos los datos de fila y sus versiones asociadas. A continuación, pueden insertarse o agregarse estos datos al sistema que contendrá los datos sincronizados.  
  
```sql  
-- Get all current rows with associated version  
SELECT e.[Emp ID], e.SSN, e.FirstName, e.LastName,  
    c.SYS_CHANGE_VERSION, c.SYS_CHANGE_CONTEXT  
FROM Employees AS e  
CROSS APPLY CHANGETABLE   
    (VERSION Employees, ([Emp ID], SSN), (e.[Emp ID], e.SSN)) AS c;  
```  
  
### <a name="b-listing-all-changes-that-were-made-since-a-specific-version"></a>B. Enumerar todos los cambios realizados desde una versión concreta  
 El siguiente ejemplo enumera todos los cambios realizados en una tabla desde una versión concreta (`@last_sync_version)`. [Emp ID] y SSN son las columnas de una clave principal compuesta.  
  
```sql  
DECLARE @last_sync_version bigint;  
SET @last_sync_version = <value obtained from query>;  
SELECT [Emp ID], SSN,  
    SYS_CHANGE_VERSION, SYS_CHANGE_OPERATION,  
    SYS_CHANGE_COLUMNS, SYS_CHANGE_CONTEXT   
FROM CHANGETABLE (CHANGES Employees, @last_sync_version) AS C;  
```  
  
### <a name="c-obtaining-all-changed-data-for-a-synchronization"></a>C. Obtener todos los datos cambiados para una sincronización  
 El siguiente ejemplo muestra cómo se pueden obtener todos los datos que han cambiado. Esta consulta une la información del seguimiento de cambios con la tabla de usuario para devolver la información de tabla de usuario. Una `LEFT OUTER JOIN` se usa para devolver una fila para las filas eliminadas.  
  
```sql  
-- Get all changes (inserts, updates, deletes)  
DECLARE @last_sync_version bigint;  
SET @last_sync_version = <value obtained from query>;  
SELECT e.FirstName, e.LastName, c.[Emp ID], c.SSN,  
    c.SYS_CHANGE_VERSION, c.SYS_CHANGE_OPERATION,  
    c.SYS_CHANGE_COLUMNS, c.SYS_CHANGE_CONTEXT   
FROM CHANGETABLE (CHANGES Employees, @last_sync_version) AS c  
    LEFT OUTER JOIN Employees AS e  
        ON e.[Emp ID] = c.[Emp ID] AND e.SSN = c.SSN;  
```  
  
### <a name="d-detecting-conflicts-by-using-changetableversion"></a>D. Detectar conflictos mediante CHANGETABLE (VERSION...)  
 El siguiente ejemplo actualiza una fila solo si la fila no ha cambiado desde la última sincronización. El número de versión de la fila concreta se obtiene mediante `CHANGETABLE`. Si se ha actualizado la fila, no se realizan los cambios y la consulta devuelve información sobre el último cambio de la fila.  
  
```sql  
-- @last_sync_version must be set to a valid value  
UPDATE  
    SalesLT.Product  
SET  
    ListPrice = @new_listprice  
FROM  
    SalesLT.Product AS P  
WHERE  
    ProductID = @product_id AND  
    @last_sync_version >= ISNULL (  
        (SELECT CT.SYS_CHANGE_VERSION FROM   
            CHANGETABLE(VERSION SalesLT.Product,  
            (ProductID), (P.ProductID)) AS CT),  
        0);  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de seguimiento de cambios &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [Seguimiento de cambios de datos &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [CHANGE_TRACKING_IS_COLUMN_IN_MASK &#40; Transact-SQL &#41;](../../relational-databases/system-functions/change-tracking-is-column-in-mask-transact-sql.md)   
 [CHANGE_TRACKING_CURRENT_VERSION &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-current-version-transact-sql.md)   
 [CHANGE_TRACKING_MIN_VALID_VERSION &#40; Transact-SQL &#41;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)  
  
  
