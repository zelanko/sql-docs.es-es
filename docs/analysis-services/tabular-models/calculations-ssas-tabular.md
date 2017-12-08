---
title: "Cálculos (SSAS Tabular) | Documentos de Microsoft"
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
ms.assetid: 738816e3-0e1d-44a5-8d1b-81068dce8ac0
caps.latest.revision: "19"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: e65847285ccfd187c0dd58824a46d1dea1271a34
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="calculations-ssas-tabular"></a>Cálculos (SSAS tabular)
  Después de importar datos en el modelo, puede agregar cálculos para agregar, filtrar, ampliar, combinar y proteger esos datos. Los modelos tabulares utilizan Expresiones de análisis de datos (DAX), un lenguaje de fórmulas para crear cálculos personalizados. En los modelos tabulares, los cálculos que crea mediante fórmulas DAX se utilizan en *Columnas calculadas*, *Medidas*y *Filtros de fila*.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Descripción de DAX en modelos tabulares &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md)|Describe el lenguaje de fórmulas Expresiones de análisis de datos (DAX) que se utiliza para crear cálculos para columnas calculadas, medidas y filtros de fila en modelos tabulares.|  
|[Compatibilidad de la fórmula DAX en el modo DirectQuery (SQL Server Analysis Services)](http://msdn.microsoft.com/en-us/981b6a68-434d-4db6-964e-d92f8eb3ee3e)|Se describen las diferencias, se enumeran las funciones que no se admiten en el modo DirectQuery y se enumeran las funciones que sí se admiten pero pueden devolver resultados distintos.|  
|[Referencia de expresiones de análisis de datos (DAX)](http://msdn.microsoft.com/en-us/70a82136-0926-4a91-bcb3-e18e82593b0d)|En esta sección se proporcionan descripciones detalladas de sintaxis, operadores, y funciones de DAX.|  
  
> [!NOTE]  
>  En esta sección no se proporcionan las tareas paso a paso para crear cálculos. Dado que los cálculos se especifican en columnas calculadas, medidas y filtros de fila (en roles), se proporcionan instrucciones sobre dónde crear fórmulas DAX en las tareas relacionadas con esas características. Para obtener más información, vea [Crear una columna calculada &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/ssas-calculated-columns-create-a-calculated-column.md), [Crear y administrar medidas &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md) y [Crear y administrar roles &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/create-and-manage-roles-ssas-tabular.md).  
  
> [!NOTE]  
>  Si bien DAX también se puede utilizar para consultar un modelo tabular, los temas de esta sección se centran concretamente en el uso de fórmulas DAX para crear cálculos.  
  
  
