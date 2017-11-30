---
title: "Función CountRows (Generador de informes y SSRS) | Microsoft Docs"
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
ms.assetid: 5b1c403d-6afd-44c8-b5f6-5ecff2a29a45
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 68ac91afabfa9f3daedc1a318c73120f0acb1126
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="report-builder-functions---countrows-function"></a>Funciones del Generador de informes: función CountRows
  Devuelve el número de filas del ámbito especificado, incluidas las filas con valores NULL.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CountRows(scope, recursive)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ámbito*  
 (**Cadena**) Nombre de un conjunto de datos, una región de datos o un grupo que contiene los elementos de informe que hay que contar.  
  
 *recursivos*  
 (**Tipo enumerado**) Opcional. **Simple** (valor predeterminado) o **RdlRecursive**. Especifica si se debe realizar la agregación de forma recursiva.  
  
## <a name="return-type"></a>Tipo devuelto  
 Devuelve un **Integer**.  
  
## <a name="remarks"></a>Comentarios  
 **CountRows** cuenta todas las filas del ámbito especificado, incluso las filas que contienen valores NULL.  
  
 El valor de *scope* no puede ser una expresión y debe hacer referencia al ámbito actual o a un ámbito contenedor.  
  
 Para más información, vea [Funciones del generador de informes - referencia de funciones de agregado &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) y [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Para más información sobre los agregados recursivos, vea [Crear un grupo de jerarquía recursiva &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="example"></a>Ejemplo  
 El ejemplo de código siguiente muestra una expresión que calcula el número de filas de un grupo de filas denominado `GroupbyCategory` (se basa en la expresión `[Category]`).  
  
```  
="Number of rows: " & CountRows("GroupbyCategory")  
```  
  
## <a name="see-also"></a>Vea también  
 [Usar expresiones en informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
