---
title: Crear la función para recuperar los datos modificados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],creating function
ms.assetid: 55dd0946-bd67-4490-9971-12dfb5b9de94
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 28878f96b843a8a557e95d6c4ddf10681f481b8c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62771441"
---
# <a name="create-the-function-to-retrieve-the-change-data"></a>Crear la función para recuperar los datos modificados
  Después de completar el flujo de control para un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que realiza una carga incremental de datos modificados, la tarea siguiente es crear una función con valores de tabla que recupere los datos modificados. Solo tiene que crear esta función una vez antes de la primera carga incremental.  
  
> [!NOTE]  
>  La creación de una función para recuperar los datos modificados es el segundo paso en el proceso de crear un paquete que realiza una carga incremental de datos modificados. Vea una descripción del proceso general para crear este paquete en [Captura de datos modificados &#40;SSIS&#41;](change-data-capture-ssis.md).  
  
## <a name="design-considerations-for-change-data-capture-functions"></a>Consideraciones de diseño para las funciones de captura de datos modificados  
 Para recuperar los datos modificados, un componente de origen en el flujo de datos del paquete llama a una de las siguientes funciones de consulta de captura de datos modificados:  
  
-   **cdc.fn_cdc_get_net_changes_<capture_instance>** Para esta consulta, la única fila devuelta para cada actualización contiene el estado final de cada fila modificada. En la mayoría de los casos, solo necesitará los datos devueltos por una consulta para los cambios netos. Para obtener más información, vea [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql).  
  
-   **cdc.fn_cdc_get_all_changes_<capture_instance>** Esta consulta devuelve todos los cambios que se han producido en cada fila durante el intervalo de captura. Para obtener más información, vea [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql).  
  
 A continuación, el componente de origen toma los resultados devueltos por la función y los pasa a las transformaciones y destinos de nivel inferior, que aplican los datos modificados al destino final.  
  
 Pero un componente de origen de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no puede llamar directamente a estas funciones de captura de datos modificados. Un componente de origen de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] requiere metadatos sobre las columnas devueltas por la consulta. Los funciones de captura de datos modificados no definen las columnas de su tabla de resultados. Así, estas funciones no devuelven metadatos suficientes para un componente de origen de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Use una función de contenedor con valores de tabla, ya que este tipo de función define explícitamente las columnas de la tabla de resultados en su cláusula RETURNS. Esta definición explícita de las columnas proporciona los metadatos que necesita un componente de origen de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Debe crear esta función para cada tabla cuyos datos modificados desee recuperar.  
  
 Tiene dos opciones para crear la función de contenedor con valores de tabla que llama a la función de consulta de captura de datos modificados:  
  
-   Puede llamar al procedimiento almacenado del sistema, **sys.sp_cdc_generate_wrapper_function** , que crea automáticamente funciones con valores de tabla.  
  
-   Puede escribir su propia función con valores de tabla siguiendo las instrucciones y el ejemplo incluidos en este tema.  
  
## <a name="calling-a-stored-procedure-to-create-the-table-valued-function"></a>Llamar a un procedimiento almacenado para crear la función con valores de tabla  
 La forma más rápida y sencilla de crear las funciones con valores de tabla que necesita es llamar al procedimiento almacenado del sistema, **sys.sp_cdc_generate_wrapper_function** . Este procedimiento almacenado genera scripts para crear funciones de contenedor diseñadas específicamente para adaptarse a las necesidades de un componente de origen de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  El procedimiento almacenado del sistema **sys.sp_cdc_generate_wrapper_function** no crea directamente las funciones de contenedor. Lo que hace es generar los scripts CREATE para las funciones de contenedor. El desarrollador debe ejecutar los scripts CREATE generados por el procedimiento almacenado antes de que un paquete de carga incremental llame a las funciones de contenedor.  
  
 Para poder entender cómo se usa este procedimiento almacenado del sistema, debe comprender lo que hace, qué scripts genera y qué funciones de contenedor crean los scripts.  
  
### <a name="understanding-and-using-the-stored-procedure"></a>Entender y usar el procedimiento almacenado  
 El procedimiento almacenado del sistema **sys.sp_cdc_generate_wrapper_function** genera los scripts necesarios para crear las funciones de contenedor que usarán los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Estas son las primeras líneas de la definición del procedimiento almacenado:  
  
 `CREATE PROCEDURE sys.sp_cdc_generate_wrapper_function`  
  
 `(`  
  
 `@capture_instance sysname = null`  
  
 `@closed_high_end_point bit = 1,`  
  
 `@column_list = null,`  
  
 `@update_flag_list = null`  
  
 `)`  
  
 Todos los parámetros del procedimiento almacenado son opcionales. Si llama al procedimiento almacenado sin haber proporcionado valores para alguno de los parámetros, dicho procedimiento creará funciones de contenedor para todas las instancias de captura a las que usted tenga acceso.  
  
> [!NOTE]  
>  Para más información sobre la sintaxis de este procedimiento almacenado y sus parámetros, vea [sys.sp_cdc_generate_wrapper_function &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql).  
  
 El procedimiento almacenado siempre genera una función de contenedor para devolver todos los cambios de cada instancia de captura. Si el *@supports_net_changes* parámetro se estableció cuando se creó la instancia de captura, el procedimiento almacenado también genera una función de contenedor para devolver los cambios netos de cada instancia de captura aplicable.  
  
 El procedimiento almacenado devuelve un conjunto de resultados con dos columnas:  
  
-   El nombre de la función de contenedor generada por el procedimiento almacenado. Este procedimiento almacenado obtiene el nombre de la función a partir del nombre de la instancia de captura. (El nombre de la función es 'fn_all_changes_' seguido por el nombre de la instancia de captura. El prefijo usado para la función de cambios netos, si se crea, es 'fn_net_changes_'.)  
  
-   La instrucción CREATE para la función de contenedor.  
  
### <a name="understanding-and-using-the-scripts-created-by-the-stored-procedure"></a>Entender y usar los scripts creados por el procedimiento almacenado  
 Normalmente, un desarrollador usa una instrucción INSERT...EXEC para llamar al procedimiento almacenado **sys.sp_cdc_generate_wrapper_function** y guarda los scripts creados por ese procedimiento en una tabla temporal. Una vez hecho esto, se podrá seleccionar y ejecutar cada script de manera individual para crear la función de contenedor correspondiente. Sin embargo, un desarrollador también puede usar un conjunto de comandos SQL para ejecutar todos los scripts CREATE, tal y como se muestra en el código de ejemplo siguiente:  
  
```  
create table #wrapper_functions  
      (function_name sysname, create_stmt nvarchar(max))  
insert into #wrapper_functions  
exec sys.sp_cdc_generate_wrapper_function  
  
declare @stmt nvarchar(max)  
declare #hfunctions cursor local fast_forward for   
      select create_stmt from #wrapper_functions  
open #hfunctions  
fetch #hfunctions into @stmt  
while (@@fetch_status <> -1)  
begin  
      exec sp_executesql @stmt  
      fetch #hfunctions into @stmt  
end  
close #hfunctions  
deallocate #hfunctions  
```  
  
### <a name="understanding-and-using-the-functions-created-by-the-stored-procedure"></a>Entender y usar las funciones creadas por el procedimiento almacenado  
 Para recorrer de forma sistemática la escala de tiempo de los datos modificados capturados, las *@end_time* funciones de contenedor generadas esperan que *@start_time* el parámetro de un intervalo sea el parámetro para el intervalo subsiguiente. Cuando se sigue esta convención, las funciones de contenedor generadas pueden realizar las tareas siguientes:  
  
-   Asignar los valores de fecha y hora a los valores LSN que se usan internamente.  
  
-   Asegurarse de que no se pierde ni se repite ningún dato.  
  
 Para simplificar las consultas de todas las filas de una tabla de cambios, las funciones de contenedor generadas también admiten las convenciones siguientes:  
  
-   Si el parámetro @start_time es NULL, las funciones de contenedor usan el valor LSN más bajo de la instancia de captura como el límite inferior de la consulta.  
  
-   Si el parámetro @end_time es NULL, las funciones de contenedor usan el valor LSN más alto de la instancia de captura como el límite superior de la consulta.  
  
 La mayoría de los usuarios podrán usar las funciones de contenedor creadas por el procedimiento almacenado del sistema, **sys.sp_cdc_generate_wrapper_function** , sin realizar ninguna modificación. Sin embargo, para personalizar las funciones de contenedor, es necesario personalizar los scripts CREATE antes de ejecutarlos.  
  
 Cuando el paquete llame a las funciones de contenedor, el paquete debe proporcionar valores para tres parámetros. Estos tres parámetros son como los tres parámetros que usan las funciones de captura de datos modificados. Los tres parámetros son los siguientes:  
  
-   Valor de fecha y hora de inicio, y valor de fecha y hora de finalización del intervalo. Aunque las funciones de contenedor usan valores de fecha y hora como los puntos inicial y final del intervalo de consulta, las funciones de captura de datos modificados usan dos valores LSN como dichos puntos.  
  
-   El filtro de filas. Para las funciones de contenedor y las funciones de captura de datos modificados, el *@row_filter_option* parámetro es el mismo. Para más información, vea [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql) y [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql).  
  
 El conjunto de resultados devuelto por las funciones de contenedor incluye los datos siguientes:  
  
-   Todas las columnas de datos modificados solicitadas.  
  
-   Una columna denominada __CDC_OPERATION que usa un campo de uno o dos caracteres para identificar la operación que está asociada a la fila. Los valores válidos para este campo son los siguientes: "I" para insertar, "D" para eliminar, "UO" para actualizar valores antiguos y "UN" para actualizar valores nuevos.  
  
-   Marcas de actualización, cuando se solicitan, que aparecen como columnas de bits después del código de operación y en el orden especificado en *@update_flag_list* el parámetro. El nombre de estas columnas se obtiene anexando “_uflag” al nombre de columna asociado.  
  
 Si el paquete llama a una función de contenedor que consulta todos los cambios, dicha función también devolverá las columnas __CDC_STARTLSN y \__CDC_SEQVAL. Estas dos columnas se convierten en la primera y en la segunda columna, respectivamente, del conjunto de resultados. La función de contenedor también ordena el conjunto de resultados basándose en estas dos columnas.  
  
## <a name="writing-your-own-table-value-function"></a>Escribir su propia función con valores de tabla  
 También puede usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para escribir su propia función de contenedor con valores de tabla que llame a la función de consulta de captura de datos modificados y almacenar la función de contenedor con valores de tabla en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para más información sobre cómo crear una función Transact-SQL, vea [CREATE FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-function-transact-sql).  
  
 En el ejemplo siguiente se define una función con valores de tabla que recupera los cambios de una tabla Customer para el intervalo de cambios especificado. Esta función utiliza las funciones de captura de datos modificados para asignar los valores `datetime` a los valores de número de flujo de registro binario (LSN) que las tablas de cambios utilizan internamente. Esta función también controla varias condiciones especiales:  
  
-   Cuando se pasa un valor nulo para la fecha y hora de inicio, esta función utiliza el primer valor disponible.  
  
-   Cuando se pasa un valor nulo para la fecha y hora de finalización, esta función utiliza el último valor disponible.  
  
-   Cuando el LSN inicial es igual que el LSN final, lo que suele implicar que no hay ningún registro para el intervalo seleccionado, esta función finaliza.  
  
### <a name="example-of-a-table-value-function-that-queries-for-change-data"></a>Ejemplo de una función con valores de tabla que consulta los datos modificados  
  
```  
CREATE function CDCSample.uf_Customer (  
     @start_time datetime  
    ,@end_time datetime  
)  
returns @Customer table (  
     CustomerID int  
    ,TerritoryID int  
    ,CustomerType nchar(1)  
    ,rowguid uniqueidentifier  
    ,ModifiedDate datetime  
    ,CDC_OPERATION varchar(1)  
) as  
begin  
    declare @from_lsn binary(10), @to_lsn binary(10)  
  
    if (@start_time is null)  
        select @from_lsn = sys.fn_cdc_get_min_lsn('Customer')  
    else  
        select @from_lsn = sys.fn_cdc_increment_lsn(sys.fn_cdc_map_time_to_lsn('largest less than or equal',@start_time))  
  
    if (@end_time is null)  
        select @to_lsn = sys.fn_cdc_get_max_lsn()  
    else  
        select @to_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal',@end_time)  
  
    if (@from_lsn = sys.fn_cdc_increment_lsn(@to_lsn))  
        return  
  
    -- Query for change data  
    insert into @Customer  
    select   
        CustomerID,      
        TerritoryID,   
        CustomerType,   
        rowguid,   
        ModifiedDate,   
        case __$operation  
                when 1 then 'D'  
                when 2 then 'I'  
                when 4 then 'U'  
                else null  
         end as CDC_OPERATION  
    from   
        cdc.fn_cdc_get_net_changes_Customer(@from_lsn, @to_lsn, 'all')  
  
    return  
end   
go  
  
```  
  
### <a name="retrieving-additional-metadata-with-the-change-data"></a>Recuperar metadatos adicionales con los datos modificados  
 Aunque la función con valores de tabla creada por el usuario y mostrada anteriormente solo usa la columna **__$operation**, la función **cdc.fn_cdc_get_net_changes_<capture_instance>** devuelve cuatro columnas de metadatos por cada fila de datos modificados. Si desea utilizar estos valores en el flujo de datos, puede devolverlos como columnas adicionales desde la función contenedora con valores de tabla.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**__$start_lsn**|`binary(10)`|Número de secuencia de registro (LSN) asociado con la transacción de confirmación para el cambio.<br /><br /> Todos los cambios confirmados en la misma transacción comparten el mismo LSN de confirmación. Por ejemplo, si una operación de actualización en la tabla de origen modifica dos filas diferentes, la tabla de cambios contendrá cuatro filas (dos con los valores anteriores y dos con los valores nuevos), cada una con el mismo valor **__$start_lsn** .|  
|**_ _ $ seqval**|`binary(10)`|Valor de secuencia que se usa para ordenar los cambios de fila en una transacción.|  
|**_ _ $ Operation**|`int`|Operación del lenguaje de manipulación de datos (DML) asociada al cambio. Puede ser uno de los siguientes:<br /><br /> 1 = eliminar<br /><br /> 2 = insertar<br /><br /> 3 = actualizar (valores antes de la operación de actualización)<br /><br /> 4 = actualizar (valores después de la operación de actualización)|  
|**_ _ $ update_mask**|`varbinary(128)`|Máscara de bits basada en los ordinales de las columnas de la tabla de cambios que identifica las columnas que han cambiado. Puede examinar este valor para determinar las columnas que han cambiado.|  
|**\<columnas de la tabla de origen capturadas>**|Varía|Las columnas restantes devueltas por la función son las columnas de la tabla de origen que se identificaron como columnas capturadas cuando se creó la instancia de captura. Si no se especificó inicialmente ninguna columna en la lista de columnas capturadas, se devuelven todas las columnas de la tabla de origen.|  
  
 Para obtener más información, vea [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql).  
  
## <a name="next-step"></a>siguiente paso  
 Una vez que haya creado la función con valores de tabla que consulta los datos modificados, el paso siguiente consiste en comenzar a diseñar el flujo de datos del paquete.  
  
 **Siguiente tema:** [recuperar y comprender los datos modificados](retrieve-and-understand-the-change-data.md)  
  
  
