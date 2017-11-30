---
title: Sys.fn_all_changes_&lt;capture_instance&gt; (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server (starting with 2008)
f1_keywords:
- fn_all_changes
- sys.fn_all_changes
- fn_all_changes_TSQL
- sys.fn_all_changes_TSQL
dev_langs: TSQL
helpviewer_keywords:
- fn_all_changes_<capture_instance>
- sys.fn_all_changes_<capture_instance>
ms.assetid: 564fae96-b88c-4f22-9338-26ec168ba6f5
caps.latest.revision: "15"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 29f9560f7308fef45468c7ce67a6f8a15e120a3b
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="sysfnallchangesltcaptureinstancegt-transact-sql"></a>Sys.fn_all_changes_&lt;capture_instance&gt; (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contenedores para la **todos los cambios** funciones de consulta. El procedimiento almacenado sys.sp_cdc_generate_wrapper_function genera los scripts necesarios para crear estas funciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn_all_changes_<capture_instance> ('start_time' ,'end_time', '<row_filter_option>' )  
  
<capture_instance> ::= The name of the capture instance.  
<row_filter_option> ::=  
{ all  
  | all update old  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *start_time*  
 El **datetime** valor que representa el extremo inferior del intervalo de entradas de la tabla de cambio que se incluirán en el conjunto de resultados.  
  
 Solo la tabla que tienen un tiempo de confirmación asociado mayor de cambios de filas de cdc. < instancia_de_captura > _CT *start_time* se incluyen en el conjunto de resultados.  
  
 Si se proporciona un valor NULL para este argumento, el extremo inferior del intervalo de consulta se corresponderá con el extremo inferior del intervalo válido de la instancia de captura.  
  
 *end_time*  
 El **datetime** valor que representa el extremo superior del intervalo de entradas de la tabla de cambio que se incluirán en el conjunto de resultados.  
  
 Este parámetro puede tener uno de dos significados posibles, según el valor elegido para @closed_high_end_point cuando se llama a sys.sp_cdc_generate_wrapper_function para generar el script de creación para la función contenedora:  
  
-   @closed_high_end_point = 1  
  
     Solo las filas de la tabla de cambios cdc.<capture_instance>_CT que tienen un tiempo de confirmación asociado menor o igual que end_time se incluyen en el conjunto de resultados.  
  
-   @closed_high_end_point = 0  
  
     Solo las filas de la tabla de cambios cdc.capture_instance_CT que tienen un tiempo de confirmación asociado estrictamente menor que end_time se incluyen en el conjunto de resultados.  
  
 Si se proporciona un valor NULL para este argumento, el extremo superior del intervalo de consulta se corresponderá con el extremo superior del intervalo válido de la instancia de captura.  
  
 <row_filter_option> ::= { all | all update old }  
 Opción que rige el contenido de las columnas de metadatos y las filas devueltas en el conjunto de resultados.  
  
 Puede ser una de las siguientes opciones:  
  
 all  
 Devuelve todos los cambios dentro del intervalo LSN especificado. Para los cambios que se producen debido a una operación de actualización, esta opción devuelve solo la fila que contiene los valores nuevos una vez aplicada la actualización.  
  
 all update old  
 Devuelve todos los cambios dentro del intervalo LSN especificado. Para los cambios que se producen debido a una operación de actualización, esta opción devuelve las filas que contienen los valores de columna antes y después de la actualización.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de columna|Description|  
|-----------------|-----------------|-----------------|  
|__CDC_STARTLSN|**binary(10)**|LSN de confirmación de la transacción que se asocia al cambio. Todos los cambios que se confirman en la misma transacción comparten el mismo LSN de confirmación.|  
|__CDC_SEQVAL|**binary(10)**|Valor de secuencia que se usa para ordenar los cambios de fila en una transacción.|  
|\<columnas de @column_list>|**varía**|Las columnas que se identifican en el *column_list* argumento para la función sp_cdc_generate_wrapper_function cuando se llama para generar el script que crea la función contenedora.|  
|__CDC_OPERATION|**nvarchar(2)**|Código de operación que indica qué operación hay que aplicar a la fila en el entorno de destino. Variará según el valor del argumento *row_filter_option* proporcionados en la llamada:<br /><br /> *row_filter_option* = 'all'<br /><br /> 'D' - operación de eliminación<br /><br /> 'I' - operación de inserción<br /><br /> 'UN' - valores nuevos de la operación de actualización<br /><br /> *row_filter_option* = 'all update old'<br /><br /> 'D' - operación de eliminación<br /><br /> 'I' - operación de inserción<br /><br /> 'UN' - valores nuevos de la operación de actualización<br /><br /> 'UO' - valores anteriores de la operación de actualización|  
|\<columnas de @update_flag_list>|**bit**|Un indicador de bits se denomina anexando _uflag al nombre de columna. La marca siempre se establece en NULL cuando \__CDC_OPERATION se tenía ', 'I', de 'UO'. Cuando \__CDC_OPERATION es 'UN', se establece en 1 si la actualización generó un cambio en la columna correspondiente. En caso contrario, es 0.|  
  
## <a name="remarks"></a>Comentarios  
 La función fn_all_changes_<capture_instance> actúa como contenedor para la función de consulta cdc.fn_cdc_get_all_changes_<capture_instance>. El procedimiento almacenado sys.sp_cdc_generate_wrapper se utiliza para generar el script que crea el contenedor.  
  
 Las funciones contenedoras no se crean automáticamente. Para crear funciones contenedoras hay que seguir dos pasos:  
  
1.  Ejecutar el procedimiento almacenado para generar el script que permite crear el contenedor.  
  
2.  Ejecutar el script para crear realmente la función contenedora.  
  
 Las funciones contenedoras permiten a los usuarios consultar cambios que se produjeron dentro de un intervalo limitado por **datetime** valores en lugar de por valores LSN. Las funciones contenedoras realizan todas las conversiones necesarias entre proporcionado **datetime** valores y los valores LSN necesarios internamente como argumentos a las funciones de consulta. Cuando las funciones contenedoras se utilizan en serie para procesar un flujo de datos modificados, asegúrese de que ningún dato se pierde o se repite siempre que se adopte la convención siguiente: el @end_time se proporciona el valor del intervalo asociado a una llamada como la @start_time valor del intervalo asociado a la llamada siguiente.  
  
 Si se usa el parámetro @closed_high_end_point al crear el script, se pueden generar contenedores para admitir un límite superior cerrado o un límite superior abierto en la ventana de consulta especificada. Es decir, puede decidir si las entradas que tienen un tiempo de confirmación igual al límite superior del intervalo de extracción se incluirán en el intervalo. De forma predeterminada, se incluye el límite superior.  
  
 El conjunto de resultados devuelto por la **todos los cambios** función contenedora devuelve __ $start_lsn y \_ \_$seqval columnas de la tabla de cambios como columnas \__CDC_STARTLSN y \__ CDC_SEQVAL, respectivamente. Sigue a estos con solo las columnas sometidas a seguimiento que aparecían en el  *@column_list*  parámetro cuando se generó el contenedor. Si  *@column_list*  es NULL, todas las columnas se devuelven de origen sometidas a seguimiento. Las columnas de origen van seguidas de una columna de operación, \__CDC_OPERATION, que es una columna de uno o dos caracteres que identifica la operación.  
  
 A continuación, las marcas de bits se anexan al conjunto de resultados para cada columna que se identifica en el parámetro @update_flag_list. Para el **todos los cambios** contenedor, las marcas de bits siempre será NULL si __CDC_OPERATION es tenía ', 'I' o 'UO'. Si \__CDC_OPERATION es 'UN', la marca se establecerá en 1 ó 0, dependiendo de si la operación de actualización produjo un cambio en la columna.  
  
 En la plantilla de configuración de captura de datos modificados 'Instantiate CDC Wrapper TVFs for Schema' se muestra cómo utilizar el procedimiento almacenado sp_cdc_generate_wrapper_function para obtener scripts CREATE para todas las funciones contenedoras de las funciones de consulta definidas para un esquema. A continuación, la plantilla crea esos scripts. Para obtener más información acerca de las plantillas, consulte [Explorador de plantillas](http://msdn.microsoft.com/library/b9ee55c5-bb44-4f76-90ac-792d8d83b4c8).  
  
## <a name="see-also"></a>Vea también  
 [Sys.sp_cdc_generate_wrapper_function &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)   
 [CDC.fn_cdc_get_all_changes_ &#60; capture_instance &#62;  &#40; Transact-SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  
