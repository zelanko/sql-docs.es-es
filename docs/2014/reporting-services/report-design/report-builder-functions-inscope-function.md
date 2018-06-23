---
title: Función InScope (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a8cd209a-e5d3-4dce-ab2d-f271f6c54955
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: e677c9e02f452a486b9168f15c662362640ea86e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199605"
---
# <a name="inscope-function-report-builder-and-ssrs"></a>Función InScope (Generador de informes y SSRS)
  Indica si la instancia actual de un elemento se encuentra en el ámbito especificado.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxis  
  
```  
InScope(scope)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ámbito*  
 (`String`) El nombre de un conjunto de datos, la región de datos o el grupo que especifica un ámbito.  
  
## <a name="return-type"></a>Tipo devuelto  
 Devuelve un `Boolean`.  
  
## <a name="remarks"></a>Notas  
 El `InScope` función comprueba el ámbito de la instancia actual de un elemento de informe de pertenencia en el ámbito especificado por el *ámbito*parámetro.  
  
 *Scope* no puede ser una expresión.  
  
 Un uso típico de la `InScope` función es en regiones de datos que tienen dinámica de ámbito. Por ejemplo, `InScope` puede usarse en un vínculo de obtención de detalles en las celdas de una región de datos para proporcionar un informe diferente nombres y diferentes conjuntos de parámetros en función de la celda que se hace clic en. He aquí un ejemplo:  
  
-   La expresión siguiente, usada como nombre de informe en un vínculo de obtención de detalles, abre el informe `ProductDetail` si la celda en la que se hace clic está en el grupo `Month` , o el informe `ProductSummary` si no lo está.  
  
    ```  
    =Iif(InScope("Month"), "ProductDetail", "ProductSummary")  
    ```  
  
-   La expresión siguiente, usada en el `Omit` propiedad de un parámetro de informe de obtención de detalles, pasa el parámetro al informe de destino solo si la celda donde ha hecho clic en el `Product` grupo.  
  
    ```  
    =Not(InScope("Product"))  
    ```  
  
 Para más información, vea [Funciones del generador de informes - referencia de funciones de agregado &#40;Generador de informes y SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) y [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo de código indica si la instancia actual del elemento está en el ámbito del conjunto de datos, la región de datos o el grupo `Product` .  
  
```  
=InScope("Product")  
```  
  
## <a name="see-also"></a>Vea también  
 [Expresión que se utiliza en los informes &#40;el generador de informes SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Ámbito de expresión para totales, agregados y colecciones integradas &#40;el generador de informes SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  