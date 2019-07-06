---
title: sys.fn_all_changes_&lt;capture_instance&gt; (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_all_changes
- sys.fn_all_changes
- fn_all_changes_TSQL
- sys.fn_all_changes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_all_changes_<capture_instance>
- sys.fn_all_changes_<capture_instance>
ms.assetid: 564fae96-b88c-4f22-9338-26ec168ba6f5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 40bf73a1cdca0bc582ac3e6ed6a977980d2aa24f
ms.sourcegitcommit: cff8dd63959d7a45c5446cadf1f5d15ae08406d8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/05/2019
ms.locfileid: "67585112"
---
# <a name="sysfnallchangesltcaptureinstancegt-transact-sql"></a>sys.fn_all_changes_&lt;capture_instance&gt; (Transact-SQL)
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
 El **datetime** valor que representa el extremo inferior del intervalo de las entradas de tabla para incluir en el conjunto de resultados.  
  
 Solo las filas de los cdc. < instancia_de_captura > _CT tabla de cambios que tienen un tiempo de confirmación asociado mayor *start_time* se incluyen en el conjunto de resultados.  
  
 Si se proporciona un valor NULL para este argumento, el extremo inferior del intervalo de consulta se corresponderá con el extremo inferior del intervalo válido de la instancia de captura.  
  
 *end_time*  
 El **datetime** valor que representa el extremo superior del intervalo de las entradas de tabla para incluir en el conjunto de resultados.  
  
 Este parámetro puede tener uno de dos significados posibles, según el valor elegido para @closed_high_end_point cuando se llama a sys.sp_cdc_generate_wrapper_function para generar el script de creación para la función contenedora:  
  
-   @closed_high_end_point = 1  
  
     Solo las filas de la tabla de cambios cdc. < instancia_de_captura > _CT que tienen una confirmación asociado tiempo menor que o igual que end_time se incluyen en el conjunto de resultados...  
  
-   @closed_high_end_point = 0  
  
     Solo las filas de la cdc.capture_instance_CT tabla de cambios que haya un tiempo de confirmación asociado estrictamente menor que end_time se incluyen en el resultado establecido.  
  
 Si se proporciona un valor NULL para este argumento, el extremo superior del intervalo de consulta se corresponderá con el extremo superior del intervalo válido de la instancia de captura.  
  
 <row_filter_option> ::= { all | all update old }  
 Opción que rige el contenido de las columnas de metadatos y las filas devueltas en el conjunto de resultados.  
  
 Puede ser una de las siguientes opciones:  
  
 all  
 Devuelve todos los cambios dentro del intervalo LSN especificado. Para los cambios que se producen debido a una operación de actualización, esta opción devuelve solo la fila que contiene los valores nuevos una vez aplicada la actualización.  
  
 all update old  
 Devuelve todos los cambios dentro del intervalo LSN especificado. Para los cambios que se producen debido a una operación de actualización, esta opción devuelve las filas que contienen los valores de columna antes y después de la actualización.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de columna|Descripción|  
|-----------------|-----------------|-----------------|  
|__CDC_STARTLSN|**binary(10)**|LSN de confirmación de la transacción que se asocia al cambio. Todos los cambios que se confirman en la misma transacción comparten el mismo LSN de confirmación.|  
|__CDC_SEQVAL|**binary(10)**|Valor de secuencia que se usa para ordenar los cambios de fila en una transacción.|  
|\<columnas de @column_list>|**varies**|Las columnas que se identifican en el *column_list* argumento para la función sp_cdc_generate_wrapper_function cuando se llama para generar el script que crea la función contenedora.|  
|__CDC_OPERATION|**nvarchar(2)**|Código de operación que indica qué operación hay que aplicar a la fila en el entorno de destino. Variará en función del valor del argumento *row_filter_option* proporcionados en la llamada:<br /><br /> *row_filter_option* = 'all'<br /><br /> 'D' - operación de eliminación<br /><br /> 'I' - operación de inserción<br /><br /> 'UN' - valores nuevos de la operación de actualización<br /><br /> *row_filter_option* = 'all update old'<br /><br /> 'D' - operación de eliminación<br /><br /> 'I' - operación de inserción<br /><br /> 'UN' - valores nuevos de la operación de actualización<br /><br /> 'UO' - valores anteriores de la operación de actualización|  
|\<columnas de @update_flag_list>|**bit**|Un indicador de bits se denomina anexando _uflag al nombre de columna. La marca siempre se establece en NULL cuando \__CDC_OPERATION se tenía ', 'I', de 'UO'. Cuando \__CDC_OPERATION es 'UN', se establece en 1 si la actualización generó un cambio en la columna correspondiente. En caso contrario, es 0.|  
  
## <a name="remarks"></a>Comentarios  
 La función fn_all_changes_ < capture_instance > actúa como contenedor para la función de consulta cdc.fn_cdc_get_all_changes_ < capture_instance >. El procedimiento almacenado sys.sp_cdc_generate_wrapper se utiliza para generar el script que crea el contenedor.  
  
 Las funciones contenedoras no se crean automáticamente. Para crear funciones contenedoras hay que seguir dos pasos:  
  
1.  Ejecutar el procedimiento almacenado para generar el script que permite crear el contenedor.  
  
2.  Ejecutar el script para crear realmente la función contenedora.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

 Las funciones contenedoras permiten a los usuarios consultar cambios ocurridos durante un intervalo limitado por **datetime** valores en lugar de por valores LSN. Las funciones contenedoras realizan todas las conversiones necesarias entre proporcionado **datetime** valores y los valores LSN necesarios internamente como argumentos a las funciones de consulta. Cuando las funciones contenedoras se utilizan en serie para procesar un flujo de datos modificados, asegúrese de que ningún dato se pierde o se repite siempre que se adopte la convención siguiente: el @end_time se proporciona el valor del intervalo asociado a una llamada como el @start_time valor para el intervalo de la llamada siguiente.  
  
 Si se usa el parámetro @closed_high_end_point al crear el script, se pueden generar contenedores para admitir un límite superior cerrado o un límite superior abierto en la ventana de consulta especificada. Es decir, puede decidir si las entradas que tienen un tiempo de confirmación igual al límite superior del intervalo de extracción se incluirán en el intervalo. De forma predeterminada, se incluye el límite superior.  
  
 El conjunto de resultados devuelven por la **todos los cambios** función devolverá el __ $start_lsn y \_ \_$seqval columnas de la tabla de cambios como columnas \__CDC_STARTLSN y \__ CDC_SEQVAL, respectivamente. Sigue estos elementos con solo las columnas sometidas a seguimiento que aparecían en el *@column_list* parámetro cuando se generó el contenedor. Si *@column_list* es NULL, todas se devuelven las columnas de origen sometidas a seguimiento. Las columnas de origen van seguidas de una columna operación, \__CDC_OPERATION, que es una columna de uno o dos caracteres que identifica la operación.  
  
 A continuación, las marcas de bits se anexan al conjunto de resultados para cada columna que se identifica en el parámetro @update_flag_list. Para el **todos los cambios** contenedor, las marcas de bits serán NULL siempre si __CDC_OPERATION es tenía ', 'I' o 'UO'. Si \__CDC_OPERATION 'UN es ', la marca se establecerá en 1 ó 0, dependiendo de si la operación de actualización produjo un cambio en la columna.  
  
 Plantilla de configuración de captura de datos modificados 'Instantiate el CDC Wrapper TVFs for Schema' muestra cómo usar el procedimiento almacenado sp_cdc_generate_wrapper_function para obtener scripts CREATE para todas las funciones de contenedor para las funciones de consulta definidas de un esquema. A continuación, la plantilla crea esos scripts. Para obtener más información acerca de las plantillas, consulte [Explorador de plantillas](../../ssms/template/template-explorer.md).  
  
## <a name="see-also"></a>Vea también  
 [sys.sp_cdc_generate_wrapper_function &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  
