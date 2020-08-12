---
title: Función Level (Generador de informes) | Microsoft Docs
description: Obtenga información sobre la función Level del Generador de informes. Esta función devuelve el nivel actual de profundidad de una jerarquía recursiva.
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 41235402-bb9e-4cb7-b91e-431e77db19cf
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: b582a1c62f92fc001b4c6047319b9100b4e27ac9
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048241"
---
# <a name="report-builder-functions---level-function"></a>Funciones del Generador de informes: función Level
  Devuelve el nivel actual de profundidad de una jerarquía recursiva.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Level(scope)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *scope*  
 (**Cadena**) Opcional. Nombre de un conjunto de datos, un grupo o una región de datos que contiene los elementos de informe a los que se va a aplicar la función de agregado. Si no se especifica el parámetro *scope* , se usa el ámbito actual.  
  
## <a name="return-type"></a>Tipo de valor devuelto  
 Devuelve un **Integer**. Si el parámetro *scope* especifica un conjunto de datos o una región de datos, o bien una agrupación no recursiva (es decir, una agrupación que no contenga el elemento **Parent** ), la función **Level** devuelve 0. Si se omite el parámetro *scope* , devuelve el nivel del ámbito actual.  
  
## <a name="remarks"></a>Observaciones  
 El valor que devuelve la función **Level** se basa en cero; es decir, el primer nivel de una jerarquía es 0.  
  
 La función **Level** puede utilizarse para aplicar sangría en una jerarquía recursiva, como puede ser una lista de empleados.  
  
 Para más información sobre jerarquías recursivas, vea [Crear grupos de jerarquía recursiva &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo de código devuelve el nivel de fila del grupo Employees:  
  
```  
=Level("Employees")  
```  
  
## <a name="see-also"></a>Consulte también  
 [Usar expresiones en informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
