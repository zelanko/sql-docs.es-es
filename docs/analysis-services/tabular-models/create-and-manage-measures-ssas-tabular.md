---
title: Crear y administrar medidas | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f6547cca48cbb846901e12cd1ab38822de9133d3
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="create-and-manage-measures"></a>Crear y administrar medidas 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Una medida es una fórmula que se crea específicamente para su uso en un informe o una tabla dinámica de Excel (o gráfico dinámico). Las medidas pueden estar basadas en funciones de agregación estándar, como COUNT o SUM, o puede definir su propia fórmula utilizando DAX. Las tareas de este tema explican cómo crear y administrar medidas mediante la cuadrícula de medidas de una tabla.  
  
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
 [Medidas](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [KPI](../../analysis-services/tabular-models/kpis-ssas-tabular.md)   
 [Columnas calculadas](../../analysis-services/tabular-models/ssas-calculated-columns.md)  
  
  
