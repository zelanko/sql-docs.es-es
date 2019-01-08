---
title: Vista de diseño de informe (Generador de informes) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10440"
- "10426"
- "10439"
- "10434"
- "10438"
- "10436"
helpviewer_keywords:
- reports, creating
- user interface
- overview of Report Builder
ms.assetid: 1544472c-2803-448d-af52-e901cb457a00
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: b052ccbd1b91ea66f150dc0995eeeb33994a5e53
ms.sourcegitcommit: 60739bcb48ccce17bca4e11a85df443e93ca23e3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52439527"
---
# <a name="report-design-view-report-builder"></a>Vista de diseño de informe (Generador de informes)
  La ventana del Generador de informes está diseñada para ayudarle a organizar con facilidad sus recursos de informes y a generar rápidamente los informes que necesita. La superficie de diseño está en el centro de la ventana, con la Cinta de opciones arriba y los paneles Datos de informe, Agrupación y Propiedades y la Galería de elementos de informe a la izquierda, abajo y a la derecha. La superficie de diseño es donde agrega y organiza sus elementos de informe. La Cinta de opciones organiza los elementos de menú tradicionales en categorías que puede buscar y utilizar con facilidad. Los paneles le ayudan a agregar, seleccionar y organizar sus recursos de informe y a cambiar las propiedades de los elementos de informe.  
  
 ![ReportDesignView](../media/reportdesignview.gif "ReportDesignView")  
  
##  <a name="Ribbon"></a> Cinta de opciones  
 La cinta de opciones está diseñada para ayudarle a buscar rápidamente los comandos que necesita para completar una tarea. Los comandos están organizados en grupos lógicos, que se recopilan juntos en las pestañas. Cada pestaña se relaciona con un tipo de actividad; por ejemplo, insertar los elementos de informe o dar formato al texto.  
  
 En la vista de diseño del informe, la cinta de opciones se divide en las siguientes pestañas: Inicio, insertar y vista. Si no encuentra una tarea en la cinta de opciones, algunos grupos de la cinta de opciones tienen un cuadro de diálogo relacionado que puede abrir haciendo clic en la flecha en el lado inferior derecho del grupo. No puede minimizar o eliminar la cinta de opciones ni reemplazarla con barras de herramientas y menús.  
  
 En modo de ejecución, la cinta de opciones tiene solo una pestaña, **ejecutar**.  
  
### <a name="home-tab"></a>Pestaña Inicio  
 La pestaña Inicio es una colección de comandos de uso frecuente, centrados en la apariencia de los elementos dentro del informe. En la pestaña Inicio, puede tener acceso a los comandos ejecutar, fuente, párrafo, borde, número y diseño. Al hacer clic en un elemento en la pestaña, cambia el elemento seleccionado en la superficie de diseño. Al hacer clic en **ejecutar**, el informe se representa en HTML para que pueda ver cómo aparecerá el contenido del informe cuando publica y vea la pestaña ejecutar en lugar de la pestaña Inicio. La pestaña Inicio es la pestaña predeterminada que se muestra al crear un informe por primera vez.  
  
### <a name="insert-tab"></a>Pestaña Insertar  
 La pestaña Insertar es una colección de comandos usados con frecuencia para agregar elementos al informe. En la pestaña Insertar, puede usar un los asistentes para agregar una tabla, una matriz, un gráfico o un mapa. También puede agregar estos elementos sin usar un asistente, y agregar otros elementos de informe como minigráficos, indicadores, cuadros de texto, imágenes, líneas, rectángulos, subinformes, encabezados del informe y pies de página.  
  
 Al hacer clic en **elementos de informe** en la instrucción Insert ficha abre la Galería de elementos de informe. Puede buscar elementos de informe guardados en un servidor de informes. Para más información, vea [Elementos de informe &#40;Generador de informes y SSRS&#41;](../report-parts-report-builder-and-ssrs.md).  
  
 Después de insertar un elemento, el Generador de informes vuelve a cambiar automáticamente a la pestaña Inicio.  
  
### <a name="view-tab"></a>Pestaña Vista  
 La pestaña Vista es una colección de comandos que controlan lo que se muestra dentro de la ventana del Generador de informes. Puede cambiar las opciones de presentación de la regla y los paneles Agrupar, Datos de informe y Propiedades.  
  
### <a name="run-tab"></a>Pestaña Ejecutar  
 Al hacer clic en **ejecutar** en la pestaña Inicio, ejecutar una vista previa del informe en el Visor HTML y vea la pestaña ejecutar en lugar de la pestaña Inicio.  
  
 La pestaña Ejecutar contiene una colección de comandos que puede usar una vez representado el informe. Puede imprimir el informe, navegar por las páginas del informe, exportar el informe a otro formato de archivo, ver el mapa del documento o los parámetros (si el informe los tiene) y buscar elementos dentro del informe. Para obtener más información, consulte [vista previa del informe en modo de ejecución](#RunMode).  
  
 Para volver a la vista de diseño de informes en el **ejecutar** , haga clic **diseño**.  
  
  
##  <a name="RptDesignSurface"></a> Superficie de diseño del informe  
 La superficie de diseño de informe del Generador de informes es el área de trabajo principal para diseñar informes. Para colocar en su informe los elementos de informe, como regiones de datos, subinformes, cuadros de texto, imágenes, rectángulos y líneas, agréguelos desde la cinta de opciones o la galería de elementos de informe a la superficie de diseño. Ahí puede agregar grupos, expresiones, parámetros, filtros, acciones, visibilidad y formato a sus elementos de informe.  
  
 También puede cambiar lo siguiente:  
  
-   Las propiedades del cuerpo del informe, como el borde y el color de relleno, haciendo clic con el botón derecho en el área blanca de la superficie de diseño, fuera de cualquier elemento de informe, y haciendo clic, después, en **Propiedades del cuerpo**.  
  
-   Las propiedades del encabezado y el pie de página, como el borde y el color de relleno, haciendo clic con el botón derecho en el área blanca de la superficie de diseño en el área de encabezado o de pie de página, fuera de cualquier elemento de informe, y haciendo clic en **Propiedades de encabezado** o **Propiedades de pie de página**.  
  
-   Las propiedades del propio informe, como la configuración de página, haciendo clic en el área azul que rodea la superficie de diseño y haga clic en **propiedades del informe**.  
  
-   Las propiedades de los elementos de informe, haciendo clic con el botón derecho en ellos y, después, haciendo clic en **Propiedades**.  
  
> [!NOTE]  
>  Si arrastra directamente un campo del panel Datos de informe a la superficie de diseño del informe en lugar de colocarlo en una región de datos, como una tabla o un gráfico, al ejecutar el informe, verá solo el primer valor de los datos en ese campo.  
  
 Para información sobre cómo usar el teclado para manipular los elementos en la superficie de diseño, vea [Métodos abreviados de teclado &#40;Generador de informes&#41;](keyboard-shortcuts-report-builder.md).  
  
### <a name="design-surface-size-and-print-area"></a>Tamaño de la superficie de diseño y del área de impresión  
 El tamaño de la superficie de diseño puede ser diferente del área de impresión del tamaño de página que especifique para imprimir el informe. El cambio del tamaño de la superficie de diseño no cambiará el área de impresión de su informe. Con independencia del tamaño que establezca para el área de impresión de su informe, el tamaño del área de diseño completa no cambia. Para más información, vea [Comportamientos de la representación &#40;Generador de informes y SSRS&#41;](../report-design/rendering-behaviors-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  Para mostrar la regla, en la pestaña **Ver** active la casilla **Regla**.  
  
  
##  <a name="ReptDataPane"></a> The Report Data Pane  
 En el panel Datos de informe, podrá definir los recursos y los datos de informe que necesita para un informe antes de diseñarlo. Por ejemplo, puede agregar orígenes de datos, conjuntos de datos, campos calculados, parámetros de informe e imágenes al panel Datos de informe.  
  
 Cuando agregue elementos al panel Datos de informe, arrástrelos hasta la superficie de diseño para controlar dónde aparecerán en el informe.  
  
 También podrá arrastrar campos integrados desde el panel Datos de informe hasta la superficie de diseño del informe. Cuando se representan, estos campos proporcionan información acerca del informe, como el nombre del informe, el número total de páginas y el número de la página actual.  
  
 Algunas cosas se agregan automáticamente al panel Datos de informe al agregar algo a la superficie de diseño del informe. Por ejemplo, si agrega un elementos de informe desde la galería de elementos de informe, y el elementos de informe es una región de datos, el conjunto de datos se agrega automáticamente al panel Datos de informe. Para obtener más información, vea [Elementos de informe y conjuntos de datos en el Generador de informes](../report-data/report-parts-and-datasets-in-report-builder.md). También, si incrusta una imagen en el informe, se agregará a la carpeta Imágenes del panel Datos de informe.  
  
> [!NOTE]  
>  Puede usar el botón **Nuevo** para agregar un nuevo elemento al panel Datos de informe. Puede agregar al informe varios conjuntos de datos del mismo origen de datos o de otros orígenes de datos. Puede agregar conjuntos de datos compartidos del servidor de informes. Para agregar un nuevo conjunto de datos desde el mismo origen de datos, haga clic con el botón derecho en un origen de datos y, después, haga clic en **Agregar conjunto de datos**.  
  
 Para obtener más información acerca de los elementos del panel Datos de informe, vea los siguientes temas:  
  
-   [Referencias a campos globales y de usuario integrados &#40;Generador de informes y SSRS&#41;](../report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md)  
  
-   [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)  
  
-   [Imágenes &#40;Generador de informes y SSRS&#41;](../report-design/images-report-builder-and-ssrs.md)  
  
-   [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
  
-   [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](../report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
  
-   [Colección Campos del conjunto de datos &#40;Generador de informes y SSRS&#41;](../report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
  
  
##  <a name="ReptPartGallery"></a> Galería de elementos de informe  
 La manera más fácil de crear un informe es encontrar un elemento de informe existente, como una tabla o un gráfico, en el servidor de informes o en un servidor de informes integrado en un sitio de SharePoint. Puede buscar elementos de informe en la galería de elementos de informe para agregarlos a un informe. Puede filtrar los elementos de informe por el nombre completo o solo parte de él, quién lo ha creado, quién lo ha modificado por última vez, cuándo se modificó por última vez, dónde está almacenado, o bien el tipo de elemento de informe. Por ejemplo, podría buscar todos los gráficos creados la semana pasada por uno de sus colaboradores.  
  
> [!NOTE]  
>  Debe estar conectado a un servidor de informes para poder ver la galería de elementos de informe.  
  
 Puede ver los resultados de la búsqueda como miniaturas o como lista, y ordenar los resultados de la búsqueda por nombre, fechas de creación y modificación, y autor. Para más información, vea [Elementos de informe &#40;Generador de informes y SSRS&#41;](../report-parts-report-builder-and-ssrs.md).  
  
  
##  <a name="PropertiesPane"></a> Panel Propiedades (Generador de informes)  
 Todos los elementos de un informe, como el cuerpo mismo del informe, las regiones de datos, las imágenes y los cuadros de texto, tienen propiedades asociadas. Por ejemplo, la propiedad BorderColor de un cuadro de texto muestra el valor de color del borde del cuadro de texto y la propiedad PageSize del informe muestra el tamaño de página del informe.  
  
 Estas propiedades se muestran en el panel de propiedades. Las propiedades del panel cambian en función del elemento de informe que seleccione.  
  
 Para ver el panel de propiedades, en la pestaña Vista, en el grupo Mostrar u ocultar, haga clic en Propiedades.  
  
### <a name="changing-property-values"></a>Cambiar valores de propiedad  
 En el Generador de informes, puede cambiar las propiedades de los elementos de informe de varias maneras:  
  
-   Haciendo clic en los botones y listas de la cinta de opciones.  
  
-   Cambiando los valores de configuración de los cuadros de diálogo.  
  
-   Cambiando los valores de propiedad del panel de propiedades.  
  
 Las propiedades que se utilizan con más frecuencia están disponibles en los cuadros de diálogo y en la cinta de opciones.  
  
 En función de la propiedad, puede establecer un valor de propiedad desde una lista desplegable, escribir el valor o hacer clic en `<Expression>` para crear una expresión.  
  
### <a name="changing-the-properties-pane-view"></a>Cambiar la vista del panel de propiedades  
 De manera predeterminada, las propiedades que se muestran en el panel de propiedades se organizan en amplias categorías como Acción, Borde, Relleno, Fuente y General. Cada una de esas categorías cuenta con un conjunto de propiedades asociadas. Por ejemplo, las siguientes propiedades se muestran dentro de la categoría fuente: Color, FontFamily, FontSize, FontStyle, FontWeight, LineHeight y TextDecoration. Si lo prefiere, puede ordenar alfabéticamente todas las propiedades enumeradas en el panel. De esta manera se quitan las categorías y se enumeran todas las propiedades en orden alfabético independientemente de la categoría.  
  
 El panel de propiedades tiene tres botones en la parte superior del panel: Categoría, ordenar alfabéticamente y las páginas de propiedades. Haga clic en los botones de categoría y alfabetización para cambiar entre las diferentes vistas del panel de propiedades. Haga clic en el botón de **páginas de propiedades** para abrir el cuadro de diálogo de propiedades de un elemento de informe seleccionado.  
  
  
##  <a name="GroupPane"></a> Panel Agrupación (Generador de informes)  
 Los grupos se utilizan para organizar los datos del informe en una jerarquía visual y calcular los totales. Puede ver los grupos de filas y columnas dentro de una región de datos en la superficie de diseño y también en el Panel de agrupación. El panel de agrupación tiene dos paneles: Grupos de filas y grupos de columnas. Al seleccionar una región de datos, el panel Agrupación muestra todos los grupos dentro de dicha región de datos como una lista jerárquica: Los grupos secundarios aparecen con sangría aplicados bajo los grupos primarios.  
  
 ![Panel de agrupación para grupos de filas y columnas anidadas](../media/rs-basictablixdesigngroupingpanedefaultview.gif "Panel de agrupación para grupos de filas y columnas anidadas")  
  
 Para crear grupos, arrastre los campos desde el panel Datos de informe y suéltelos en la superficie de diseño o en el Panel de agrupación. En el Panel de agrupación, puede agregar grupos primarios, adyacentes o secundarios, cambiar propiedades de grupo y eliminar grupos.  
  
 El Panel de agrupación se muestra de manera predeterminada, pero puede cerrarlo si deshabilita la casilla del panel en la pestaña Vista. El panel de agrupación no está disponible para las regiones de datos Gráfico o Medidor.  
  
 Para obtener más información, vea [Panel de agrupación &#40;Generador de informes&#41;](../report-design/grouping-pane-report-builder.md) y [Descripción de los grupos &#40;Generador de informes y SSRS&#41;](../report-design/understanding-groups-report-builder-and-ssrs.md).  
  
  
##  <a name="RunMode"></a> Vista previa del informe en modo de ejecución  
 En la vista de diseño del informe, no se trabaja con los datos reales, sino con una representación de los datos que viene indicada por el nombre de campo o de expresión. Cuando quiera ver los datos reales mostrados en el contexto del informe que diseñó, puede ejecutar el informe para obtener una vista previa de los datos desde la base de datos subyacente mostrada en el diseño del informe. Cambiar entre el diseño y la ejecución del informe le permite ajustar su diseño y ver los resultados de forma inmediata. Para obtener una vista previa del informe, haga clic en **ejecutar** en el **vistas** grupo en la cinta de opciones.  
  
 Al hacer clic en **Ejecutar**, el Generador de informes se conecta con los orígenes de datos del informe, almacena en memoria caché los datos del equipo, combina los datos y el diseño y, a continuación, representa el informe en el Visor HTML. Puede ejecutar el informe con la frecuencia que desee mientras continúa diseñándolo. Cuando esté satisfecho con el informe, puede guardarlo en el servidor de informes, donde podrán verlo otros usuarios que tengan los permisos adecuados.  
  
### <a name="running-a-report-with-parameters"></a>Ejecutar un informe con parámetros  
 Al ejecutar su informe, se procesa automáticamente. Si el informe contiene parámetros, todos ellos deben tener los valores predeterminados antes de que el informe se pueda ejecutar automáticamente. Si un parámetro no tiene un valor predeterminado, al ejecutar el informe necesita elegir un valor para ese parámetro y, a continuación, hacer clic en **Ver informe** en la pestaña Ejecutar. Para obtener más información, vea [Report Parameters &#40;Report Builder and Report Designer&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
### <a name="print-preview"></a>Vista previa de impresión  
 La vista previa de un informe en modo de ejecución se parece a un informe generado en HTML. La vista previa no es HTML, pero el diseño y la paginación del informe son similares a la salida con formato HTML. Para cambiar la vista de manera que represente un informe impreso, cambie al modo de vista previa de impresión. Haga clic en el botón **Vista previa de impresión** en la pestaña **Ejecutar** . El informe se mostrará como si estuviera en una página física. Esta vista se asemeja a la salida que se obtiene mediante las extensiones de representación en imágenes y en PDF. La vista previa de impresión no es un archivo de imagen ni un archivo PDF, pero el diseño y la paginación del informe son similares al resultado de estos formatos.  
  
  
## <a name="see-also"></a>Vea también  
 [Buscar, ver y administrar informes &#40;Generador de informes y SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Generador de informes en SQL Server 2014](report-builder-in-sql-server-2016.md)  
  
  
