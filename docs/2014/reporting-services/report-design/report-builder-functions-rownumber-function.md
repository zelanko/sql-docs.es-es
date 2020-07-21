---
title: Función RowNumber (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 9d718ba8-d323-49fb-aac8-e7013a117b75
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d4a06a24525b3d9d0c4e4a5f3f0b749a7db70261
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66105170"
---
# <a name="rownumber-function-report-builder-and-ssrs"></a>Función RowNumber (Generador de informes y SSRS)
  Devuelve un recuento actualizado del número de filas para el ámbito especificado.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RowNumber(scope)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *scope*  
 (`String`). Nombre de un conjunto de datos, región de datos, grupo o valor NULL (`Nothing` en [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]) que especifica el contexto en el que se evaluará el número de filas. `Nothing` especifica el contexto más externo, normalmente el conjunto de datos de informe.  
  
## <a name="remarks"></a>Observaciones  
 `RowNumber`Devuelve un valor de ejecución del recuento de filas dentro del ámbito especificado, al igual que [RunningValue](report-builder-functions-runningvalue-function.md) devuelve el valor de ejecución de una función de agregado. Cuando especifique un ámbito, especifique cuándo se deberá restablecer el recuento de filas en 1.  
  
 *scope* no puede ser una expresión. *scope* debe ser un ámbito contenedor. Entre los ámbitos más habituales, desde el contenedor más externo al más interno, se encuentran los conjuntos de datos de informe, las regiones de datos, los grupos de filas o los grupos de columnas.  
  
 Para incrementar los valores por columnas, especifique como ámbito el nombre de un grupo de columnas. Para incrementar los números por filas, especifique como ámbito el nombre de un grupo de filas.  
  
> [!NOTE]  
>  No se admite la inclusión de agregados que especifican un grupo de filas y un grupo de columnas en una sola expresión.  
  
 Para más información, vea [Funciones del generador de informes - referencia de funciones de agregado &#40;Generador de informes y SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) y [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 La expresión siguiente se puede usar con la propiedad `BackgroundColor` de una fila de detalles de región de datos Tablix para alternar el color de las filas de detalles para cada grupo, comenzando siempre por el blanco.  
  
```  
=IIF(RowNumber("GroupbyCategory") Mod 2, "White", "PaleGreen")  
```  
  
## <a name="see-also"></a>Consulte también  
 [Usar expresiones en informes &#40;Generador de informes y SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
