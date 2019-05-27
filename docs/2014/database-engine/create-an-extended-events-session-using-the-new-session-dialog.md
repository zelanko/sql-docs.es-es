---
title: Crear una sesión de eventos extendidos mediante el cuadro de diálogo nueva sesión | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.SSMS.XEDISPLAY.GROUPING.F1
- SQL12.SSMS.XEDISPLAY.AGGREGATION.F1
- SQL12.SSMS.XEDISPLAY.NEWMERGEDCOLUMN.F1
- SQL12.SSMS.XENEWEVENTSESSION.GENERAL.F1
- SQL12.SSMS.XEDISPLAY.EDITCOLUMNS.F1
- SQL12.SSMS.XEDISPLAY.FILTERS.F1
helpviewer_keywords:
- Extended Events Dialog Box
ms.assetid: 6b2244bc-df6a-4b0a-990e-ddd8d42f7907
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 39dd8c4f333df1528f3894ffc6dfe01a48a91f2c
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66065015"
---
# <a name="create-an-extended-events-session-using-the-new-session-dialog"></a>Crear una sesión de eventos extendidos utilizando el cuadro de diálogo Nueva sesión
  El cuadro de diálogo Nueva sesión permite definir una sesión de Extended Events que capture, presente y analice los datos. El cuadro de diálogo Nueva sesión expone toda la funcionalidad de Extended Events.  
  
 El [Asistente para nueva sesión](../ssms/object/object-explorer.md) también permite definir una sesión de Extended Events que admita la mayor parte de la funcionalidad de Extended Events.  
  
## <a name="before-you-begin"></a>Antes de empezar  
 Para abrir el cuadro de diálogo Nueva sesión, en el Explorador de objetos, expanda el nodo **Administración** y, a continuación, expanda **Extended Events**. Haga clic con el botón secundario en **Sesiones**y, a continuación, haga clic en **Nueva sesión**.  
  
##  <a name="BeforeYouBegin"></a> Permisos  
 Para crear una sesión de eventos extendidos, debe disponer del permiso ALTER ANY EVENT SESSION.  
  
## <a name="to-create-an-extended-events-session-using-the-new-session-dialog"></a>Para crear una sesión de Extended Events utilizando el cuadro de diálogo Nueva sesión  
 Utilice la página **General** para seleccionar una plantilla y programar una sesión de eventos.  
  
#### <a name="to-select-a-template-and-schedule-an-event-session"></a>Para seleccionar una plantilla y programar una sesión de eventos  
  
1.  En el Explorador de objetos, expanda el nodo **Administración** y, a continuación, expanda **Eventos extendidos**. Haga clic con el botón derecho en **Sesiones**y, luego, haga clic en **Nueva sesión**.  
  
2.  En la página **General** , en el cuadro **Nombre de sesión** , escriba un nombre descriptivo para la sesión de eventos.  
  
3.  En el cuadro **Plantilla** , seleccione la plantilla que quiere usar en la lista desplegable.  
  
     Puede seleccionar entre un conjunto de plantillas preconfiguradas diseñadas para solucionar problemas comunes o puede seleccionar **De archivo** para usar un archivo de plantilla exportado de una definición de sesión anterior. Observe que también puede cambiar la configuración de la sesión después de aplicar la plantilla.  
  
4.  En la sección **Programación** , si desea que la sesión se inicie al iniciarse el servidor, active la casilla **Iniciar la sesión de eventos al iniciar el servidor** .  
  
     Si desea que la sesión se inicie después de crearse la sesión, active la casilla **Iniciar la sesión de eventos inmediatamente después de crear la sesión** .  
  
5.  Para ver los datos en directo de la sesión de eventos, haga clic en **Observar datos en directo en la pantalla mientras se capturan**. Los datos en directo iniciarán la presentación del seguimiento inmediatamente después de crearse la sesión.  
  
6.  En la sección de **Seguimiento de causalidad** , active la casilla **Realizar un seguimiento de cómo se relacionan los eventos entre sí** para realizar el seguimiento del trabajo en varias tareas.  
  
     Para obtener más información acerca del seguimiento de causalidad, vea "Contenido y características de la sesión" en el [SQL Server Extended Events Sessions](../relational-databases/extended-events/sql-server-extended-events-sessions.md) tema.  
  
     Para agregar eventos a la sesión, en la sección **Seleccionar una página** , haga clic en **Eventos**.  
  
    > [!NOTE]  
    >  No haga clic en **Aceptar** hasta haber terminado de crear la sesión de eventos.  
  
 Utilice la página **Eventos** para buscar y agregar los eventos que desee capturar para la sesión.  
  
#### <a name="to-add-events-to-a-session"></a>Para agregar eventos a una sesión  
  
1.  En el cuadro de diálogo Nueva sesión, en la sección **Seleccionar una página** , seleccione **Eventos**.  
  
2.  En la página **Eventos** , haga clic en **Seleccionar** (el botón **Seleccionar** aparece atenuado si se encuentra en la página **Seleccione los eventos que desee capturar** ).  
  
     Puede buscar cualquier palabra en la tabla especificando el texto que desea buscar en el cuadro **Biblioteca de eventos** . Por ejemplo, si quiere buscar el evento **lock_acquired** , puede especificar **lock** o **lock acquire**.  
  
3.  En la sección **Biblioteca de eventos** , seleccione cómo quiere buscar los eventos que quiere capturar en la lista desplegable. Por ejemplo, puede buscar nombres de evento o nombres de evento con sus descripciones. Escriba los criterios de búsqueda en el cuadro **Buscar** .  
  
    > [!NOTE]  
    >  Los eventos del canal **Depurar** permanecen ocultos de forma predeterminada. Para mostrar eventos de depuración, seleccione **Depurar** en la lista desplegable **Canal** .  
  
     Los detalles de los eventos seleccionados aparecen en el panel Detalles debajo de **Biblioteca de eventos**.  
  
     Los eventos se ordenan por nombre en orden alfabético. Puede ordenar por otros detalles de eventos haciendo clic en el encabezado de columna correspondiente. Por ejemplo, puede ordenar por la columna **Categoría** o **Canal** .  
  
4.  Seleccione los eventos que quiere capturar y, luego, haga clic en la flecha derecha para moverlos a la sección **Eventos seleccionados** .  
  
    > [!NOTE]  
    >  Puede seleccionar varios eventos al mismo tiempo de la **Biblioteca de eventos** utilizando las teclas CTRL o MAYÚS.  
  
     Para configurar los eventos seleccionados, haga clic en **Configurar**.  
  
    > [!NOTE]  
    >  No haga clic en **Aceptar** hasta haber terminado de crear la sesión de eventos.  
  
 La página **Almacenamiento de datos** se utiliza para agregar destinos a una sesión de eventos. Los destinos almacenan datos de evento y pueden realizar acciones como guardar eventos en un archivo para verlos posteriormente y agregar datos de evento para la sesión. Para obtener más información acerca de los destinos de eventos extendidos, vea [SQL Server Extended Events Targets](../../2014/database-engine/sql-server-extended-events-targets.md).  
  
 A continuación se enumeran los destinos que pueden utilizarse en una sesión de eventos extendidos:  
  
-   **etw_classic_sync_target**. Se usa para establecer correlaciones entre eventos de SQL Server y datos de evento de la aplicación o del sistema operativo Windows.  
  
-   **event_counter**. Cuenta todos los eventos especificados que se producen después de iniciarse una sesión de eventos extendidos. Se usa para obtener información sobre las características de carga de trabajo sin agregar la sobrecarga que supone una colección de eventos completa.  
  
-   **event_file**. Se usa para escribir en disco la salida de la sesión de eventos de los búferes de memoria completos.  
  
-   **histogram**. Se usa para contar el número de veces que se produce el evento especificado en función de la acción o columna de evento indicada.  
  
-   **pair_matching**. Se usa para determinar cuándo un determinado evento emparejado no se produce en el conjunto correspondiente.  
  
-   **ring_buffer**. Se usa para mantener los datos de evento en memoria con un orden FIFO (primero en entrar, primero en salir) o con un orden FIFO por evento.  
  
#### <a name="to-configure-global-fields-for-a-session"></a>Para configurar campos globales para una sesión  
  
1.  En la página **Eventos** , después de seleccionar el evento o eventos que desea agregar a la sesión de eventos, haga clic en **Configurar**.  
  
     Después de hacer clic en **Configurar**, la sección **Biblioteca de eventos** se contrae y la sección **Eventos seleccionados** se desplaza a la izquierda de la página. La sección **Opciones de configuración de eventos** que se utiliza para configurar los eventos aparece en el lado derecho de la página. Utilice las pestañas de esta página para configurar las acciones de la sesión de eventos.  
  
2.  En la pestaña **Campos globales** , seleccione los campos que desea aplicar a los eventos seleccionados.  
  
     Puede seleccionar varios campos para cada evento.  
  
    > [!NOTE]  
    >  Si dos eventos ya seleccionados tienen acciones configuradas diferentes, los eventos extendidos mostrarán las acciones activadas parcialmente. Para buscar rápidamente las acciones habilitadas, puede ordenar por estado habilitado/deshabilitado haciendo clic en el encabezado de columna sobre las casillas.  
  
3.  En la pestaña  **Filtros** , aplique los filtros (también denominados predicados) para limitar los eventos que quiere capturar.  
  
     Si se aplica un filtro al evento seleccionado, aparece una marca de comprobación en la columna.  
  
    > [!NOTE]  
    >  Puede seleccionar varios eventos a los que desee aplicar un filtro utilizando las teclas CTRL o MAYÚS. Sin embargo, solo los campos de evento comunes aparecerán para la configuración. Si dos eventos seleccionados tienen ya filtros diferentes configurados para ellos, el filtro no aparecerá. Si se configuran de nuevo los filtros, se sobrescribirán los valores de filtro existentes.  
  
    > [!NOTE]  
    >  Cuando configure una cláusula de grupo para el filtro, se quitarán los paréntesis redundantes del filtro después de guardar el resultado. Por ejemplo, si crea un filtro que agrupe **Cláusula 1** y **Cláusula 2**, aparecerán paréntesis alrededor de las cláusulas. Después de guardar el filtro, se quitan los paréntesis redundantes. La eliminación de los paréntesis no afecta a la lógica del filtro.  
  
4.  En la pestaña **Campos de evento** , seleccione los campos de evento que desee aplicar a un evento seleccionado.  
  
     Los eventos contienen una serie de campos que siempre se recopilan, que se muestran en la pestaña **Campos de evento** sin casillas. Un evento también puede tener campos opcionales que no se recopilan de forma predeterminada (por ejemplo, los campos opcionales costosos no se seleccionan). Los campos opcionales también se muestran en la pestaña **Campos de evento** con casillas. Para recopilar un campo opcional, active la casilla situada delante del campo opcional.  
  
    > [!NOTE]  
    >  Las opciones de campos de evento mostrarán campos que se capturarán y verán en los resultados de seguimiento. (Los eventos extendidos solo muestran tipos de datos de los campos de evento. Por ejemplo, los campos de solo lectura del evento no se muestran). Si selecciona dos o más eventos, el cuadro de diálogo Nueva sesión mostrará un espacio en blanco en la pestaña **Campos de evento** .  
  
5.  Para agregar destinos a una sesión de eventos, en la sección **Seleccionar una página** , seleccione **Almacenamiento de datos**.  
  
    > [!NOTE]  
    >  No haga clic en **Aceptar** hasta haber terminado de crear la sesión de eventos.  
  
#### <a name="to-add-targets-to-an-event-session"></a>Para agregar destinos a una sesión de eventos  
  
1.  En el cuadro de diálogo Nueva sesión, en la sección **Seleccionar una página** , seleccione **Almacenamiento de datos**.  
  
2.  En la página **Almacenamiento de datos** , seleccione el tipo de destino en la lista desplegable.  
  
     Después de seleccionar el tipo de destino, se muestra la descripción del destino. Un destino se puede agregar solo una vez. Si ya ha agregado el destino a la sesión, no aparecerá en la lista desplegable.  
  
3.  Haga clic en **Agregar** para agregar un destino para la sesión de eventos. Si desea quitar un destino, haga clic en **Quitar**.  
  
     Las propiedades de destino aparecen debajo de la sección **Destinos** , dependiendo del destino que seleccione.  
  
4.  A continuación se enumeran las propiedades que puede especificar, en función de los destinos que seleccione:  
  
    |Destino|Propiedad del destino|  
    |------------|-----------------------|  
    |**etw_classic_sync_target**|**Nombre del archivo de registro de sesión en el servidor**. Escriba el directorio y el nombre de archivo de registro en el servidor, o haga clic en **Examinar** para buscar y seleccionar el archivo de registro.<br /><br /> **Tamaño máximo del archivo de registro**. Especifique el tamaño máximo del archivo de registro para el evento de seguimiento de eventos para Windows (ETW). El valor predeterminado es de 20 megabytes. Puede seleccionar otra unidad de almacenamiento de la lista desplegable.<br /><br /> **Tamaño del búfer**. Especifique el tamaño del búfer en memoria para la sesión de eventos. El valor predeterminado es 128 kilobytes (KB). Puede seleccionar otra unidad de almacenamiento de la lista desplegable.<br /><br /> **Nombre de sesión**. Escriba un nombre descriptivo de la sesión ETW.<br /><br /> **Volver a intentar tras error al escribir en ETW**. Active esta casilla para reintentar la publicación del evento al subsistema de ETW.<br /><br /> **Número máximo de reintentos**. Especifique el número máximo de veces que desea que se reintente la publicación del evento en el subsistema de ETW antes de quitar el evento. El número predeterminado de reintentos es cero (0). Para esta propiedad de destino, cero (0) indica que no hay ningún reintento.|  
    |**event_counter**|No hay propiedades de destino para el contador de eventos.|  
    |**event_file**|**Nombre de archivo en el servidor**. Escriba el directorio y el nombre de archivo de destino en el servidor, o haga clic en **Examinar** para buscar y seleccionar el archivo de destino.<br /><br /> **Tamaño máximo del archivo**. Especifique el tamaño máximo de archivo para el destino del archivo. Si no especifica el tamaño máximo de archivo, el archivo crecerá hasta llenar el disco. El tamaño de archivo predeterminado es 1 gigabyte (GB). Puede seleccionar otra unidad de almacenamiento de la lista desplegable.<br /><br /> **Habilitar sustitución incremental de archivos**. Active esta casilla para habilitar la sustitución incremental de archivos para el destino de archivos.<br /><br /> **Número máximo de archivos**. Especifique el número máximo de archivos que desea conservar en el sistema de archivos.|  
    |**histogram**|**Evento para filtrar**. Seleccione el evento en que desea filtrar en la lista desplegable. Puede filtrar en cualquier evento que existe en la sesión de eventos. También puede seleccionar  **\<None >** en la lista desplegable para incluir todos los eventos y basar los depósitos en la acción.<br /><br /> **Basar depósitos en: Acción**. Seleccione esta opción para basar los depósitos en el nombre de acción que se utiliza como origen de datos y, a continuación, seleccione la acción en la lista desplegable.<br /><br /> **Basar depósitos en: Campo**. Seleccione esta opción para basar los depósitos en el campo de evento que se utiliza como origen de datos y, a continuación, seleccione el campo en la lista desplegable.<br /><br /> **Número máximo de depósitos**. Escriba el número máximo de depósitos que desea conservar. Cuando se alcance este valor, la sesión de eventos omitirá cualquier evento nuevo que no pertenezca a los depósitos existentes.|  
    |**pair_matching**|**Eventos: Comenzar con**. Seleccione el nombre de evento en la lista desplegable que especifica el evento de comienzo en una secuencia emparejada.<br /><br /> **Eventos: Terminar con**. Seleccione el nombre de evento en la lista desplegable que especifica el evento de terminación en una secuencia emparejada.<br /><br /> **Campos y acciones: Comenzar con**. Seleccione el campo y/o acción de comienzo en una secuencia emparejada en la lista desplegable.<br /><br /> **Campos y acciones: Terminar con**. Seleccione el campo y/o acción de terminación en una secuencia emparejada en la lista desplegable.<br /><br /> **Descartar nuevos eventos desemparejados en caso de presión de memoria**. Active esta casilla para detener la recopilación de eventos en el destino pair_matching cuando el equipo está bajo presión de memoria. Cuando ya no haya presión de memoria, la recopilación de eventos se reanudará.<br /><br /> **Máximo de eventos huérfanos**. Especifique el número máximo de eventos huérfanos que desea conservar en memoria.|  
    |**ring_buffer**|**Número de eventos para mantener**. Utilice las flechas arriba y abajo para especificar el número de eventos que desea conservar. El valor predeterminado es 1000.<br /><br /> **Tamaño máximo del búfer de memoria** Especifique la cantidad máxima de memoria que se va a utilizar. Los eventos existentes se quitan al alcanzar este valor. El tamaño de memoria predeterminado es 0 megabytes (MB), lo que significa valor ilimitado. Puede seleccionar otra unidad de almacenamiento de la lista desplegable.<br /><br /> **Mantener un número especificado de eventos (por tipo) cuando el búfer esté lleno**. Seleccione esta opción para mantener un número especificado de eventos de cada tipo en el búfer.<br /><br /> **Número de eventos para mantener (por tipo)**. Especifique el número preferido de eventos de cada tipo que desea conservar en el búfer.|  
  
5.  Si desea establecer propiedades de configuración avanzadas, seleccione **Avanzadas** en la sección **Seleccionar una página** .  
  
    > [!NOTE]  
    >  No haga clic en **Aceptar** hasta haber terminado de crear la sesión de eventos.  
  
#### <a name="to-set-advanced-configurations"></a>Para establecer configuraciones avanzadas  
  
1.  En el cuadro de diálogo Nueva sesión, en la sección **Seleccionar una página** , seleccione **Avanzadas**.  
  
2.  En la página **Avanzadas** , para especificar las opciones de **Modo de retención de eventos** para la sesión de eventos, realice lo siguiente:  
  
    1.  **Pérdida de evento único**. Seleccione esta opción para permitir la pérdida de un solo evento.  
  
    2.  **Pérdida de eventos múltiples**. Seleccione esta opción para permitir la pérdida de varios eventos.  
  
    3.  **Sin pérdida de eventos**. Seleccione esta opción si desea evitar la pérdida de eventos. No se recomienda seleccionar esta opción.  
  
        > [!NOTE]  
        >  Algunos eventos, como el evento **sqlos.wait_info** , no son compatibles con el modo de retención de eventos **Sin pérdida de eventos** .  
  
3.  Para especificar las opciones de **Latencia máxima de envío** para la sesión de eventos, realice lo siguiente:  
  
    1.  **En segundos**. Seleccione esta opción para prolongar o reducir la latencia máxima de envío. Utilice las flechas arriba y abajo para especificar la latencia máxima de envío en segundos.  
  
    2.  **Ilimitado**. Seleccione esta opción si desea que los eventos se envíen solo cuando el búfer esté lleno.  
  
4.  En el cuadro **Tamaño máximo de memoria** , especifique el tamaño máximo de la memoria. Los eventos existentes se quitan al alcanzar este valor. Puede seleccionar otra unidad de almacenamiento de la lista desplegable.  
  
5.  En el cuadro **Tamaño máximo de eventos** , especifique el tamaño máximo de los eventos que son demasiado grandes para poder estar contenidos en **Tamaño máximo de memoria**. Si no va a recopilar eventos muy grandes, no es necesario configurar esta opción. Puede seleccionar otra unidad de almacenamiento de la lista desplegable.  
  
6.  Para especificar las opciones de **Modo de partición de memoria** para la sesión de eventos, realice lo siguiente:  
  
    1.  **Ninguna**. Seleccione esta opción si no desea un modo de partición de memoria.  
  
    2.  **Por nodo**. Seleccione esta opción si desea crear particiones de memoria por nodo.  
  
    3.  **Por CPU**. Seleccione esta opción si desea crear particiones de memoria por CPU.  
  
 Para restaurar los valores predeterminados de configuración correspondientes a propiedades de sesión anteriores, haga clic en **Restaurar valores predeterminados**.  
  
## <a name="see-also"></a>Vea también  
 [Crear una sesión de eventos extendidos mediante el Editor de consultas](../../2014/database-engine/create-an-extended-events-session-using-query-editor.md)   
 [Crear una sesión de eventos extendidos utilizando el asistente &#40;Explorador de objetos&#41;](../ssms/object/object-explorer.md)   
 [Crear un script para una sesión de eventos extendidos](../../2014/database-engine/script-an-extended-event-session.md)  
  
  
