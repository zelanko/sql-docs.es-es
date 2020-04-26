---
title: Crear y administrar KPI (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.kpi.f1
ms.assetid: c96026c2-4394-4c3c-986b-4c95a4421900
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc0bd941392c208ad693be21a391d7b9e3f587a1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/25/2020
ms.locfileid: "66067511"
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
>  Antes de crear un KPI, debe crear primero una medida base que se evalúe como un valor. Después, extienda la medida base a un KPI. La forma de crear medidas se describe en el tema [Crear y administrar medidas &#40;SSAS tabular&#41;](measures-ssas-tabular.md). Un KPI también necesita un valor de destino. Este valor puede ser de otra medida predefinida o puede ser un valor absoluto. Una vez extendida una medida base a un KPI, puede seleccionar el valor de destino y definir umbrales de estado en el cuadro de diálogo Indicador clave de rendimiento.  
  
###  <a name="to-create-a-kpi"></a><a name="bkmk_create_KPI"></a> Para crear un KPI  
  
1.  En la cuadrícula de medidas, haga clic con el botón derecho en la medida que actuará como medida base (valor) y, después, haga clic en **Crear KPI**.  
  
2.  En el cuadro de diálogo **Indicador clave de rendimiento** , en **Definir el valor de destino**, seleccione una de las opciones siguientes:  
  
     Seleccione **Medida**y, a continuación, seleccione una medida de destino en el cuadro de lista.  
  
     Seleccione **Valor absoluto**y escriba un valor numérico.  
  
3.  En **Definir umbrales de estado**, haga clic y deslice los valores de umbral inferior y superior.  
  
4.  En **Seleccionar estilo de icono**, haga clic en un tipo de imagen.  
  
5.  Haga clic en **Descripciones**y, a continuación, escriba las descripciones para KPI, Valor, Estado y Destino.  
  
> [!TIP]  
>  Puede usar la característica Analizar en Excel para probar el KPI. Para obtener más información, vea [Analizar en Excel &#40;SSAS tabular&#41;](analyze-in-excel-ssas-tabular.md).  
  
###  <a name="to-edit-a-kpi"></a><a name="bkmk_edit_KPI"></a> Para editar un KPI  
  
-   En la cuadrícula de medidas, haga clic con el botón derecho en la medida que actúa como medida base (valor) del KPI y, después, haga clic en **Editar configuración de KPI**.  
  
###  <a name="to-delete-a-kpi-and-the-base-measure"></a><a name="bkmk_delete"></a> Para eliminar un KPI y la medida base  
  
-   En la cuadrícula de medidas, haga clic con el botón derecho en la medida que actúa como medida base (valor) del KPI y, después, haga clic en **Eliminar**.  
  
###  <a name="to-delete-a-kpi-but-keep-the-base-measure"></a><a name="bkmk_delete_KPI"></a>Para eliminar un KPI, pero mantener la medida base  
  
-   En la cuadrícula de medidas, haga clic con el botón derecho en la medida que actúa como medida base (valor) del KPI y, después, haga clic en **Eliminar KPI**.  
  
## <a name="alt-shortcuts"></a>Accesos directos con ALT  
  
|Sección IU|Comando de teclas|  
|----------------|-----------------|  
|Medida de base de KPI|ALT+B|  
|Estado de KPI|ALT+S|  
|Measure|ALT+M|  
|Valor absoluto|ALT + A|  
|Definir umbrales de estado|ALT+U|  
|Seleccionar estilo de icono|Alt+I|  
|Tendencia|ALT+T|  
|Descripciones|ALT+D|  
|Tendencia|ALT+T|  
  
## <a name="see-also"></a>Consulte también  
 [KPI &#40;&#41;tabular de SSAS](kpis-ssas-tabular.md)   
 [Medidas &#40;&#41;tabular de SSAS](measures-ssas-tabular.md)   
 [Crear y administrar medidas &#40;SSAS tabular&#41;](create-and-manage-measures-ssas-tabular.md)  
  
  
