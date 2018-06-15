---
title: 'Lección tutorial de Analysis Services 7: crear indicadores clave de rendimiento | Documentos de Microsoft'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 03dd09c8f06c8e4d96176f47dcc310008feaf564
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34042719"
---
# <a name="create-key-performance-indicators"></a>Crear indicadores clave de rendimiento

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

En esta lección, creará indicadores clave de rendimiento (KPI). KPI se usan para medir el rendimiento de un valor definido por una *Base* medida, con un *destino* valor también se define una medida o un valor absoluto. En aplicaciones cliente de informes, los KPI pueden proporcionar a los profesionales del negocio una manera rápida y sencilla de identificar un resumen de logros empresariales o tendencias. Para obtener más información, consulte [KPI](../tabular-models/kpis-ssas-tabular.md)
  
Tiempo estimado para completar esta lección: **15 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  

Este artículo forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [lección 6: crear medidas](../tutorial-tabular-1400/as-lesson-6-create-measures.md).   
  
## <a name="create-key-performance-indicators"></a>Crear indicadores clave de rendimiento  
  
#### <a name="to-create-an-internetcurrentquartersalesperformance-kpi"></a>Para crear un KPI InternetCurrentQuarterSalesPerformance  
  
1.  En el Diseñador de modelos, haga clic en el **FactInternetSales** tabla.  
  
2.  En la cuadrícula de medidas, haga clic en una celda vacía.  
  
3.  En la barra de fórmulas situada encima de la tabla, escriba la siguiente fórmula: 
 
    ```  
    InternetCurrentQuarterSalesPerformance :=DIVIDE([InternetCurrentQuarterSales]/[InternetPreviousQuarterSalesProportionToQTD],BLANK())  
    ```

    Esta medida actúa como medida Base del KPI.  
  
4.  En la cuadrícula de medidas, haga clic en **InternetCurrentQuarterSalesPerformance** > **crear KPI**.   
  
5.  En el cuadro de diálogo indicador clave de rendimiento (KPI), en **destino** seleccione **valor absoluto**y, a continuación, escriba **1.1**.  
  
7.  En el campo de control deslizante situado abajo a la izquierda, escriba **1**y, en el de arriba a la derecha, escriba **1.07**.  
  
8.  En **Seleccionar el estilo de icono**, seleccione el tipo de icono de rombo (rojo), triángulo (amarillo), círculo (verde).
  
    ![kpi como lesson7](../tutorial-tabular-1400/media/as-lesson7-kpi.png)
    
    > [!TIP]  
    > Tenga en cuenta la expandible **descripciones** etiqueta debajo de los estilos de icono disponibles. Use las descripciones de los distintos elementos KPI para que sean más fáciles de identificar en las aplicaciones cliente.  
  
9. Haga clic en **Aceptar** para completar el KPI.  
  
    En la cuadrícula de medidas, observe el icono situado junto a la **InternetCurrentQuarterSalesPerformance** medida. Este icono indica que esta medida actúa como valor base de un KPI.  
  
#### <a name="to-create-an-internetcurrentquartermarginperformance-kpi"></a>Para crear un KPI InternetCurrentQuarterMarginPerformance  
  
1.  En la cuadrícula de medidas para la **FactInternetSales** de tabla, haga clic en una celda vacía.  
  
2.  En la barra de fórmulas situada encima de la tabla, escriba la siguiente fórmula:  

    ```
    InternetCurrentQuarterMarginPerformance :=IF([InternetPreviousQuarterMarginProportionToQTD]<>0,([InternetCurrentQuarterMargin]-[InternetPreviousQuarterMarginProportionToQTD])/[InternetPreviousQuarterMarginProportionToQTD],BLANK())  
    ```
 
3.  Haga clic en **InternetCurrentQuarterMarginPerformance** > **crear KPI**.  
  
4.  En el cuadro de diálogo indicador clave de rendimiento (KPI), en **destino** seleccione **valor absoluto**y, a continuación, escriba **1.25**.   
  
5.  En el campo de control deslizante (baja) izquierdo, deslice hasta que el campo muestre **0,8**y, a continuación, diapositiva campo el control deslizante de la derecha (alto), hasta que el campo muestre **1.03**.  
  
6.  En **Seleccionar estilo de icono**, seleccione el tipo de icono de rombo (rojo), triángulo (amarillo) y círculo (verde), y haga clic en **Aceptar**.  
  
## <a name="whats-next"></a>¿Qué sigue?

[Lección 8: Crear perspectivas](../tutorial-tabular-1400/as-lesson-8-create-perspectives.md).
  
  
