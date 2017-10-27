---
title: "Nivel de función (generador de informes y SSRS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 41235402-bb9e-4cb7-b91e-431e77db19cf
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 171842909a300d0c98fca2a26bbf4567810e8e95
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="report-builder-functions---level-function"></a>Funciones del generador de informes - función Level
  Devuelve el nivel actual de profundidad de una jerarquía recursiva.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Level(scope)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ámbito*  
 (**Cadena**) Opcional. Nombre de un conjunto de datos, un grupo o una región de datos que contiene los elementos de informe a los que se va a aplicar la función de agregado. Si no se especifica el parámetro *scope* , se usa el ámbito actual.  
  
## <a name="return-type"></a>Tipo devuelto  
 Devuelve un **Integer**. Si el parámetro *scope* especifica un conjunto de datos o una región de datos, o bien una agrupación no recursiva (es decir, una agrupación que no contenga el elemento **Parent** ), la función **Level** devuelve 0. Si se omite el parámetro *scope* , devuelve el nivel del ámbito actual.  
  
## <a name="remarks"></a>Comentarios  
 El valor que devuelve la función **Level** se basa en cero; es decir, el primer nivel de una jerarquía es 0.  
  
 La función **Level** puede utilizarse para aplicar sangría en una jerarquía recursiva, como puede ser una lista de empleados.  
  
 Para obtener más información sobre las jerarquías recursivas, vea [Crear grupos de jerarquía recursiva &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo de código devuelve el nivel de fila del grupo Employees:  
  
```  
=Level("Employees")  
```  
  
## <a name="see-also"></a>Vea también  
 [Usar expresiones en informes &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ámbito de expresión para totales, agregados y colecciones integradas &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  

