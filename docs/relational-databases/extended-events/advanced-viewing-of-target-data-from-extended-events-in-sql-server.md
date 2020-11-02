---
title: Visualización avanzada de datos de destino de eventos extendidos
description: Use las características avanzadas de SQL Server Management Studio para ver los datos de destino de eventos extendidos con todo detalle. Puede ver, exportar y manipular los datos.
ms.date: 05/24/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: tutorial
ms.assetid: b2e839d7-1872-46d9-b7b7-6dcb3984829f
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 174873d62a2c90ba6309f9063294a27517326d62
ms.sourcegitcommit: 67befbf7435f256e766bbce6c1de57799e1db9ad
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/24/2020
ms.locfileid: "92523996"
---
# <a name="advanced-viewing-of-target-data-from-extended-events-in-sql-server"></a>Advanced Viewing of Target Data from Extended Events in SQL Server (Visualización avanzada de datos de destino de eventos extendidos en SQL Server)

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]


En este artículo se explica cómo usar las características avanzadas de SQL Server Management Studio (SSMS.exe) para ver los datos de destino de eventos extendidos con todo detalle. En este artículo se explica cómo:


- Abrir y ver los datos de destino de diversas formas.
- Exportar los datos de destino a varios formatos por medio del menú especial o la barra de herramientas de eventos extendidos.
- Manipular los datos mientras se ven o antes de exportarlos.



### <a name="prerequisites"></a>Prerrequisitos

En este artículo se da por hecho que ya sabe cómo crear e iniciar una sesión de eventos. En este artículo encontrará instrucciones sobre cómo crear una sesión de eventos:

[Inicio rápido: Eventos extendidos en SQL Server](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)


En este artículo también se da por hecho que ha instalado una versión mensual muy reciente de SSMS. Encontrará ayuda para instalarlo en:

- [Descarga de SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md)



### <a name="differences-with-azure-sql-database"></a>Diferencias con Base de datos SQL de Azure


Existe un grado de similitud muy elevado en la implementación y las capacidades de los eventos extendidos entre los productos Microsoft SQL Server y Base de datos SQL de Azure. Aun así, hay algunas diferencias que afectan a la interfaz de usuario de SSMS.


- En Base de datos SQL, el archivo de destino package0.event_file no puede ser un archivo ubicado en el disco duro local, sino que hay que usar un contenedor de almacenamiento de Azure en su lugar. Por lo tanto, si está conectado a Base de datos SQL, la interfaz de usuario de SSMS pide un contenedor de almacenamiento, en lugar de un nombre de archivo y una ruta de acceso local.


- En la interfaz de usuario de SSMS, si ve que la casilla **Observar datos en directo** está atenuada y deshabilitada, es porque esa característica no está disponible en Base de datos SQL.


- Algunos eventos extendidos se instalan con SQL Server. En el nodo **Sesiones** , podemos ver **AlwaysOn_health** y algunos más. Estos eventos no están visibles cuando se conecta a Base de datos SQL, porque no existen para Bases de datos SQL.


Este artículo está redactado desde la perspectiva de SQL Server. En él se usa el archivo de destino event_file, que es un área donde existen diferencias. Las menciones a otras diferencias se reducen a diferencias que son importantes o que no son evidentes.


Para obtener documentación sobre los eventos extendidos específicos de Base de datos SQL de Azure, vea:

- [Eventos extendidos en Base de datos SQL](/azure/azure-sql/database/xevent-db-diff-from-svr)



## <a name="a-general-options"></a>A. Opciones generales


Por lo general, el acceso a las opciones avanzadas se logra por medio de uno de los siguientes métodos:


- El menú habitual de **Archivo** > **Abrir** > **Archivo** .
- Haciendo clic con el botón derecho en **Administración** Eventos extendidos **en el** > **Explorador de objetos** .
- El menú especial **Eventos extendidos** y la barra de herramientas especial para eventos extendidos.
- Haciendo clic con el botón derecho en el panel con pestañas que muestra los datos de destino.



## <a name="b-bring-target-data-into-ssms-for-display"></a>B. Recuperar datos de destino para mostrarlos en SSMS


Existen varias maneras de incorporar datos de destino del archivo event_file a la interfaz de usuario de SSMS. Al especificar un archivo de destino event_file, hay que definir un nombre y una ruta de acceso:

- .XEL es la extensión del nombre de archivo.


- Cada vez que se inicia la sesión de eventos, el sistema inserta un número entero grande al nuevo nombre de archivo para que ese nombre de archivo sea único y diferente de la ocasión anterior en que se inició la sesión.
  - *Ejemplo* : Checkpoint_Begins_ES_0_131103935140400000.xel


- El contenido de un .XEL no es texto sin formato que puede verse con Notepad.exe.
  - Si quiere, puede agregar varios archivos .XEL al mismo tiempo usando el menú **Archivo** > **Abrir** > **Combinar archivos de eventos extendidos** .



SSMS puede mostrar datos procedentes de cualquier destino. Pero la forma en que se visualicen será distinta en función del destino:

- *event_file:* los datos de un archivo de destino event_file se muestran muy bien, con todas las características disponibles.


- *ring_buffer:* los datos de un archivo destino ring_buffer se muestran como XML sin formato.


- En el resto de destinos, la eficacia de la visualización estará a medio camino entre event_file y ring_buffer.
  - Esos otros destinos son event_counter, histogram y pair_matching.


- *etw_classic_sync_target:* SSMS no puede mostrar datos procedentes del tipo de destino etw_classic_sync_target.



### <a name="b1-open-xel-with-menu-file--open--file"></a>B.1 Abrir el archivo .XEL con el menú Archivo > Abrir > archivo


Puede abrir un archivo .XEL concreto con el menú estándar **Archivo** > **Abrir** > **Archivo** .

También puede arrastrarlo y colocarlo en la barra de pestañas de la interfaz de usuario de SSMS.



### <a name="b2-view-target-data"></a>B.2 Ver datos de destino


La opción **Ver datos de destino** muestra los datos que se han capturado hasta ahora.


En el panel del **Explorador de objetos** puede expandir los nodos y, luego, hacer clic con el botón derecho en:

- **Administración** > **Eventos extendidos** > **Sesiones** >  *[su sesión]*  >  *[su nodo de destino]*  > **Ver datos de destino** .


Los datos de destino se muestran en un panel con pestañas en SSMS. Esto se refleja en el siguiente ejemplo.


![su destino > Ver datos de destino](../../relational-databases/extended-events/media/xevents-ssms-ui20-viewtargetdata.png)


> [!NOTE] 
> **Ver datos de destino** muestra los *datos acumulados procedentes de varios archivos .XEL* de la sesión de eventos en cuestión. Con cada ciclo **Iniciar**-**Detener** se crea un archivo con un entero derivado con una hora posterior insertado en el nombre, si bien cada archivo comparte el mismo nombre raíz.



#### <a name="b3-watch-live-data"></a>B.3 Observar datos en directo


Cuando la sesión de eventos está activa, puede que quiera ver los datos de eventos en tiempo real, a medida que el destino los vaya recibiendo.


- **Administración** > **Eventos extendidos** > **Sesiones** >  *[su sesión]*  > **Observar datos en directo** .


![su sesión > Observar datos en directo](../../relational-databases/extended-events/media/xevents-ssms-ui55-watchlivedata.png)


La presentación de datos se actualiza en un intervalo que se puede especificar. Vea la **Latencia máxima de envío** haciendo lo siguiente:

- **Eventos extendidos** > **Sesiones** >  *[su sesión]*  > **Propiedades** > **Avanzadas** > **Latencia máxima de envío**



### <a name="b4-view-xel-with-sysfn_xe_file_target_read_file-function"></a>B.4 Ver .XEL con la función sys.fn_xe_file_target_read_file


En un procesamiento por lotes, la siguiente función de sistema puede generar XML para los registros de un archivo .XEL:

- [sys.fn\_xe\_file\_target\_read\_file](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md)



## <a name="c-export-the-target-data"></a>C. Exportar los datos de destino


Una vez que tenemos los datos de destino en SSMS, se pueden exportar a diversos formatos haciendo lo siguiente:


1. Mantenga el foco en la presentación de datos.

    - De repente, aparecerán una nueva barra de herramientas y un nuevo elemento de menú para eventos extendidos.

    ![Exportación de datos en pantalla: Eventos extendidos > Exportar a > (.csv, .xel o a una tabla)](../../relational-databases/extended-events/media/xevents-ssms-ui75-menuextevent-exportto-xel.png)

2. Haga clic en el nuevo elemento de menú **Eventos extendidos** .
3. Haga clic en **Exportar a** y, después, elija un formato.



## <a name="d-manipulate-data-in-the-display"></a>D. Manipular los datos en pantalla


La interfaz de usuario de SSMS no solo muestra los datos para verlos tal cual, sino que ofrece varias maneras de manipularlos.



### <a name="d1-context-menus-in-the-data-display"></a>D.1 Menús contextuales en la presentación de datos


En varios sitios de la presentación de datos se puede tener acceso a menús contextuales haciendo clic con el botón derecho.



#### <a name="d11-right-click-a-data-cell"></a>D.1.1 Hacer clic con el botón derecho en una celda de datos


En la siguiente captura de pantalla se muestra el menú contextual que aparece cuando se hace clic con el botón derecho en una celda en la presentación de datos. La captura de pantalla refleja también el elemento de menú **Copia** extendido.


![Hacer clic con el botón derecho en una celda en la presentación de datos](../../relational-databases/extended-events/media/xevents-ssms-ui25-rightclickcell.png)



#### <a name="d12-right-click-a-column-header"></a>D.1.2 Hacer clic con el botón derecho en un encabezado de columna


En la siguiente captura de pantalla se muestra el menú contextual que aparece cuando se hace clic con el botón derecho en el encabezado **timestamp** .


![Hacer clic con el botón derecho en un encabezado de columna en la presentación de datos. También, la cuadrícula Detalles.](../../relational-databases/extended-events/media/xevents-ssms-ui40-toolbar.png)


La captura de pantalla anterior muestra también la barra de herramientas especial para eventos extendidos. El brillo del botón Detalles denota que está activo. Por lo tanto, la imagen muestra también la pestaña **Detalles** ficha y se ve una cuadrícula como una segunda parte de la presentación de datos.



### <a name="d2-choose-columns-merge-columns"></a>D.2 Elegir columnas, Combinar columnas


La opción **Elegir columnas** permite controlar qué columnas de datos se muestran y cuáles no. El elemento de menú **Elegir columnas** se encuentra en varios sitios:

- En el menú **Eventos extendidos** .
- En la barra de herramientas de eventos extendidos.
- En el menú contextual de un encabezado en la presentación de datos.


Al hacer clic en **Elegir columnas** , se abre un cuadro de diálogo con el mismo nombre.


![Cuadro de diálogo Elegir columnas, también con opciones de Combinar columnas](../../relational-databases/extended-events/media/xevents-ssms-ui35-choosecolumns.png)



#### <a name="d21-merge-columns"></a>D.2.1 Combinar columnas


El cuadro de diálogo **Elegir columnas** tiene una sección dedicada a la combinación de varias columnas en una para uno de dos fines:

- Visualización.
- Exportación.



### <a name="d3-filters"></a>D.3 Filtros


En el área de eventos extendidos, hay dos tipos principales de filtros que se pueden especificar:

- *Filtros previos al destino:* filtros que reducen la cantidad de datos que el motor de eventos envía a su destino.

- *Filtros posteriores al destino:* filtros que se pueden seleccionar en la interfaz de usuario de SSMS para excluir algunos registros de destino de la visualización.


Los filtros de visualización de SSMS son los siguientes:

- Un filtro de *rango de tiempo* , que examina la columna **timestamp** .
- Un filtro de *valores de columna* .


La relación entre el filtro de tiempo y el filtro de columnas es un valor booleano ' *AND* '.


![Filtros de rango de tiempo y de columnas en el cuadro de diálogo Filtros](../../relational-databases/extended-events/media/xevents-ssms-ui45-filters.png)



### <a name="d4-grouping-and-aggregation"></a>D.4 Agrupación y agregación


Agrupar filas con valores coincidentes en una misma columna es el primer paso para la agregación de datos.



#### <a name="d41-grouping"></a>D.4.1 Agrupación


En la barra de herramientas de eventos extendidos, el botón **Agrupación** abre un cuadro de diálogo que sirve para agrupar los datos recogidos en una columna determinada. En la siguiente captura de pantalla se muestra un cuadro de diálogo en el que los datos se agrupan por la columna *name* .

![Captura de pantalla en la que se muestran la barra de herramientas con la opción Agrupación seleccionada y el cuadro de diálogo Agrupación.](../../relational-databases/extended-events/media/xevents-ssms-ui53-grouping.png)

Tras realizar la agrupación, la presentación de datos adquiere un nuevo aspecto, como se aprecia aquí.

![Nuevo aspecto tras la agrupación](../../relational-databases/extended-events/media/xevents-ssms-ui54-grouped.png)



#### <a name="d42-aggregation"></a>D.4.2 Agregación


Una vez agrupados los datos mostrados, puede pasar a agregar datos en otras columnas.  En la siguiente captura de pantalla se muestran los datos agrupados agregados por *count* .

![Captura de pantalla en la que se muestran la barra de herramientas con la opción Agregación seleccionada y el cuadro de diálogo Agregación.](../../relational-databases/extended-events/media/xevents-ssms-ui51-aggregdialogcount.png)

Tras realizar la agregación, la presentación de datos adquiere un nuevo aspecto, como se aprecia aquí.

![Captura de pantalla en la que se muestra que se ha agregado un valor de recuento.](../../relational-databases/extended-events/media/xevents-ssms-ui52-aggregnewdisplay.png)



### <a name="d5-view-run-time-query-plan"></a>D.5 Ver el plan de consulta en tiempo de ejecución


El evento **query_post_execution_showplan** permite ver el plan de consulta real en la interfaz de usuario de SSMS. Cuando el panel **Detalles** está visible, se puede ver un gráfico del plan de consulta en la pestaña **Plan de consulta** . Si se mantiene el puntero sobre un nodo del plan de consulta, verá una lista de nombres de propiedad y sus valores para el nodo.


![Plan de consulta con la lista de propiedades de un nodo](../../relational-databases/extended-events/media/xevents-ssms-ui60-showplangraph.png)

## <a name="see-also"></a>Consulte también

[XELite: biblioteca multiplataforma para leer XEvents de archivos XEL o secuencias en directo de SQL](https://www.nuget.org/packages/Microsoft.SqlServer.XEvent.XELite/); publicada en mayo de 2019.

[Cmdlet de PowerShell Read-SQLXEvent](https://www.powershellgallery.com/packages/SqlServer), publicado en julio de 2019.