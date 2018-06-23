---
title: Crear grupos de jerarquía recursiva (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 06eccab6-4089-46e8-a84f-5bf3bbe0c23b
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 52410faf7827c6692575aff641070565d0ef6243
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202451"
---
# <a name="creating-recursive-hierarchy-groups-report-builder-and-ssrs"></a>Crear grupos de jerarquía recursiva (Generador de informes y SSRS)
  Para mostrar datos recursivos donde la relación entre primarios y secundarios se representa mediante campos del conjunto de datos, puede establecer la expresión de grupo de región de datos basada en el campo secundario y establecer la propiedad Parent basada en el campo primario.  
  
 Un uso habitual de los grupos de jerarquía recursiva es mostrar datos jerárquicos, por ejemplo, los empleados en un organigrama. El conjunto de datos incluye una lista de empleados y jefes, donde los nombres de los jefes también aparecen en la lista de empleados.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="creating-recursive-hierarchies"></a>Crear jerarquías recursivas  
 Para generar una jerarquía recursiva en una región de datos Tablix, establezca la expresión de grupo en el campo que especifica los datos secundarios y la propiedad Parent del grupo en el campo que especifica los datos primarios. Por ejemplo, para un conjunto de datos que contiene campos para identificador de empleado e identificador de administrador, establezca la expresión de grupo en el identificador de empleado y la propiedad Parent en el identificador de administrador.  
  
 Los grupos que se definen como jerarquía recursiva (es decir, los que usan la propiedad Parent) solo pueden tener una expresión de grupo. Puede usar la función `Level` en el margen del cuadro de texto para aplicar sangría a los nombres de los empleados en función de su nivel en la jerarquía.  
  
 Para más información, vea [Agregar o eliminar un grupo en una región de datos &#40;Generador de informes y SSRS&#41;](add-or-delete-a-group-in-a-data-region-report-builder-and-ssrs.md) y [Crear un grupo de jerarquía recursiva &#40;Generador de informes y SSRS&#41;](create-a-recursive-hierarchy-group-report-builder-and-ssrs.md).  
  
### <a name="aggregate-functions-that-support-recursion"></a>Funciones de agregado que admiten recursividad  
 Puede usar funciones de agregado de Reporting Services que aceptan el parámetro *Recursive* para calcular los datos de resumen para una jerarquía recursiva. The following functions accept `Recursive` as a parameter: [Sum](report-builder-functions-sum-function.md), [Avg](report-builder-functions-avg-function.md), [Count](report-builder-functions-count-function.md), [CountDistinct](report-builder-functions-countdistinct-function.md), [CountRows](report-builder-functions-countrows-function.md), [Max](report-builder-functions-max-function.md), [Min](report-builder-functions-min-function.md), [StDev](report-builder-functions-stdev-function.md), [StDevP](report-builder-functions-stdevp-function.md), [Sum](report-builder-functions-sum-function.md), [Var](report-builder-functions-var-function.md), and [VarP](report-builder-functions-varp-function.md). Para más información, vea [Referencia a las funciones de agregado &#40;Generador de informes y SSRS&#41;](report-builder-functions-aggregate-functions-reference.md).  
  
## <a name="see-also"></a>Vea también  
 [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)   
 [Región de datos Tablix &#40;Generador de informes y SSRS&#41;](../tablix-data-region-report-builder-and-ssrs.md)   
 [Referencia a las funciones de agregado &#40;el generador de informes SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)   
 [Tablas &#40;Generador de informes y SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrices &#40;Generador de informes y SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Generador de informes y SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tablas, matrices y listas &#40;Generador de informes y SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  