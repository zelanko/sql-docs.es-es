---
title: Referencia de funciones de agregado (Generador de informes y SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: db6542ee-02d0-4073-90e6-cba8f9510fbb
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: e7b1a8f740ed11bf476bb72896cc14954c63536f
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/15/2019
ms.locfileid: "56287723"
---
# <a name="aggregate-functions-reference-report-builder-and-ssrs"></a>Referencia a las funciones de agregado (Generador de informes y SSRS)
  Para incluir valores de agregado en un informe, puede utilizar las funciones de agregado integradas en las expresiones. La función de agregado predeterminada para los campos numéricos es SUM. Puede modificar la expresión y utilizar una función de agregado integrada diferente o especificar un ámbito diferente. El ámbito identifica qué conjunto de datos utilizar para el cálculo.  
  
 Cuando el procesador de informes combina los datos y el diseño de los informes, se evalúan las expresiones para cada elemento de informe. Al ver cada página del informe, ve los resultados de cada expresión en los elementos de informe representados.  
  
 La siguiente tabla incluye las categorías de funciones integradas que se pueden incluir en una expresión:  
  
-   [Funciones de agregado integradas](#CalculatingAggregates)  
  
-   [Restricciones en los campos integrados, colecciones y funciones de agregado](#Restrictions)  
  
-   [Restricciones en agregados anidados](#NestedRestrictions)  
  
-   [Calcular valores actuales](#CalculatingRunningValues)  
  
-   [Recuperar recuentos de filas](#RetrievingRowCounts)  
  
-   [Buscar valores de otro conjunto de datos](#LookupFunctions)  
  
-   [Recuperar valores dependientes de la ordenación](#RetrievingPostsortValues)  
  
-   [Recuperar agregados de servidor](#RetrievingServerAggregates)  
  
-   [Recuperar nivel recursivo](#RetrievingRecursiveLevel)  
  
-   [Comprobar el ámbito](#TestingforScope)  
  
 Para determinar los ámbitos válidos para una función, vea el tema de referencia de la función en cuestión. Para más información y ejemplos, vea [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="CalculatingAggregates"></a> Funciones de agregado integradas  
 Las funciones integradas siguientes calculan valores de resumen para un conjunto de datos numéricos no NULL del ámbito predeterminado o el ámbito con nombre.  
  
|**Función**|**Descripción**|  
|------------------|---------------------|  
|[Avg](report-builder-functions-avg-function.md)|Devuelve el promedio de todos los valores numéricos no NULL especificados por la expresión, que se evalúa en el contexto del ámbito especificado.|  
|[Count](report-builder-functions-count-function.md)|Devuelve un recuento de los valores no NULL especificados por la expresión, que se evalúa en el contexto del ámbito indicado.|  
|[CountDistinct](report-builder-functions-countdistinct-function.md)|Devuelve un recuento de todos los valores no NULL distintos especificados por la expresión, que se evalúa en el contexto del ámbito especificado.|  
|[Max](report-builder-functions-max-function.md)|Devuelve el valor máximo de todos los valores numéricos no NULL especificados por la expresión, en el contexto del ámbito especificado. Puede usarla para especificar un valor máximo para el eje del gráfico para controlar la escala.|  
|[Min](report-builder-functions-min-function.md)|Devuelve el valor mínimo de todos los valores numéricos no NULL especificados por la expresión, en el contexto del ámbito especificado. Puede usarla para especificar un valor mínimo para el eje del gráfico para controlar la escala.|  
|[StDev](report-builder-functions-stdev-function.md)|Devuelve la desviación estándar de todos los valores numéricos no NULL especificados por la expresión, que se evalúa en el contexto del ámbito especificado.|  
|[StDevP](report-builder-functions-stdevp-function.md)|Devuelve la desviación estándar de población de todos los valores numéricos no NULL especificados por la expresión, que se evalúa en el contexto del ámbito especificado.|  
|[Sum](report-builder-functions-sum-function.md)|Devuelve la suma de todos los valores numéricos no NULL especificados por la expresión, que se evalúa en el contexto del ámbito especificado.|  
|[Union](report-builder-functions-union-function.md)|Devuelve la unión de todos los valores de datos espaciales no NULL del tipo `SqlGeometry` o `SqlGeography` especificados por la expresión, que se evalúa en el ámbito especificado.|  
|[Var](report-builder-functions-var-function.md)|Devuelve la varianza de todos los valores numéricos no NULL especificados por la expresión, que se evalúa en el contexto del ámbito especificado.|  
|[VarP](report-builder-functions-varp-function.md)|Devuelve la varianza de población de todos los valores numéricos no NULL especificados por la expresión, que se evalúa en el contexto del ámbito especificado.|  
  
##  <a name="Restrictions"></a> Restricciones en los campos integrados, colecciones y funciones de agregado  
 La tabla siguiente resume las restricciones de las ubicaciones de informes donde puede agregar expresiones que contienen referencias a las colecciones integradas globales.  
  
|Ubicación en informe|Campos|Parámetros|ReportItems|PageNumber<br /><br /> TotalPages|DataSource<br /><br /> DataSet|Variables|RenderFormat|  
|------------------------|------------|----------------|-----------------|-------------------------------|----------------------------|---------------|------------------|  
|Encabezado de página<br /><br /> Pie de página|Sí|Sí|A lo sumo uno<br /><br /> Nota 1|Sí|Sí|Sí|Sí|  
|Cuerpo|Sí<br /><br /> Nota 2|Sí|Solo los elementos del ámbito actual o de un ámbito que lo contenga<br /><br /> Nota 3|No|Sí|Sí|Sí|  
|Parámetro de informe|No|Solo los parámetros anteriores en la lista<br /><br /> Nota 4|No|No|No|No|No|  
|Campo|Sí|Sí|No|No|No|No|No|  
|Parámetro de consulta|No|Sí|No|No|No|No|No|  
|Expresión de grupo|Sí|Sí|No|No|Sí|No|No|  
|Expresión de ordenación|Sí|Sí|No|No|Sí|Sí<br /><br /> Nota 5|No|  
|Expresión de filtro|Sí|Sí|No|No|Sí|Sí<br /><br /> Nota 6|No|  
|Código|No|Sí<br /><br /> Nota 7|No|No|No|No|No|  
|Idioma de los informes|No|Sí|No|No|No|No|No|  
|Variables|Sí|Sí|No|No|Sí|Ámbito actual o que lo contiene|No|  
|Agregados|Sí|Sí|Solo en encabezado de página o pie de página|Solo en agregados de elementos de informe|Sí|No|No|  
|Funciones de búsqueda|Sí|Sí|Sí|No|Sí|No|No|  
  
-   **Nota 1.** ReportItems debe existir en la página del informe representado o su valor es Null. Si la visibilidad de un elemento de informe depende de una expresión que se evalúa como False, el elemento de informe no existe en la página.  
  
-   **Nota 2.** Si una referencia de campo se utiliza en un ámbito de grupo y no está incluida en la expresión de grupo, el valor para el campo es indefinido, a menos que haya solo un valor en el ámbito. Para especificar un valor, utilice Primero o Último, y el ámbito de grupo.  
  
-   **Nota 3.** Las expresiones que incluyen una referencia a ReportItems pueden especificar los valores para otros ReportItems en el mismo ámbito de grupo o en un ámbito de grupo contenedor.  
  
-   **Nota 4.** Los valores de propiedad para los parámetros anteriores podrían ser Null.  
  
-   **Nota 5.** Solo en las ordenaciones de miembro. No puede usarse en expresiones de ordenación de regiones de datos.  
  
-   **Nota 6.** Solo en los filtros de miembros. No puede utilizar en expresiones de filtro de conjunto de datos o región de datos.  
  
-   **Nota 7.** La colección de parámetros no se inicializa hasta después de procesar el bloque de código, por lo que no se pueden usar los métodos controlar los parámetros en la inicialización.  
  
-   **Nota 8.** El tipo de datos de todos los agregados excepto Count y CountDistinct debe ser el mismo o null para todos los valores.  
  
##  <a name="NestedRestrictions"></a> Restricciones en agregados anidados  
 En la tabla siguiente se resumen las restricciones en las que las funciones de agregados pueden especificar otras funciones de agregado como agregados anidados.  
  
|Contexto|RunningValue|RowNumber|Primero<br /><br /> Último|Previous|Funciones de suma y otras de ordenación previa|Agregados ReportItem|Funciones de búsqueda|Función de agregado|  
|-------------|------------------|---------------|--------------------|--------------|-------------------------------------|---------------------------|----------------------|------------------------|  
|Valor actual|No|No|No|No|Sí|No|Sí|No|  
|Primero<br /><br /> Último|No|No|No|No|Sí|No|No|No|  
|Previous|Sí|Sí|Sí|No|Sí|No|Sí|No|  
|Funciones de suma y otras de ordenación previa|No|No|No|No|Sí|No|Sí|No|  
|Agregados ReportItem|No|No|No|No|No|No|No|No|  
|Funciones de búsqueda|Sí|Sí<br /><br /> Nota 1|Sí<br /><br /> Nota 1|Sí<br /><br /> Nota 1|Sí<br /><br /> Nota 1|Sí<br /><br /> Nota 1|No|No|  
|Función de agregado|No|No|No|No|No|No|No|No|  
  
-   **Nota 1.** Las funciones de agregado solo se permiten dentro de la expresión *Source* de una función de búsqueda si la función de búsqueda no está contenida en un agregado. Las funciones de agregado no se permiten dentro de las expresiones *Destination* o *Result* de una función Lookup.  
  
##  <a name="CalculatingRunningValues"></a> Calcular valores actuales  
 Las siguientes funciones incorporadas calculan los valores actuales para un conjunto de datos. `RowNumber` se parece a `RunningValue` en que devuelve el valor actual de un recuento que se incrementa por cada fila del ámbito contenedor. El parámetro de ámbito para estas funciones debe especificar un ámbito contenedor, que controla cuándo se reinicia el recuento.  
  
|**Función**|**Descripción**|  
|------------------|---------------------|  
|[RowNumber](report-builder-functions-rownumber-function.md)|Devuelve un recuento actualizado del número de filas para el ámbito especificado. La función `RowNumber` reinicia el recuento en 1, no en 0.|  
|[RunningValue](report-builder-functions-runningvalue-function.md)|Devuelve un agregado actualizado de todos los valores numéricos no NULL especificados por la expresión, que se evalúa en el contexto del ámbito especificado.|  
  
##  <a name="RetrievingRowCounts"></a> Recuperar recuentos de filas  
 La función integrada siguiente calcula el número de filas existentes en el ámbito especificado. Use esta función para contar todas las filas, incluso las filas con valores NULL.  
  
|**Función**|**Descripción**|  
|------------------|---------------------|  
|[CountRows](report-builder-functions-countrows-function.md)|Devuelve el número de filas del ámbito especificado, incluidas las filas con valores NULL.|  
  
##  <a name="LookupFunctions"></a> Buscar valores de otro conjunto de datos  
 Las siguientes funciones de búsqueda recuperan valores de un conjunto de datos especificado.  
  
|**Función**|**Descripción**|  
|------------------|---------------------|  
|[Función Lookup](report-builder-functions-lookup-function.md)|Devuelve un valor de un conjunto de datos para una expresión especificada.|  
|[Función LookupSet](report-builder-functions-lookupset-function.md)|Devuelve un conjunto de valores de un conjunto de datos para una expresión especificada.|  
|[Función Multilookup](report-builder-functions-multilookup-function.md)|Devuelve el conjunto de valores de primera coincidencia para un conjunto de nombres a partir de un conjunto de datos que contiene pares de nombre/valor.|  
  
##  <a name="RetrievingPostsortValues"></a> Recuperar valores dependientes de la ordenación  
 Las funciones integradas siguientes devuelven el primer valor, el último valor o el valor anterior dentro de un ámbito determinado. Estas funciones dependen del criterio de ordenación de los valores de datos. Por ejemplo, use estas funciones para encontrar el primer y el último valor de una página para crear un encabezado de página de estilo diccionario. Use `Previous` para comparar un valor de una fila con el valor de la fila anterior dentro de un ámbito específico, como por ejemplo, para encontrar los valores de los porcentajes de año a año en una tabla.  
  
|**Función**|**Descripción**|  
|------------------|---------------------|  
|[Primero](report-builder-functions-first-function.md)|Devuelve el primer valor de la expresión especificada en el ámbito especificado.|  
|[Último](report-builder-functions-last-function.md)|Devuelve el último valor de la expresión especificada en el ámbito especificado.|  
|[Previous](report-builder-functions-previous-function.md)|Devuelve el valor o el valor agregado especificado para la instancia anterior de un elemento dentro del ámbito especificado.|  
  
##  <a name="RetrievingServerAggregates"></a> Recuperar agregados de servidor  
 La función integrada siguiente recupera agregados personalizados del proveedor de datos. Por ejemplo, usando un tipo de origen de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , puede recuperar agregados calculados en el servidor del origen de datos para su uso en un encabezado de grupo.  
  
|**Función**|**Descripción**|  
|------------------|---------------------|  
|[Agregado](report-builder-functions-aggregate-function.md)|Devuelve un agregado personalizado de la expresión especificada, según esté definido en el proveedor de datos.|  
  
##  <a name="TestingforScope"></a> Comprobar el ámbito  
 La función integrada siguiente comprueba el contexto actual de un elemento de informe para ver si es un miembro de un ámbito determinado.  
  
|Función|Descripción|  
|--------------|-----------------|  
|[InScope](report-builder-functions-inscope-function.md)|Indica si la instancia actual de un elemento se halla en el ámbito especificado.|  
  
##  <a name="RetrievingRecursiveLevel"></a> Recuperar nivel recursivo  
 La función integrada siguiente recupera el nivel actual cuando se procesa una jerarquía recursiva. Use el resultado de esta función con la propiedad `Padding` de un cuadro de texto para controlar el nivel de sangría de una jerarquía visual para un grupo recursivo. Para obtener más información, vea [Crear grupos de jerarquía recursiva &#40;Generador de informes y SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
|Función|Descripción|  
|--------------|-----------------|  
|[Nivel](report-builder-functions-level-function.md)|Devuelve el nivel actual de profundidad de una jerarquía recursiva.|  
  
## <a name="see-also"></a>Vea también  
 [Usar expresiones en informes &#40;Generador de informes y SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Ejemplos de expresiones &#40;Generador de informes y SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Ámbito de expresión para los totales, agregados y colecciones integradas &#40;Generador de informes y SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
