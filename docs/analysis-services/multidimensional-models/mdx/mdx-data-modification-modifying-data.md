---
title: Modificar datos (MDX) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 265d375b7481885f168d3c39a960d2a17db46c67
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-modification---modifying-data"></a>Modificación de datos MDX: modificar datos
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Además de usar las expresiones multidimensionales (MDX) para recuperar y administrar los datos de las dimensiones y los cubos, MDX también permite actualizar o *reescribir* los datos de las dimensiones y los cubos. Dichas actualizaciones pueden ser temporales, como los análisis especulativos o de escenarios condicionales, o permanentes (cuando los cambios se producen a partir del análisis de los datos).  
  
 La actualización de los datos puede realizarse en los niveles de dimensión o de cubo:  
  
 **Reescritura de dimensiones**  
 [ALTER CUBE (Instrucción, MDX)](../../../mdx/mdx-data-definition-alter-cube.md) permite cambiar los datos de una dimensión habilitada para escritura y [REFRESH CUBE (Instrucción, MDX)](../../../mdx/mdx-data-definition-refresh-cube.md) permite reflejar la eliminación, creación y actualización de los valores de atributo. La instrucción ALTER CUBE también se puede utilizar para realizar operaciones complejas como la eliminación de todo un subárbol de una jerarquía y la promoción de los elementos secundarios de un miembro eliminado.  
  
 **Reescritura de cubos**  
 La instrucción [UPDATE CUBE](../../../mdx/mdx-data-manipulation-update-cube.md) permite efectuar actualizaciones en un cubo habilitado para escritura. Esta instrucción permite actualizar una tupla con un valor específico. [REFRESH CUBE (Instrucción, MDX)](../../../mdx/mdx-data-definition-refresh-cube.md) permite actualizar los datos de una sesión de cliente con datos actualizados del servidor.  
  
 Para más información, vea [Usar reescrituras de cubos &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-data-modification-using-cube-writebacks.md).  
  
## <a name="see-also"></a>Vea también  
 [Aspectos básicos de consulta MDX & #40; Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
