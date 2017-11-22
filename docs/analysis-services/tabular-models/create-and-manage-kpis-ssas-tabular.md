---
title: Crear y administrar KPI (SSAS Tabular) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.bidtoolset.kpi.f1
ms.assetid: c96026c2-4394-4c3c-986b-4c95a4421900
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1eec54bdb45111be19536f598990d1e6889140bc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="create-and-manage-kpis-ssas-tabular"></a>Crear y administrar KPI (SSAS tabular)
  En este tema se describe cómo crear, editar o eliminar un KPI (indicador clave de rendimiento) en un modelo tabular. Para crear un KPI, seleccione una medida que se evalúe como el valor base del KPI. A continuación, use el cuadro de diálogo Indicador clave de rendimiento para seleccionar una segunda medida o un valor absoluto que se evalúe como un valor de destino. Después puede definir umbrales de estado que miden el rendimiento entre las medidas Base y Destino.  
  
 En este tema se incluyen las tareas siguientes:  
  
-   [Para crear un KPI](#bkmk_create_KPI)  
  
-   [Para editar un KPI](#bkmk_edit_KPI)  
  
-   [Para eliminar un KPI y la medida base](#bkmk_delete)  
  
-   [Para eliminar un KPI, pero mantener la medida base](#bkmk_delete_KPI)  
  
## <a name="tasks"></a>Tareas  
  
> [!IMPORTANT]  
>  Antes de crear un KPI, debe crear primero una medida base que se evalúe como un valor. Después, extienda la medida base a un KPI. La forma de crear medidas se describe en el tema [Crear y administrar medidas &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md). Un KPI también necesita un valor de destino. Este valor puede ser de otra medida predefinida o puede ser un valor absoluto. Una vez extendida una medida base a un KPI, puede seleccionar el valor de destino y definir umbrales de estado en el cuadro de diálogo Indicador clave de rendimiento.  
  
###  <a name="bkmk_create_KPI"></a> Para crear un KPI  
  
1.  En la cuadrícula de medidas, haga clic con el botón derecho en la medida que actuará como medida base (valor) y, después, haga clic en **Crear KPI**.  
  
2.  En el cuadro de diálogo **Indicador clave de rendimiento** , en **Definir el valor de destino**, seleccione una de las opciones siguientes:  
  
     Seleccione **Medida**y, a continuación, seleccione una medida de destino en el cuadro de lista.  
  
     Seleccione **Valor absoluto**y escriba un valor numérico.  
  
3.  En **Definir umbrales de estado**, haga clic y deslice los valores de umbral inferior y superior.  
  
4.  En **Seleccionar estilo de icono**, haga clic en un tipo de imagen.  
  
5.  Haga clic en **Descripciones**y, a continuación, escriba las descripciones para KPI, Valor, Estado y Destino.  
  
> [!TIP]  
>  Puede usar la característica Analizar en Excel para probar el KPI. Para obtener más información, vea [Analizar en Excel &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md).  
  
###  <a name="bkmk_edit_KPI"></a> Para editar un KPI  
  
-   En la cuadrícula de medidas, haga clic con el botón derecho en la medida que actúa como medida base (valor) del KPI y, después, haga clic en **Editar configuración de KPI**.  
  
###  <a name="bkmk_delete"></a> Para eliminar un KPI y la medida base  
  
-   En la cuadrícula de medidas, haga clic con el botón derecho en la medida que actúa como medida base (valor) del KPI y, después, haga clic en **Eliminar**.  
  
###  <a name="bkmk_delete_KPI"></a> Para eliminar un KPI, pero mantener la medida base  
  
-   En la cuadrícula de medidas, haga clic con el botón derecho en la medida que actúa como medida base (valor) del KPI y, después, haga clic en **Eliminar KPI**.  
  
## <a name="alt-shortcuts"></a>Accesos directos con ALT  
  
|Sección IU|Comando de teclas|  
|----------------|-----------------|  
|Medida de base de KPI|ALT+B|  
|Estado de KPI|ALT+S|  
|Medida|ALT+M|  
|Valor absoluto|ALT+A|  
|Definir umbrales de estado|ALT+U|  
|Seleccionar estilo de icono|Alt+I|  
|Tendencia|ALT+T|  
|Descripciones|ALT+D|  
|Tendencia|ALT+T|  
  
## <a name="see-also"></a>Vea también  
 [KPI &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/kpis-ssas-tabular.md)   
 [Medidas &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [Crear y administrar medidas &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md)  
  
  
