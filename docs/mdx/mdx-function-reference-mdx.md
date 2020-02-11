---
title: Referencia de funciones MDX (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: ff14718e09fa3732a40ea245430f33c599325eea
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68003512"
---
# <a name="mdx-function-reference-mdx"></a>Referencia de funciones MDX (MDX)


  Analysis Services proporciona el uso de funciones en la sintaxis de expresiones multidimensionales (MDX). Las funciones se pueden utilizar en cualquier instrucción de MDX válida y se utilizan a menudo en consultas, definiciones de resumen personalizadas y otros cálculos. En esta sección se proporciona información sobre las funciones MDX.  
  
 Puede utilizar las siguientes tablas para buscar funciones por la categoría del valor devuelto, o bien puede seleccionar una función por el nombre en la lista alfabética de la tabla de contenidos.  
  
## <a name="array-functions"></a>Funciones de matriz  
  
|Función|Descripción|  
|--------------|-----------------|  
|[&#41;SetToArray &#40;MDX](../mdx/settoarray-mdx.md)|Convierte uno o más conjuntos en una matriz, para usarla en funciones definidas por el usuario.|  
  
## <a name="hierarchy-functions"></a>Funciones de jerarquía  
  
|Función|Descripción|  
|--------------|-----------------|  
|[Jerarquía &#40;MDX&#41;](../mdx/hierarchy-mdx.md)|Devuelve la jerarquía que contiene un miembro o nivel especificado.|  
|[Dimension &#40;MDX&#41;](../mdx/dimension-mdx.md)|Devuelve la dimensión que contiene un miembro, nivel o jerarquía especificado.|  
|[Dimensiones &#40;&#41;MDX](../mdx/dimensions-mdx.md)|Devuelve una jerarquía especificada mediante una expresión numérica o de cadena.|  
  
## <a name="level-functions"></a>Funciones de nivel  
  
|Función|Descripción|  
|--------------|-----------------|  
|[Nivel &#40;&#41;MDX](../mdx/level-mdx.md)|Devuelve el nivel de un miembro.|  
|[Niveles &#40;&#41;MDX](../mdx/levels-mdx.md)|Devuelve el nivel cuya posición en una dimensión o jerarquía se especifica mediante una expresión numérica, o cuyo nombre se especifica mediante una expresión de cadena.|  
  
## <a name="logical-functions"></a>Funciones lógicas  
  
|Función|Descripción|  
|--------------|-----------------|  
|[&#41;IsAncestor &#40;MDX](../mdx/isancestor-mdx.md)|Informa de si un miembro especificado es un antecesor de otro miembro especificado.|  
|[IsEmpty &#40;&#41;MDX](../mdx/isempty-mdx.md)|Informa de si la expresión evaluada es el valor de celda vacía.|  
|[&#41;IsGeneration &#40;MDX](../mdx/isgeneration-mdx.md)|Informa de si un miembro especificado es una generación especificada.|  
|[IsLeaf &#40;&#41;MDX](../mdx/isleaf-mdx.md)|Informa de si un miembro especificado es un miembro hoja.|  
|[&#41;IsSibling &#40;MDX](../mdx/issibling-mdx.md)|Informa de si un miembro especificado está en el mismo nivel que otro miembro especificado.|  
  
## <a name="member-functions"></a>Funciones de miembro  
  
|Función|Descripción|  
|--------------|-----------------|  
|[&#41;&#40;de MDX](../mdx/ancestor-mdx.md)|Devuelve el antecesor de un miembro en un nivel o distancia especificados.|  
|[&#41;ClosingPeriod &#40;MDX](../mdx/closingperiod-mdx.md)|Devuelve el último elemento del mismo nivel entre los descendientes de un miembro en un nivel especificado.|  
|[Primo &#40;MDX&#41;](../mdx/cousin-mdx.md)|Devuelve el miembro secundario con la misma posición relativa bajo un miembro primario que el miembro secundario especificado.|  
|[CurrentMember &#40;MDX&#41;](../mdx/currentmember-mdx.md)|Devuelve el miembro actual de una dimensión o jerarquía especificada durante la iteración.|  
|[DataMember &#40;&#41;MDX](../mdx/datamember-mdx.md)|Devuelve el miembro de datos generados por el sistema asociado a un miembro no hoja de una dimensión.|  
|[DefaultMember &#40;MDX&#41;](../mdx/defaultmember-mdx.md)|Devuelve el miembro predeterminado de una dimensión o jerarquía.|  
|[FirstChild &#40;&#41;MDX](../mdx/firstchild-mdx.md)|Devuelve el primer elemento secundario de un miembro.|  
|[&#41;FirstSibling &#40;MDX](../mdx/firstsibling-mdx.md)|Devuelve el primer elemento secundario del elemento primario de un miembro.|  
|[Elemento &#40;miembro&#41; &#40;MDX&#41;](../mdx/item-member-mdx.md)|Devuelve un miembro de una tupla especificada.|  
|[Lag &#40;&#41;MDX](../mdx/lag-mdx.md)|Devuelve el miembro que se encuentra un número especificado de posiciones antes de un miembro especificado en la dimensión del miembro.|  
|[LastChild &#40;MDX&#41;](../mdx/lastchild-mdx.md)|Devuelve el último elemento secundario de un miembro especificado.|  
|[&#41;LastSibling &#40;MDX](../mdx/lastsibling-mdx.md)|Devuelve el último elemento secundario del elemento primario de un miembro especificado.|  
|[Cliente potencial &#40;MDX&#41;](../mdx/lead-mdx.md)|Devuelve el miembro que se encuentra un número especificado de posiciones que siguen a un miembro especificado en la dimensión del miembro.|  
|[&#41;LinkMember &#40;MDX](../mdx/linkmember-mdx.md)|Devuelve el miembro equivalente a un miembro especificado de una jerarquía especificada.|  
|[Miembros &#40;cadena&#41; &#40;MDX&#41;](../mdx/members-string-mdx.md)|Devuelve un miembro especificado por una expresión de cadena.|  
|[&#41;NextMember &#40;MDX](../mdx/nextmember-mdx.md)|Devuelve el siguiente miembro del nivel que contiene un miembro especificado|  
|[&#41;OpeningPeriod &#40;MDX](../mdx/openingperiod-mdx.md)|Devuelve el primer miembro del mismo nivel entre los descendientes de un nivel especificado (opcionalmente, en un miembro especificado).|  
|[&#41;ParallelPeriod &#40;MDX](../mdx/parallelperiod-mdx.md)|Devuelve un miembro de un periodo anterior en la misma posición relativa que el indicado.|  
|[&#41;&#40;MDX](../mdx/parent-mdx.md)|Devuelve el elemento primario de un miembro.|  
|[&#41;PrevMember &#40;MDX](../mdx/prevmember-mdx.md)|Devuelve el miembro anterior en el nivel que contiene un miembro especificado.|  
|[&#41;StrToMember &#40;MDX](../mdx/strtomember-mdx.md)|Devuelve el miembro especificado por una cadena con formato MDX.|  
|[UnknownMember &#40;&#41;MDX](../mdx/unknownmember-mdx.md)|Devuelve el miembro desconocido asociado con un nivel o miembro.|  
|[&#41;ValidMeasure &#40;MDX](../mdx/validmeasure-mdx.md)|Devuelve una medida válida de un cubo virtual, al forzar dimensiones no aplicables al nivel superior.|  
  
## <a name="numeric-functions"></a>Funciones numéricas  
  
|Función|Descripción|  
|--------------|-----------------|  
|[&#40;de&#41;MDX de agregado](../mdx/aggregate-mdx.md)|Devuelve un valor escalar calculado al agregar medidas o bien una expresión numérica especificada de forma opcional sobre las tuplas de un conjunto especificado.|  
|[Promedio de&#41;MDX de &#40;](../mdx/avg-mdx.md)|Devuelve el valor medio de las medidas o el valor medio de una expresión numérica opcional, evaluado sobre un conjunto especificado.|  
|[&#41;CalculationCurrentPass &#40;MDX](../mdx/calculationcurrentpass-mdx.md)|Devuelve el paso de cálculo actual de un cubo para el contexto de consulta especificado.|  
|[&#41;CalculationPassValue &#40;MDX](../mdx/calculationpassvalue-mdx.md)|Devuelve el valor de una expresión MDX evaluada sobre el paso de cálculo especificado de un cubo.|  
|[&#41;CoalesceEmpty &#40;MDX](../mdx/coalesceempty-mdx.md)|Fusiona en un número o en una cadena un valor de celda vacía, y devuelve el valor fusionado.|  
|[Correlación &#40;&#41;MDX](../mdx/correlation-mdx.md)|Devuelve el coeficiente de correlación de dos series evaluadas en un conjunto.|  
|[Recuento &#40;dimensión&#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)|Devuelve el número de dimensiones de un cubo.|  
|[Recuento &#40;niveles de jerarquía&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)|Devuelve el número de niveles de una dimensión o jerarquía.|  
|[Count &#40;establecer&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)|Devuelve el número de celdas de un conjunto.|  
|[Count &#40;tupla&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)|Devuelve el número de dimensiones de una tupla.|  
|[Covarianza &#40;MDX&#41;](../mdx/covariance-mdx.md)|Devuelve la covarianza de población de dos series evaluadas en un conjunto utilizando la fórmula de llenado sesgada.|  
|[&#41;MDX &#40;de covarianza](../mdx/covariancen-mdx.md)|Devuelve la covarianza de muestra de dos series evaluadas en un conjunto utilizando la fórmula de población no sesgada.|  
|[DistinctCount &#40;MDX&#41;](../mdx/distinctcount-mdx.md)|Devuelve el número de tuplas distintas y no vacías de un conjunto.|  
|[IIf &#40;&#41;MDX](../mdx/iif-mdx.md)|Devuelve uno de los dos valores determinados por una prueba lógica.|  
|[&#41;LinRegIntercept &#40;MDX](../mdx/linregintercept-mdx.md)|Calcula la regresión lineal de un conjunto y devuelve el valor de la intercepción en la línea de regresión, y = AX + b.|  
|[&#41;LinRegPoint &#40;MDX](../mdx/linregpoint-mdx.md)|Calcula la regresión lineal de un conjunto y devuelve el valor de *y* en la línea de regresión, y = AX + b.|  
|[&#41;LinRegR2 &#40;MDX](../mdx/linregr2-mdx.md)|Calcula la regresión lineal de un conjunto y devuelve el coeficiente de determinación, R2.|  
|[&#41;LinRegSlope &#40;MDX](../mdx/linregslope-mdx.md)|Calcula la regresión lineal de un conjunto y devuelve el valor de la pendiente en la línea de regresión, y = AX + b.|  
|[&#41;LinRegVariance &#40;MDX](../mdx/linregvariance-mdx.md)|Calcula la regresión lineal de un conjunto y devuelve la varianza asociada a la línea de regresión, y = AX + b.|  
|[&#41;MDX &#40;MDX](../mdx/lookupcube-mdx.md)|Devuelve el valor de una expresión MDX evaluada sobre otro cubo especificado en la misma base de datos.|  
|[&#41;MDX &#40;máx.](../mdx/max-mdx.md)|Devuelve el valor máximo de una expresión numérica evaluada sobre un conjunto.|  
|[Mediana &#40;MDX&#41;](../mdx/median-mdx.md)|Devuelve el valor medio de una expresión numérica evaluada sobre un conjunto.|  
|[&#41;mínimo &#40;MDX](../mdx/min-mdx.md)|Devuelve el valor mínimo de una expresión numérica evaluada sobre un conjunto.|  
|[Ordinal &#40;MDX&#41;](../mdx/ordinal-mdx.md)|Devuelve el valor ordinal (con base cero) asociado a un nivel.|  
|[Predecir &#40;MDX&#41;](../mdx/predict-mdx.md)|Devuelve un valor de una expresión numérica evaluada sobre un modelo de minería de datos.|  
|[Rango &#40;MDX&#41;](../mdx/rank-mdx.md)|Devuelve el intervalo con base uno de una tupla especificada en un conjunto especificado.|  
|[RollupChildren &#40;MDX&#41;](../mdx/rollupchildren-mdx.md)|Devuelve un valor generado mediante la acumulación de los valores de los elementos secundarios de un miembro especificado, utilizando el operador unario especificado.|  
|[&#41;StdDev &#40;MDX](../mdx/stddev-mdx.md)|Alias para [Stdev &#40;&#41;MDX ](../mdx/stdev-mdx.md).|  
|[&#41;StddevP &#40;MDX](../mdx/stddevp-mdx.md)|Alias para [StdevP &#40;&#41;MDX ](../mdx/stdevp-mdx.md).|  
|[DesvEst &#40;&#41;MDX](../mdx/stdev-mdx.md)|Devuelve la desviación de muestra estándar de una expresión numérica evaluada sobre un conjunto, mediante la fórmula de población no sesgada.|  
|[StdevP &#40;&#41;MDX](../mdx/stdevp-mdx.md)|Devuelve la desviación estándar de población de una expresión numérica evaluada sobre un conjunto, mediante la fórmula de población sesgada.|  
|[&#41;StrToValue &#40;MDX](../mdx/strtovalue-mdx.md)|Devuelve el valor especificado por una cadena con formato MDX.|  
|[SUM &#40;MDX&#41;](../mdx/sum-mdx.md)|Devuelve la suma de una expresión numérica evaluada sobre un conjunto.|  
|[Valor &#40;&#41;MDX](../mdx/value-mdx.md)|Devuelve el valor de una medida.|  
|[&#41;&#40;MDX](../mdx/var-mdx.md)|Devuelve la varianza de muestra de una expresión numérica evaluada en un conjunto, mediante la fórmula de población no sesgada.|  
|[Varianza &#40;&#41;MDX](../mdx/variance-mdx.md)|Alias para la [&#41;de &#40;MDX ](../mdx/var-mdx.md).|  
|[&#41;VarianceP &#40;MDX](../mdx/variancep-mdx.md)|Alias para [VarP &#40;&#41;MDX ](../mdx/varp-mdx.md).|  
|[VarP &#40;&#41;MDX](../mdx/varp-mdx.md)|Devuelve la varianza de población de una expresión numérica evaluada en un conjunto, mediante la fórmula de población sesgada.|  
  
## <a name="set-functions"></a>Funciones de conjunto  
  
|Función|Descripción|  
|--------------|-----------------|  
|[&#41;AddCalculatedMembers &#40;MDX](../mdx/addcalculatedmembers-mdx.md)|Devuelve un conjunto generado al agregar miembros calculados a un conjunto especificado.|  
|[&#41;AllMembers &#40;MDX](../mdx/allmembers-mdx.md)|Devuelve un conjunto que contiene todos los miembros de la dimensión, jerarquía o nivel especificados, incluyendo los miembros calculados.|  
|[Antecesores &#40;&#41;MDX](../mdx/ancestors-mdx.md)|Devuelve un conjunto de todos los antecesores de un miembro en un nivel o distancia especificados.|  
|[Antecesores &#40;&#41;MDX](../mdx/ascendants-mdx.md)|Devuelve el conjunto de antecesores de un miembro especificado, incluyendo el propio miembro.|  
|[&#41;de &#40;de los ejes MDX](../mdx/axis-mdx.md)|Devuelve un conjunto definido en un eje.|  
|[&#41;BottomCount &#40;MDX](../mdx/bottomcount-mdx.md)|Ordena un conjunto de forma ascendente y devuelve el número de tuplas especificado con los valores más bajos.|  
|[&#41;BottomPercent &#40;MDX](../mdx/bottompercent-mdx.md)|Ordena un conjunto de forma ascendente y devuelve un conjunto de tuplas con los valores más bajos con un total acumulado igual o inferior a un porcentaje especificado.|  
|[&#41;BottomSum &#40;MDX](../mdx/bottomsum-mdx.md)|Ordena un conjunto de forma ascendente y devuelve un conjunto de tuplas con los valores más bajos con un total igual o inferior a un valor especificado.|  
|[Secundarios &#40;&#41;MDX](../mdx/children-mdx.md)|Devuelve el elemento secundario de un miembro especificado.|  
|[Crossjoin &#40;MDX&#41;](../mdx/crossjoin-mdx.md)|Devuelve el producto cruzado de uno o más conjuntos.|  
|[&#41;CurrentOrdinal &#40;MDX](../mdx/currentordinal-mdx.md)|Devuelve el número de iteración actual dentro de un conjunto durante la iteración.|  
|[Descendientes &#40;&#41;MDX](../mdx/descendants-mdx.md)|Devuelve el conjunto de descendientes de un miembro en el nivel o distancia especificados; opcionalmente puede incluir o excluir los descendientes de otros niveles.|  
|[DISTINCT &#40;MDX&#41;](../mdx/distinct-mdx.md)|Devuelve un conjunto, eliminando tuplas duplicadas de un conjunto especificado.|  
|[&#41;DrilldownLevel &#40;MDX](../mdx/drilldownlevel-mdx.md)|Aumenta los detalles de los miembros de un conjunto a un nivel por debajo del nivel más bajo representado en el conjunto o un nivel por debajo del nivel especificado opcionalmente de un miembro representado en el conjunto.|  
|[&#41;DrilldownLevelBottom &#40;MDX](../mdx/drilldownlevelbottom-mdx.md)|Aumenta el detalle de los miembros inferiores de un conjunto, de un nivel especificado a otro inferior.|  
|[&#41;DrilldownLevelTop &#40;MDX](../mdx/drilldownleveltop-mdx.md)|Aumenta el detalle de los miembros superiores de un conjunto, de un nivel especificado a otro inferior.|  
|[DrilldownMember &#40;&#41;MDX](../mdx/drilldownmember-mdx.md)|Aumenta el detalle de los miembros de un conjunto especificado presentes en un segundo conjunto especificado. Alternativamente, esta función aumenta el detalle de un conjunto de tuplas.|  
|[&#41;DrilldownMemberBottom &#40;MDX](../mdx/drilldownmemberbottom-mdx.md)|Aumenta el nivel de detalle de miembros de un conjunto especificado que están presentes en otro conjunto especificado, lo que limita el conjunto de resultados a un número específico de miembros. Alternativamente, esta función también aumenta el detalle de un conjunto de tuplas.|  
|[&#41;DrilldownMemberTop &#40;MDX](../mdx/drilldownmembertop-mdx.md)|Aumenta el nivel de detalle de miembros de un conjunto especificado que están presentes en otro conjunto especificado, lo que limita el conjunto de resultados a un número específico de miembros. Como alternativa, esta función profundiza en un conjunto de tuplas.|  
|[&#41;DrillupLevel &#40;MDX](../mdx/drilluplevel-mdx.md)|Reduce el detalle de los miembros de un conjunto por debajo de un nivel especificado.|  
|[&#41;DrillupMember &#40;MDX](../mdx/drillupmember-mdx.md)|Reduce el detalle de los miembros de un conjunto especificado presentes en un segundo conjunto especificado.|  
|[Excepto &#40;&#41;MDX](../mdx/except-mdx-function.md)|Encuentra la diferencia entre dos conjuntos, reteniendo opcionalmente los duplicados.|  
|[Existe &#40;&#41;MDX](../mdx/exists-mdx.md)|Devuelve el conjunto de miembros de un conjunto que existen con una o más tuplas de otros conjuntos.|  
|[Extraer &#40;&#41;MDX](../mdx/extract-mdx.md)|Devuelve un conjunto de tuplas a partir de elementos de dimensión extraídos.|  
|[Filtrar &#40;&#41;MDX](../mdx/filter-mdx.md)|Devuelve el conjunto resultante de filtrar un determinado conjunto con una condición de búsqueda.|  
|[Generar &#40;&#41;MDX](../mdx/generate-mdx.md)|Aplica un conjunto a cada miembro de otro conjunto y a continuación combina los conjuntos resultantes mediante unión. Alternativamente, esta función devuelve una cadena concatenada que se creó evaluando una expresión de cadena en un conjunto.|  
|[&#40;&#41;MDX del encabezado](../mdx/head-mdx.md)|Devuelve el primer número de elementos especificado en un conjunto y retiene los duplicados.|  
|[Jerarquía &#40;&#41;MDX](../mdx/hierarchize-mdx.md)|Ordena los miembros de un conjunto en una jerarquía.|  
|[Intersección &#40;MDX&#41;](../mdx/intersect-mdx.md)|Devuelve la intersección de dos conjuntos de entrada; conservando opcionalmente los duplicados.|  
|[&#41;LastPeriods &#40;MDX](../mdx/lastperiods-mdx.md)|Devuelve un conjunto de miembros hasta un miembro determinado, éste inclusive.|  
|[Miembros &#40;establecer&#41; &#40;MDX&#41;](../mdx/members-set-mdx.md)|Devuelve el conjunto de miembros en una dimensión, nivel o jerarquía.|  
|[MTD &#40;MDX&#41;](../mdx/mtd-mdx.md)|Devuelve un conjunto de miembros del mismo nivel que un miembro determinado, empezando por el primer miembro del mismo nivel y acabando con el miembro en cuestión, de acuerdo con la restricción del nivel de año en la dimensión de tiempo.|  
|[&#41;NameToSet &#40;MDX](../mdx/nametoset-mdx.md)|Devuelve un conjunto que contiene el miembro especificado por una cadena con formato MDX.|  
|[NonEmptyCrossjoin &#40;&#41;MDX](../mdx/nonemptycrossjoin-mdx.md)|Devuelve el producto cruzado de uno o más conjuntos de un conjunto, excluidas las tuplas vacías o sin datos de tabla de hechos asociada.|  
|[Orden &#40;MDX&#41;](../mdx/order-mdx.md)|Organiza los miembros de un conjunto especificado; opcionalmente preservando o rompiendo la jerarquía.|  
|[&#40;&#41;MDX de PeriodsToDate](../mdx/periodstodate-mdx.md)|Devuelve un conjunto de miembros del mismo nivel que un miembro determinado, empezando por el primer miembro del mismo nivel y acabando con el miembro en cuestión, de acuerdo con la restricción del nivel especificado en la dimensión de tiempo.|  
|[&#41;hasta &#40;MDX](../mdx/qtd-mdx.md)|Devuelve un conjunto de miembros del mismo nivel que un miembro determinado, empezando por el primer elemento del mismo nivel y finalizando con el miembro dado, restringido por el nivel de *trimestre* de la dimensión de tiempo.|  
|[Elementos del mismo nivel &#40;&#41;MDX](../mdx/siblings-mdx.md)|Devuelve los miembros del mismo nivel que un miembro especificado, incluyendo el propio miembro.|  
|[&#41;StripCalculatedMembers &#40;MDX](../mdx/stripcalculatedmembers-mdx.md)|Devuelve un conjunto generado al eliminar miembros calculados de un conjunto especificado.|  
|[&#41;StrToSet &#40;MDX](../mdx/strtoset-mdx.md)|Devuelve el conjunto especificado por una cadena con formato MDX.|  
|[Subconjunto &#40;MDX&#41;](../mdx/subset-mdx.md)|Devuelve un subconjunto de tuplas a partir de un conjunto especificado.|  
|[Tail &#40;MDX&#41;](../mdx/tail-mdx.md)|Devuelve un subconjunto del final de un conjunto.|  
|[&#41;ToggleDrillState &#40;MDX](../mdx/toggledrillstate-mdx.md)|Alterna el estado de detalle de los miembros.|  
|[&#40;MDX&#41;](../mdx/topcount-mdx.md)|Ordena un conjunto de forma descendente y devuelve el número de elementos especificado con los valores más altos.|  
|[&#41;&#40;MDX](../mdx/toppercent-mdx.md)|Ordena un conjunto de forma descendente y devuelve un conjunto de tuplas con los valores más altos con un total acumulado igual o inferior a un porcentaje especificado.|  
|[&#41;MDX &#40;MDX](../mdx/topsum-mdx.md)|Ordena un conjunto y devuelve los elementos de nivel superior cuyo total acumulado sea igual o superior a un valor especificado.|  
|[Unión &#40;MDX&#41;](../mdx/union-mdx.md)|Devuelve la unión de dos conjuntos; opcionalmente conserva los duplicados.|  
|[Desordene &#40;&#41;MDX](../mdx/unorder-mdx.md)|Quita cualquier orden impuesto sobre un conjunto especificado.|  
|[VisualTotals &#40;MDX&#41;](../mdx/visualtotals-mdx.md)|Devuelve un conjunto que se genera calculando de forma dinámica el total de miembros secundarios de un conjunto especificado; opcionalmente puede utilizar un patrón para el nombre del miembro primario en el conjunto de celdas resultante.|  
|[&#41;WTD &#40;MDX](../mdx/wtd-mdx.md)|Devuelve un conjunto de miembros del mismo nivel que un miembro determinado, empezando por el primer miembro del mismo nivel y acabando con el miembro en cuestión, de acuerdo con la restricción del nivel de semana en la dimensión de tiempo.|  
|[&#41;MDX &#40;](../mdx/ytd-mdx.md)|Devuelve un conjunto de miembros del mismo nivel que un miembro determinado, empezando por el primer elemento del mismo nivel y finalizando con el miembro dado, restringido por el nivel de *año* de la dimensión de tiempo.|  
  
## <a name="string-functions"></a>Funciones de cadena  
  
|Función|Descripción|  
|--------------|-----------------|  
|[&#41;CalculationPassValue &#40;MDX](../mdx/calculationpassvalue-mdx.md)|Devuelve el valor de una expresión MDX evaluada sobre el paso de cálculo especificado de un cubo.|  
|[&#41;CoalesceEmpty &#40;MDX](../mdx/coalesceempty-mdx.md)|Fusiona en un número o en una cadena un valor de celda vacía, y devuelve el valor fusionado.|  
|[Generar &#40;&#41;MDX](../mdx/generate-mdx.md)|Aplica un conjunto a cada miembro de otro conjunto y a continuación combina los conjuntos resultantes mediante unión. Alternativamente, esta función devuelve una cadena concatenada que se creó evaluando una expresión de cadena en un conjunto.|  
|[IIf &#40;&#41;MDX](../mdx/iif-mdx.md)|Devuelve uno de los dos valores determinados por una prueba lógica.|  
|[&#41;MDX &#40;MDX](../mdx/lookupcube-mdx.md)|Devuelve el valor de una expresión MDX evaluada sobre otro cubo especificado en la misma base de datos.|  
|[&#41;MemberToStr &#40;MDX](../mdx/membertostr-mdx.md)|Devuelve una cadena con formato MDX que corresponde a un miembro especificado.|  
|[Nombre &#40;&#41;MDX](../mdx/name-mdx.md)|Devuelve el nombre de una dimensión, jerarquía, nivel o miembro.|  
|[Propiedades &#40;&#41;MDX](../mdx/properties-mdx.md)|Devuelve una cadena, o un valor con tipos muy marcados, que contiene un valor de propiedad de miembro.|  
|[&#41;SetToStr &#40;MDX](../mdx/settostr-mdx.md)|Devuelve una cadena con formato de MDX que corresponde a un conjunto especificado.|  
|[&#41;TupleToStr &#40;MDX](../mdx/tupletostr-mdx.md)|Devuelve una cadena con formato MDX que corresponde a la tupla especificada.|  
|[UniqueName &#40;MDX&#41;](../mdx/uniquename-mdx.md)|Devuelve el nombre único de una dimensión, jerarquía, nivel o miembro especificado.|  
|[Nombre de usuario &#40;MDX&#41;](../mdx/username-mdx.md)|Devuelve el nombre de dominio y el nombre de usuario de la conexión actual.|  
  
## <a name="subcube-functions"></a>Funciones de subcubo  
  
|Función|Descripción|  
|--------------|-----------------|  
|[Esta &#40;MDX&#41;](../mdx/this-mdx.md)|Devuelve el subcubo actual.|  
|[Deja &#40;&#41;MDX](../mdx/leaves-mdx.md)|Devuelve el conjunto de miembros hoja en la dimensión, miembro o tupla especificada.|  
  
## <a name="tuple-functions"></a>funciones de tupla  
  
|Función|Descripción|  
|--------------|-----------------|  
|[&#41;&#40;MDX actual](../mdx/current-mdx.md)|Devuelve la tupla actual de un conjunto durante la iteración.|  
|[&#41;de&#41; &#40;de tupla de &#40;de elemento MDX](../mdx/item-tuple-mdx.md)|Devuelve una tupla desde un conjunto.|  
|[&#41;raíz &#40;MDX](../mdx/root-mdx.md)|Devuelve una tupla que consta de **todos** los miembros de cada jerarquía de atributo de un cubo, una dimensión o una tupla.|  
|[&#41;StrToTuple &#40;MDX](../mdx/strtotuple-mdx.md)|Devuelve la tupla especificada por una cadena con formato MDX.|  
  
## <a name="other-functions"></a>Otras funciones  
  
|Función|Descripción|  
|--------------|-----------------|  
|[Error &#40;&#41;MDX](../mdx/error-mdx.md)|Genera un error y puede, opcionalmente, proporcionar un mensaje de error especificado.|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia del lenguaje MDX &#40;MDX&#41;](../mdx/mdx-language-reference-mdx.md)  
  
  
