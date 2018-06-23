---
title: Interfaz de usuario del Diseñador de consultas SAP NetWeaver BI | Microsoft Docs
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
- "10014"
- sql12.rtp.rptdesigner.dataview.sapbwquerydesigner.f1
helpviewer_keywords:
- data sources [Reporting Services], SAP NetWeaver Business Intelligence
- SAP NetWeaver Business Intelligence [Reporting Services], query designer
- query designers [Reporting Services]
ms.assetid: 102da66e-ca31-41aa-ab4b-c9b5ab752a72
caps.latest.revision: 36
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 58b6e6d5f005e4a121afe0151b965a6e04896386
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111296"
---
# <a name="sap-netweaver-bi-query-designer-user-interface"></a>Interfaz de usuario del Diseñador de consultas SAP NetWeaver BI
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona un diseñador gráfico de consultas que permite crear consultas MDX (expresiones multidimensionales) para un origen de datos de SAP NetWeaver® Business Intelligence. El diseñador gráfico de consultas MDX tiene dos modos: modo de diseño y modo de consulta. Cada modo proporciona un panel Metadatos desde el que puede arrastrar miembros de un InfoCubo, un MultiSitio, o bien de una consulta habilitada para web definidos en el origen de datos; de esta forma, se puede crear una consulta MDX que recupera datos cuando se procesa el informe.  
  
> [!IMPORTANT]  
>  Los usuarios tienen acceso a los orígenes de datos cuando crean y ejecutan las consultas. Debe conceder permisos mínimos para los orígenes de datos, por ejemplo permisos de solo lectura.  
  
 Para más información sobre cómo trabajar con un origen de datos multidimensionales de SAP, vea [Tipo de conexión BI de SAP NetWeaver &#40;SSRS&#41;](sap-netweaver-bi-connection-type-ssrs.md).  
  
 En esta sección se describen los botones de la barra de tareas y los paneles del diseñador para cada modo del diseñador gráfico de consultas.  
  
## <a name="graphical-query-designer-in-design-mode"></a>Diseñador gráfico de consultas en modo de diseño  
 Al crear o editar una consulta de conjunto de datos que use un origen de datos de [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] , el diseñador gráfico de consultas se abre en el modo de diseño. En la siguiente ilustración se indican los nombres de los paneles del modo de diseño.  
  
 ![Diseñador de consultas que usa MDX en modo de diseño](../media/rsqd-dssapbw-mdx-designmode.gif "Diseñador de consultas que usa MDX en modo de diseño")  
  
 En la tabla siguiente, aparecen los paneles de este modo.  
  
|Panel|Función|  
|----------|--------------|  
|Botón Selección de cubo|Muestra el InfoCubo, el MultiSitio o la consulta habilitada para web seleccionados actualmente.|  
|Panel Metadatos|Muestra una lista jerárquica de InfoCubos, MultiSitios y consultas. Las consultas creadas en el origen de datos pueden aparecer bajo el cubo correspondiente.|  
|Panel Miembros calculados|Muestra los miembros calculados definidos actualmente que se encuentran disponibles para utilizarse en la consulta.|  
|Panel Datos|Muestra los resultados de la ejecución de la consulta.|  
  
 Puede arrastrar las dimensiones y las cifras clave desde el panel Metadatos, y los miembros calculados desde el panel Miembros calculados al panel Datos. Si el botón de alternancia **Ejecución automática** de la barra de herramientas está activado, el diseñador de consultas ejecuta la consulta cada vez que coloque un objeto en el panel Datos. Si **Ejecución automática** está desactivado, el diseñador de consultas no ejecuta la consulta cuando realice cambios en el panel Datos. Puede ejecutar la consulta manualmente mediante el botón **Ejecutar** de la barra de herramientas.  
  
### <a name="toolbar-for-the-graphical-query-designer-in-design-mode-toolbar"></a>Barra de herramientas del diseñador gráfico de consultas en la barra de herramientas del modo de diseño  
 La barra de herramientas del diseñador de consultas proporciona botones que le ayudan a diseñar consultas MDX mediante la interfaz gráfica. En la tabla siguiente, se describen los botones y sus funciones.  
  
|Botón|Descripción|  
|------------|-----------------|  
|**Editar como texto**|Alterna entre el diseñador de consultas basado en texto y el diseñador gráfico de consultas. No está disponible para este tipo de origen de datos.|  
|**Importar**|Importa una consulta existente desde un archivo de definición de informe (.rdl) del sistema de archivos. Para más información, vea [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|  
|![Actualizar campos del conjunto de datos](../media/rsqdicon-refreshfields.gif "Actualizar campos del conjunto de datos")|Actualiza los metadatos desde el origen de datos.|  
|![Agregar miembro calculado](../../analysis-services/media/rsqdicon-addcalculatedmember.gif "Agregar miembro calculado")|Muestra el cuadro de diálogo **Generador de miembros calculados** .|  
|![Alternar para mostrar celdas vacías](../../analysis-services/media/rsqdicon-showemptycells.gif "Alternar para mostrar celdas vacías")|Muestra y oculta las celdas vacías del panel Datos. Esto equivale a utilizar la cláusula NON EMPTY en MDX.|  
|![Ejecutar la consulta automáticamente](../../analysis-services/media/rsqdicon-autoexecute.gif "Ejecutar la consulta automáticamente")|Ejecuta automáticamente la consulta y muestra el resultado cada vez que se realice un cambio, por ejemplo al eliminar una columna en el panel Datos. Los resultados se mostrarán en el panel Datos.|  
|![Eliminar](../../analysis-services/media/rsqdicon-delete.gif "eliminar")|Elimina la columna seleccionada en el panel Datos de la consulta.|  
|![Icono del cuadro de diálogo Parámetros de consulta](../../analysis-services/media/iconqueryparameter.gif "Icono del cuadro de diálogo Parámetros de consulta")|Muestra el cuadro de diálogo **Variables** . Este botón se habilita solo cuando el cubo seleccionado es un cubo de consulta; únicamente los cubos de consulta admiten variables. Al asignar un valor predeterminado a una variable, se crea un parámetro de informe correspondiente.|  
|![Ejecutar la consulta](../../analysis-services/media/rsqdicon-run.gif "Ejecutar la consulta")|Ejecuta la consulta y muestra los resultados en el panel Datos.|  
|![Cancelar la consulta](../../analysis-services/media/rsqdicon-cancel.gif "Cancelar la consulta")|Cancela la consulta.|  
|![Cambiar al modo de diseño](../../analysis-services/media/rsqdicon-designmode.gif "Cambiar al modo de diseño")|Alterna el modo de diseño y el modo de consulta.|  
  
## <a name="graphical-query-designer-in-query-mode"></a>Diseñador gráfico de consultas en modo de consulta  
 Para cambiar el diseñador gráfico de consultas al modo de consulta, haga clic en el botón de alternancia **Modo de diseño** de la barra de herramientas.  
  
 En la siguiente ilustración se indican las partes del diseñador de consultas en el modo de consulta.  
  
 ![Diseñador de consultas SAP BW MDX en vista de consulta](../media/rsqd-dssapbw-mdx-querymode.gif "Diseñador de consultas SAP BW MDX en vista de consulta")  
  
 En la siguiente tabla se describe la función de cada panel.  
  
|Panel|Función|  
|----------|--------------|  
|Botón Selección de cubo|Muestra el InfoCubo, el MultiSitio u otro cubo seleccionados actualmente.|  
|Panel Metadatos/Funciones|Muestra una ventana con pestañas que muestra una lista de metadatos o funciones disponibles para utilizarse en la creación de texto de consulta.|  
|Panel Variables|Muestra las variables definidas actualmente que se encuentran disponibles para utilizarse en la consulta.|  
|Panel de consulta|Muestra el texto de consulta actual.|  
|Panel Resultado|Muestra los resultados de la consulta.|  
  
 En el panel Metadatos, puede arrastrar dimensiones y cifras clave desde la pestaña **Metadatos** hasta el panel Consulta MDX; el nombre técnico de los metadatos se inserta en el cursor. Puede arrastrar funciones desde la pestaña **Funciones** hasta el panel Consulta MDX. Cuando ejecute la consulta, en el panel Resultado se mostrarán los resultados de la consulta MDX actual.  
  
 Si el cubo seleccionado es una consulta habilitada para web, se le pedirá que establezca valores predeterminados estáticos para las variables existentes. A continuación, podrá arrastrar variables al panel Consulta MDX.  
  
 Los paneles Metadatos y Variables muestran nombres sencillos. Al colocar los objetos en el panel Consulta MDX, verá los nombres técnicos que necesita el origen de datos insertado en la consulta MDX.  
  
### <a name="toolbar-for-the-graphical-query-designer-in-query-mode"></a>Barra de herramientas del diseñador gráfico de consultas en el modo de consulta  
 La barra de herramientas del diseñador de consultas proporciona botones que le ayudan a diseñar consultas MDX mediante la interfaz gráfica. Los botones de la barra de herramientas son idénticos en los modos de diseño y de consulta. Sin embargo, los siguientes botones no están habilitados para el modo de consulta:  
  
-   **Editar como texto**  
  
-   **Agregar miembro calculado** (![Agregar miembro calculado](../../analysis-services/media/rsqdicon-addcalculatedmember.gif "Agregar miembro calculado"))  
  
-   **Mostrar celdas vacías** (![Alternar para mostrar celdas vacías](../../analysis-services/media/rsqdicon-showemptycells.gif "Alternar para mostrar celdas vacías"))  
  
-   **Ejecución automática** (![Ejecutar la consulta automáticamente](../../analysis-services/media/rsqdicon-autoexecute.gif "Ejecutar la consulta automáticamente"))  
  
-   **Eliminar** (![eliminar](../../analysis-services/media/rsqdicon-delete.gif "eliminar"))  
  
## <a name="see-also"></a>Vea también  
 [Crear un conjunto de datos compartido o un conjunto de datos incrustado &#40;Generador de informes y SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)   
 [Archivo de configuración RSReportDesigner](../report-server/rsreportdesigner-configuration-file.md)  
  
  