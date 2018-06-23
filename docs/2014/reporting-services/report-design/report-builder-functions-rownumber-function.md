---
title: Función RowNumber (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9d718ba8-d323-49fb-aac8-e7013a117b75
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 150a46a736a9c6ddd2f8c394f3f173906cd07132
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107551"
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
 *ámbito*  
 (`String`) El nombre de un conjunto de datos, región de datos, o grupo o null (`Nothing` en [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]), que especifica el contexto en el que se va a evaluar el número de filas. `Nothing` Especifica el contexto más externo, normalmente el conjunto de datos de informe.  
  
## <a name="remarks"></a>Notas  
 `RowNumber` Devuelve el valor actual del recuento de filas dentro del ámbito especificado, al igual que [RunningValue](report-builder-functions-runningvalue-function.md) devuelve el valor actual de una función de agregado. Cuando especifique un ámbito, especifique cuándo se deberá restablecer el recuento de filas en 1.  
  
 *scope* no puede ser una expresión. *scope* debe ser un ámbito contenedor. Entre los ámbitos más habituales, desde el contenedor más externo al más interno, se encuentran los conjuntos de datos de informe, las regiones de datos, los grupos de filas o los grupos de columnas.  
  
 Para incrementar los valores por columnas, especifique como ámbito el nombre de un grupo de columnas. Para incrementar los números por filas, especifique como ámbito el nombre de un grupo de filas.  
  
> [!NOTE]  
>  No se admite la inclusión de agregados que especifican un grupo de filas y un grupo de columnas en una sola expresión.  
  
 Para más información, vea [Funciones del generador de informes - referencia de funciones de agregado &#40;Generador de informes y SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) y [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 La siguiente es una expresión que puede usar para la `BackgroundColor` propiedad de una fila de detalles de región de datos Tablix para alternar el color de las filas de detalles para cada grupo, comenzando siempre por el blanco.  
  
```  
=IIF(RowNumber("GroupbyCategory") Mod 2, "White", "PaleGreen")  
```  
  
## <a name="see-also"></a>Vea también  
 [Expresión que se utiliza en los informes &#40;el generador de informes SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Ámbito de expresión para totales, agregados y colecciones integradas &#40;el generador de informes SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  