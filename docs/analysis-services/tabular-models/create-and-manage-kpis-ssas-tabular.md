---
title: Crear y administrar KPI | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 07403f0fba6b96601771b070b139b2e1a282574d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="create-and-manage-kpis"></a>Crear y administrar KPI 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  En este artículo se describe cómo crear, editar o eliminar un KPI (indicador clave de rendimiento) en un modelo tabular. Para crear un KPI, seleccione una medida que se evalúe como el valor base del KPI. A continuación, use el cuadro de diálogo Indicador clave de rendimiento para seleccionar una segunda medida o un valor absoluto que se evalúe como un valor de destino. Después puede definir umbrales de estado que miden el rendimiento entre las medidas Base y Destino.  
  
## <a name="tasks"></a>Tareas  
  
> [!IMPORTANT]  
>  Antes de crear un KPI, debe crear primero una medida base que se evalúe como un valor. Después, extienda la medida base a un KPI. En otro tema, se describe cómo crear medidas [crear y administrar medidas](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md). Un KPI también necesita un valor de destino. Este valor puede ser de otra medida predefinida o puede ser un valor absoluto. Una vez extendida una medida base a un KPI, puede seleccionar el valor de destino y definir umbrales de estado en el cuadro de diálogo Indicador clave de rendimiento.  
  
###  <a name="bkmk_create_KPI"></a> Para crear un KPI  
  
1.  En la cuadrícula de medidas, haga clic con el botón derecho en la medida que actuará como medida base (valor) y, después, haga clic en **Crear KPI**.  
  
2.  En el cuadro de diálogo **Indicador clave de rendimiento** , en **Definir el valor de destino**, seleccione una de las opciones siguientes:  
  
     Seleccione **Medida**y, a continuación, seleccione una medida de destino en el cuadro de lista.  
  
     Seleccione **Valor absoluto**y escriba un valor numérico.  
  
3.  En **Definir umbrales de estado**, haga clic y deslice los valores de umbral inferior y superior.  
  
4.  En **Seleccionar estilo de icono**, haga clic en un tipo de imagen.  
  
5.  Haga clic en **Descripciones**y, a continuación, escriba las descripciones para KPI, Valor, Estado y Destino.  
  
> [!TIP]  
>  Puede usar la característica Analizar en Excel para probar el KPI. Para obtener más información, consulte [analizar en Excel](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md).  
  
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
|Measure|ALT+M|  
|Valor absoluto|ALT+A|  
|Definir umbrales de estado|ALT+U|  
|Seleccionar estilo de icono|Alt+I|  
|Tendencia|ALT+T|  
|Descripciones|ALT+D|  
|Tendencia|ALT+T|  
  
## <a name="see-also"></a>Vea también  
 [KPI](../../analysis-services/tabular-models/kpis-ssas-tabular.md)   
 [Medidas](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [Crear y managemeasures](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md)  
  
  
