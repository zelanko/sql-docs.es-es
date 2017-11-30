---
title: Sys.fn_net_changes_&lt;capture_instance&gt; (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
- sys.fn_net_changes_TSQL
- fn_net_changes_TSQL
- fn_net_changes
- sys.fn_net_changes
dev_langs: TSQL
helpviewer_keywords:
- fn_net_changes_<capture_instance>
- sys.fn_net_changes_<capture_instance>
ms.assetid: 342fa030-9fd9-4b74-ae4d-49f6038a5073
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: be3cd4da4aa890624dc33f36af135bd96dbc3057
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
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
 El **datetime** valor que representa el extremo inferior del intervalo de entradas de la tabla de cambio que se incluirán en el conjunto de resultados.  
  
 Únicamente filas de cdc. < instancia_de_captura > _CT cambiar la tabla que tienen un tiempo de confirmación asociado estrictamente mayor que *start_time* se incluyen en el conjunto de resultados.  
  
 Si se proporciona un valor NULL para este argumento, el extremo inferior del intervalo de consulta se corresponderá con el extremo inferior del intervalo válido de la instancia de captura.  
  
 *end_time*  
 El **datetime** valor que representa el extremo superior del intervalo de entradas de la tabla de cambio que se incluirán en el conjunto de resultados.  
  
 Este parámetro puede tener uno de dos significados, según el valor elegido para @closed_high_end_point cuando se llama a sys.sp_cdc_generate_wrapper_function para generar el script para crear la función contenedora:  
  
-   @closed_high_end_point = 1  
  
     Solo filas de cdc. < instancia_de_captura > _CT tabla de cambios que tienen un valor en \_ \_$start_lsn y una confirmación correspondiente menor o igual a tiempo **start_time** se incluyen en el conjunto de resultados.  
  
-   @closed_high_end_point = 0  
  
     Solo filas de cdc. < instancia_de_captura > _CT tabla de cambios que tienen un valor en \_ \_$start_lsn y un tiempo de confirmación estrictamente menor que **start_time** se incluyen en el conjunto de resultados.  
  
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
  
|Nombre de columna|Tipo de columna|Description|  
|-----------------|-----------------|-----------------|  
|\<columnas de @column_list>|**varía**|Las columnas que se identifican en el **column_list** argumento pasado a la función sp_cdc_generate_wrapper_function cuando se llama para generar el script para crear el contenedor. Si *column_list* es NULL, todas las columnas de origen sometidas a seguimiento aparecerán en el conjunto de resultados.|  
|__CDC_OPERATION|**nvarchar(2)**|Un código de operación que indica qué operación se debe aplicar la fila en el entorno de destino. La operación varían según el valor del argumento *row_filter_option* que se proporciona en la siguiente llamada:<br /><br /> *row_filter_option* = 'all', 'all with mask'<br /><br /> 'D' - operación de eliminación<br /><br /> 'I' - operación de inserción<br /><br /> 'UN' - operación de actualización<br /><br /> *row_filter_option* = 'all with merge'<br /><br /> 'D' - operación de eliminación<br /><br /> 'M' - operación de inserción o de actualización|  
|\<columnas de @update_flag_list>|**bit**|Marca de bits que se denomina anexando _uflag al nombre de columna. La marca acepta un valor distinto de null solo cuando *row_filter_option* **= 'all with mask'** y \__CDC_OPERATION **= 'UN'**. Se establece en 1 si la columna correspondiente se modificó dentro de la ventana de consulta. En caso contrario, es 0.|  
  
## <a name="remarks"></a>Comentarios  
 La función fn_net_changes_<instancia_de_captura> actúa de contenedor para la función de consulta cdc.fn_cdc_get_net_changes_<instancia_de_captura>. El procedimiento almacenado sys.sp_cdc_generate_wrapper se utiliza para crear el script del contenedor.  
  
 Las funciones contenedoras no se crean automáticamente. Para crear funciones contenedoras hay que seguir dos pasos:  
  
1.  Ejecutar el procedimiento almacenado para generar el script que permite crear el contenedor.  
  
2.  Ejecutar el script para crear realmente la función contenedora.  
  
 Las funciones contenedoras permiten a los usuarios consultar cambios que se produjeron dentro de un intervalo limitado por **datetime** valores en lugar de por valores LSN. Las funciones contenedoras realizan todas las conversiones necesarias entre proporcionado **datetime** valores y los valores LSN necesarios internamente como argumentos a las funciones de consulta. Cuando las funciones contenedoras se utilizan en serie para procesar un flujo de datos modificados, asegúrese de que ningún dato se pierde o se repite siempre que se adopte la convención siguiente: el @end_time se proporciona el valor del intervalo asociado a una llamada como la @start_time valor del intervalo asociado a la llamada siguiente.  
  
 Si se usa el parámetro @closed_high_end_point al crear el script, se pueden generar contenedores para admitir un límite superior cerrado o un límite superior abierto en la ventana de consulta especificada. Es decir, puede decidir si las entradas que tienen un tiempo de confirmación igual al límite superior del intervalo de extracción se incluirán en el intervalo. De forma predeterminada, se incluye el límite superior.  
  
 El conjunto de resultados devuelto por la **net cambios** contenedor función devuelve solo las columnas que se encontraban en sometidas a seguimiento la @column_list cuando se generó el contenedor. Si @column_list es NULL, se devuelven todas las columnas de origen sometidas a seguimiento. Las columnas de origen van seguidas de una columna de operación, __CDC_OPERATION, que es una columna de uno o dos caracteres que identifica la operación.  
  
 Marcas de bits, a continuación, se anexan al conjunto de resultados para cada columna que se identifica en el parámetro @update_flag_list. Para el **net cambios** contenedor, el bit de marcas tendrán siempre es NULL si el @row_filter_option decir se utiliza en la llamada a la función contenedora es 'all' o 'all with merge'. Si el @row_filter_option se establece en 'all with mask' y __CDC_OPERATION es tenía ' o 'I', el valor de la marca también será NULL. Si \__CDC_OPERATION 'UN es ', la marca se establecerá en 1 ó 0, dependiendo de si la **net** provocada un cambio en la columna de la operación de actualización.  
  
 En la plantilla de configuración de captura de datos modificados 'Instantiate CDC Wrapper TVFs for Schema' se muestra cómo utilizar el procedimiento almacenado sp_cdc_generate_wrapper_function para obtener scripts CREATE para todas las funciones contenedoras de las funciones de consulta definidas para un esquema. A continuación, la plantilla crea esos scripts. Para obtener más información acerca de las plantillas, consulte [Explorador de plantillas](http://msdn.microsoft.com/library/b9ee55c5-bb44-4f76-90ac-792d8d83b4c8).  
  
## <a name="see-also"></a>Vea también  
 [Sys.sp_cdc_generate_wrapper_function &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)   
 [CDC.fn_cdc_get_net_changes_ &#60; capture_instance &#62; &#40; Transact-SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)  
  
  
