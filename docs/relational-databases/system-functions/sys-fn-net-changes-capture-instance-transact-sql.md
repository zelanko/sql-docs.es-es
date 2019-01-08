---
title: Sys.fn_net_changes_&lt;capture_instance&gt; (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_net_changes_TSQL
- fn_net_changes_TSQL
- fn_net_changes
- sys.fn_net_changes
dev_langs:
- TSQL
helpviewer_keywords:
- fn_net_changes_<capture_instance>
- sys.fn_net_changes_<capture_instance>
ms.assetid: 342fa030-9fd9-4b74-ae4d-49f6038a5073
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 081eaa3995507edf20be0b83f3e0ce766135139c
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52416326"
---
# <a name="sysfnnetchangesltcaptureinstancegt-transact-sql"></a>Sys.fn_net_changes_&lt;capture_instance&gt; (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contenedores para la **net cambios** funciones de consulta. El procedimiento almacenado sys.sp_cdc_generate_wrapper_function genera los scripts necesarios para crear estas funciones.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn_net_changes_<capture_instance> ('start_time', 'end_time', '<row_filter_option>' )  
  
<capture_instance> ::= The name of the capture instance.  
<row_filter_option> ::=  
{ all  
  | all with mask  
  | all with merge  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *start_time*  
 El **datetime** valor que representa el extremo inferior del intervalo de las entradas de tabla para incluir en el conjunto de resultados.  
  
 Solo las filas de los cdc. < instancia_de_captura > _CT tabla de cambios que tienen un tiempo de confirmación asociado estrictamente mayor que *start_time* se incluyen en el conjunto de resultados.  
  
 Si se proporciona un valor NULL para este argumento, el extremo inferior del intervalo de consulta se corresponderá con el extremo inferior del intervalo válido de la instancia de captura.  
  
 *end_time*  
 El **datetime** valor que representa el extremo superior del intervalo de las entradas de tabla para incluir en el conjunto de resultados.  
  
 Este parámetro puede tomar uno de dos significados posibles, según el valor elegido para @closed_high_end_point cuando se llama a sys.sp_cdc_generate_wrapper_function para generar el script para crear la función contenedora:  
  
-   @closed_high_end_point = 1  
  
     Solo las filas de los cdc. < instancia_de_captura > _CT tabla de cambios que tienen un valor en \_ \_$start_lsn y un confirmación correspondiente menor o igual a hora **start_time** se incluyen en el conjunto de resultados.  
  
-   @closed_high_end_point = 0  
  
     Solo las filas de los cdc. < instancia_de_captura > _CT tabla de cambios que tienen un valor en \_ \_$start_lsn y un tiempo de confirmación estrictamente menor que **start_time** se incluyen en el conjunto de resultados.  
  
 Si se proporciona un valor NULL para este argumento, el extremo superior del intervalo de consulta se corresponderá con el extremo superior del intervalo válido de la instancia de captura.  
  
 *< row_filter_option >* :: = {todos | todos con máscara | todos con combinación}  
 Una opción que rige el contenido de las columnas de metadatos y las filas devueltas en el conjunto de resultados. Puede ser una de las siguientes opciones:  
  
 all  
 Devuelve el contenido final de una fila cambiada en las columnas de contenido y la operación que se necesita para aplicar la fila en la columna de metadatos __CDC_OPERATION.  
  
 all with mask  
 Devuelve el contenido final de todas las filas cambiadas en las columnas de contenido y la operación necesaria para aplicar cada fila en la columna de metadatos __CDC_OPERATION. Si se especificó una lista de marcas de actualización al generar el script para crear la función contenedora, esta opción es necesaria para rellenar la máscara de actualización.  
  
 todos con combinación  
 Devuelve el contenido final de todas las filas cambiadas en las columnas de contenido.  
  
 La columna __CDC_OPERATION contendrá uno de los dos valores siguientes:  
  
-   D, si la fila se debe eliminar  
  
-   M, si la fila se debe insertar o actualizar.  
  
 La lógica para determinar si se requiere una operación de inserción o actualización para aplicar un cambio al destino agrega complejidad a la consulta. Utilice esta opción para mejorar el rendimiento cuando no sea necesario diferenciar entre operaciones de inserción y actualización. Este enfoque funciona mejor en entornos de destino en los que las operaciones de mezcla están disponibles directamente, por ejemplo en un entorno de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de columna|Descripción|  
|-----------------|-----------------|-----------------|  
|\<columnas de @column_list>|**Varía**|Las columnas que se identifican en el **column_list** argumento a la función sp_cdc_generate_wrapper_function cuando se llama para generar el script que crea el contenedor. Si *column_list* es NULL, todas las columnas de origen sometidas a seguimiento aparecerán en el conjunto de resultados.|  
|__CDC_OPERATION|**nvarchar (2)**|Un código de operación que indica qué operación se debe aplicar la fila en el entorno de destino. La operación variará en función del valor del argumento *row_filter_option* que se proporciona en la siguiente llamada:<br /><br /> *row_filter_option* = 'all', 'all with mask'<br /><br /> 'D' - operación de eliminación<br /><br /> 'I' - operación de inserción<br /><br /> 'UN' - operación de actualización<br /><br /> *row_filter_option* = 'all with merge'<br /><br /> 'D' - operación de eliminación<br /><br /> 'M' - operación de inserción o de actualización|  
|\<columnas de @update_flag_list>|**bit**|Marca de bits que se denomina anexando _uflag al nombre de columna. La marca acepta un valor distinto de null solo cuando *row_filter_option* **= 'all with mask'** y \__CDC_OPERATION **'UN ='**. Se establece en 1 si la columna correspondiente se modificó dentro de la ventana de consulta. En caso contrario, es 0.|  
  
## <a name="remarks"></a>Comentarios  
 La función fn_net_changes_<instancia_de_captura> actúa de contenedor para la función de consulta cdc.fn_cdc_get_net_changes_<instancia_de_captura>. El procedimiento almacenado sys.sp_cdc_generate_wrapper se utiliza para crear el script del contenedor.  
  
 Las funciones contenedoras no se crean automáticamente. Para crear funciones contenedoras hay que seguir dos pasos:  
  
1.  Ejecutar el procedimiento almacenado para generar el script que permite crear el contenedor.  
  
2.  Ejecutar el script para crear realmente la función contenedora.  
  
 Las funciones contenedoras permiten a los usuarios consultar cambios ocurridos durante un intervalo limitado por **datetime** valores en lugar de por valores LSN. Las funciones contenedoras realizan todas las conversiones necesarias entre proporcionado **datetime** valores y los valores LSN necesarios internamente como argumentos a las funciones de consulta. Cuando las funciones contenedoras se utilizan en serie para procesar un flujo de datos modificados, asegúrese de que ningún dato se pierde o se repite siempre que se adopte la convención siguiente: el @end_time se proporciona el valor del intervalo asociado a una llamada como el @start_time valor para el intervalo de la llamada siguiente.  
  
 Si se usa el parámetro @closed_high_end_point al crear el script, se pueden generar contenedores para admitir un límite superior cerrado o un límite superior abierto en la ventana de consulta especificada. Es decir, puede decidir si las entradas que tienen un tiempo de confirmación igual al límite superior del intervalo de extracción se incluirán en el intervalo. De forma predeterminada, se incluye el límite superior.  
  
 El conjunto de resultados devuelven por la **net cambios** contenedor función devuelve solo las columnas que se encontraban en sometidas a seguimiento los @column_list cuando se generó el contenedor. Si @column_list es NULL, se devuelven todas las columnas de origen sometidas a seguimiento. Las columnas de origen van seguidas de una columna de operación, __CDC_OPERATION, que es una columna de uno o dos caracteres que identifica la operación.  
  
 Las marcas de bits, a continuación, se anexan al conjunto de resultados para cada columna que se identifica en el parámetro @update_flag_list. Para el **net cambios** contenedor, el bit de marcas will siempre es NULL si el @row_filter_option que es utilizada en la llamada a la función contenedora es 'all' o 'all with merge'. Si el @row_filter_option se establece en 'todos con máscara' y __CDC_OPERATION es tenía ' o 'I', el valor de la marca también será NULL. Si \__CDC_OPERATION 'UN es ', la marca se establecerá en 1 ó 0, dependiendo de si el **net** provocada un cambio en la columna de la operación de actualización.  
  
 Plantilla de configuración de captura de datos modificados 'Instantiate el CDC Wrapper TVFs for Schema' muestra cómo usar el procedimiento almacenado sp_cdc_generate_wrapper_function para obtener scripts CREATE para todas las funciones de contenedor para las funciones de consulta definidas de un esquema. A continuación, la plantilla crea esos scripts. Para obtener más información acerca de las plantillas, consulte [Explorador de plantillas](../../ssms/template/template-explorer.md).  
  
## <a name="see-also"></a>Vea también  
 [sys.sp_cdc_generate_wrapper_function &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)  
  
  
