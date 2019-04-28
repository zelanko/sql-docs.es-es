---
title: Ver datos de sesión de eventos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: ac742a01-2a95-42c7-b65e-ad565020dc49
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: befef498ab4cda12ce38a34678b78a2b5dcd278c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62842902"
---
# <a name="view-event-session-data"></a>Ver datos de sesiones de eventos
  En este tema describe cómo usar la interfaz de usuario de presentación para ver y analizar datos de eventos extendidos:  
  
-   View Target Data (Ver datos de destino)  
  
-   Trabajar con datos  
  
## <a name="view-target-data"></a>Ver los datos de destino  
 Puede mostrar los datos recopilados en el destino especificado en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
### <a name="view-target-data"></a>View Target Data (Ver datos de destino)  
 Para ver los datos de destino:  
  
1.  En el Explorador de objetos, expanda **Administración**, **Eventos extendidos**, **Sesiones**y después una sesión.  
  
2.  Haga clic con el botón secundario en el nombre de destino y, a continuación, haga clic en **Ver los datos de destino** para mostrar los datos de destino.  
  
     La ventana de los datos de destino aparece en la vista predeterminada y muestra los datos de destino.  
  
 Notas sobre la consulta de datos de destino:  
  
-   Los datos de destino no están disponibles para el destino ETW.  
  
-   Para ver los datos ring_buffer en formato xml, en la ventana de datos de destino, haga clic en el vínculo **datos de destino ring_buffer** . El archivo ring_buffer.xml aparece en el editor xml.  
  
-   Para un destino event_file, vea los datos del destino de archivo (archivo .XEL) mediante uno de los métodos siguientes:  
  
    -   Usar el archivo -> Abrir en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
    -   Arrastre y coloque el archivo en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
    -   Haga doble clic en el archivo .XEL.  
  
    -   En [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], haga clic con el botón secundario en una sesión de eventos extendidos en ejecución y seleccione Ver datos de destino.  
  
    -   [fn_xe_file_target_read_file](/sql/relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql)  
  
    -   Puede ver más de uno. Archivo XEL seleccionando **combinar archivos de eventos extendidos** desde el archivo -> menú Abrir.  
  
### <a name="watching-live-data"></a>Observar datos en directo  
 Puede observar los datos en directo a medida que se capturan.  
  
-   En el Explorador de objetos, expanda los nodos **Administración**, **Eventos extendidos**y después **Sesiones** .  
  
-   Haga clic con el botón secundario en el nombre de sesión y, a continuación, haga clic en **Observar datos en directo** para iniciar la presentación de los datos de seguimiento.  
  
     Las columnas de presentación predeterminadas son **Nombre de evento** y **Marca de tiempo**.  
  
     Para agregar columnas adicionales a la ventana de seguimiento, haga clic en el botón **Elegir columnas** en la barra de herramientas de los eventos extendidos. La pestaña **Detalles** muestra todos los detalles del evento seleccionado.  
  
     Los eventos normalmente se muestran en 30 segundos aproximadamente. Si desea cambiar el periodo de latencia, puede cambiar **Latencia máxima de envío** en la página **Opciones avanzadas** del cuadro de diálogo **Nueva sesión** .  
  
### <a name="to-refresh-target-data"></a>Para actualizar los datos de destino  
 No se permite actualizar datos de destino para los destinos event_files:  
  
1.  Para actualizar los datos de destino automáticamente, haga clic con el botón secundario en los datos de destino, seleccione **Intervalo de actualización**y, a continuación, seleccione el intervalo de actualización en la lista de intervalos.  
  
2.  Para pausar y reanudar la actualización automática, haga clic con el botón secundario en los datos de destino y, a continuación, seleccione **Pausar** o **Reanudar**.  
  
3.  Para actualizar los datos de destino manualmente, haga clic con el botón secundario en los datos de destino y, a continuación, seleccione **Actualizar**.  
  
## <a name="working-with-data"></a>Trabajar con datos  
 Puede utilizar las funciones de análisis de la interfaz de usuario de eventos extendidos para identificar problemas.  
  
### <a name="details-pane"></a>Panel de detalles  
 En el panel **Detalles** se muestran todas las columnas del evento seleccionado, incluidos los campos y las acciones. Puede agregar una columna a la tabla de datos de destino haciendo clic con el botón secundario en una fila en el panel **Detalles** y seleccionando **Mostrar columna en tabla**.  
  
### <a name="create-modify-or-delete-merged-columns"></a>Crear, modificar o eliminar columnas combinadas  
 Una columna combinada permite combinar un conjunto de campos para que se muestren en una sola columna. La columna combinada mostrará los datos del primer campo distinto de NULL según el orden en que se agregaron a la lista de campos. Es similar a lo que se ve en el generador de perfiles de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , donde una columna específica puede mostrar datos diferentes en función del evento (el ejemplo más común es el campo TextData en el generador de perfiles de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ). Para obtener un ejemplo, puede combinar los campos statement y batch_text de los eventos sql_statement_completed y sql_batch_completed, respectivamente, en un campo denominado myStatement. Cuando se muestre la columna myStatement en la tabla, esta mostrará los datos correspondientes al evento asociado.  
  
 Puede crear, modificar o eliminar columnas combinadas:  
  
1.  Abra un archivo .XEL para ver los resultados de seguimiento. (También puede hacer clic con el botón secundario en el nombre de la sesión y, a continuación, seleccionar **Observar datos en directo**).  
  
2.  En la ventana de resultados de seguimiento, haga clic con el botón secundario en el encabezado de columna y, a continuación, haga clic en **Elegir columnas**.  
  
 Para crear una columna combinada, haga clic en **Nuevo** en el cuadro de diálogo **Elegir columnas** .  En el cuadro de diálogo **Nueva columna combinada** , asigne un nombre a la columna combinada y seleccione las columnas originales que se van a incluir en la columna combinada.  
  
 Para modificar una columna combinada, seleccione una columna combinada en el cuadro de diálogo **Elegir columnas** y haga clic en **Editar**. En el cuadro de diálogo **Editar columna combinada** , cambie el nombre de la columna combinada o modifique las columnas originales que se van a incluir en la columna combinada.  
  
 Para eliminar una columna combinada, seleccione una columna combinada en el cuadro de diálogo **Elegir columnas** y haga clic en **Eliminar**.  
  
### <a name="filter-results"></a>Filtrar los resultados  
 Puede ver los resultados de seguimiento y, a continuación, aplicar filtros para reducir los resultados de seguimiento que se muestran en la ventana de seguimiento. El filtro de visualización incluye un filtro horario y un filtro avanzado. Puede utilizar el filtro horario para filtrar el resultado de seguimiento por la marca de tiempo del evento y utilizar el filtro avanzado para crear condiciones de filtro mediante los campos de evento y las acciones. Hay una relación "and" entre el filtro horario y los filtros avanzados.  
  
 Para crear un filtro:  
  
1.  Abra un archivo .XEL para ver los resultados de seguimiento. (También puede hacer clic con el botón secundario en el nombre de la sesión y, a continuación, seleccionar **Observar datos en directo**).  
  
2.  En la ventana de resultados de seguimiento, seleccione los resultados que desee filtrar, y a continuación, en la barra de herramientas **Eventos extendidos** , haga clic en **Filtros**.  
  
3.  En el cuadro de diálogo **Filtros** , seleccione **Establecer filtro de tiempo** para establecer el filtro horario arrastrando las barras deslizantes o modificando la hora en el cuadro de edición.  
  
4.  En la sección **Filtros adicionales** , aplique sus criterios de filtro y, a continuación, haga clic en **Aplicar**.  
  
### <a name="sort-results"></a>Ordenar los resultados  
 Para ordenar los resultados en orden ascendente o descendente:  
  
1.  Abra un archivo .XEL para ver los resultados de seguimiento. (También puede hacer clic con el botón secundario en el nombre de la sesión, seleccionar **Observar datos en directo**y, a continuación, hacer clic en el botón **Detener fuente de distribución de datos** de la barra de herramientas).  
  
2.  En la ventana de resultados de seguimiento, haga clic con el botón secundario en el encabezado de columna que desea ordenar y haga clic en **Orden ascendente** u **Orden descendente**.  
  
 También puede hacer clic en el encabezado de columna para invertir el criterio de ordenación.  
  
 Si ha agrupado las columnas, al ordenar la columna, solo se ordenarán los datos que contiene el grupo.  
  
### <a name="group-results"></a>Agrupar los resultados  
 La agrupación de resultados es equivalente a la funcionalidad de la cláusula de `GROUP BY` en [!INCLUDE[tsql](../includes/tsql-md.md)]. La tabla de datos de destino mostrará los datos agrupados, lo que permite expandir y contraer los datos.  
  
 Debe agrupar los datos para poder agregarlos. Por ejemplo, puede agrupar según el valor de query_hash, ordenar de forma descendente por la duración, obtener la duración media de cada grupo y después ordenar de forma descendente de acuerdo con la agregación.  Esto creará una lista en la que se muestra la lista de instrucciones únicas desde la duración media mayor a la menor. Cuando expanda el grupo superior, verá las ejecuciones individuales de esa consulta específica ordenadas de mayor a menor.  
  
 Puede agrupar los resultados por una sola columna o por varias columnas.  
  
 Abra un archivo .XEL para ver los resultados de seguimiento. (También puede hacer clic con el botón secundario en el nombre de la sesión, seleccionar **Observar datos en directo**y, a continuación, hacer clic en el botón **Detener fuente de distribución de datos** de la barra de herramientas).  
  
 Para agrupar los resultados por una sola columna, haga clic con el botón secundario en el encabezado de columna en la ventana de resultados de seguimiento y haga clic en **Agrupar por esta columna**. Para deshacer la agrupación, seleccione una de las filas y haga clic en **Quitar todos los grupos**.  
  
 Para agrupar los resultados por varias columnas, haga clic en el botón **Agrupación** en la barra de herramientas **Eventos extendidos** . En el cuadro **Columnas disponibles** del cuadro de diálogo **Agrupación** , seleccione las columnas que desea agrupar y muévalas al cuadro **Columnas agrupadas en** . Para cambiar el orden del cuadro **Columnas agrupadas en** , haga clic en las flechas arriba o abajo.  
  
### <a name="aggregate-results"></a>Agregar los resultados  
 Puede ver los resultados de seguimiento y, a continuación, analizar con mayor profundidad los datos del evento agregando columnas en los resultados. Los eventos extendidos admiten cinco funciones de agregación:  
  
-   sum  
  
-   min  
  
-   max  
  
-   average  
  
-   count  
  
 Sum, min, max y average solo se pueden usar con las columnas numéricas. Count es el número de valores distintos de null que existen para la columna seleccionada del grupo.  
  
 La agregación se realiza en un grupo, por lo que debe agrupar los resultados antes de realizar la agregación. Para agregar los resultados:  
  
1.  Abra un archivo .XEL para ver los resultados de seguimiento. (También puede hacer clic con el botón secundario en el nombre de la sesión, seleccionar **Observar datos en directo**y, a continuación, hacer clic en el botón **Detener fuente de distribución de datos** de la barra de herramientas).  
  
2.  En la barra de herramientas **Eventos extendidos** , haga clic en el botón **Agregación** . En el cuadro de diálogo Agregación se mostrarán las columnas disponibles para la agregación.  
  
3.  En la columna **Tipo de agregación** , seleccione el tipo de agregación.  
  
4.  En el cuadro **Ordenar agregación por** , seleccione la columna de ordenación. A continuación, seleccione orden ascendente o descendente.  
  
### <a name="search-for-text-in-columns"></a>Buscar texto en columnas  
 Puede buscar texto en columnas:  
  
1.  Abra un archivo .XEL para ver los resultados de seguimiento. (También puede hacer clic con el botón secundario en el nombre de la sesión y seleccionar **Observar datos en directo**).  
  
2.  Haga clic en **Buscar** en la barra de herramientas **Eventos extendidos** .  
  
3.  En el cuadro **Buscar** del cuadro de diálogo **Buscar en eventos extendidos** , escriba el texto que desea buscar. Puede seleccionar una de sus últimas 20 cadenas de búsqueda en la lista desplegable.  
  
4.  En el cuadro **Buscar** , seleccione la ubicación donde debe buscarse el texto seleccionado. Utilice las siguientes opciones para buscar:  
  
    -   Columnas de la tabla Utilice esta opción para buscar en todas las columnas visibles en la ventana de seguimiento.  
  
    -   Detalles Utilice esta opción para buscar todas las columnas (promocionadas y no promocionadas) en la ventana de seguimiento que se seleccionaron antes de abrir el **buscar en eventos extendidos** cuadro de diálogo.  
  
    -   *Event_column_name*. Utilice esta opción para buscar en una columna de evento concreta de la lista desplegable.  
  
5.  Utilice las siguientes opciones para especificar cómo desea definir la búsqueda:  
  
    -   Coincidir mayúsculas y minúsculas. Utilice esta opción para mostrar los resultados de búsqueda del texto que escribió en el cuadro Buscar que coincidan tanto en contenido como en el uso de mayúsculas y minúsculas.  
  
    -   Solo palabras completas. Utilice esta opción para mostrar solo los resultados de búsqueda del texto especificado cuyas palabras completas coincidan.  
  
    -   Buscar hacia atrás. Utilice esta opción para buscar desde la ubicación del cursor hasta el principio de los resultados.  
  
    -   Uso Utilice esta opción para interpretar los caracteres especiales y las expresiones regulares que escribió en el cuadro Buscar. Los caracteres especiales incluyen los caracteres comodín (*) y (?) para representar uno o más caracteres. Las expresiones regulares son notaciones especiales utilizadas para definir patrones de texto de búsqueda.  
  
    -   Haga clic en **Buscar siguiente** para buscar siguiente el texto que escribió en el cuadro **Buscar** .  
  
### <a name="bookmarks"></a>Marcadores  
 Para facilitar el cambio a una fila, puede marcar una o varias filas en los datos de destino. Haga clic con el botón secundario en una fila para cambiar el marcador. Utilice los botones anterior y siguiente de la barra de herramientas **Eventos extendidos** para navegar por las filas marcadas.  
  
### <a name="change-display-settings"></a>Cambiar la configuración de presentación  
 Puede guardar la información de columna (orden de columna, columna de combinación y ancho de columna) y la información de filtro de un resultado de seguimiento en un archivo de configuración de presentación de eventos extendidos (archivo .viewsetting). Después de guardar el archivo, puede aplicarlo a los resultados de seguimiento para cambiar la vista.  
  
 Para cambiar la configuración de presentación:  
  
1.  Abra un archivo .XEL para ver los resultados de seguimiento. (También puede hacer clic con el botón secundario en el nombre de la sesión y seleccionar **Observar datos en directo**).  
  
2.  En la barra de herramientas **Eventos extendidos** , seleccione **Configuración de presentación**. En la lista desplegable, seleccione una de las opciones siguientes:  
  
    -   Guardar como. Guarde la información de filtro y columnas del resultado de un seguimiento en un archivo .viewsetting.  
  
    -   Abrir. Abra un archivo .viewsetting existente.  
  
    -   Abrir reciente. Abra un archivo .viewsetting guardado recientemente.  
  
### <a name="copy-or-export-trace-results"></a>Copiar o exportar resultados de seguimiento  
 Puede copiar celdas, filas y detalles a determinas filas de los resultados de seguimiento. También puede exportar los resultados de seguimiento a:  
  
-   archivo .XEL  
  
-   table  
  
-   archivo .CSV  
  
 Para copiar los resultados de seguimiento, seleccione una celda, una fila o varias filas, haga clic con el botón secundario, seleccione **Copiar** y, a continuación, seleccione **Celda**, **Fila**o **Detalles**. Los eventos extendidos admiten la copia de un máximo de 1000 filas.  
  
 Puede exportar los resultados de seguimiento en un archivo .XEL, una tabla o un archivo .CSV seleccionando **Exportar a** en la opción de menú **Eventos extendidos** en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
### <a name="view-a-deadlock-graph-and-query-plans"></a>Ver un evento Deadlock Graph y planes de consulta  
 Puede ver el gráfico de interbloqueo de **xml_deadlock_report** en el panel de detalles para ayudarle a solucionar los interbloqueos. También puede ver los gráficos de plan de consulta para los siguientes eventos:  
  
-   query_post_compilation_showplan  
  
-   query_pre_execution_showplan  
  
-   query_post_execution_showplan  
  
 Para ver el gráfico de interbloqueo:  
  
-   En el Explorador de objetos, expanda los nodos **Administración**, **Eventos extendidos**y después **Sesiones** .  
  
-   Haga clic con el botón secundario en la sesión que contiene el evento de interbloqueo configurado que desea ver y, a continuación, seleccione **Observar datos en directo**.  
  
-   Seleccione el evento de interbloqueo y vea el gráfico en la pestaña **Interbloqueo** en el panel de detalles.  
  
 Para ver los gráficos del plan de consulta:  
  
1.  En el Explorador de objetos, expanda los nodos **Administración**, **Eventos extendidos**y después **Sesiones** .  
  
2.  Haga clic con el botón secundario en la sesión que contiene el gráfico del plan de consulta que desea ver (por ejemplo, query_post_compilation_showplan) y, a continuación, seleccione **Observar datos en directo**.  
  
3.  Seleccione el evento de gráfico del plan de consulta (por ejemplo, query_post_compilation_showplan) y visualice el gráfico en la pestaña **Plan de consulta** en el panel de detalles.  
  
  
