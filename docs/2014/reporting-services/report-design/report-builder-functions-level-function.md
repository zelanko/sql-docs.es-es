---
title: Función Level (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 41235402-bb9e-4cb7-b91e-431e77db19cf
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 3df298cda1e6439d9c539c125689a3687cdc97f8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201534"
---
# <a name="level-function-report-builder-and-ssrs"></a>Función Level (Generador de informes y SSRS)
  Devuelve el nivel actual de profundidad de una jerarquía recursiva.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Level(scope)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ámbito*  
 (`String`) (Opcional). Nombre de un conjunto de datos, un grupo o una región de datos que contiene los elementos de informe a los que se va a aplicar la función de agregado. Si no se especifica el parámetro *scope* , se usa el ámbito actual.  
  
## <a name="return-type"></a>Tipo devuelto  
 Devuelve un `Integer`. Si *ámbito* especifica un conjunto de datos o región de datos o una agrupación no recursiva (es decir, una agrupación que no `Parent` elemento), `Level` devuelve 0. Si se omite el parámetro *scope* , devuelve el nivel del ámbito actual.  
  
## <a name="remarks"></a>Notas  
 El valor que devuelve la función `Level` se basa en cero; es decir, el primer nivel de una jerarquía es 0.  
  
 La función `Level` puede utilizarse para aplicar sangría en una jerarquía recursiva, como puede ser una lista de empleados.  
  
 Para más información sobre jerarquías recursivas, vea [Crear grupos de jerarquía recursiva &#40;Generador de informes y SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo de código devuelve el nivel de fila del grupo Employees:  
  
```  
=Level("Employees")  
```  
  
## <a name="see-also"></a>Vea también  
 [Expresión que se utiliza en los informes &#40;el generador de informes SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Ámbito de expresión para totales, agregados y colecciones integradas &#40;el generador de informes SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  