---
title: Función Multilookup (Generador de informes y SSRS) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 1fec079e-33b3-4e4d-92b3-6b4d06a49a77
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c0425be1f799a078a22965150e10525780e5b687
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2019
ms.locfileid: "56287453"
---
# <a name="report-builder-functions---multilookup-function"></a>Funciones del Generador de informes: función Multilookup
  Devuelve el conjunto de valores de primera coincidencia para el conjunto especificado de nombres a partir de un conjunto de datos que contiene pares nombre/valor.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Multilookup(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *source_expression*  
 (**VariantArray**) Una expresión que se evalúa en el ámbito actual y que especifica el conjunto de nombres o claves que se buscará. Por ejemplo, para un parámetro de varios valores, `=Parameters!IDs.value`.  
  
 *destination_expression*  
 (**Variant**) Una expresión que se evalúa para cada fila de un conjunto de datos y que especifica el nombre o la clave que se hará coincidir. Por ejemplo, `=Fields!ID.Value`.  
  
 *result_expression*  
 (**Variant**) Una expresión que se evalúa para la fila de un conjunto de datos donde *source_expression* = *destination_expression*, y que especifica el valor que se va a recuperar. Por ejemplo, `=Fields!Name.Value`.  
  
 *conjunto de datos*  
 Una constante que especifica el nombre de un conjunto de datos del informe. Por ejemplo, "Colores".  
  
## <a name="return"></a>Devolución  
 Devuelve **VariantArray**o **Nothing** si no hay ninguna coincidencia.  
  
## <a name="remarks"></a>Notas  
 Use **Multilookup** para recuperar un conjunto de valores de un conjunto de datos para los pares nombre-valor donde cada par tiene una relación de uno a uno. **MultiLookup** es equivalente de llamar **Lookup** para un conjunto de nombres o de claves. Por ejemplo, para un parámetro de varios valores que se base en identificadores de clave principal, puede usar **Multilookup** en una expresión de un cuadro de texto en una tabla para recuperar los valores asociados de un conjunto de datos que no esté enlazado al parámetro ni a la tabla.  
  
 **Multilookup** realiza las operaciones siguientes:  
  
-   Evalúa la expresión de origen en el ámbito actual y genera una matriz de objetos de variantes.  
  
-   Para cada objeto de la matriz, llama a la [Función Lookup &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookup-function.md) y agrega el resultado a la matriz de devolución.  
  
-   Devuelve el conjunto de resultados.  
  
 Para recuperar un único valor de un conjunto de datos con pares de nombre y valor para un nombre especificado donde hay una relación de uno a uno, use la [función Lookup &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookup-function.md). Para recuperar varios valores de un conjunto de datos con pares de nombre y valor para un nombre donde hay una relación de uno a varios, use la [Función LookupSet &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookupset-function.md).  
  
 Se aplican las siguientes restricciones:  
  
-   Se evalúa**Multilookup** después de aplicar todas las expresiones de filtro.  
  
-   Solo se admite un nivel de búsqueda. Un origen, un destino o una expresión de resultado no pueden incluir una referencia a una función de búsqueda.  
  
-   Las expresiones de origen y de destino deben dar el mismo tipo de datos.  
  
-   Las expresiones de origen, destino y resultado no pueden incluir referencias a variables de informe o de grupo.  
  
-   **Multilookup** no se puede usar como una expresión para los siguientes elementos de informe:  
  
    -   Cadenas de conexión dinámicas para un origen de datos.  
  
    -   Campos calculados de un conjunto de datos.  
  
    -   Parámetros de consulta de un conjunto de datos.  
  
    -   Filtros de un conjunto de datos.  
  
    -   Parámetros de informe.  
  
    -   La propiedad Report.Language.  
  
 Para más información, vea [Funciones del generador de informes - referencia de funciones de agregado &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) y [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="example"></a>Ejemplo  
 Suponga que un conjunto de datos denominado "Category" contiene el campo CategoryList, que es un campo que incluye una lista separada por comas de identificadores de categoría, "2, 4, 2, 1", por ejemplo.  
  
 El conjunto de datos CategoryNames contiene el identificador y el nombre de la categoría, tal como se muestra en la siguiente tabla.  
  
|Id.|Nombre|  
|--------|----------|  
|1|Accessories|  
|2|Bikes|  
|3|Clothing|  
|4|Components|  
  
 Para buscar los nombres que corresponden a la lista de identificadores, use **Multilookup**. Primero debe dividir la lista en una matriz de cadenas, llamar a **Multilookup** para recuperar los nombres de categoría y concatenar los resultados en una cadena.  
  
 La expresión siguiente, cuando se coloca en un cuadro de texto en una región de datos enlazada al conjunto de datos Category, muestra "Bikes, Components, Bikes, Accessories":  
  
```  
=Join(MultiLookup(Split(Fields!CategoryList.Value,","),  
   Fields!CategoryID.Value,Fields!CategoryName.Value,"Category")),  
   ", ")  
```  
  
## <a name="example"></a>Ejemplo  
 Suponga que un conjunto de datos ProductColors contiene un campo de identificador de color, ColorID, y un campo de valor de color, Color, tal como se muestra en la siguiente tabla.  
  
|ColorID|Color|  
|-------------|-----------|  
|1|Rojo|  
|2|Azul|  
|3|Verde|  
  
 Suponga que el parámetro de varios valores *MyColors* no está enlazado a un conjunto para sus valores disponibles. Los valores predeterminados para el parámetro están establecidos en 2 y 3. La siguiente expresión, cuando se coloca en un cuadro de texto en una tabla, concatena múltiples valores seleccionados para el parámetro en una lista separada por comas y muestra "Blue, Green".  
  
```  
=Join(MultiLookup(Parameters!MyColors.Value,Fields!ColorID.Value,Fields!Color.Value,"ProductColors"),", ")  
```  
  
## <a name="see-also"></a>Consulte también  
 [Usar expresiones en informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
