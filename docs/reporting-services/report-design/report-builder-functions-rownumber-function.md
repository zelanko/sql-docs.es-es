---
title: Función RowNumber (Generador de informes) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 9d718ba8-d323-49fb-aac8-e7013a117b75
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7af8523acb3bf531589a04268de1139d8bcefd35
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "77081174"
---
# <a name="report-builder-functions---rownumber-function"></a>Funciones del Generador de informes: función RowNumber
  Devuelve un recuento actualizado del número de filas para el ámbito especificado.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RowNumber(scope)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *scope*  
 (**String**) El nombre de un conjunto de datos, región de datos, grupo o valor NULL (**Nothing** en [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]) que especifica el contexto en el que se evaluará el número de filas. **Nothing** especifica el contexto más externo, normalmente el conjunto de datos de informe.  
  
## <a name="remarks"></a>Observaciones  
 **RowNumber** devuelve el valor actual del recuento de filas dentro del ámbito especificado, al igual que [RunningValue](../../reporting-services/report-design/report-builder-functions-runningvalue-function.md) devuelve el valor actual de una función de agregado. Cuando especifique un ámbito, especifique cuándo se deberá restablecer el recuento de filas en 1.  
  
 *scope* no puede ser una expresión. *scope* debe ser un ámbito contenedor. Entre los ámbitos más habituales, desde el contenedor más externo al más interno, se encuentran los conjuntos de datos de informe, las regiones de datos, los grupos de filas o los grupos de columnas.  
  
 Para incrementar los valores por columnas, especifique como ámbito el nombre de un grupo de columnas. Para incrementar los números por filas, especifique como ámbito el nombre de un grupo de filas.  
  
> [!NOTE]  
>  No se admite la inclusión de agregados que especifican un grupo de filas y un grupo de columnas en una sola expresión.  
  
 Para más información, vea [Funciones del generador de informes - referencia de funciones de agregado &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) y [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 La expresión siguiente se puede usar con la propiedad **BackgroundColor** de una fila de detalles de región de datos Tablix para alternar el color de las filas de detalles para cada grupo, comenzando siempre por el blanco.  
  
```  
=IIF(RowNumber("GroupbyCategory") Mod 2, "White", "PaleGreen")  
```  
  
## <a name="see-also"></a>Consulte también  
 [Usar expresiones en informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
