---
title: Cálculos (SSAS Tabular) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 738816e3-0e1d-44a5-8d1b-81068dce8ac0
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f17c8ab9ebf08379bf0b989924221995d7eaf891
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199208"
---
# <a name="calculations-ssas-tabular"></a>Cálculos (SSAS tabular)
  Después de importar datos en el modelo, puede agregar cálculos para agregar, filtrar, ampliar, combinar y proteger esos datos. Los modelos tabulares utilizan Expresiones de análisis de datos (DAX), un lenguaje de fórmulas para crear cálculos personalizados. En los modelos tabulares, los cálculos que crea mediante fórmulas DAX se utilizan en *Columnas calculadas*, *Medidas*y *Filtros de fila*.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Descripción de DAX en modelos tabulares &#40;SSAS Tabular&#41;](understanding-dax-in-tabular-models-ssas-tabular.md)|Describe el lenguaje de fórmulas Expresiones de análisis de datos (DAX) que se utiliza para crear cálculos para columnas calculadas, medidas y filtros de fila en modelos tabulares.|  
|[Compatibilidad de las fórmulas en el modo DirectQuery](../dax-formula-compatibility-in-directquery-mode-ssas-2014.md)|Se describen las diferencias, se enumeran las funciones que no se admiten en el modo DirectQuery y se enumeran las funciones que sí se admiten pero pueden devolver resultados distintos.|  
|[Expresiones de análisis de datos &#40;DAX&#41; referencia](https://msdn.microsoft.com/library/gg413422(v=sql.120).aspx)|En esta sección se proporcionan descripciones detalladas de sintaxis, operadores, y funciones de DAX.|  
  
> [!NOTE]  
>  En esta sección no se proporcionan las tareas paso a paso para crear cálculos. Dado que los cálculos se especifican en columnas calculadas, medidas y filtros de fila (en roles), se proporcionan instrucciones sobre dónde crear fórmulas DAX en las tareas relacionadas con esas características. Para obtener más información, vea [Crear una columna calculada &#40;SSAS tabular&#41;](ssas-calculated-columns-create-a-calculated-column.md), [Crear y administrar medidas &#40;SSAS tabular&#41;](measures-ssas-tabular.md) y [Crear y administrar roles &#40;SSAS tabular&#41;](roles-ssas-tabular.md).  
  
> [!NOTE]  
>  Si bien DAX también se puede utilizar para consultar un modelo tabular, los temas de esta sección se centran concretamente en el uso de fórmulas DAX para crear cálculos.  
  
  