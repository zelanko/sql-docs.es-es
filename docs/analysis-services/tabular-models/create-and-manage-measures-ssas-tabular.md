---
title: Crear y administrar medidas (SSAS Tabular) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: edc1a4b2-96d3-4f34-bb70-6cacec79e819
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 799ada43cebe2f6358c88c0b4aa8719186f67823
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="create-and-manage-measures-ssas-tabular"></a>Crear y administrar medidas (SSAS tabular)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Una medida es una fórmula que se crea para su uso en un informe o la tabla dinámica de Excel (o gráfico dinámico). Las medidas pueden estar basadas en funciones de agregación estándar, como COUNT o SUM, o puede definir su propia fórmula utilizando DAX. Las tareas de este tema explican cómo crear y administrar medidas mediante la cuadrícula de medidas de una tabla.  
  
 En este tema se incluyen las tareas siguientes:  
  
-   [Para crear una medida usando una fórmula de agregación estándar](#bkmk_create_stand)  
  
-   [Para crear una medida usando una fórmula personalizada](#bkmk_create_custom)  
  
-   [Para editar las propiedades de las medidas](#bkmk_edit)  
  
-   [Para cambiar el nombre de una medida](#bkmk_rename)  
  
-   [Para eliminar una medida](#bkmk_delete)  
  
## <a name="tasks"></a>Tareas  
 Para crear y administrar medidas, usará la cuadrícula de medidas de una tabla. Solo puede ver la cuadrícula de medidas de una tabla en el diseñador de modelos en la Vista de datos. No puede crear medidas ni ver la cuadrícula de medidas en la Vista Diagrama; sin embargo, podrá ver las medidas existentes en dicha vista. Para mostrar la cuadrícula de medidas de una tabla, haga clic en el menú **Tabla** y en **Mostrar cuadrícula de medidas**.  
  
###  <a name="bkmk_create_stand"></a> Para crear una medida usando una fórmula de agregación estándar  
  
-   Haga clic en la columna para la que desea crear la medida, haga clic en el menú **Columna** , seleccione **Autosuma**y, a continuación, haga clic en un tipo de agregación.  
  
     La medida se creará automáticamente con un nombre predeterminado, seguido de la fórmula en la primera celda de la cuadrícula de medidas directamente debajo de la columna.  
  
###  <a name="bkmk_create_custom"></a> Para crear una medida usando una fórmula personalizada  
  
-   En la cuadrícula de medidas, debajo de la columna para la que quiere crear la medida, haga clic en una celda y, después, en la barra de fórmulas, escriba un nombre, seguido de un signo de dos puntos (:), un signo igual (=) y de la fórmula. Presione ENTRAR para aceptar la fórmula.  
  
###  <a name="bkmk_edit"></a> Para editar las propiedades de las medidas  
  
-   En la cuadrícula de medidas, haga clic en una medida y, a continuación, en la ventana **Propiedades** , escriba o seleccione un valor de propiedad distinto.  
  
###  <a name="bkmk_rename"></a> Para cambiar el nombre de una medida  
  
-   En la cuadrícula de medidas, haga clic en una medida y, a continuación, en la ventana **Propiedades** , en **Nombre de medida**, escriba un nombre nuevo y haga clic en ENTRAR.  
  
     También puede cambiar el nombre de una medida en la barra de fórmulas. El nombre de la medida precede a la fórmula, y va seguido de un signo de dos puntos.  
  
###  <a name="bkmk_delete"></a> Para eliminar una medida  
  
-   En la cuadrícula de medidas, haga clic con el botón derecho en una medida y, después, haga clic en **Eliminar**.  
  
## <a name="see-also"></a>Vea también  
 [Medidas &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [KPI &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/kpis-ssas-tabular.md)   
 [Columnas calculadas &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/ssas-calculated-columns.md)  
  
  
