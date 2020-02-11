---
title: Modificar la vista de resultados de seguimiento | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 860a80dc-bac0-4ef0-bf7f-7a9b430d7aa3
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 780772f7703e4499c13eb9373ccad4252097b536
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66089435"
---
# <a name="modify-the-trace-results-view"></a>Modificar la vista de resultados del seguimiento
  En este tema se describe cómo modificar la vista de resultados de seguimiento de una sesión de eventos extendidos en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] realizando las siguientes tareas.  
  
1.  [Agregar o quitar columnas](#AddRemoveColumns)  
  
2.  [Crear, modificar o eliminar columnas combinadas](#ChangeColumns)  
  
3.  [Ordenar los resultados](#SortResults)  
  
4.  [Agrupar los resultados](#GroupResults)  
  
5.  [Agregar los resultados](#AggregateResults)  
  
6.  [Filtrar los resultados](#Filter)  
  
7.  [Buscar texto en columnas](#Search)  
  
8.  [Cambiar la configuración de presentación](#ChangeDisplay)  
  
##  <a name="AddRemoveColumns"></a>Agregar o quitar columnas  
  
1.  Abra un archivo .XEL para ver los resultados de seguimiento.  
  
    > [!NOTE]  
    >  También puede hacer clic con el botón secundario en el nombre de la sesión y, a continuación, seleccionar **observar datos en directo**.  
  
2.  En la ventana de resultados de seguimiento, haga clic con el botón secundario del mouse en el encabezado de columna y, a continuación, seleccione **Elegir columnas**.  
  
3.  En el cuadro de diálogo **Elegir columnas** , en la sección **Columnas disponibles** , seleccione los nombres de columna que desea agregar y, a continuación, haga clic en la flecha derecha.  
  
    > [!NOTE]  
    >  De forma predeterminada, las columnas se organizan por nombre. Para mostrar las columnas por evento, haga clic en **Organizar por evento**.  
  
     Para quitar las columnas, en la sección **Columnas seleccionadas** , seleccione las columnas que desea quitar, y haga clic en la flecha izquierda.  
  
4.  En la sección **Columnas seleccionadas** , para cambiar la presentación del orden de columnas, haga clic en **Subir** o **Bajar** respectivamente. No puede mover varias filas.  
  
5.  Haga clic en **OK**.  
  
##  <a name="ChangeColumns"></a>Crear, editar o eliminar columnas combinadas  
  
#### <a name="to-create-merged-columns"></a>Para crear columnas combinadas  
  
1.  Abra un archivo .XEL para ver los resultados de seguimiento.  
  
    > [!NOTE]  
    >  También puede hacer clic con el botón secundario en el nombre de la sesión y, a continuación, seleccionar **observar datos en directo**.  
  
2.  En la ventana de resultados de seguimiento, haga clic con el botón secundario en el encabezado de columna y, a continuación, haga clic en **Elegir columnas**.  
  
3.  En el cuadro de diálogo **Elegir columnas** , haga clic en **Nueva**.  
  
4.  En el cuadro de diálogo **Nueva columna combinada** , en el cuadro **Nombre de columna combinada** , escriba un nombre para las columnas combinadas.  
  
5.  En el cuadro **Columnas originales para combinar** , seleccione dos o más columnas para combinar en la lista desplegable.  
  
    > [!NOTE]  
    >  Los eventos extendidos solo permiten combinar hasta cinco columnas.  
  
6.  Haga clic en **OK**.  
  
#### <a name="to-edit-merged-columns"></a>Para editar columnas combinadas  
  
1.  Abra un archivo .XEL para ver los resultados de seguimiento.  
  
    > [!NOTE]  
    >  También puede hacer clic con el botón secundario en el nombre de la sesión y, a continuación, seleccionar **observar datos en directo**.  
  
2.  En la ventana de resultados de seguimiento, haga clic con el botón secundario en el encabezado de columna y, a continuación, haga clic en **Elegir columnas**.  
  
3.  En el cuadro de diálogo **Elegir columnas** , haga clic en **Editar**.  
  
4.  Para cambiar el nombre de la columna combinada, en el cuadro de diálogo **Nueva columna combinada** , en el cuadro **Nombre de columna combinada** , escriba el nuevo nombre.  
  
     Para cambiar las columnas que desea combinar, en el cuadro **Columnas originales para combinar** , seleccione las columnas que desee combinar en la lista desplegable, y, a continuación, haga clic en **Aceptar**.  
  
#### <a name="to-delete-merged-columns"></a>Para eliminar columnas combinadas  
  
1.  Abra un archivo .XEL para ver los resultados de seguimiento.  
  
    > [!NOTE]  
    >  También puede hacer clic con el botón secundario en el nombre de la sesión y, a continuación, seleccionar **observar datos en directo**.  
  
2.  En la ventana de resultados de seguimiento, haga clic con el botón secundario en el encabezado de columna y, a continuación, haga clic en **Elegir columnas**.  
  
3.  En el cuadro de diálogo **Elegir columnas** , seleccione el nombre de la columna combinada que desee eliminar y, a continuación, haga clic en **Eliminar**.  
  
##  <a name="SortResults"></a>Ordenar los resultados  
  
#### <a name="to-sort-the-results-in-ascending-or-descending-order"></a>Para ordenar los resultados en orden ascendente o descendente  
  
-   Abra un archivo .XEL para ver los resultados de seguimiento.  
  
    > [!NOTE]  
    >  También puede hacer clic con el botón secundario en el nombre de la sesión, seleccionar **observar datos en directo**y, a continuación, hacer clic en el botón **detener fuente** de distribución de datos de la barra de herramientas.  
  
-   En la ventana de resultados de seguimiento, haga clic con el botón secundario del mouse en el encabezado de columna que desea ordenar. Haga clic **Orden ascendente** o en **Orden descendente** para ordenar la columna en orden ascendente o descendente respectivamente.  
  
     Si ha agrupado las columnas, al ordenar la columna, solo se ordenarán los datos que contiene el grupo.  
  
##  <a name="GroupResults"></a>Agrupar resultados  
  
#### <a name="to-group-the-results-by-a-single-column"></a>Para agrupar los resultados por una única columna  
  
1.  Abra un archivo .XEL para ver los resultados de seguimiento.  
  
    > [!NOTE]  
    >  También puede hacer clic con el botón secundario del mouse en el nombre de la sesión, seleccionar **Observar datos en directo**y, a continuación, hacer clic en el botón **Detener fuente de distribución de datos** de la barra de herramientas de eventos extendidos.  
  
2.  En la ventana de resultados de seguimiento, haga clic con el botón secundario del mouse en el encabezado de columna que desea agrupar, y, a continuación, haga clic en **Agrupar por esta columna**.  
  
#### <a name="to-group-the-results-by-multiple-columns"></a>Para agrupar los resultados por varias columnas  
  
1.  Abra un archivo .XEL para ver los resultados de seguimiento.  
  
    > [!NOTE]  
    >  También puede hacer clic con el botón secundario en el nombre de la sesión, seleccionar **observar datos en directo**y, a continuación, hacer clic en el botón **detener fuente** de distribución de datos de la barra de herramientas.  
  
2.  Haga clic en el botón **Agrupación** en la barra de herramientas de eventos extendidos.  
  
3.  En el cuadro de diálogo **Agrupación** , en el cuadro **Columnas disponibles** , seleccione las columnas que desee agrupar y, a continuación, haga clic en la flecha derecha.  
  
     Para cambiar el orden de agrupación, en la sección **Columnas agrupadas en** , haga clic en las flechas arriba o abajo.  
  
     Para quitar las columnas de la agrupación, en el cuadro **Columnas agrupadas en** , seleccione las columnas que desea quitar y, a continuación, haga clic en la flecha izquierda.  
  
4.  Haga clic en **OK**.  
  
##  <a name="AggregateResults"></a>Resultados agregados  
 Los eventos extendidos admiten cinco funciones de agregación:  
  
-   Sum  
  
-   Min  
  
-   Max  
  
-   Average  
  
-   Count  
  
 Sum, Min, Max y Average solo se pueden usar con las columnas numéricas disponibles. Count es el número de valores distintos de null que existen para la columna seleccionada del grupo.  
  
#### <a name="to-aggregate-results"></a>Para agregar los resultados  
  
1.  Abra un archivo .XEL para ver los resultados de seguimiento.  
  
    > [!NOTE]  
    >  También puede hacer clic con el botón secundario en el nombre de la sesión, seleccionar **observar datos en directo**y, a continuación, hacer clic en el botón **detener fuente** de distribución de datos de la barra de herramientas.  
  
    > [!NOTE]  
    >  La agregación se ejecuta en un grupo, de modo que debe agrupar los resultados para realizar la agregación.  
  
2.  En la barra de herramientas de Eventos extendidos, haga clic en el botón **Agregado** .  
  
     El cuadro de diálogo **Agregación** aparece mostrando las columnas disponibles para la agregación.  
  
3.  En **Tipo de agregación**, seleccione cómo desea agregar la columna correspondiente en la lista desplegable.  
  
4.  En el cuadro **Ordenar agregación por** , seleccione la columna por la que desea ordenar en la lista desplegable.  
  
5.  Seleccione la opción **En orden ascendente** para clasificar el resultado de la agregación en orden ascendente.  
  
6.  Seleccione la opción **En orden descendente** para clasificar el resultado de la agregación en orden descendente.  
  
7.  Haga clic en **OK**.  
  
##  <a name="Filter"></a>Filtrar resultados  
 Puede aplicar filtros para reducir los resultados de seguimiento que se muestran en la ventana de seguimiento. El filtro de visualización incluye un filtro horario y un filtro avanzado. Puede utilizar el filtro horario para filtrar el resultado de seguimiento por la marca de tiempo del evento y utilizar el filtro avanzado para crear condiciones de filtro mediante los campos de evento y las acciones. Hay una relación de AND lógico entre el filtro horario y el filtro avanzado.  
  
#### <a name="to-create-a-filter"></a>Para crear un filtro  
  
1.  Abra un archivo .XEL para ver los resultados de seguimiento.  
  
    > [!NOTE]  
    >  También puede hacer clic con el botón secundario en el nombre de la sesión y, a continuación, seleccionar **observar datos en directo**.  
  
2.  En la ventana de resultados de seguimiento, seleccione los resultados que desee filtrar, y a continuación, en la barra de herramientas Eventos extendidos, haga clic en el botón **Filtros** .  
  
3.  En el cuadro de diálogo **Filtros** , seleccione **Establecer filtro de tiempo** para establecer el filtro horario arrastrando las barras deslizantes para establecer la escala de tiempo. Tenga en cuenta que al mover las barras deslizantes, el cuadro horario muestra el valor de tiempo en consecuencia. También puede especificar el tiempo en los cuadros horarios o seleccionarlo en la lista desplegable. Tenga en cuenta que al especificar el tiempo, el control deslizante horario de la izquierda se moverá en consecuencia.  
  
4.  En la sección **filtros adicionales** , aplique los criterios de filtro y, a continuación, haga clic en **aplicar**. Cuando acabe de crear el filtro, haga clic en **Aceptar**.  
  
 Un caso especial es cuando un campo de evento tiene el mismo nombre que una acción. Por ejemplo, session_id. Hay varios eventos que contienen un campo session_id y, además, podría agregarse la acción session_id. Estos dos fragmentos de información se recopilan, pero la cuadrícula de presentación del generador de perfiles Eventos extendidos usa la lógica siguiente.  
  
-   En la ventana de la cuadrícula solo se muestra una copia de la columna (session_id en este caso).  
  
-   Si existen dos campos y una acción en los datos, se muestra el valor del campo.  
  
-   Si solo existe el campo o la acción en los datos, se muestra el campo o la acción.  
  
-   Si no existe ni la acción ni el campo, se muestra NULL.  
  
##  <a name="Search"></a>Buscar texto en columnas  
  
1.  Abra un archivo .XEL para ver los resultados de seguimiento.  
  
    > [!NOTE]  
    >  También puede hacer clic con el botón secundario en el nombre de la sesión y, a continuación, seleccionar **observar datos en directo**.  
  
2.  En la barra de herramientas de eventos extendidos, haga clic en el botón **Buscar** .  
  
3.  En el cuadro de diálogo **Buscar en eventos extendidos** , en el cuadro **Buscar** , escriba el texto que desea buscar.  
  
     Puede seleccionar una de sus últimas 20 cadenas de búsqueda en la lista desplegable.  
  
4.  En el cuadro **Buscar en** , seleccione la ubicación en la que desea buscar el texto especificado en la lista desplegable. Utilice las siguientes opciones para buscar:  
  
    -   **Columnas**de la tabla. Utilice esta opción para buscar en todas las columnas visibles en la ventana de seguimiento.  
  
    -   **Detalles**. Utilice esta opción para buscar en todas las columnas (promocionadas y no promocionadas) en la ventana de seguimiento que se seleccionaron antes de abrir el cuadro **de diálogo Buscar en eventos extendidos** .  
  
    -   **Nombre de columna de evento>. \< ** Utilice esta opción para buscar en una columna de evento concreta de la lista desplegable.  
  
5.  Utilice las siguientes opciones para especificar cómo desea definir la búsqueda:  
  
    1.  **Coincidencia de mayúsculas y minúsculas**. Utilice esta opción para mostrar los resultados de la búsqueda del texto que escribió en el cuadro **Buscar** y que coincidan tanto con el contenido como con el uso de mayúsculas y minúsculas.  
  
    2.  Solo **palabras completas**. Utilice esta opción para mostrar solo los resultados de búsqueda del texto especificado cuyas palabras completas coincidan.  
  
    3.  **Buscar hacia arriba**. Utilice esta opción para buscar desde la ubicación del cursor hasta el principio de los resultados.  
  
    4.  **Use**. Utilice esta opción para interpretar los caracteres especiales y las expresiones regulares que escribió en el cuadro **Buscar** . Los caracteres especiales incluyen los caracteres comodín (*) y (?) para representar uno o más caracteres. Las expresiones regulares son notaciones especiales utilizadas para definir patrones de texto de búsqueda.  
  
6.  Haga clic en **Buscar siguiente** para buscar siguiente el texto que escribió en el cuadro **Buscar** .  
  
##  <a name="ChangeDisplay"></a>Cambiar la configuración de pantalla  
 Puede guardar la información de columna (orden de columna, columna de combinación y ancho de columna) y la información de filtro de un resultado de seguimiento en un archivo de configuración de presentación de eventos extendidos (archivo .viewsetting). Después de guardar el archivo, puede aplicarlo a los resultados de seguimiento para cambiar la vista.  
  
#### <a name="to-change-the-display-settings"></a>Para cambiar la configuración de presentación  
  
1.  Abra un archivo .XEL para ver los resultados de seguimiento.  
  
    > [!NOTE]  
    >  También puede hacer clic con el botón secundario en el nombre de la sesión y, a continuación, seleccionar **observar datos en directo**.  
  
2.  En la ventana de resultados de seguimiento, en la barra de herramientas o el menú de eventos extendidos, seleccione **Opciones de presentación**.  
  
3.  En la lista desplegable, seleccione una de las opciones siguientes:  
  
    -   **Guardar como**. Guarde la información de filtro y columnas del resultado de un seguimiento en un archivo .viewsetting.  
  
    -   **Abra**. Abra un archivo .viewsetting existente.  
  
    -   **Abrir recientes**. Abra un archivo .viewsetting guardado recientemente.  
  
  
