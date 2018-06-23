---
title: Modificar datos (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- modifying data [MDX]
- Multidimensional Expressions [Analysis Services], data modifications
- MDX [Analysis Services], data modifications
- data modifications [MDX]
ms.assetid: 363b662c-b839-4971-bbd7-1842f73ce141
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3a1523655490e9dad4fc42f3a0f256f39a60c21b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107311"
---
# <a name="modifying-data-mdx"></a>Modificar datos (MDX)
  Además de usar las expresiones multidimensionales (MDX) para recuperar y administrar los datos de las dimensiones y los cubos, MDX también permite actualizar o *reescribir* los datos de las dimensiones y los cubos. Dichas actualizaciones pueden ser temporales, como los análisis especulativos o de escenarios condicionales, o permanentes (cuando los cambios se producen a partir del análisis de los datos).  
  
 La actualización de los datos puede realizarse en los niveles de dimensión o de cubo:  
  
 **Reescritura de dimensiones**  
 [ALTER CUBE (Instrucción, MDX)](/sql/mdx/mdx-data-definition-alter-cube) permite cambiar los datos de una dimensión habilitada para escritura y [REFRESH CUBE (Instrucción, MDX)](/sql/mdx/mdx-data-definition-refresh-cube) permite reflejar la eliminación, creación y actualización de los valores de atributo. La instrucción ALTER CUBE también se puede utilizar para realizar operaciones complejas como la eliminación de todo un subárbol de una jerarquía y la promoción de los elementos secundarios de un miembro eliminado.  
  
 **Reescritura de cubos**  
 La instrucción [UPDATE CUBE](/sql/mdx/mdx-data-manipulation-update-cube) permite efectuar actualizaciones en un cubo habilitado para escritura. Esta instrucción permite actualizar una tupla con un valor específico. [REFRESH CUBE (Instrucción, MDX)](/sql/mdx/mdx-data-definition-refresh-cube) permite actualizar los datos de una sesión de cliente con datos actualizados del servidor.  
  
 Para más información, vea [Usar reescrituras de cubos &#40;MDX&#41;](mdx-data-modification-using-cube-writebacks.md).  
  
## <a name="see-also"></a>Vea también  
 [Aspectos básicos de consulta MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
