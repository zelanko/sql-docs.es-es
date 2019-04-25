---
title: Crear conjuntos con nombre en MDX (MDX) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b893dcd86ffcfa68c55057796c431e694903c46a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740065"
---
# <a name="mdx-named-sets---building-named-sets"></a>Conjuntos con nombre MDX: crear conjuntos con nombre
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Una expresión de conjunto puede ser una declaración extensa, compleja y, por tanto, difícil de seguir o entender. O bien, una expresión de conjunto puede utilizarse con tanta frecuencia que definir repetidamente el conjunto sea fatigoso. Para facilitar el trabajo con una expresión larga, compleja o de uso habitual, las expresiones multidimensionales (MDX) permiten expresiones como un *conjunto con nombre*.  
  
 Esencialmente, un conjunto con nombre es una expresión de conjunto a la que se ha asignado un alias. Un conjunto con nombre puede incorporar miembros o funciones que se pueden incorporar normalmente a un conjunto. Como MDX trata el alias del conjunto con nombre como una expresión de conjunto, puede utilizar ese alias en cualquier lugar en que se acepte una expresión de conjunto.  
  
 Puede definir un conjunto con nombre para que tenga uno de los contextos siguientes:  
  
-   **Ámbito de consulta** Para crear un conjunto con nombre definido como parte de una consulta MDX (y, por lo tanto, con un ámbito limitado a la consulta) es necesario usar la palabra clave WITH. Puede utilizar el conjunto con nombre en una instrucción MDX SELECT. De esta manera, el conjunto con nombre creado con la palabra clave WITH se puede cambiar sin tener que tocar la instrucción SELECT.  
  
     Para más información sobre cómo usar la palabra clave WITH para crear conjuntos con nombre, vea [Crear conjuntos con nombre de ámbito de consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets.md).  
  
-   **Ámbito de sesión** Para crear un conjunto con nombre cuyo ámbito sea más amplio que el contexto de la consulta (es decir, un ámbito que represente el período de duración de la sesión MDX) es necesario usar la instrucción CREATE SET. Un conjunto con nombre definido por la utilización de la instrucción CREATE SET está disponible para todas las consultas de MDX de esa sesión. La instrucción CREATE SET tiene sentido, por ejemplo, en una aplicación cliente que reutilice un conjunto de un modo coherente en varias consultas diferentes.  
  
     Para más información sobre cómo usar la instrucción CREATE SET para crear conjuntos de nombre en una sesión, vea [Crear conjuntos con nombre del ámbito de consulta &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-session-scoped-named-sets.md).  
  
## <a name="see-also"></a>Vea también  
 [SELECT &#40;Instrucción, MDX&#41;](../../../mdx/mdx-data-manipulation-select.md)   
 [CREATE SET &#40;Instrucción, MDX&#41;](../../../mdx/mdx-data-definition-create-set.md)   
 [Aspectos básicos de las consultas MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
