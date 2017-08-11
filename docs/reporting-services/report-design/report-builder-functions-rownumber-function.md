---
title: "Función RowNumber (generador de informes y SSRS) | Documentos de Microsoft"
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
ms.assetid: 9d718ba8-d323-49fb-aac8-e7013a117b75
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 25084e7140855c6535ef6432afdc09bee02a23e6
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="report-builder-functions---rownumber-function"></a>Notificar a las funciones del generador - función RowNumber
  Devuelve un recuento actualizado del número de filas para el ámbito especificado.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RowNumber(scope)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ámbito*  
 (**String**) El nombre de un conjunto de datos, región de datos, grupo o valor NULL (**Nothing** en [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]) que especifica el contexto en el que se evaluará el número de filas. **Nothing** especifica el contexto más externo, normalmente el conjunto de datos de informe.  
  
## <a name="remarks"></a>Comentarios  
 **RowNumber** devuelve el valor actual del recuento de filas dentro del ámbito especificado, al igual que [RunningValue](../../reporting-services/report-design/report-builder-functions-runningvalue-function.md) devuelve el valor actual de una función de agregado. Cuando especifique un ámbito, especifique cuándo se deberá restablecer el recuento de filas en 1.  
  
 *scope* no puede ser una expresión. *scope* debe ser un ámbito contenedor. Entre los ámbitos más habituales, desde el contenedor más externo al más interno, se encuentran los conjuntos de datos de informe, las regiones de datos, los grupos de filas o los grupos de columnas.  
  
 Para incrementar los valores por columnas, especifique como ámbito el nombre de un grupo de columnas. Para incrementar los números por filas, especifique como ámbito el nombre de un grupo de filas.  
  
> [!NOTE]  
>  No se admite la inclusión de agregados que especifican un grupo de filas y un grupo de columnas en una sola expresión.  
  
 Para obtener más información, consulte [Referencia a las funciones de agregado &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) y [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 La expresión siguiente se puede usar con la propiedad **BackgroundColor** de una fila de detalles de región de datos Tablix para alternar el color de las filas de detalles para cada grupo, comenzando siempre por el blanco.  
  
```  
=IIF(RowNumber("GroupbyCategory") Mod 2, "White", "PaleGreen")  
```  
  
## <a name="see-also"></a>Vea también  
 [Usar expresiones en informes &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ámbito de expresión para totales, agregados y colecciones integradas &#40; El generador de informes y SSRS &#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
