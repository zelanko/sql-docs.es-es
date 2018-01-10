---
title: "Función LookupSet (Generador de informes y SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7685acfd-1c8d-420c-993c-903236fbe1ff
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 54455fd8ab820d9f32525308220c5dd427470d07
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2018
---
# <a name="report-builder-functions---lookupset-function"></a>Funciones del Generador de informes: función LookupSet
  Devuelve el conjunto de valores coincidentes para el nombre especificado de un conjunto de datos que contiene pares nombre/valor.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
LookupSet(source_expression, destination_expression, result_expression, dataset)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *source_expression*  
 (**Variant**) Una expresión que se evalúa en el ámbito actual y que especifica el nombre o la clave que se buscará. Por ejemplo, `=Fields!ID.Value`.  
  
 *destination_expression*  
 (**Variant**) Una expresión que se evalúa para cada fila de un conjunto de datos y que especifica el nombre o la clave que se hará coincidir. Por ejemplo, `=Fields!CustomerID.Value`.  
  
 *result_expression*  
 (**Variant**) Una expresión que se evalúa para la fila de un conjunto de datos donde *source_expression* = *destination_expression*, y que especifica el valor que se va a recuperar. Por ejemplo, `=Fields!PhoneNumber.Value`.  
  
 *conjunto de datos*  
 Una constante que especifica el nombre de un conjunto de datos del informe. Por ejemplo, "ContactInformation".  
  
## <a name="return"></a>Devolución  
 Devuelve **VariantArray**o **Nothing** si no hay ninguna coincidencia.  
  
## <a name="remarks"></a>Notas  
 Use **LookupSet** para recuperar un conjunto de valores del conjunto de datos especificado correspondiente a un par nombre-valor donde hay una relación de uno a varios. Por ejemplo, para un identificador de cliente en una tabla, puede usar **LookupSet** para recuperar todos los números de teléfono asociados a ese cliente de un conjunto de datos que no está enlazado a la región de datos.  
  
 **LookupSet** realiza las operaciones siguientes:  
  
-   Evalúa la expresión de origen en el ámbito actual.  
  
-   Evalúa la expresión de destino para cada fila del conjunto de datos especificado una vez aplicados los filtros, según la intercalación del conjunto de datos especificado.  
  
-   Por cada coincidencia de las expresiones de origen y de destino, evalúa la expresión de resultado para dicha fila del conjunto de datos.  
  
-   Devuelve el conjunto de valores de expresión de resultado.  
  
 Para recuperar un único valor de un conjunto de datos con pares nombre-valor para un nombre especificado donde hay una relación de uno a uno, use la [función Lookup &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/report-builder-functions-lookup-function.md). Para llamar a **Lookup** para un conjunto de valores, use la [función Multilookup &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/report-builder-functions-multilookup-function.md).  
  
 Se aplican las siguientes restricciones:  
  
-   Se evalúa**LookupSet** después de aplicar todas las expresiones de filtro.  
  
-   Solo se admite un nivel de búsqueda. Un origen, un destino o una expresión de resultado no pueden incluir una referencia a una función de búsqueda.  
  
-   Las expresiones de origen y de destino deben dar el mismo tipo de datos.  
  
-   Las expresiones de origen, destino y resultado no pueden incluir referencias a variables de informe o de grupo.  
  
-   **LookupSet** no se puede usar como una expresión para los siguientes elementos de informe:  
  
    -   Cadenas de conexión dinámicas para un origen de datos.  
  
    -   Campos calculados de un conjunto de datos.  
  
    -   Parámetros de consulta de un conjunto de datos.  
  
    -   Filtros de un conjunto de datos.  
  
    -   Parámetros de informe.  
  
    -   La propiedad Report.Language.  
  
 Para más información, vea [Funciones del generador de informes - referencia de funciones de agregado &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) y [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="example"></a>Ejemplo  
 En el siguiente ejemplo se supone que la tabla está enlazada a un conjunto de datos que incluye un identificador de territorio de ventas, TerritoryGroupID. Un conjunto de datos independiente denominado "Stores" contiene la lista de todas las tiendas de un territorio e incluye el identificador de territorio, ID, y el nombre de la tienda, StoreName.  
  
 En la siguiente expresión, **LookupSet** compara el valor TerritoryGroupID con ID por cada fila del conjunto de datos denominado "Stores". Por cada coincidencia, el valor del campo StoreName de dicha fila se agrega al conjunto de resultados.  
  
```  
=LookupSet(Fields!TerritoryGroupID.Value, Fields!ID.Value, Fields!StoreName.Value, "Stores")  
```  
  
## <a name="example"></a>Ejemplo  
 Dado que **LookupSet** devuelve una colección de objetos, no se puede mostrar la expresión de resultado directamente en un cuadro de texto. Puede concatenar el valor de cada objeto de la colección como una cadena.  
  
 Use la función [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] Join **de** para crear una cadena delimitada a partir de un conjunto de objetos. Use la coma como separador para combinar los objetos en una sola línea. En algunos representadores, puede usar un salto de línea de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] (`vbCrLF`) como separador para enumerar cada valor en una nueva línea.  
  
 La siguiente expresión, cuando se usa como la propiedad Value para un cuadro de texto, usa **Join** para crear una lista.  
  
```  
=Join(LookupSet(Fields!TerritoryGroupID.Value, Fields!ID.Value, Fields!StoreName.Value, "Stores"),",")  
```  
  
## <a name="example"></a>Ejemplo  
 Para los cuadros de texto que solo se representan pocas veces, puede agregar código personalizado para generar el código HTML para mostrar valores en un cuadro de texto. El código HTML en un cuadro de texto requiere procesamiento adicional, por lo que no es una buena opción para un cuadro de texto que se representa miles de veces.  
  
 Copie las siguientes funciones de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] en un bloque Code en una definición de informe. **MakeList** toma la matriz de objetos que se devuelve en *result_expression* y genera una lista no ordenada mediante etiquetas HTML. **Length** devuelve el número de elementos en la matriz de objetos.  
  
```  
Function MakeList(ByVal items As Object()) As String  
   If items Is Nothing Then  
      Return Nothing  
   End If  
  
   Dim builder As System.Text.StringBuilder =   
      New System.Text.StringBuilder()  
   builder.Append("<ul>")  
  
   For Each item As Object In items  
      builder.Append("<li>")  
      builder.Append(item)  
   Next  
   builder.Append("</ul>")  
  
   Return builder.ToString()  
End Function  
  
Function Length(ByVal items as Object()) as Integer  
   If items is Nothing Then  
      Return 0  
   End If  
   Return items.Length  
End Function  
```  
  
## <a name="example"></a>Ejemplo  
 Para generar el código HTML, debe llamar a la función. Pegue la siguiente expresión en la propiedad Value del cuadro de texto y establezca el tipo de marcado del texto en HTML. Para más información, vea [Agregar HTML a un informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/add-html-into-a-report-report-builder-and-ssrs.md).  
  
```  
=Code.MakeList(LookupSet(Fields!TerritoryGroupID.Value, Fields!ID.Value, Fields!StoreName.Value, "Stores"))  
```  
  
## <a name="see-also"></a>Ver también  
 [Usar expresiones en informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de datos en expresiones &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
