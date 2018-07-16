---
title: Función CountRows (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5b1c403d-6afd-44c8-b5f6-5ecff2a29a45
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 86b8b79fc5bcac1842a4fae82535afdff06c305e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37280271"
---
# <a name="countrows-function-report-builder-and-ssrs"></a>Función CountRows (Generador de informes y SSRS)
  Devuelve el número de filas del ámbito especificado, incluidas las filas con valores NULL.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CountRows(scope, recursive)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ámbito*  
 (`String`) Nombre de un conjunto de datos, una región de datos o un grupo que contiene los elementos de informe que hay que contar.  
  
 *recursivos*  
 (**Tipo enumerado**) Opcional. `Simple` (valor predeterminado) o `RdlRecursive`. Especifica si se debe realizar la agregación de forma recursiva.  
  
## <a name="return-type"></a>Tipo devuelto  
 Devuelve un `Integer`.  
  
## <a name="remarks"></a>Notas  
 `CountRows` cuenta todas las filas del ámbito especificado, incluidas las filas que tienen valores null.  
  
 El valor de *scope* no puede ser una expresión y debe hacer referencia al ámbito actual o a un ámbito contenedor.  
  
 Para más información, vea [Funciones del generador de informes - referencia de funciones de agregado &#40;Generador de informes y SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) y [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Para más información sobre los agregados recursivos, vea [Crear un grupo de jerarquía recursiva &#40;Generador de informes y SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="example"></a>Ejemplo  
 El ejemplo de código siguiente muestra una expresión que calcula el número de filas de un grupo de filas denominado `GroupbyCategory` (se basa en la expresión `[Category]`).  
  
```  
="Number of rows: " & CountRows("GroupbyCategory")  
```  
  
## <a name="see-also"></a>Vea también  
 [Usar expresiones en informes &#40;generador de informes y SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Ámbito de expresión para totales, agregados y colecciones integradas &#40;generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
