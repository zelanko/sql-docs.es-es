---
title: Modificar datos (MDX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying data [MDX]
- Multidimensional Expressions [Analysis Services], data modifications
- MDX [Analysis Services], data modifications
- data modifications [MDX]
ms.assetid: 363b662c-b839-4971-bbd7-1842f73ce141
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4c490f3998b148691f35328fe5543874be92f997
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="mdx-data-modification---modifying-data"></a>Modificación de datos MDX: modificar datos
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Además de usar las expresiones multidimensionales (MDX) para recuperar y administrar los datos de dimensiones y cubos, puede usar MDX para actualizar o *reescritura* datos de cubos y dimensiones. Dichas actualizaciones pueden ser temporales, como los análisis especulativos o de escenarios condicionales, o permanentes (cuando los cambios se producen a partir del análisis de los datos).  
  
 La actualización de los datos puede realizarse en los niveles de dimensión o de cubo:  
  
 **Reescritura de dimensiones**  
 [ALTER CUBE (Instrucción, MDX)](../../../mdx/mdx-data-definition-alter-cube.md) permite cambiar los datos de una dimensión habilitada para escritura y [REFRESH CUBE (Instrucción, MDX)](../../../mdx/mdx-data-definition-refresh-cube.md) permite reflejar la eliminación, creación y actualización de los valores de atributo. La instrucción ALTER CUBE también se puede utilizar para realizar operaciones complejas como la eliminación de todo un subárbol de una jerarquía y la promoción de los elementos secundarios de un miembro eliminado.  
  
 **Reescritura de cubos**  
 La instrucción [UPDATE CUBE](../../../mdx/mdx-data-manipulation-update-cube.md) permite efectuar actualizaciones en un cubo habilitado para escritura. Esta instrucción permite actualizar una tupla con un valor específico. [REFRESH CUBE (Instrucción, MDX)](../../../mdx/mdx-data-definition-refresh-cube.md) permite actualizar los datos de una sesión de cliente con datos actualizados del servidor.  
  
 Para más información, vea [Usar reescrituras de cubos &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-modification-using-cube-writebacks.md).  
  
## <a name="see-also"></a>Vea también  
 [Aspectos básicos de las consultas MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
