---
title: Trabajar con datos modificados (SQL Server) | Microsoft Docs
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- change data [SQL Server]
- change data capture [SQL Server], query function scenarios
- change data capture [SQL Server], LSN boundaries
- change data capture [SQL Server], query functions
ms.assetid: 5346b852-1af8-4080-b278-12efb9b735eb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 62c705432367b8d2ad7b5de7de30c840be368aac
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52405240"
---
# <a name="work-with-change-data-sql-server"></a>Trabajar con datos modificados (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Los datos modificados están a disposición de los consumidores de capturas de datos modificados a través de las funciones con valores de tabla (TVF). Todas las consultas de estas funciones requieren dos parámetros para definir el intervalo de números de flujo de registro (LSN) que se pueden elegir al desarrollar el conjunto de resultados devuelto. Se considera que los valores superior e inferior de LSN que limitan el intervalo están incluidos dentro del intervalo.  
  
 Se proporcionan varias funciones que ayudan a determinar los valores de LSN adecuados para utilizarse al consultar una función TVF. La función [sys.fn_cdc_get_min_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md) devuelve el LSN más pequeño asociado a un intervalo de validez de la instancia de captura. El intervalo de validez es el intervalo de tiempo durante el cual los datos modificados están actualmente disponibles en sus instancias de captura. La función [sys.fn_cdc_get_max_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md) devuelve el LSN más grande del intervalo de validez. Las funciones [sys.fn_cdc_map_time_to_lsn](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) y [sys.fn_cdc_map_lsn_to_time](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md) están disponibles para ayudar a ubicar los valores LSN en una escala de tiempo convencional. Dado que la captura de datos modificados utiliza intervalos de consulta cerrados, a veces es necesario generar el valor de LSN siguiente en un flujo para garantizar que los cambios no estén duplicados en ventanas de consulta consecutivas. Las funciones [sys.fn_cdc_increment_lsn](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md) y [sys.fn_cdc_decrement_lsn](../../relational-databases/system-functions/sys-fn-cdc-decrement-lsn-transact-sql.md) son útiles cuando es necesario realizar un ajuste incremental en un valor LSN.  
  
##  <a name="LSN"></a> Validar los límites de LSN  
 Se recomienda validar los límites de LSN que se van a utilizar en una consulta de TVF antes de su uso. Los extremos nulos o los que quedan fuera del intervalo de validez para una instancia de captura obligarán a la función TVF de captura de datos modificados a devolver un error.  
  
 Por ejemplo, el error siguiente se devuelve en una consulta de todos los cambios cuando un parámetro que se utiliza para definir el intervalo de la consulta no es válido o está fuera del intervalo, o bien cuando la opción de filtro de filas no es válida.  
  
 `Msg 313, Level 16, State 3, Line 1`  
  
 `An insufficient number of arguments were supplied for the procedure or function cdc.fn_cdc_get_all_changes_ ...`  
  
 El error correspondiente devuelto para una consulta **net changes** es el siguiente:  
  
 `Msg 313, Level 16, State 3, Line 1`  
  
 `An insufficient number of arguments were supplied for the procedure or function cdc.fn_cdc_get_net_changes_ ...`  
  
> [!NOTE]  
>  Es obvio que el mensaje 313 es confuso y no comunica la causa real del error. Este uso inadecuado proviene de la incapacidad de generar un error explícito desde dentro de una función TVF. No obstante, se consideró que era preferible devolver un error reconocible, aunque inexacto, a devolver simplemente un resultado vacío. Un conjunto de resultados vacío no sería discernible de una consulta válida que no devolviese ningún cambio.  
  
 Los errores de autorización devolverán errores al consultar todos los cambios, como se muestra a continuación:  
  
 `Msg 229, Level 14, State 5, Line 1`  
  
 `The SELECT permission was denied on the object 'fn_cdc_get_all_changes_...', database 'MyDB', schema 'cdc'.`  
  
 Se da la misma circunstancia al consultar los cambios de red:  
  
 `Msg 229, Level 14, State 5, Line 1`  
  
 `The SELECT permission was denied on the object fn_cdc_get_net_changes_...', database 'MyDB', schema 'cdc'.`  
  
 Vea la plantilla para enumerar cambios netos con TRY CATCH, que contiene una demostración acerca de cómo se pueden interceptar estos errores de TVF conocidos y se puede devolver información más significativa sobre el error.  
  
> [!NOTE]  
>  Para buscar las plantillas de captura de datos modificados en SQL Server Management Studio, en el menú **Ver** , haga clic en **Explorador de plantillas**, expanda **Plantillas de SQL Server** y, luego, la carpeta **Captura de datos modificados** .  
  
##  <a name="Functions"></a> Funciones de consulta  
 Según sean las características de la tabla de origen que se someta a seguimiento y la manera en que se configure su instancia de captura, se generarán una o las dos funciones TVF para la consulta de datos modificados.  
  
-   La función [cdc.fn_cdc_get_all_changes_<instancia_captura>](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) devuelve todos los cambios producidos durante el intervalo especificado. Siempre se genera esta función. Las entradas siempre se devuelven ordenadas, primero por el SLN de confirmación de la transacción del cambio y, a continuación, por un valor que secuencia el cambio dentro de su transacción. Según sea la opción de filtro de filas elegida, se devuelve la fila final de la actualización (opción de filtro de filas "all") o los valores nuevo y antiguo de la actualización (opción de filtro de filas "all update old").  
  
-   La función [cdc.fn_cdc_get_net_changes_<capture_instance>](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md) se genera si el parámetro @supports_net_changes se establece en 1 cuando la tabla de origen está habilitada.  
  
    > [!NOTE]  
    >  Solo se admite esta opción si la tabla de origen tiene definida una clave principal o si el parámetro @index_name se ha usado para identificar un índice único.  
  
     La función **netchanges** devuelve un cambio por cada fila de la tabla de origen modificada. Si se registra más de un cambio para la fila durante el intervalo especificado, los valores de la columna reflejarán el contenido final de la fila. Para identificar correctamente la operación necesaria para actualizar el entorno de destino, la función TVF debe considerar tanto la operación inicial en la fila durante el intervalo como la operación final en la fila. Cuando se especifica la opción de filtro de filas “all”, las operaciones que devuelva una consulta **net changes** podrán ser inserciones, eliminaciones o actualizaciones (valores nuevos). Esta opción siempre devuelve el valor NULL para la máscara de actualización porque hay un costo asociado al cálculo de una máscara agregada. Si necesita una máscara agregada que refleje todos los cambios efectuados en una fila, use la opción 'all with mask'. Si el procesamiento posterior no precisa distinguir entre inserciones y actualizaciones, use la opción 'all with merge'. En este caso, el valor de la operación aceptará solo dos valores: 1 para la eliminación y 5 para una operación que podría ser una inserción o una actualización. Esta opción elimina el procesamiento adicional necesario para determinar si la operación derivada debía ser una inserción o una actualización, y puede mejorar el rendimiento de la consulta cuando no sea necesaria esta diferenciación.  
  
 La máscara de la actualización devuelta por una función de consulta es una representación compacta que identifica todas las columnas que han cambiado en una fila de datos modificados. Normalmente, esta información solo es necesaria para un pequeño subconjunto de las columnas capturadas. Hay funciones que se pueden usar para ayudar a extraer información de la máscara de una forma que sea más fácilmente utilizable por las aplicaciones. La función [sys.fn_cdc_get_column_ordinal](../../relational-databases/system-functions/sys-fn-cdc-get-column-ordinal-transact-sql.md) devuelve la posición ordinal de una columna con nombre de una determinada instancia de captura, mientras que la función [sys.fn_cdc_is_bit_set](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md) devuelve la paridad del bit de la máscara proporcionada en función del ordinal que se pasó en la llamada a la función. La combinación de estas dos funciones permite extraer eficazmente información de la máscara de actualización y devolverla con la solicitud de datos modificados. Vea la plantilla para enumerar cambios netos con 'All With Mask', que contiene una demostración acerca de cómo se utilizan estas funciones.  
  
##  <a name="Scenarios"></a> Escenarios de funciones de consulta  
 En las secciones siguientes se describen los escenarios comunes de consulta de los datos modificados de las capturas mediante las funciones de consulta cdc.fn_cdc_get_all_changes_<capture_instance> y cdc.fn_cdc_get_net_changes_<capture_instance>.  
  
### <a name="querying-for-all-changes-within-the-capture-instance-validity-interval"></a>Consultar todos los cambios del intervalo de validez de la instancia de captura  
 La solicitud más sencilla de los datos modificados es la que devuelve todo los datos modificados actuales comprendidos en un intervalo de validez de una instancia de captura. Para realizar esta solicitud, primero debe determinarse el límite inferior y el límite superior de LSN del intervalo de validez. Después, use estos valores para identificar los parámetros @from_lsn y @to_lsn pasados a la función de consulta cdc.fn_cdc_get_all_changes_<capture_instance> o cdc.fn_cdc_get_net_changes_<capture_instance>. Use la función [sys.fn_cdc_get_min_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md) para obtener el límite inferior y la función [sys.fn_cdc_get_max_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md) para obtener el límite superior. Vea la plantilla para enumerar todos los cambios del rango válido, que contiene un ejemplo de código sobre una consulta de todos los cambios válidos actuales con la función de consulta cdc.fn_cdc_get_all_changes_<capture_instance>. Vea la plantilla para enumerar cambios netos del rango válido, que contiene un ejemplo similar sobre el uso de la función cdc.fn_cdc_get_net_changes_<capture_instance>.  
  
### <a name="querying-for-all-new-changes-since-the-last-set-of-changes"></a>Consultar todos los cambios nuevos desde el último conjunto de cambios  
 En las aplicaciones típicas, la consulta de los datos modificados constituye un proceso continuo en el que se realizan solicitudes periódicas de todos los cambios acaecidos desde la última solicitud. En este tipo de consultas, puede usar la función [sys.fn_cdc_increment_lsn](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md) para derivar el límite inferior de la consulta actual del límite superior de la consulta anterior. Con este método se asegura de que ninguna fila se repite, porque el intervalo de búsqueda se trata siempre como un intervalo cerrado en el que se incluyen los dos extremos. Luego, use la función [sys.fn_cdc_get_max_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md) para obtener el extremo superior del nuevo intervalo de la solicitud. Vea la plantilla para enumerar todos los cambios desde la solicitud anterior, que contiene un ejemplo de código en el que la ventana de consulta se mueve sistemáticamente para obtener todos los cambios desde la última solicitud.  
  
### <a name="querying-for-all-new-changes-up-until-now"></a>Consultar todos los cambios nuevos hasta este momento  
 Una restricción habitual que se aplica a los cambios devueltos por una función de consulta es que solo se incluyen los cambios producidos entre la solicitud anterior y la fecha y hora actual. En esta consulta, aplique la función sys.fn_cdc_increment_lsn al valor @from_lsn que se ha usado en la solicitud anterior para determinar el límite inferior. Dado que el límite superior del intervalo de tiempo se expresa como un punto concreto en el tiempo, debe convertirse en un valor LSN antes de poder utilizarse en una función de consulta. Antes de que el valor de fecha y hora se pueda convertir en el valor LSN correspondiente, debe asegurarse de que el proceso de captura ha procesado todos los cambios que se confirmaron a través del límite superior especificado. Esta operación es necesaria para asegurarse de que todos los cambios certificados se propagaron en la tabla de cambios. Un modo de hacerlo consiste en estructurar un bucle de espera que periódicamente compruebe si el LSN de confirmación registrado en una tabla de cambios de base de datos supera la hora de finalización deseada del intervalo de la solicitud.  
  
 Una vez que el bucle de espera comprueba que el proceso de captura ha procesado todas las entradas de registro correspondientes, use la función [sys.fn_cdc_map_time_to_lsn](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) para determinar el nuevo extremo superior expresado con un valor LSN. Para asegurarse de que todas las entradas confirmadas en la hora especificada se recuperan, llame a la función sys.fn_cdc_map_time_to_lsn y utilice la opción 'largest less than or equal'.  
  
> [!NOTE]  
>  En períodos de inactividad, se agrega una entrada ficticia a la tabla cdc.lsn_time_mapping para marcar el hecho de que el proceso de captura ha procesado los cambios hasta una hora de confirmación establecida. De este modo, impide que parezca que el proceso de captura se ha retrasado cuando lo que ocurre es que simplemente no hay cambios que procesar.  
  
 En la plantilla para enumerar todos los cambios hasta este momento se muestra cómo se utiliza la estrategia anterior para consultar los datos modificados.  
  
### <a name="adding-a-commit-time-to-an-all-changes-result-set"></a>Agregar una hora de confirmación a todos los cambios de un conjunto de resultados  
 La hora de confirmación de cada transacción con una entrada asociada en una tabla de cambios de base de datos está disponible en la tabla [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md). Al unir el valor __$start_lsn devuelto en una solicitud de todos los cambios con el valor start_lsn de una entrada de la tabla cdc.lsn_time_mapping, puede devolver tran_end_time junto con los datos modificados para marcar el cambio con la hora de confirmación de la transacción en el origen. En la plantilla para anexar una hora de confirmación a todos los cambios del conjunto de resultados se muestra cómo se realiza esta unión.  
  
### <a name="joining-change-data-with-other-data-from-the-same-transaction"></a>Unir los datos modificados con otros datos de la misma transacción  
 En ocasiones, resulta útil unir los datos modificados con otra información recopilada sobre la transacción cuando se confirma en el origen. En la columna tran_begin_lsn de la tabla cdc.lsn_time_mapping se proporciona la información necesaria para realizar este tipo de unión. Cuando se produce la actualización del origen, el valor de database_transaction_begin_lsn procedente de la vista dinámica del sistema [sys.dm_tran_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md) debe guardarse junto con cualquier otra información que se vaya a unir a los datos modificados. Utilice la función fn_convertnumericlsntobinary para comparar los valores database_transaction_begin_lsn y tran_begin_lsn. El código para generar esta función está disponible en la plantilla para la creación de la función fn_convertnumericlsntobinary. En la plantilla para devolver todos los cambios con un determinado valor tran_begin_lsn se muestra cómo se efectúa la unión.  
  
### <a name="querying-using-datetime-wrapper-functions"></a>Realizar consultas con funciones contenedoras de fecha y hora  
 Un escenario de aplicación común para consultar los datos modificados consiste en solicitar periódicamente los datos modificados a través de una ventana deslizante enlazada a valores de fecha y hora. En esta clase de consumidores, la captura de datos modificados proporciona el procedimiento almacenado [sys.sp_cdc_generate_wrapper_function](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md) que genera scripts para crear funciones contenedoras personalizadas para las funciones de consulta de captura de datos modificados. Estos contenedores personalizados permiten que el intervalo de la consulta se exprese como un par de fecha y hora.  
  
 Al llamar a las opciones del procedimiento almacenado, pueden generarse los contenedores de todas las instancias de captura a las que el autor de la llamada tiene acceso o solo de una instancia de captura determinada. Entre las opciones admitidas también se incluye la capacidad de especificar si el extremo superior del intervalo de captura debe estar abierto o cerrado, cuáles de las columnas capturadas disponibles deben incluirse en el conjunto de resultados y cuáles de las columnas incluidas deben asociarse a marcas de actualización. El procedimiento devuelve un conjunto de resultados con dos columnas: el nombre de la función generada, que se deriva del nombre de la instancia de captura, y la instrucción CREATE del procedimiento almacenado del contenedor. La función que va a contener la consulta de todos los cambios siempre se genera. Si el parámetro @supports_net_changes se ha definido al crear la instancia de captura, también se genera la función que va a contener los cambios netos.  
  
 Es responsabilidad del diseñador de la aplicación llamar al procedimiento almacenado de generación de scripts para generar las instrucciones CREATE de los procedimientos almacenados del contenedor y ejecutar los scripts CREATE resultantes para generar las funciones. Esto no se produce automáticamente cuando se crea una instancia de captura.  
  
 El usuario es el propietario de los contenedores de fecha y hora, que no se crean en el esquema predeterminado del autor de la llamada. La función generada resulta conveniente sin modificaciones para la mayoría de los usuarios. No obstante, siempre puede aplicarse alguna personalización más extensa al script generado antes de crear la función.  
  
 El nombre de la función que va a contener la consulta de todos los cambios es fn_all_changes_ seguido del nombre de la instancia de captura. El prefijo que se utiliza para el contenedor de los cambios netos es fn_net_changes_. Las dos funciones toman tres argumentos, al igual que sus TVF de captura de cambios modificados. Sin embargo, el intervalo de la consulta de los contenedores está limitado por dos valores de fecha y hora y no por dos valores LSN. El parámetro @row_filter_option es el mismo para los dos conjuntos de funciones.  
  
 Las funciones contenedoras generadas admiten la siguiente convención para recorrer de forma sistemática la escala de tiempo de captura de datos modificados: se espera que el parámetro @end_time del intervalo anterior se use como parámetro @start_time del intervalo siguiente. La función contenedora se encarga de asignar los valores de fecha y hora a los valores LSN y se asegura de que no se pierde ni se repite ningún dato si se sigue esta convención.  
  
 Los contenedores se pueden generar para admitir un límite superior cerrado o un límite superior abierto en la ventana de consulta especificada. Es decir, al autor de la llamada puede especificar si las entradas que tienen un tiempo de confirmación igual al límite superior del intervalo de extracción se van a incluir en el intervalo. De forma predeterminada, se incluye el límite superior.  
  
 Aunque se produzca un error en las TVF de consulta generadas si se proporciona un valor NULL para los valores @from_lsn o @to_lsn, las funciones contenedores de fecha y hora usan el valor NULL para permitir que los contenedores de fecha y hora devuelvan todos los cambios actuales. Es decir, si se pasa un valor NULL como extremo inferior de la ventana de consulta para el contenedor de fecha y hora, el extremo inferior del intervalo de validez de la instancia de captura se utiliza en la instrucción SELECT subyacente que se aplica a la TVF de consulta. Del mismo modo, si se pasa un valor NULL como extremo superior de la ventana de consulta, el extremo superior del intervalo de validez de la instancia de captura se utiliza al realizar la selección en la TVF de consulta.  
  
 El conjunto de resultados devuelto por una función contenedora incluye todas las columnas solicitadas seguidas por una columna de operación, que se codifica de nuevo como uno o dos caracteres para identificar la operación que está asociada a la fila. Si las marcas de actualización se han solicitado, aparecen como columnas de bits después del código de operación en el orden especificado en el parámetro @update_flag_list. Para obtener información sobre la llamada de opciones para personalizar los contenedores de fecha y hora generados, vea [sys.sp_cdc_generate_wrapper_function &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md).  
  
 En la plantilla para la creación de instancias de una TVF contenedora con una marca de actualización, se muestra cómo se personaliza una función contenedora para anexar una marca de actualización de una determinada columna al conjunto de resultados devuelto por una consulta de cambios netos. En la plantilla para la creación de instancias de TVF contenedoras de CDC para un esquema, se muestra cómo se crean instancias de los contenedores de fecha y hora para las TVF de consulta de todas las instancias de captura creadas para las tablas de origen en un esquema de la base de datos específico.  
  
 Para obtener un ejemplo en el que se utiliza un contenedor de fecha y hora para consultar los datos modificados, vea la plantilla para la obtención de cambios netos utilizando un contenedor con marcas de actualización. En esta plantilla se muestra cómo se consultan los cambios netos con una función contenedora cuando el contenedor está configurado para devolver marcas de actualización. Tenga en cuenta que la opción de filtro de filas 'all with mask' es necesaria para que la función de consulta subyacente devuelva una máscara de actualización que no sea NULL. Los valores NULL se pasan para los límites inferior y superior del intervalo de fecha y hora con el fin de señalar la función que va a utilizar los extremos inferior y superior del intervalo de validez de la instancia de captura cuando realice la consulta basada en LSN subyacente. La consulta devuelve una fila por cada modificación de una fila de origen que se produjo en el intervalo válido de la instancia de captura.  
  
### <a name="using-the-datetime-wrapper-functions-to-transition-between-capture-instances"></a>Utilizar las funciones contenedoras de fecha y hora en transiciones entre instancias de captura  
 La captura de datos modificados admite un máximo de dos instancias de captura para una única tabla de origen sometida a seguimiento. El uso principal de esta capacidad consiste en alojar una transición entre varias instancias de captura cuando los cambios del lenguaje de definición de datos (DDL) efectuados en la tabla de origen amplían el conjunto de columnas disponibles para llevar a cabo el seguimiento. Cuando la transición se realiza a una nueva instancia de captura, un modo de proteger los niveles superiores de la aplicación para que no se produzcan cambios en los nombres de las funciones de consulta subyacentes consiste en utilizar una función contenedora que incluya la llamada subyacente. A continuación, asegúrese de que el nombre de la función contenedora sigue siendo el mismo. Cuando vaya a producirse el cambio, la función contenedora antigua se puede quitar, pues se crea una nueva con el mismo nombre que hace referencia a las nuevas funciones de consulta. Al modificar primero el script generado para crear una función contenedora con el mismo nombre, puede hacer el cambio a la nueva instancia de captura sin que esto afecte a los niveles superiores de la aplicación.  
  
## <a name="see-also"></a>Ver también  
 [Seguimiento de cambios de datos &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [Acerca de la captura de datos modificados &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [Habilitar y deshabilitar la captura de datos modificados &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server.md)   
 [Administrar y supervisar la captura de datos modificados &#40;SQL Server&#41;](../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  
