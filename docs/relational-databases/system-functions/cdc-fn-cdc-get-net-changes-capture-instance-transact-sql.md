---
title: CDC.fn_cdc_get_net_changes_&lt;capture_instance&gt; (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_net_changes_<capture_instance>
- change data capture [SQL Server], querying metadata
- cdc.fn_cdc_get_net_changes_<capture_instance>
ms.assetid: 43ab0d1b-ead4-471c-85f3-f6c4b9372aab
author: rothja
ms.author: jroth
ms.openlocfilehash: 77fb03c71bd0773cc8f004a89c28c1925284876b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68043043"
---
# <a name="cdcfncdcgetnetchangesltcaptureinstancegt-transact-sql"></a>cdc.fn_cdc_get_net_changes_&lt;capture_instance&gt; (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila de cambio neto por cada fila de origen cambiada dentro del intervalo de números de secuencia de registro (LSN) especificado.  
  
 **Espere, ¿qué es un LSN?** Todos los registros en el [registro de transacciones de SQL Server](../logs/the-transaction-log-sql-server.md) se identifica mediante un número de secuencia de registro (LSN). Los LSN se ordenan de manera que si LSN2 es mayor que LSN1, se produjo el cambio descrito por la entrada del registro que hace referencia LSN2 **después** del cambio descrito por la entrada del registro LSN.  
  
 El LSN de una entrada de registro donde se produjo un evento importante puede ser útil para generar secuencias de restauración correcta. Dado que los LSN se ordenan, se puede comparar de igualdad y desigualdad (es decir, \<, >, =, \<=, > =). Estas comparaciones son útiles para generar secuencias de restauración.  
  
 Cuando una fila de origen tiene varios cambios durante el intervalo de LSN, se devuelve una fila única que refleja el contenido final de la fila por la función de enumeración que se describen a continuación. Por ejemplo, si una transacción inserta una fila en la tabla de origen y una transacción subsiguiente dentro del intervalo LSN actualiza una o varias columnas de esa fila, la función devuelve solo **uno** fila, que incluye los valores de columna actualizada.  
  
 Esta función de enumeración se crea cuando se habilita una tabla de origen para la captura de datos modificados y se especifica seguimientos de cambios en la red. Para habilitar el seguimiento de cambios netos, la tabla de origen debe tener una clave principal o índice único. El nombre de función y se obtiene del formato cdc.fn_cdc_get_net_changes_ se utiliza*capture_instance*, donde *capture_instance* es el valor especificado para la instancia de captura cuando la tabla de origen estaba habilitado para la captura de datos modificados. Para obtener más información, consulte [sys.sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
cdc.fn_cdc_get_net_changes_capture_instance ( from_lsn , to_lsn , '<row_filter_option>' )  
  
<row_filter_option> ::=  
{ all  
 | all with mask  
 | all with merge  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *from_lsn*  
 El LSN que representa el extremo inferior del rango de LSN que se va a incluir en el conjunto de resultados. *from_lsn* es **binary (10)** .  
  
 Solo las filas de la [cdc.&#91; capture_instance&#93;_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md) cambiar la tabla con un valor de __ $ start_lsn sea mayor o igual que *from_lsn* se incluyen en el conjunto de resultados.  
  
 *to_lsn*  
 El LSN que representa el extremo superior del rango de LSN que se va a incluir en el conjunto de resultados. *to_lsn* es **binary (10)** .  
  
 Solo las filas de la [cdc.&#91; capture_instance&#93;_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md) cambiar la tabla con un valor en __ $ start_lsn sea menor o igual que *from_lsn* o igual que *to_lsn* se incluyen en el conjunto de resultados.  
  
 *< row_filter_option >* :: = {todos | todos con máscara | todos con combinación}  
 Una opción que rige el contenido de las columnas de metadatos y las filas devueltas en el conjunto de resultados. Puede ser una de las siguientes opciones:  
  
 all  
 Devuelve el LSN del último cambio realizado en la fila y la operación necesaria para aplicar la fila en las columnas de metadatos __ $start_lsn y \_ \_$operation. La columna \_ \_$update_mask es siempre NULL.  
  
 all with mask  
 Devuelve el LSN del último cambio realizado en la fila y la operación necesaria para aplicar la fila en las columnas de metadatos __ $start_lsn y \_ \_$operation. Además, cuando una operación de actualización devuelve (\_\_$operation = 4) las columnas capturadas modificadas en la actualización se marcan en el valor devuelto en \_ \_$update_mask.  
  
 todos con combinación  
 Devuelve el LSN del último cambio realizado en la fila en las columnas de metadatos __$start_lsn. La columna \_ \_$operation será uno de dos valores: 1 para eliminar y 5 para indicar que la operación necesaria para aplicar el cambio es una inserción o una actualización. La columna \_ \_$update_mask es siempre NULL.  
  
 Debido a que la lógica para determinar la operación precisa de un cambio determinado agrega mayor complejidad a la consulta, esta opción se ha diseñado para mejorar el rendimiento de las consultas cuando es suficiente indicar que la operación necesaria para aplicar los datos de cambio es una inserción o una actualización, pero no es necesario distinguir explícitamente entre las dos. Esta opción resulta muy útil en entornos de destino donde las operaciones Combinar están directamente disponibles, como en un entorno [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|__$start_lsn|**binary(10)**|Número de secuencia de registro (LSN) asociado con la transacción de confirmación para el cambio.<br /><br /> Todos los cambios confirmados en la misma transacción comparten el mismo LSN de confirmación. Por ejemplo, si una operación de actualización en la tabla de origen modifica dos columnas en dos filas, la tabla de cambios contendrá cuatro filas, cada uno con el mismo start_lsnvalue$ de __.|  
|__$operation|**int**|Identifica la operación del lenguaje de manipulación de datos (DML) necesaria para aplicar la fila de datos modificados al origen de datos de destino.<br /><br /> Si el valor del parámetro row_filter_option es todos o todos con máscara, el valor de esta columna puede ser uno de los siguientes:<br /><br /> 1 = eliminar<br /><br /> 2 = insertar<br /><br /> 4 = actualizar<br /><br /> Si el valor del parámetro row_filter_option es todos con combinación, el valor de esta columna puede ser uno de los siguientes:<br /><br /> 1 = eliminar|  
|__$update_mask|**varbinary(128)**|Máscara de bits con un bit que corresponde a cada columna capturada identificada para la instancia de captura. Este valor tiene todos los bits definidos establecidos en 1 si __$operation = 1 o 2. Cuando \_ \_$operation = 3 o 4, solo los bits que corresponden a columnas que han cambiado se establecen en 1.|  
|*\<columnas de la tabla de origen capturadas>*|varía|Las columnas restantes devueltas por la función son las columnas de la tabla de origen que se identificaron como columnas capturadas cuando se creó la instancia de captura. Si no se especificó ninguna columna en la lista de columnas capturadas, se devuelven todas las columnas de la tabla de origen.|  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol fijo de servidor sysadmin o al rol fijo de base de datos db_owner. Para el resto de usuarios, requiere el permiso SELECT en todas las columnas capturadas en la tabla de origen y, si se ha definido un rol de acceso para la instancia de captura, la pertenencia a ese rol de base de datos. Cuando el autor de la llamada no tiene permiso para ver los datos de origen, la función devuelve el error 208 (Nombre de objeto no válido).  
  
## <a name="remarks"></a>Comentarios  
 Si el intervalo del LSN especificado no se encuentra dentro de la escala temporal del seguimiento de cambios de la instancia de captura, la función devuelve el error 208 (Nombre de objeto no válido).

 Las modificaciones en el identificador único de una fila hará que fn_cdc_get_net_changes mostrar el comando de actualización inicial con una eliminación y, a continuación, insertar comandos en su lugar.  Este comportamiento es necesario realizar un seguimiento de la clave antes y después del cambio.
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa la función `cdc.fn_cdc_get_net_changes_HR_Department` para notificar los cambios netos realizados en la tabla de origen `HumanResources.Department` durante un intervalo de tiempo específico.  
  
 En primer lugar, se usa la función `GETDATE` para marcar el inicio del intervalo de tiempo. Después de aplicar varias instrucciones DML a la tabla de origen, se llama de nuevo a la función `GETDATE` para identificar el final del intervalo de tiempo. La función [sys.fn_cdc_map_time_to_lsn](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) , a continuación, se usa para asignar el intervalo de tiempo para un intervalo de consulta de captura de datos modificados limitado por valores LSN. Por último, se consulta la función `cdc.fn_cdc_get_net_changes_HR_Department` para obtener los cambios de la red realizados en la tabla de origen durante el intervalo de tiempo. Observe que la fila que se inserta y, a continuación, se elimina no aparece en el conjunto de resultados devuelto por la función. Esto se debe a que una fila que primero se agrega y luego se elimina dentro de una ventana de consulta no genera ningún cambio de la red en la tabla de origen para el intervalo. Antes de ejecutar este ejemplo, primero debe ejecutar el ejemplo B en [sys.sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md).  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @begin_time datetime, @end_time datetime, @from_lsn binary(10), @to_lsn binary(10);  
-- Obtain the beginning of the time interval.  
SET @begin_time = GETDATE() -1;  
-- DML statements to produce changes in the HumanResources.Department table.  
INSERT INTO HumanResources.Department (Name, GroupName)  
VALUES (N'MyDept', N'MyNewGroup');  
  
UPDATE HumanResources.Department  
SET GroupName = N'Resource Control'  
WHERE GroupName = N'Inventory Management';  
  
DELETE FROM HumanResources.Department  
WHERE Name = N'MyDept';  
  
-- Obtain the end of the time interval.  
SET @end_time = GETDATE();  
-- Map the time interval to a change data capture query range.  
SET @from_lsn = sys.fn_cdc_map_time_to_lsn('smallest greater than or equal', @begin_time);  
SET @to_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal', @end_time);  
  
-- Return the net changes occurring within the query window.  
SELECT * FROM cdc.fn_cdc_get_net_changes_HR_Department(@from_lsn, @to_lsn, 'all');  
```  
  
## <a name="see-also"></a>Vea también  
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [sys.fn_cdc_map_time_to_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)   
 [sys.sp_cdc_enable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-table-transact-sql.md)   
 [sys.sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [Acerca de la captura de datos modificados &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
