---
title: Función Lookup (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e60e5bab-b286-4897-9685-9ff12703517d
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 8e2617d9704db585e4f8ac3558941a957876fc05
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107562"
---
# <a name="lookup-function-report-builder-and-ssrs"></a>Función Lookup (Generador de informes y SSRS)
  Devuelve el primer valor coincidente para el nombre especificado de un conjunto de datos que contiene pares nombre/valor.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Lookup(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *source_expression*  
 (`Variant`) Una expresión que se evalúa en el ámbito actual y que especifica el nombre o la clave que se buscará. Por ejemplo, `=Fields!ProdID.Value`.  
  
 *destination_expression*  
 (`Variant`) Una expresión que se evalúa para cada fila de un conjunto de datos y que especifica el nombre o la clave que se hará coincidir. Por ejemplo, `=Fields!ProductID.Value`.  
  
 *result_expression*  
 (`Variant`) Una expresión que se evalúa para la fila del conjunto de datos donde *source_expression* = *destination_expression*, y que especifica el valor que se recuperará. Por ejemplo, `=Fields!ProductName.Value`.  
  
 *conjunto de datos*  
 Una constante que especifica el nombre de un conjunto de datos del informe. Por ejemplo, "Productos".  
  
## <a name="return"></a>Devolución  
 Devuelve un `Variant`, o `Nothing` si no hay ninguna coincidencia.  
  
## <a name="remarks"></a>Notas  
 Use `Lookup` para recuperar el valor del conjunto de datos especificado para un par de nombre/valor donde hay una relación de 1 a 1. Por ejemplo, para un campo de identificador, puede usar `Lookup` para recuperar el campo Name correspondiente de un conjunto de datos que no está enlazado a la región de datos.  
  
 `Lookup` hace lo siguiente:  
  
-   Evalúa la expresión de origen en el ámbito actual.  
  
-   Evalúa la expresión de destino para cada fila del conjunto de datos especificado una vez aplicados los filtros, según la intercalación del conjunto de datos especificado.  
  
-   En la primera coincidencia de las expresiones de origen y de destino, evalúa la expresión de resultado para dicha fila del conjunto de datos.  
  
-   Devuelve el valor de la expresión de resultado.  
  
 Para recuperar varios valores para un único nombre o campo de clave donde hay una relación de uno a varios, use la [función LookupSet &#40;Generador de informes y SSRS&#41;](report-builder-functions-lookupset-function.md). Para llamar a `Lookup` para un conjunto de valores, utilice [función Multilookup &#40;el generador de informes y SSRS&#41;](report-builder-functions-lookup-function.md).  
  
 Se aplican las siguientes restricciones:  
  
-   `Lookup` se evalúa después de aplicar todas las expresiones de filtro.  
  
-   Solo se admite un nivel de búsqueda. Un origen, un destino o una expresión de resultado no pueden incluir una referencia a una función de búsqueda.  
  
-   Las expresiones de origen y de destino deben dar el mismo tipo de datos. El tipo de devolución es el mismo que el tipo de datos de la expresión de resultado evaluada.  
  
-   Las expresiones de origen, destino y resultado no pueden incluir referencias a variables de informe o de grupo.  
  
-   `Lookup` no se puede usar como una expresión para los siguientes elementos de informe:  
  
    -   Cadenas de conexión dinámicas para un origen de datos.  
  
    -   Campos calculados de un conjunto de datos.  
  
    -   Parámetros de consulta de un conjunto de datos.  
  
    -   Filtros de un conjunto de datos.  
  
    -   Parámetros de informe.  
  
    -   La propiedad Report.Language.  
  
 Para más información, vea [Funciones del generador de informes - referencia de funciones de agregado &#40;Generador de informes y SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) y [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente, se supone que una tabla está enlazada a un conjunto de datos que incluye un campo para el identificador de producto ProductID. Un conjunto de datos independiente denominado "Product" contiene el identificador de producto, ID, y el nombre de producto, Name.  
  
 En la expresión siguiente, `Lookup` compara el valor de ProductID con ID en cada fila del conjunto de datos denominado "Product" y, cuando se encuentra una coincidencia, devuelve el valor del campo Name para dicha fila.  
  
```  
=Lookup(Fields!ProductID.Value, Fields!ID.Value, Fields!Name.Value, "Product")  
```  
  
## <a name="see-also"></a>Vea también  
 [Expresión que se utiliza en los informes &#40;el generador de informes SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Ámbito de expresión para totales, agregados y colecciones integradas &#40;el generador de informes SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  