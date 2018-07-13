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
ms.topic: conceptual
ms.assetid: a8cd209a-e5d3-4dce-ab2d-f271f6c54955
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: ebf90710587c73206408dfda1429a90b58f39621
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37228845"
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
 (`String`) El nombre de un conjunto de datos, región de datos o grupo que especifica un ámbito.  
  
## <a name="return-type"></a>Tipo devuelto  
 Devuelve un `Boolean`.  
  
## <a name="remarks"></a>Notas  
 El `InScope` función comprueba el ámbito de la instancia actual de un elemento de informe pertenece al ámbito especificado por el *ámbito*parámetro.  
  
 *Scope* no puede ser una expresión.  
  
 Un uso típico de la `InScope` función está en regiones de datos dinámicos de ámbito. Por ejemplo, `InScope` puede utilizarse en un vínculo de obtención de detalles en las celdas de una región de datos para proporcionar un informe diferente de nombre y diferentes conjuntos de parámetros en función de la celda que se hace clic en. He aquí un ejemplo:  
  
-   La expresión siguiente, usada como nombre de informe en un vínculo de obtención de detalles, abre el informe `ProductDetail` si la celda en la que se hace clic está en el grupo `Month` , o el informe `ProductSummary` si no lo está.  
  
    ```  
    =Iif(InScope("Month"), "ProductDetail", "ProductSummary")  
    ```  
  
-   La expresión siguiente, usada en el `Omit` propiedad de un parámetro de informe detallado, pasa el parámetro al informe de destino solo si la celda donde ha hecho clic en el `Product` grupo.  
  
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
 [Usar expresiones en informes &#40;generador de informes y SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Ámbito de expresión para totales, agregados y colecciones integradas &#40;generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
