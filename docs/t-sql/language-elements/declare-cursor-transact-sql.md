---
title: DECLARE CURSOR (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECLARE_CURSOR_TSQL
- CURSOR_TSQL
- DECLARE CURSOR
- CURSOR
dev_langs:
- TSQL
helpviewer_keywords:
- DECLARE CURSOR statement
- cursors [SQL Server], attributes
- local cursors [SQL Server]
- nesting cursors
- Transact-SQL cursors, attributes
- global cursors [SQL Server]
ms.assetid: 5a3a27aa-03e8-4c98-a27e-809282379b21
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3119038bac239e20ed903ef198674a74f9818eac
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47609193"
---
# <a name="declare-cursor-transact-sql"></a>DECLARE CURSOR (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Define los atributos de un cursor de servidor de [!INCLUDE[tsql](../../includes/tsql-md.md)], como su comportamiento de desplazamiento y la consulta utilizada para generar el conjunto de resultados sobre el que opera el cursor. DECLARE CURSOR acepta tanto una sintaxis basada en el estándar ISO como una sintaxis que utiliza un conjunto de extensiones [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ISO Syntax  
DECLARE cursor_name [ INSENSITIVE ] [ SCROLL ] CURSOR   
     FOR select_statement   
     [ FOR { READ ONLY | UPDATE [ OF column_name [ ,...n ] ] } ]  
[;]  
Transact-SQL Extended Syntax  
DECLARE cursor_name CURSOR [ LOCAL | GLOBAL ]   
     [ FORWARD_ONLY | SCROLL ]   
     [ STATIC | KEYSET | DYNAMIC | FAST_FORWARD ]   
     [ READ_ONLY | SCROLL_LOCKS | OPTIMISTIC ]   
     [ TYPE_WARNING ]   
     FOR select_statement   
     [ FOR UPDATE [ OF column_name [ ,...n ] ] ]  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *cursor_name*  
 Es el nombre del cursor de servidor de [!INCLUDE[tsql](../../includes/tsql-md.md)] definido. *cursor_name* debe respetar las reglas de los identificadores.  
  
 INSENSITIVE  
 Define un cursor que hace una copia temporal de los datos que utiliza. Todas las solicitudes que se realizan al cursor se responden desde esta tabla temporal de **tempdb**; por tanto, las modificaciones realizadas en las tablas base no se reflejan en los datos devueltos por las operaciones de captura realizadas en el cursor y, además, este cursor no admite modificaciones. Cuando se utiliza la sintaxis de ISO, si se omite INSENSITIVE, las eliminaciones y actualizaciones confirmadas realizadas en las tablas subyacentes (por cualquier usuario) se reflejan en capturas posteriores.  
  
 SCROLL  
 Especifica que están disponibles todas las opciones de captura (FIRST, LAST, PRIOR, NEXT, RELATIVE, ABSOLUTE). Si no se especifica SCROLL en una instrucción DECLARE CURSOR de ISO, la única opción de captura que se admite es NEXT. No es posible especificar SCROLL si se incluye también FAST_FORWARD.  
  
 *select_statement*  
 Es una instrucción SELECT estándar que define el conjunto de resultados del cursor. Las palabras clave FOR BROWSE e INTO no están permitidas en la instrucción *select_statement* de una declaración de cursor.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] convierte implícitamente el cursor a otro tipo si las cláusulas de la instrucción *select_statement* entran en conflicto con la funcionalidad del tipo de cursor solicitado.  
  
 READ ONLY  
 Evita que se efectúen actualizaciones a través de este cursor. No es posible hacer referencia al cursor en una cláusula WHERE CURRENT OF de una instrucción UPDATE o DELETE. Esta opción reemplaza la capacidad predeterminada de actualizar el cursor.  
  
 UPDATE [OF *column_name* [**,**...*n*]]  
 Define las columnas actualizables en el cursor. Si se especifica OF *column_name* [**,**..*.n*], solo las columnas enumeradas admiten modificaciones. Si se especifica UPDATE sin indicar una lista de columnas, se pueden actualizar todas las columnas.  
  
 *cursor_name*  
 Es el nombre del cursor de servidor de [!INCLUDE[tsql](../../includes/tsql-md.md)] definido. *cursor_name* debe respetar las reglas de los identificadores.  
  
 LOCAL  
 Especifica que el alcance del cursor es local para el proceso por lotes, procedimiento almacenado o desencadenador en que se creó el cursor. El nombre del cursor solo es válido en este ámbito. Es posible hacer referencia al cursor mediante variables de cursor locales del lote, procedimiento almacenado, desencadenador o parámetro OUTPUT del procedimiento almacenado. El parámetro OUTPUT se utiliza para devolver el cursor local al proceso por lotes, procedimiento almacenado o desencadenador que realiza la llamada, el cual puede asignar el parámetro a una variable de cursor para hacer referencia al cursor después de que el procedimiento almacenado finalice. La asignación del cursor se cancela implícitamente cuando el proceso por lotes, procedimiento almacenado o desencadenador finaliza, a menos que el cursor se haya devuelto en un parámetro OUTPUT. En ese caso, la asignación del cursor se cancela cuando se cancela la asignación de la última variable que hace referencia al mismo o cuando ésta se sale del ámbito.  
  
 GLOBAL  
 Especifica que el alcance del cursor es global para la conexión. Se puede hacer referencia al nombre del cursor en cualquier procedimiento almacenado o lote que se ejecute durante la conexión. La asignación del cursor solo se cancela implícitamente cuando se produce la desconexión.  
  
> [!NOTE]  
>  Si no se especifica GLOBAL ni LOCAL, el valor predeterminado se controla mediante la configuración de la opción de base de datos **default to local cursor**.  
  
 FORWARD_ONLY  
 Especifica que el cursor solo se puede desplazar de la primera a la última fila. FETCH NEXT es la única opción de captura admitida. Si se especifica FORWARD_ONLY sin las palabras clave STATIC, KEYSET o DYNAMIC, el cursor funciona como un cursor DYNAMIC. Cuando no se especifica FORWARD_ONLY ni SCROLL, FORWARD_ONLY es la opción predeterminada, salvo que se incluyan las palabras clave STATIC, KEYSET o DYNAMIC. Los cursores STATIC, KEYSET y DYNAMIC utilizan SCROLL como valor predeterminado. A diferencia de las API de base de datos, como ODBC y ADO, FORWARD_ONLY se puede utilizar con los cursores STATIC, KEYSET y DYNAMIC de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 STATIC  
 Define un cursor que hace una copia temporal de los datos que utiliza. Todas las solicitudes que se realizan al cursor se responden desde esta tabla temporal de **tempdb**; por tanto, las modificaciones realizadas en las tablas base no se reflejan en los datos devueltos por las operaciones de captura realizadas en el cursor y, además, este cursor no admite modificaciones.  
  
 KEYSET  
 Especifica que la pertenencia y el orden de las filas del cursor se fijan cuando se abre este cursor. El conjunto de claves que identifica las filas de forma única está integrado en la tabla denominada **tempdb** de **keyset**.  
  
> [!NOTE]  
>  Si la consulta hace referencia por lo menos a una tabla sin un índice único, el cursor de conjunto de claves se convierte en cursor estático.  
  
 Los cambios realizados en valores de las tablas base que no son de clave, ya sean realizados por el propietario del cursor o confirmados por otros usuarios, son visibles cuando el propietario se desplaza por el cursor. Las inserciones realizadas por otros usuarios no son visibles (no es posible hacer inserciones a través de un cursor de servidor de [!INCLUDE[tsql](../../includes/tsql-md.md)]). Si se elimina una fila, un intento para capturar la fila devuelve un @@FETCH_STATUS de -2. Las actualizaciones de valores de clave de fuera del cursor son similares a la eliminación de la fila anterior seguida por la inserción de la nueva fila. La fila con los nuevos valores no está visible, y los intentos de capturar la fila con los valores anteriores devuelven un @@FETCH_STATUS de -2. Los nuevos valores están visibles si la actualización se realiza a través del cursor especificando la cláusula WHERE CURRENT OF.  
  
 DYNAMIC  
 Define un cursor que, al desplazarse por él, refleja en su conjunto de resultados todos los cambios realizados en los datos de las filas. Los valores de los datos, el orden y la pertenencia de las filas pueden cambiar en cada captura. La opción de captura ABSOLUTE no se puede utilizar en los cursores dinámicos.  
  
 FAST_FORWARD  
 Especifica un cursor FORWARD_ONLY, READ_ONLY con las optimizaciones de rendimiento habilitadas. No se puede especificar FAST_FORWARD si se especifica también SCROLL o FOR_UPDATE.  
  
> [!NOTE]  
>  FAST_FORWARD y FORWARD_ONLY pueden usarse en la misma instrucción DECLARE CURSOR.  
  
 READ_ONLY  
 Evita que se efectúen actualizaciones a través de este cursor. No es posible hacer referencia al cursor en una cláusula WHERE CURRENT OF de una instrucción UPDATE o DELETE. Esta opción reemplaza la capacidad predeterminada de actualizar el cursor.  
  
 SCROLL_LOCKS  
 Especifica que existan garantías de que las actualizaciones o las cancelaciones posicionadas realizadas a través del cursor se lleven a cabo correctamente. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bloquea las filas mientras se leen en el cursor para garantizar su disponibilidad en modificaciones posteriores. No es posible especificar SCROLL_LOCKS si se especifica también FAST_FORWARD o STATIC.  
  
 OPTIMISTIC  
 Especifica que las actualizaciones o las cancelaciones posicionadas realizadas a través del cursor no se lleven a cabo correctamente si la fila se ha actualizado desde que se leyó en el cursor. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no bloquea las filas cuando se leen en el cursor. En su lugar, usa comparaciones de valores de columna **timestamp** o un valor de suma de comprobación si la tabla no tiene columnas **timestamp** para determinar si la fila se ha modificado después de leerla en el cursor. Si la fila se ha modificado, la actualización o eliminación posicionada fracasa. No es posible especificar OPTIMISTIC si se especifica también FAST_FORWARD.  
  
 TYPE_WARNING  
 Especifica que se envía un mensaje de advertencia al cliente si el cursor se convierte implícitamente del tipo solicitado a otro.  
  
 *select_statement*  
 Es una instrucción SELECT estándar que define el conjunto de resultados del cursor. Las palabras clave COMPUTE, COMPUTE BY, FOR BROWSE e INTO no están permitidas en la instrucción *select_statement* de una declaración de cursor.  
  
> [!NOTE]  
>  Puede usar una sugerencia de consulta en una declaración de cursor, pero si usa también la cláusula FOR UPDATE OF, debe especificar OPTION (*query_hint*) después de FOR UPDATE OF.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] convierte implícitamente el cursor a otro tipo si las cláusulas de la instrucción *select_statement* entran en conflicto con la funcionalidad del tipo de cursor solicitado. Para obtener más información, vea el tema relativo a las conversiones de cursor implícitas.  
  
 FOR UPDATE [OF *column_name* [**,**...*n*]]  
 Define las columnas actualizables en el cursor. Si se especifica OF*column_name* [**,**...*n*], solo las columnas enumeradas admiten modificaciones. Si se especifica UPDATE sin una lista de columnas, se pueden actualizar todas las columnas, a menos que se haya especificado la opción de simultaneidad READ_ONLY.  
  
## <a name="remarks"></a>Notas  
 DECLARE CURSOR define los atributos de un cursor de servidor de [!INCLUDE[tsql](../../includes/tsql-md.md)], como su comportamiento de desplazamiento y la consulta utilizada para generar el conjunto de resultados sobre el que opera el cursor. La instrucción OPEN llena el conjunto de resultados y la instrucción FETCH devuelve una fila del conjunto de resultados. La instrucción CLOSE libera el conjunto de resultados actual asociado al cursor. La instrucción DEALLOCATE libera los recursos que utiliza el cursor.  
  
 La primera forma de la instrucción DECLARE CURSOR usa la sintaxis de ISO para declarar comportamientos del cursor. La segunda forma de DECLARE CURSOR utiliza extensiones de [!INCLUDE[tsql](../../includes/tsql-md.md)] que permiten definir cursores con los mismos tipos de cursor utilizados en las funciones de cursor de la API de base de datos de ODBC o ADO.  
  
 No se pueden combinar las dos formas. Si especifica las palabras clave SCROLL o INSENSITIVE antes de la palabra clave CURSOR, no puede usar ninguna palabra clave entre las palabras clave CURSOR y FOR de la instrucción *select_statement*. Si especifica alguna palabra clave entre CURSOR y FOR de la instrucción *select_statement*, no puede especificar SCROLL o INSENSITIVE delante de la palabra clave CURSOR.  
  
 Si una instrucción DECLARE CURSOR con sintaxis de [!INCLUDE[tsql](../../includes/tsql-md.md)] no especifica READ_ONLY, OPTIMISTIC o SCROLL_LOCKS, el valor predeterminado es el siguiente:  
  
-   Si la instrucción SELECT no acepta actualizaciones (permisos insuficientes, acceso a tablas remotas que no aceptan actualizaciones, etc.), el cursor es de tipo READ_ONLY.  
  
-   El valor predeterminado de los cursores de tipo STATIC y FAST_FORWARD es READ_ONLY.  
  
-   El valor predeterminado de los cursores de tipo KEYSET y DYNAMIC es OPTIMISTIC.  
  
 Solo se puede hacer referencia a nombres de cursores mediante otras instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)]. No se puede hacer referencia a nombres de cursores mediante funciones de la API de base de datos. Por ejemplo, después de declarar un cursor, no se puede hacer referencia al nombre del cursor desde funciones o métodos de OLE DB, ODBC o ADO. No se pueden capturar las filas del cursor con las funciones o métodos de captura de las API; las filas solo se pueden capturar mediante instrucciones FETCH de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Una vez que se ha declarado un cursor, se pueden utilizar estos procedimientos almacenados del sistema para determinar las características del cursor.  
  
|Procedimientos almacenados del sistema|Descripción|  
|------------------------------|-----------------|  
|**sp_cursor_list**|Devuelve la lista de los cursores que están visibles actualmente en la conexión y sus atributos.|  
|**sp_describe_cursor**|Describe los atributos de un cursor, por ejemplo si es de solo avance o de desplazamiento.|  
|**sp_describe_cursor_columns**|Describe los atributos de las columnas en el conjunto de resultados del cursor.|  
|**sp_describe_cursor_tables**|Describe las tablas base a las que tiene acceso el cursor.|  
  
 Se pueden usar variables como parte de la instrucción *select_statement* que declara un cursor. Los valores de las variables de cursor no cambian después de que se declara el cursor.  
  
## <a name="permissions"></a>Permisos  
 Los permisos para utilizar DECLARE CURSOR corresponden de manera predeterminada a los usuarios que dispongan de permisos para utilizar SELECT en las vistas, tablas y columnas utilizadas en el cursor.
 
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones

No puede usar cursores ni desencadenadores en una tabla con un índice clúster de almacén de columnas. Esta restricción no se aplica a los índices no clúster de almacén de columnas; puede usar cursores y desencadenadores en una tabla con un índice no clúster de almacén de columnas. 
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-simple-cursor-and-syntax"></a>A. Uso de cursores simples y su sintaxis  

El conjunto de resultados generado al abrir este cursor contiene todas las filas y todas las columnas de la tabla. Este cursor se puede actualizar, y todas las actualizaciones y eliminaciones se representan en las búsquedas realizadas para este cursor. `FETCH NEXT` es la única búsqueda disponible porque la opción `SCROLL` no se ha especificado.  

  
```  
DECLARE vend_cursor CURSOR  
    FOR SELECT * FROM Purchasing.Vendor  
OPEN vend_cursor  
FETCH NEXT FROM vend_cursor;  
```  
  
### <a name="b-using-nested-cursors-to-produce-report-output"></a>B. Uso de cursores anidados para elaborar resultados de informes  
 En el ejemplo siguiente se muestra cómo se pueden anidar los cursores para elaborar informes complejos. El cursor interno se declara para cada proveedor.  
  
```  
SET NOCOUNT ON;  
  
DECLARE @vendor_id int, @vendor_name nvarchar(50),  
    @message varchar(80), @product nvarchar(50);  
  
PRINT '-------- Vendor Products Report --------';  
  
DECLARE vendor_cursor CURSOR FOR   
SELECT VendorID, Name  
FROM Purchasing.Vendor  
WHERE PreferredVendorStatus = 1  
ORDER BY VendorID;  
  
OPEN vendor_cursor  
  
FETCH NEXT FROM vendor_cursor   
INTO @vendor_id, @vendor_name  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
    PRINT ' '  
    SELECT @message = '----- Products From Vendor: ' +   
        @vendor_name  
  
    PRINT @message  
  
    -- Declare an inner cursor based     
    -- on vendor_id from the outer cursor.  
  
    DECLARE product_cursor CURSOR FOR   
    SELECT v.Name  
    FROM Purchasing.ProductVendor pv, Production.Product v  
    WHERE pv.ProductID = v.ProductID AND  
    pv.VendorID = @vendor_id  -- Variable value from the outer cursor  
  
    OPEN product_cursor  
    FETCH NEXT FROM product_cursor INTO @product  
  
    IF @@FETCH_STATUS <> 0   
        PRINT '         <<None>>'       
  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
  
        SELECT @message = '         ' + @product  
        PRINT @message  
        FETCH NEXT FROM product_cursor INTO @product  
        END  
  
    CLOSE product_cursor  
    DEALLOCATE product_cursor  
        -- Get the next vendor.  
    FETCH NEXT FROM vendor_cursor   
    INTO @vendor_id, @vendor_name  
END   
CLOSE vendor_cursor;  
DEALLOCATE vendor_cursor;  
```  
  
## <a name="see-also"></a>Ver también  
 [@@FETCH_STATUS &#40;Transact-SQL&#41;](../../t-sql/functions/fetch-status-transact-sql.md)   
 [CLOSE &#40;Transact-SQL&#41;](../../t-sql/language-elements/close-transact-sql.md)   
 [Cursores &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)   
 [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
