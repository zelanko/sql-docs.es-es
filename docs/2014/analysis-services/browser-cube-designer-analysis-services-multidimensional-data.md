---
title: Explorador (diseñador de cubos) (Analysis Services-datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.view.f1
ms.assetid: efb5ee1c-de50-4bfc-83ff-08a4f03c3ece
author: minewiskan
ms.author: owend
ms.openlocfilehash: 221f6d0c51b3c0a688a8bf3f002bfd4d31c04a45
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527791"
---
# <a name="browser-cube-designer-analysis-services---multidimensional-data"></a>Explorador (Diseñador de cubos) (Analysis Services - Datos multidimensionales)
  Utilice la pestaña **Explorador** del Diseñador de cubos para explorar las dimensiones, medidas y KPI de un cubo. En [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], el explorador de cubo de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] se ha integrado con el diseñador de consultas MDX, y proporciona una interfaz gráfica de usuario para ayudar a crear consultas MDX, filtrar y segmentar cubos y explorar en profundidad jerarquías.

 La pestaña **Explorador** tiene dos modos: **Modo de diseño** y **Modo de consulta**. En cualquiera de los modos, puede utilizar los objetos del panel **Metadatos** para explorar el cubo, o puede arrastrar miembros del panel **Metadatos** al área de consulta, para crear una consulta MDX que recupere los datos que desee usar.

 **Examinar y consultar mediante el modo de diseño gráfico**

 La ilustración siguiente muestra la interfaz de **Explorador** en **Modo de diseño**gráfico.

 ![Diseñador de consultas MDX de Analysis Services, vista de diseño](media/rsqd-dsawas-mdx-designmode.gif "Diseñador de consultas MDX de Analysis Services, vista de diseño")

 Mientras trabaja en el modo de diseño gráfico, si se selecciona el botón de alternancia **ejecución** automática (![ejecutar la consulta](media/rsqdicon-autoexecute.gif "Ejecutar la consulta automáticamente")automáticamente) en la barra de herramientas, el **Explorador** ejecuta una consulta cada vez que se coloca un objeto de metadatos en el panel datos. También puede ejecutar la consulta manualmente mediante el botón **Ejecutar consulta** (![ejecutar la consulta](media/rsqdicon-run.gif "Ejecutar la consulta")) de la barra de herramientas.

 Para cambiar el diseñador gráfico de consultas al modo **Consulta** y trabajar con el texto de las instrucciones MDX, haga clic en el botón de **Modo de diseño** en la barra de herramientas.

 **Examinar y consultar mediante el modo de texto MDX**

 Estando en modo de diseño de texto MDX, puede trabajar con MDX directamente. El panel **Metadatos** sigue estando disponible para poder agregar objetos al área de diseño de consulta, y se pueden arrastrar y colocar funciones y operadores de MDX de la lista del panel **Funciones** .

 La ilustración siguiente muestra la interfaz de **Explorador** para el modo de consulta.

 ![Diseñador de consultas MDX de Analysis Services, vista de consulta](media/rsqd-dsawas-mdx-querymode.gif "Diseñador de consultas MDX de Analysis Services, vista de consulta")

 Puede empezar a trabajar en modo de diseño gráfico, agregar los objetos necesarios, agregar filtros para segmentar el cubo y, a continuación, cambiar al modo de texto para extender la consulta MDX predeterminada que se generó e incluir propiedades de celda y propiedades de miembro adicionales.

 El panel **Metadatos** muestra pestañas para **Metadatos** y **Funciones**. Desde la pestaña **Metadatos** , puede arrastrar dimensiones, jerarquías, KPI y medidas al área de diseño de consulta. Desde la pestaña **Funciones** , puede arrastrar funciones al área de diseño de la consulta. Cuando ejecute la consulta, el área de diseño de consulta mostrará los resultados de la consulta MDX. También puede hacer clic en **Analizar en Excel** , en la **Barra de herramientas** , para exportar los datos a Microsoft Office Excel y ver los resultados tal y como los verían los usuarios, en una tabla dinámica. En las secciones siguientes se describe con más detalle la barra de herramientas y todos los recuadros de cada modo del **Explorador** .

 Tenga en cuenta que, mientras trabaja en modo de texto, el botón de alternancia **ejecución** automática (![ejecutar la consulta](media/rsqdicon-autoexecute.gif "Ejecutar la consulta automáticamente")automáticamente) de la barra de herramientas no está disponible. Sin embargo, puede ejecutar consultas manualmente mediante el botón **Ejecutar consulta** (![ejecutar la consulta](media/rsqdicon-run.gif "Ejecutar la consulta")) de la barra de herramientas.

## <a name="sections"></a>Secciones
 **Barra de herramientas** La barra de herramientas contiene herramientas que se pueden utilizar en la vista de diseño o en la vista de consulta. Para más información sobre la barra de herramientas y cómo usar estas características, vea [Barra de herramientas &#40;pestaña Explorador, Diseñador de cubos&#41; &#40;Analysis Services - Datos multidimensionales&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md).

 **Analizar en Excel** Utilice la pestaña **Analizar en Excel** para enviar la selección actual de datos del cubo a Excel y poder obtener una vista previa de los datos en una tabla dinámica. La selección actual de datos se basa en los elementos agregados del panel **Metadatos** y los filtros que pueda haber definido mediante las funciones de creación de consultas y filtros. Para obtener más información, vea [Analizar en Excel &#40;pestaña Explorador, Diseñador de cubos&#41; &#40;Analysis Services - Datos multidimensionales&#41;](analyze-in-excel-browser-cube-designer-analysis-services-multidimensional-data.md).

 **Metadatos** Utilice la pestaña **Metadatos** para ver los objetos contenidos en el cubo, explorar en profundidad las jerarquías, y explorar y utilizar medidas. Después de realizar la selección, puede ver los datos asociados a ellos en el panel **Informe** . Para más información sobre este panel, vea [Metadatos &#40;pestaña Explorador, Diseñador de cubos&#41; &#40;Analysis Services - Datos multidimensionales&#41;](metadata-browser-tab-cube-designer-analysis-services-multidimensional-data.md).

 **Filtro y consulta** Utilice este área de la superficie de diseño para generar consultas MDX, arrastrando y colocando objetos del panel **Metadatos** , y especificando criterios de filtro en el cubo o la dimensión de origen. Para más información, vea [Consulta y filtro &#40;pestaña Explorador del Diseñador de cubos&#41; &#40;Analysis Services - Datos multidimensionales&#41;](query-filter-browser-cube-designer-analysis-services-multidimensional-data.md).

## <a name="see-also"></a>Consulte también
 [Objetos de cubo &#40;Analysis Services de datos multidimensionales&#41;](multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md) [cubos en modelos multidimensionales diseñador de](multidimensional-models/cubes-in-multidimensional-models.md) [cubos &#40;Analysis Services de datos multidimensionales&#41;](cube-designer-analysis-services-multidimensional-data.md)


