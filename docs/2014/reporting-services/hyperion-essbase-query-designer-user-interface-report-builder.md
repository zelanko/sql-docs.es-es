---
title: Interfaz de usuario del Diseñador de Hyperion Essbase consulta (generador de informes) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- "10013"
helpviewer_keywords:
- Hyperion Essbase query designer
- query designers, Hyperion
ms.assetid: d89a6773-dbe5-48e5-bda9-db0e67100696
caps.latest.revision: 13
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 27dd20fae08317cd58fd9ca9b5084fda000906c3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112898"
---
# <a name="hyperion-essbase-query-designer-user-interface-report-builder"></a>Interfaz de usuario del Diseñador de consultas de Hyperion Essbase (Generador de informes)
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] proporciona un diseñador gráfico de consultas que permite crear consultas MDX (expresiones multidimensionales) para un origen de datos de [!INCLUDE[extEssbase](../includes/extessbase-md.md)]. El diseñador gráfico de consultas MDX tiene dos modos: modo de diseño y modo de consulta. Cada modo proporciona un panel de metadatos desde el que puede arrastrar miembros de un cubo definido en el origen de datos para crear una consulta MDX que recupere datos cuando se procese el informe.  
  
> [!IMPORTANT]  
>  Los usuarios tienen acceso a los orígenes de datos cuando crean y ejecutan las consultas. Debe conceder permisos mínimos para los orígenes de datos, por ejemplo permisos de solo lectura.  
  
 En esta sección se describen los botones de la barra de tareas y los paneles del diseñador para cada modo del diseñador gráfico de consultas.  
  
## <a name="graphical-query-designer-in-design-mode"></a>Diseñador gráfico de consultas en modo de diseño  
 Al editar una consulta MDX para un conjunto de datos que utiliza un [!INCLUDE[extEssbase](../includes/extessbase-md.md)] origen de datos, el diseñador gráfico de consultas se abre en modo de diseño. En la siguiente ilustración se indican los nombres de los paneles del modo de diseño.  
  
 ![Diseñador de consultas para el origen de datos de Hyperion Essbase](media/rsqd-dshyperionessbase-mdx-designmode.gif "Diseñador de consultas para el origen de datos de Hyperion Essbase")  
  
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
  
|Botón|Descripción|  
|------------|-----------------|  
|**Editar como texto**|Alterna entre el diseñador de consultas basado en texto y el diseñador gráfico de consultas. No está disponible para este tipo de origen de datos.|  
|**Importar**|Importa una consulta existente desde un archivo de definición de informe (.rdl) del sistema de archivos.|  
|![Actualizar campos del conjunto de datos](media/rsqdicon-refreshfields.gif "Actualizar campos del conjunto de datos")|Actualiza los metadatos desde el origen de datos.|  
|![Agregar miembro calculado](../analysis-services/media/rsqdicon-addcalculatedmember.gif "Agregar miembro calculado")|Muestra el cuadro de diálogo **Generador de miembros calculados** . Use este cuadro de diálogo para crear o editar expresiones para un miembro calculado, incluido el establecimiento de la propiedad **Orden de resolución** .|  
|![Alternar para mostrar celdas vacías](../analysis-services/media/rsqdicon-showemptycells.gif "Alternar para mostrar celdas vacías")|Muestra y oculta las celdas vacías del panel Datos. Esto equivale a utilizar la cláusula NON EMPTY en MDX.|  
|![Ejecutar la consulta automáticamente](../analysis-services/media/rsqdicon-autoexecute.gif "Ejecutar la consulta automáticamente")|Ejecuta automáticamente la consulta y muestra el resultado cada vez que se realice un cambio, por ejemplo al eliminar una columna en el panel Datos. Los resultados se mostrarán en el panel Datos.|  
|![Eliminar](../analysis-services/media/rsqdicon-delete.gif "eliminar")|Elimina el elemento seleccionado de la consulta. Use este botón para eliminar las filas seleccionadas en el panel Filtro.|  
|![Ejecutar la consulta](../analysis-services/media/rsqdicon-run.gif "Ejecutar la consulta")|Ejecuta la consulta y muestra los resultados en el panel Datos.|  
|![Cancelar la consulta](../analysis-services/media/rsqdicon-cancel.gif "Cancelar la consulta")|Cancela la consulta.|  
|![Cambiar al modo de diseño](../analysis-services/media/rsqdicon-designmode.gif "Cambiar al modo de diseño")|Alterna el modo de diseño y el modo de consulta.|  
  
## <a name="graphical-query-designer-in-query-mode"></a>Diseñador gráfico de consultas en modo de consulta  
 Para cambiar el diseñador gráfico de consultas al modo de consulta, haga clic en el botón de alternancia **Modo de diseño** de la barra de herramientas.  
  
 ![Diseñador de consultas en modo de consulta para Hyperion](media/rsqd-hyperionessbase-mdx-querymode.gif "Diseñador de consultas en modo de consulta para Hyperion")  
  
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
  
-   **Agregar miembro calculado** (![Agregar miembro calculado](../analysis-services/media/rsqdicon-addcalculatedmember.gif "Agregar miembro calculado"))  
  
-   **Mostrar celdas vacías** (![Alternar para mostrar celdas vacías](../analysis-services/media/rsqdicon-showemptycells.gif "Alternar para mostrar celdas vacías"))  
  
-   **Ejecución automática** (![Ejecutar la consulta automáticamente](../analysis-services/media/rsqdicon-autoexecute.gif "Ejecutar la consulta automáticamente"))  
  
## <a name="see-also"></a>Vea también  
 [Diseñadores de consultas &#40;Generador de informes&#41;](../../2014/reporting-services/query-designers-report-builder.md)  
  
  