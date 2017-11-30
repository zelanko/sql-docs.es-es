---
title: "Función InScope (Generador de informes y SSRS) | Microsoft Docs"
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
ms.assetid: a8cd209a-e5d3-4dce-ab2d-f271f6c54955
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: e9e909533634ca806de9da7723acbd13d3986cda
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="report-builder-functions---inscope-function"></a>Funciones del Generador de informes: función InScope
  Indica si la instancia actual de un elemento se encuentra en el ámbito especificado.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxis  
  
```  
InScope(scope)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ámbito*  
 (**Cadena**) Nombre de un conjunto de datos, una región de datos o un grupo que especifica un ámbito.  
  
## <a name="return-type"></a>Tipo devuelto  
 Devuelve un **Boolean**.  
  
## <a name="remarks"></a>Comentarios  
 La función **InScope** comprueba si el ámbito de la instancia actual de un elemento de informe pertenece al ámbito especificado por el parámetro *scope*.  
  
 *Scope* no puede ser una expresión.  
  
 La función **InScope** se usa habitualmente en regiones de datos que tienen un ámbito dinámico. Por ejemplo, se puede usar **InScope** en un vínculo de obtención de detalles de las celdas de una región de datos para ofrecer un nombre de informe distinto y diferentes conjuntos de parámetros en función de la celda en la que se haga clic. He aquí un ejemplo:  
  
-   La expresión siguiente, usada como nombre de informe en un vínculo de obtención de detalles, abre el informe `ProductDetail` si la celda en la que se hace clic está en el grupo `Month` , o el informe `ProductSummary` si no lo está.  
  
    ```  
    =Iif(InScope("Month"), "ProductDetail", "ProductSummary")  
    ```  
  
-   La expresión siguiente, usada en la propiedad **Omit** de un parámetro de informe detallado, pasa el parámetro al informe de destino solo si la celda en la que se hace clic está en el grupo `Product` .  
  
    ```  
    =Not(InScope("Product"))  
    ```  
  
 Para más información, vea [Referencia de funciones de agregado &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) y [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="example"></a>Ejemplo  
 El siguiente ejemplo de código indica si la instancia actual del elemento está en el ámbito del conjunto de datos, la región de datos o el grupo `Product` .  
  
```  
=InScope("Product")  
```  
  
## <a name="see-also"></a>Vea también  
 [Usar expresiones en informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
