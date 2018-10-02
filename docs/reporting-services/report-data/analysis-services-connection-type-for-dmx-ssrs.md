---
title: Tipo de conexión de Analysis Services para DMX (SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- parameters [Reporting Services], DMX
- Data Mining Prediction [Reporting Services]
- query view [Reporting Services]
- DMX [Reporting Services]
- design view [Reporting Services]
- data mining [Reporting Services]
- passing parameters [Reporting Services]
ms.assetid: 2de825e9-6d8a-4128-add0-da15dc6cea3e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 98230dfb1287460e9844c4adb87a47943edabcc2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47666223"
---
# <a name="analysis-services-connection-type-for-dmx-ssrs"></a>Tipo de conexión de Analysis Services para DMX (SSRS)
  Cuando se crea un conjunto de datos usando un origen de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , el Diseñador de informes muestra el diseñador de consultas de expresiones multidimensionales (MDX) si detecta un cubo válido. Si no se detecta ningún cubo pero está disponible un modelo de minería de datos, el Diseñador de informes muestra el diseñador de consultas de extensiones de minería de datos (DMX). Para cambiar entre los diseñadores MDX y DMX, haga clic en el botón **Tipo de comando DMX** (![Cambiar a la vista del lenguaje de consultas DMX](../../reporting-services/report-data/media/rsqdicon-commandtypedmx.gif "Cambiar a la vista del lenguaje de consultas DMX")) en la barra de herramientas. Use el diseñador de consultas DMX para crear interactivamente una consulta DMX con elementos gráficos. Para utilizar el Diseñador de consultas DMX, el origen de datos que especifique debe tener previamente un modelo de minería de datos que aporte los datos. Los resultados de la consulta se convierten en un conjunto de filas planas que se utilizará en el informe.  
  
> [!NOTE]  
>  Debe entrenar el modelo antes de diseñar el informe. Para obtener más información, vea [Soluciones de minería de datos](../../analysis-services/data-mining/data-mining-solutions.md).  
  
## <a name="design-mode"></a>Modo de diseño  
 El diseñador de consultas DMX se abre en modo de diseño. El modo de diseño incluye una superficie de diseño gráfica que se utiliza para seleccionar un modelo de minería de datos individual, así como una tabla de entrada y una cuadrícula que se utiliza para especificar la consulta de predicción. Existen otros dos modos en el diseñador de consultas DMX: modo de consulta y modo de resultados. En el modo de consulta, la cuadrícula del modo de diseño se sustituye por un panel de consulta, que se puede utilizar para escribir consultas DMX. En el modo de resultados, el conjunto de resultados devuelto por la consulta aparece en una cuadrícula de datos.  
  
 Para cambiar de modo en el diseñador de consultas DMX, haga clic con el botón derecho en la superficie de diseño de la consulta y seleccione **Diseño**, **Consulta**o **Resultado**. Para más información, vea [Interfaz de usuario del Diseñador de consultas DMX de Analysis Services](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md) y [Recuperar datos de un modelo de minería de datos &#40;DMX&#41; &#40;SSRS&#41;](../../reporting-services/report-data/retrieve-data-from-a-data-mining-model-dmx-ssrs.md).  
  
## <a name="designing-a-prediction-query"></a>Diseñar una consulta de predicción  
 El panel Diseño de consulta del modo de diseño contiene dos ventanas: **Modelo de minería de datos** y **Seleccionar tabla(s) de entrada**. Use la ventana **Modelo de minería de datos** para seleccionar el modelo de minería de datos que va a utilizar en la consulta. Use la ventana **Seleccionar tabla(s) de entrada** para seleccionar la tabla en la que se basarán las predicciones. Si quiere usar una consulta singleton en lugar de una tabla de entrada, haga clic con el botón derecho en el panel Diseño de consulta y elija **Consulta singleton**. Una ventana **Entrada de consulta singleton** reemplaza a la ventana **Seleccionar tabla(s) de entrada** .  
  
 En el modo de diseño, arrastre los campos desde las ventanas **Modelo de minería de datos** y **Seleccionar tabla(s) de entrada** hasta la columna **Campo** del panel Cuadrícula. También puede rellenar las columnas restantes para especificar un alias, mostrar el campo en los resultados, agrupar campos y especificar un operador para restringir el valor del campo a un criterio o argumento determinado. Si está en el modo de consulta, genere la consulta DMX arrastrando los campos al panel Consulta.  
  
## <a name="using-parameters"></a>Usar parámetros  
 Puede pasar los parámetros del informe a un parámetro de la consulta DMX. Para hacerlo, agregue un parámetro a la consulta DMX, defina los parámetros de la consulta en el cuadro de diálogo **Parámetros de la consulta** y, a continuación, modifique los parámetros del informe asociados. Para definir un parámetro de consulta, haga clic en el botón **Parámetros de consulta** (![Icono del cuadro de diálogo Parámetros de consulta](../../reporting-services/report-data/media/iconqueryparameter.gif "Icono del cuadro de diálogo Parámetros de consulta")) en la barra de herramientas. Para ver instrucciones sobre cómo definir parámetros en una consulta DMX, consulte [Definir parámetros en el diseñador de consultas MDX para Analysis Services &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/define-parameters-in-the-mdx-query-designer-for-analysis-services.md).  
  
 Para más información sobre cómo administrar la relación entre los parámetros de consulta y los parámetros de informe, vea [Asociar un parámetro de consulta a un parámetro de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/associate-a-query-parameter-with-a-report-parameter-report-builder-and-ssrs.md). Para más información sobre parámetros, vea [Parámetros de informe &#40;Generador de informes y Diseñador de informes&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
## <a name="see-also"></a>Ver también  
 [Soluciones de minería de datos](../../analysis-services/data-mining/data-mining-solutions.md)   
 [Herramientas de diseño de consulta &#40;SSRS&#41;](../../reporting-services/report-data/query-design-tools-ssrs.md)   
 [Conexiones de datos, orígenes de datos y cadenas de conexión &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  
