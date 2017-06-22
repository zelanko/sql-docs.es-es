---
title: "Interfaz de usuario del Diseñador de Hyperion Essbase consulta | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10013"
- sql13.rtp.rptdesigner.dataview.hyperionessbasequerydesigner.f1
helpviewer_keywords:
- Hyperion Essbase Query Designer
- data sources [Reporting Services], Hyperion Essbase
- multidimensional data [Reporting Services]
- query designers [Reporting Services]
- Hyperion Essbase [Reporting Services], query designer
ms.assetid: bc91b422-c6ab-4062-a300-8290fae6191b
caps.latest.revision: 23
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 68a0a5da224c0f6f78eca8df1ae766e85d7750f2
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="hyperion-essbase-query-designer-user-interface"></a>Interfaz de usuario del Diseñador de consultas de Hyperion Essbase
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona un diseñador gráfico de consultas que permite crear consultas MDX (expresiones multidimensionales) para un origen de datos de [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] . El diseñador gráfico de consultas MDX tiene dos modos: modo de diseño y modo de consulta. Cada modo proporciona un panel de metadatos desde el que puede arrastrar miembros de un cubo definido en el origen de datos para crear una consulta MDX que recupere datos cuando se procese el informe.  
  
> [!IMPORTANT]  
>  Los usuarios tienen acceso a los orígenes de datos cuando crean y ejecutan las consultas. Debe conceder permisos mínimos para los orígenes de datos, por ejemplo permisos de solo lectura.  
  
 Para más información sobre cómo trabajar con un origen de datos multidimensionales de [!INCLUDE[extEssbase](../../includes/extessbase-md.md)], vea [Tipo de conexión Hyperion Essbase &#40;SSRS&#41;](../../reporting-services/report-data/hyperion-essbase-connection-type-ssrs.md).  
  
 En esta sección se describen los botones de la barra de tareas y los paneles del diseñador para cada modo del diseñador gráfico de consultas.  
  
## <a name="graphical-query-designer-in-design-mode"></a>Diseñador gráfico de consultas en modo de diseño  
 Al editar una consulta MDX para un conjunto de datos que usa un origen de datos de [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] , el diseñador gráfico de consultas se abre en el modo de diseño.  
  
 En la siguiente ilustración se indican los nombres de los paneles del modo de diseño.  
  
 ![Diseñador de consultas para el origen de datos de Hyperion Essbase](../../reporting-services/report-data/media/rsqd-dshyperionessbase-mdx-designmode.gif "Diseñador de consultas para el origen de datos de Hyperion Essbase")  
  
 En la tabla siguiente, aparecen los paneles de este modo.  
  
|Panel|Función|  
|----------|--------------|  
|Botón Selección de cubo|Muestra el cubo seleccionado actualmente.|  
|Panel Metadatos|Muestra una lista jerárquica de cubos.|  
|Panel Miembros calculados|Muestra los miembros calculados definidos actualmente que se encuentran disponibles para utilizarse en la consulta.|  
|Panel Filtro|Muestra los filtros que se van a aplicar a la consulta.|  
|Panel Datos|Muestra los resultados de la ejecución de la consulta.|  
  
 Puede arrastrar dimensiones y medidas desde el panel Metadatos, y miembros calculados desde el panel Miembros calculados hasta el panel Datos. Si el botón de alternancia **Ejecución automática** de la barra de herramientas está activado, el diseñador de consultas ejecuta la consulta cada vez que coloque un objeto en el panel Datos. Si **Ejecución automática** está desactivado, el diseñador de consultas no ejecuta la consulta cuando realice cambios en el panel Datos. Puede ejecutar la consulta manualmente mediante el botón **Ejecutar** de la barra de herramientas.  
  
 En el panel Filtro, puede seleccionar valores de dimensión para limitar los datos recuperados desde el origen de datos. Los valores que defina en el modo de diseño aparecerán en la cláusula WHERE de MDX en el modo de consulta.  
  
### <a name="toolbar-for-the-graphical-query-designer-in-design-mode-toolbar"></a>Barra de herramientas del diseñador gráfico de consultas en la barra de herramientas del modo de diseño  
 La barra de herramientas del diseñador de consultas proporciona botones que le ayudan a diseñar consultas MDX mediante la interfaz gráfica. En la tabla siguiente se muestran los botones y se describen sus funciones.  
  
|Botón|Description|  
|------------|-----------------|  
|**Editar como texto**|Alterna entre el diseñador de consultas basado en texto y el diseñador gráfico de consultas. No está disponible para este tipo de origen de datos.|  
|**Importar**|Importa una consulta existente desde un archivo de definición de informe (.rdl) del sistema de archivos. Para obtener más información, vea [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|  
|![Actualizar los campos de conjunto de datos](../../reporting-services/report-data/media/rsqdicon-refreshfields.gif "actualizar los campos de conjunto de datos")|Actualiza los metadatos desde el origen de datos.|  
|![Add calculated member](../../reporting-services/report-data/media/rsqdicon-addcalculatedmember.gif "Add calculated member")|Muestra el cuadro de diálogo **Generador de miembros calculados** . Use este cuadro de diálogo para crear o editar expresiones para un miembro calculado, incluido el establecimiento de la propiedad **Orden de resolución** .|  
|![Alternar para mostrar celdas vacías](../../reporting-services/report-data/media/rsqdicon-showemptycells.gif "alternar para mostrar celdas vacías")|Muestra y oculta las celdas vacías del panel Datos. Esto equivale a utilizar la cláusula NON EMPTY en MDX.|  
|![Ejecutar la consulta automáticamente](../../reporting-services/report-data/media/rsqdicon-autoexecute.gif "ejecutar la consulta automáticamente")|Ejecuta automáticamente la consulta y muestra el resultado cada vez que se realice un cambio, por ejemplo al eliminar una columna en el panel Datos. Los resultados se mostrarán en el panel Datos.|  
|![Eliminar](../../reporting-services/report-data/media/rsqdicon-delete.gif "Eliminar")|Elimina el elemento seleccionado de la consulta. Use este botón para eliminar las filas seleccionadas en el panel Filtro.|  
|![Ejecute la consulta](../../reporting-services/report-data/media/rsqdicon-run.gif "ejecutar la consulta")|Ejecuta la consulta y muestra los resultados en el panel Datos.|  
|![Cancelar la consulta](../../reporting-services/report-data/media/rsqdicon-cancel.gif "cancelar la consulta")|Cancela la consulta.|  
|![Cambiar al modo de diseño](../../reporting-services/media/rsqdicon-designmode.gif "cambiar al modo de diseño")|Alterna el modo de diseño y el modo de consulta.|  
  
## <a name="graphical-query-designer-in-query-mode"></a>Diseñador gráfico de consultas en modo de consulta  
 Para cambiar el diseñador gráfico de consultas al modo de consulta, haga clic en el botón de alternancia **Modo de diseño** de la barra de herramientas. En la siguiente ilustración se indican las partes del diseñador de consultas en el modo de consulta.  
  
 ![Diseñador de consultas en modo de consulta para Hyperion](../../reporting-services/report-data/media/rsqd-hyperionessbase-mdx-querymode.gif "Diseñador de consultas en modo de consulta para Hyperion")  
  
 En la siguiente tabla se describe la función de cada panel.  
  
|Panel|Función|  
|----------|--------------|  
|Botón Selección de cubo|Muestra el cubo seleccionado actualmente.|  
|Panel Metadatos/Funciones|Muestra una ventana con pestañas que muestra una lista de metadatos o funciones disponibles para utilizarse en la creación de texto de consulta.|  
|Panel de consulta|Muestra el texto de consulta actual.|  
|Panel Resultado|Muestra los resultados de la consulta.|  
  
 En el panel Metadatos, puede arrastrar medidas y dimensiones desde la pestaña **Metadatos** hasta el panel Consulta MDX. Puede arrastrar funciones desde la pestaña **Funciones** hasta el panel Consulta MDX. Cuando ejecute la consulta, en el panel Resultado se mostrarán los resultados de la consulta MDX actual.  
  
### <a name="toolbar-for-the-graphical-query-designer-in-query-mode"></a>Barra de herramientas del diseñador gráfico de consultas en el modo de consulta  
 La barra de herramientas del diseñador de consultas proporciona botones que le ayudan a diseñar consultas MDX mediante la interfaz gráfica. Los botones de la barra de herramientas son idénticos en los modos de diseño y de consulta. Sin embargo, los siguientes botones no están habilitados para el modo de consulta:  
  
-   **Editar como texto**  
  
-   **Agregar miembro calculado** (![Add calculated member](../../reporting-services/report-data/media/rsqdicon-addcalculatedmember.gif "Add calculated member"))  
  
-   **Mostrar celdas vacías** (![alternar para mostrar celdas vacías](../../reporting-services/report-data/media/rsqdicon-showemptycells.gif "alternar para mostrar celdas vacías"))  
  
-   **Ejecución automática** (![ejecutar la consulta automáticamente](../../reporting-services/report-data/media/rsqdicon-autoexecute.gif "ejecutar la consulta automáticamente"))  
  
## <a name="see-also"></a>Vea también  
 [Crear un conjunto de datos compartido o un conjunto de datos incrustado &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [Archivo de configuración RSReportDesigner](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)  
  
  
