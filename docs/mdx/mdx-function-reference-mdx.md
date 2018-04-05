---
title: Referencia de funciones MDX (MDX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- member functions [MDX]
- level functions [MDX]
- MDX [Analysis Services], functions
- array functions
- string functions
- Multidimensional Expressions [Analysis Services], functions
- hierarchy functions [MDX]
- numeric functions [MDX]
- tuple functions
- subcube functions [MDX]
- functions [MDX]
- logical functions [MDX]
- set functions [MDX]
ms.assetid: e363722a-3e5b-40a9-a0b5-399dd2d93f6d
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: d6a0eecf1084cc17b1a2a08b7ef1c43c81d2e346
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-function-reference-mdx"></a>Referencia de funciones MDX (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] proporciona para el uso de funciones en la sintaxis de expresiones multidimensionales (MDX). Las funciones se pueden utilizar en cualquier instrucción de MDX válida y se utilizan a menudo en consultas, definiciones de resumen personalizadas y otros cálculos. Esta sección proporciona información sobre las funciones de MDX incluidas en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Puede utilizar las siguientes tablas para buscar funciones por la categoría del valor devuelto, o bien puede seleccionar una función por el nombre en la lista alfabética de la tabla de contenidos.  
  
## <a name="array-functions"></a>Funciones de matriz  
  
|Función|Description|  
|--------------|-----------------|  
|[SetToArray &#40; MDX &#41;](../mdx/settoarray-mdx.md)|Convierte uno o más conjuntos en una matriz, para usarla en funciones definidas por el usuario.|  
  
## <a name="hierarchy-functions"></a>Funciones de jerarquía  
  
|Función|Description|  
|--------------|-----------------|  
|[Jerarquía de &#40; MDX &#41;](../mdx/hierarchy-mdx.md)|Devuelve la jerarquía que contiene un miembro o nivel especificado.|  
|[Dimensión &#40; MDX &#41;](../mdx/dimension-mdx.md)|Devuelve la dimensión que contiene un miembro, nivel o jerarquía especificado.|  
|[Dimensiones &#40; MDX &#41;](../mdx/dimensions-mdx.md)|Devuelve una jerarquía especificada mediante una expresión numérica o de cadena.|  
  
## <a name="level-functions"></a>Funciones de nivel  
  
|Función|Description|  
|--------------|-----------------|  
|[Nivel &#40; MDX &#41;](../mdx/level-mdx.md)|Devuelve el nivel de un miembro.|  
|[Niveles de &#40; MDX &#41;](../mdx/levels-mdx.md)|Devuelve el nivel cuya posición en una dimensión o jerarquía se especifica mediante una expresión numérica, o cuyo nombre se especifica mediante una expresión de cadena.|  
  
## <a name="logical-functions"></a>Funciones lógicas  
  
|Función|Description|  
|--------------|-----------------|  
|[IsAncestor &#40; MDX &#41;](../mdx/isancestor-mdx.md)|Informa de si un miembro especificado es un antecesor de otro miembro especificado.|  
|[IsEmpty &#40; MDX &#41;](../mdx/isempty-mdx.md)|Informa de si la expresión evaluada es el valor de celda vacía.|  
|[IsGeneration &#40; MDX &#41;](../mdx/isgeneration-mdx.md)|Informa de si un miembro especificado es una generación especificada.|  
|[IsLeaf &#40; MDX &#41;](../mdx/isleaf-mdx.md)|Informa de si un miembro especificado es un miembro hoja.|  
|[IsSibling &#40; MDX &#41;](../mdx/issibling-mdx.md)|Informa de si un miembro especificado está en el mismo nivel que otro miembro especificado.|  
  
## <a name="member-functions"></a>Funciones de miembro  
  
|Función|Description|  
|--------------|-----------------|  
|[Antecesor &#40; MDX &#41;](../mdx/ancestor-mdx.md)|Devuelve el antecesor de un miembro en un nivel o distancia especificados.|  
|[ClosingPeriod &#40; MDX &#41;](../mdx/closingperiod-mdx.md)|Devuelve el último elemento del mismo nivel entre los descendientes de un miembro en un nivel especificado.|  
|[Elemento Cousin &#40; MDX &#41;](../mdx/cousin-mdx.md)|Devuelve el miembro secundario con la misma posición relativa bajo un miembro primario que el miembro secundario especificado.|  
|[CurrentMember &#40; MDX &#41;](../mdx/currentmember-mdx.md)|Devuelve el miembro actual de una dimensión o jerarquía especificada durante la iteración.|  
|[DataMember &#40; MDX &#41;](../mdx/datamember-mdx.md)|Devuelve el miembro de datos generados por el sistema asociado a un miembro no hoja de una dimensión.|  
|[DefaultMember &#40; MDX &#41;](../mdx/defaultmember-mdx.md)|Devuelve el miembro predeterminado de una dimensión o jerarquía.|  
|[FirstChild &#40; MDX &#41;](../mdx/firstchild-mdx.md)|Devuelve el primer elemento secundario de un miembro.|  
|[FirstSibling &#40; MDX &#41;](../mdx/firstsibling-mdx.md)|Devuelve el primer elemento secundario del elemento primario de un miembro.|  
|[Elemento &#40; Miembro &#41; &#40; MDX &#41;](../mdx/item-member-mdx.md)|Devuelve un miembro de una tupla especificada.|  
|[Lag &#40; MDX &#41;](../mdx/lag-mdx.md)|Devuelve el miembro que se encuentra un número especificado de posiciones antes de un miembro especificado en la dimensión del miembro.|  
|[LastChild &#40; MDX &#41;](../mdx/lastchild-mdx.md)|Devuelve el último elemento secundario de un miembro especificado.|  
|[LastSibling &#40; MDX &#41;](../mdx/lastsibling-mdx.md)|Devuelve el último elemento secundario del elemento primario de un miembro especificado.|  
|[Responsable de &#40; MDX &#41;](../mdx/lead-mdx.md)|Devuelve el miembro que se encuentra un número especificado de posiciones que siguen a un miembro especificado en la dimensión del miembro.|  
|[LinkMember &#40; MDX &#41;](../mdx/linkmember-mdx.md)|Devuelve el miembro equivalente a un miembro especificado de una jerarquía especificada.|  
|[Los miembros &#40; Cadena &#41; &#40; MDX &#41;](../mdx/members-string-mdx.md)|Devuelve un miembro especificado por una expresión de cadena.|  
|[NextMember &#40; MDX &#41;](../mdx/nextmember-mdx.md)|Devuelve el siguiente miembro del nivel que contiene un miembro especificado|  
|[OpeningPeriod &#40; MDX &#41;](../mdx/openingperiod-mdx.md)|Devuelve el primer miembro del mismo nivel entre los descendientes de un nivel especificado (opcionalmente, en un miembro especificado).|  
|[ParallelPeriod &#40; MDX &#41;](../mdx/parallelperiod-mdx.md)|Devuelve un miembro de un periodo anterior en la misma posición relativa que el indicado.|  
|[Elemento primario &#40; MDX &#41;](../mdx/parent-mdx.md)|Devuelve el elemento primario de un miembro.|  
|[PrevMember &#40; MDX &#41;](../mdx/prevmember-mdx.md)|Devuelve el miembro anterior en el nivel que contiene un miembro especificado.|  
|[StrToMember &#40; MDX &#41;](../mdx/strtomember-mdx.md)|Devuelve el miembro especificado por una cadena con formato de MDX.|  
|[UnknownMember &#40; MDX &#41;](../mdx/unknownmember-mdx.md)|Devuelve el miembro desconocido asociado con un nivel o miembro.|  
|[ValidMeasure &#40; MDX &#41;](../mdx/validmeasure-mdx.md)|Devuelve una medida válida de un cubo virtual, al forzar dimensiones no aplicables al nivel superior.|  
  
## <a name="numeric-functions"></a>Funciones numéricas  
  
|Función|Description|  
|--------------|-----------------|  
|[Agregado &#40; MDX &#41;](../mdx/aggregate-mdx.md)|Devuelve un valor escalar calculado al agregar medidas o bien una expresión numérica especificada de forma opcional sobre las tuplas de un conjunto especificado.|  
|[AVG &#40; MDX &#41;](../mdx/avg-mdx.md)|Devuelve el valor medio de las medidas o el valor medio de una expresión numérica opcional, evaluado sobre un conjunto especificado.|  
|[CalculationCurrentPass &#40;MDX&#41;](../mdx/calculationcurrentpass-mdx.md)|Devuelve el paso de cálculo actual de un cubo para el contexto de consulta especificado.|  
|[CalculationPassValue &#40;MDX&#41;](../mdx/calculationpassvalue-mdx.md)|Devuelve el valor de una expresión MDX evaluada sobre el paso de cálculo especificado de un cubo.|  
|[CoalesceEmpty &#40; MDX &#41;](../mdx/coalesceempty-mdx.md)|Fusiona en un número o en una cadena un valor de celda vacía, y devuelve el valor fusionado.|  
|[Correlación &#40; MDX &#41;](../mdx/correlation-mdx.md)|Devuelve el coeficiente de correlación de dos series evaluadas en un conjunto.|  
|[Número de &#40; dimensión &#41; &#40; MDX &#41;](../mdx/count-dimension-mdx.md)|Devuelve el número de dimensiones de un cubo.|  
|[Número de &#40; Niveles de jerarquía &#41; &#40; MDX &#41;](../mdx/count-hierarchy-levels-mdx.md)|Devuelve el número de niveles de una dimensión o jerarquía.|  
|[Número de &#40; Conjunto de &#41; &#40; MDX &#41;](../mdx/count-set-mdx.md)|Devuelve el número de celdas de un conjunto.|  
|[Número de &#40; Tupla &#41; &#40; MDX &#41;](../mdx/count-tuple-mdx.md)|Devuelve el número de dimensiones de una tupla.|  
|[Covarianza &#40; MDX &#41;](../mdx/covariance-mdx.md)|Devuelve la covarianza de población de dos series evaluadas en un conjunto utilizando la fórmula de llenado sesgada.|  
|[CovarianceN &#40; MDX &#41;](../mdx/covariancen-mdx.md)|Devuelve la covarianza de muestra de dos series evaluadas en un conjunto utilizando la fórmula de población no sesgada.|  
|[DistinctCount &#40; MDX &#41;](../mdx/distinctcount-mdx.md)|Devuelve el número de tuplas distintas y no vacías de un conjunto.|  
|[IIf &#40; MDX &#41;](../mdx/iif-mdx.md)|Devuelve uno de los dos valores determinados por una prueba lógica.|  
|[LinRegIntercept &#40; MDX &#41;](../mdx/linregintercept-mdx.md)|Calcula la regresión lineal de un conjunto y devuelve el valor de la intersección de la recta de regresión y = ax + b.|  
|[LinRegPoint &#40; MDX &#41;](../mdx/linregpoint-mdx.md)|Calcula la regresión lineal de un conjunto y devuelve el valor de *y* en la recta de regresión y = ax + b.|  
|[LinRegR2 &#40; MDX &#41;](../mdx/linregr2-mdx.md)|Calcula la regresión lineal de un conjunto y devuelve el coeficiente de determinación, R2.|  
|[LinRegSlope &#40; MDX &#41;](../mdx/linregslope-mdx.md)|Calcula la regresión lineal de un conjunto y devuelve el valor de la pendiente de la recta de regresión y = ax + b.|  
|[LinRegVariance &#40; MDX &#41;](../mdx/linregvariance-mdx.md)|Calcula la regresión lineal de un conjunto y devuelve la varianza asociada a la recta de regresión y = ax + b.|  
|[LookupCube &#40; MDX &#41;](../mdx/lookupcube-mdx.md)|Devuelve el valor de una expresión MDX evaluada sobre otro cubo especificado en la misma base de datos.|  
|[Max &#40; MDX &#41;](../mdx/max-mdx.md)|Devuelve el valor máximo de una expresión numérica evaluada sobre un conjunto.|  
|[Mediana &#40; MDX &#41;](../mdx/median-mdx.md)|Devuelve el valor medio de una expresión numérica evaluada sobre un conjunto.|  
|[Min &#40; MDX &#41;](../mdx/min-mdx.md)|Devuelve el valor mínimo de una expresión numérica evaluada sobre un conjunto.|  
|[Ordinal &#40; MDX &#41;](../mdx/ordinal-mdx.md)|Devuelve el valor ordinal (con base cero) asociado a un nivel.|  
|[Predecir &#40; MDX &#41;](../mdx/predict-mdx.md)|Devuelve un valor de una expresión numérica evaluada sobre un modelo de minería de datos.|  
|[Rango &#40; MDX &#41;](../mdx/rank-mdx.md)|Devuelve el intervalo con base uno de una tupla especificada en un conjunto especificado.|  
|[RollupChildren &#40; MDX &#41;](../mdx/rollupchildren-mdx.md)|Devuelve un valor generado mediante la acumulación de los valores de los elementos secundarios de un miembro especificado, utilizando el operador unario especificado.|  
|[StdDev &#40; MDX &#41;](../mdx/stddev-mdx.md)|Alias de [Stdev &#40; MDX &#41; ](../mdx/stdev-mdx.md).|  
|[StddevP &#40; MDX &#41;](../mdx/stddevp-mdx.md)|Alias de [StdevP &#40; MDX &#41; ](../mdx/stdevp-mdx.md).|  
|[STDEV &#40; MDX &#41;](../mdx/stdev-mdx.md)|Devuelve la desviación de muestra estándar de una expresión numérica evaluada sobre un conjunto, mediante la fórmula de población no sesgada.|  
|[StdevP &#40; MDX &#41;](../mdx/stdevp-mdx.md)|Devuelve la desviación estándar de población de una expresión numérica evaluada sobre un conjunto, mediante la fórmula de población sesgada.|  
|[StrToValue &#40; MDX &#41;](../mdx/strtovalue-mdx.md)|Devuelve el valor especificado por una cadena con formato de MDX.|  
|[Suma &#40; MDX &#41;](../mdx/sum-mdx.md)|Devuelve la suma de una expresión numérica evaluada sobre un conjunto.|  
|[Valor &#40; MDX &#41;](../mdx/value-mdx.md)|Devuelve el valor de una medida.|  
|[Var &#40; MDX &#41;](../mdx/var-mdx.md)|Devuelve la varianza de muestra de una expresión numérica evaluada en un conjunto, mediante la fórmula de población no sesgada.|  
|[Varianza &#40; MDX &#41;](../mdx/variance-mdx.md)|Alias de [Var &#40; MDX &#41; ](../mdx/var-mdx.md).|  
|[VarianceP &#40; MDX &#41;](../mdx/variancep-mdx.md)|Alias de [VarP &#40; MDX &#41; ](../mdx/varp-mdx.md).|  
|[VarP &#40; MDX &#41;](../mdx/varp-mdx.md)|Devuelve la varianza de población de una expresión numérica evaluada en un conjunto, mediante la fórmula de población sesgada.|  
  
## <a name="set-functions"></a>Funciones de conjunto  
  
|Función|Description|  
|--------------|-----------------|  
|[AddCalculatedMembers &#40; MDX &#41;](../mdx/addcalculatedmembers-mdx.md)|Devuelve un conjunto generado al agregar miembros calculados a un conjunto especificado.|  
|[AllMembers &#40; MDX &#41;](../mdx/allmembers-mdx.md)|Devuelve un conjunto que contiene todos los miembros de la dimensión, jerarquía o nivel especificados, incluyendo los miembros calculados.|  
|[Antecesores &#40; MDX &#41;](../mdx/ancestors-mdx.md)|Devuelve un conjunto de todos los antecesores de un miembro en un nivel o distancia especificados.|  
|[Ascendants &#40; MDX &#41;](../mdx/ascendants-mdx.md)|Devuelve el conjunto de antecesores de un miembro especificado, incluyendo el propio miembro.|  
|[Eje &#40; MDX &#41;](../mdx/axis-mdx.md)|Devuelve un conjunto definido en un eje.|  
|[BottomCount &#40; MDX &#41;](../mdx/bottomcount-mdx.md)|Ordena un conjunto de forma ascendente y devuelve el número de tuplas especificado con los valores más bajos.|  
|[BottomPercent &#40; MDX &#41;](../mdx/bottompercent-mdx.md)|Ordena un conjunto de forma ascendente y devuelve un conjunto de tuplas con los valores más bajos con un total acumulado igual o inferior a un porcentaje especificado.|  
|[BottomSum &#40; MDX &#41;](../mdx/bottomsum-mdx.md)|Ordena un conjunto de forma ascendente y devuelve un conjunto de tuplas con los valores más bajos con un total igual o inferior a un valor especificado.|  
|[Elementos secundarios &#40; MDX &#41;](../mdx/children-mdx.md)|Devuelve el elemento secundario de un miembro especificado.|  
|[Combinación cruzada &#40; MDX &#41;](../mdx/crossjoin-mdx.md)|Devuelve el producto cruzado de uno o más conjuntos.|  
|[CurrentOrdinal &#40; MDX &#41;](../mdx/currentordinal-mdx.md)|Devuelve el número de iteración actual dentro de un conjunto durante la iteración.|  
|[Descendientes &#40; MDX &#41;](../mdx/descendants-mdx.md)|Devuelve el conjunto de descendientes de un miembro en el nivel o distancia especificados; opcionalmente puede incluir o excluir los descendientes de otros niveles.|  
|[DISTINCT &#40; MDX &#41;](../mdx/distinct-mdx.md)|Devuelve un conjunto, eliminando tuplas duplicadas de un conjunto especificado.|  
|[DrilldownLevel &#40; MDX &#41;](../mdx/drilldownlevel-mdx.md)|Aumenta los detalles de los miembros de un conjunto a un nivel por debajo del nivel más bajo representado en el conjunto o un nivel por debajo del nivel especificado opcionalmente de un miembro representado en el conjunto.|  
|[DrilldownLevelBottom &#40; MDX &#41;](../mdx/drilldownlevelbottom-mdx.md)|Aumenta el detalle de los miembros inferiores de un conjunto, de un nivel especificado a otro inferior.|  
|[DrilldownLevelTop &#40; MDX &#41;](../mdx/drilldownleveltop-mdx.md)|Aumenta el detalle de los miembros superiores de un conjunto, de un nivel especificado a otro inferior.|  
|[DrilldownMember &#40; MDX &#41;](../mdx/drilldownmember-mdx.md)|Aumenta el detalle de los miembros de un conjunto especificado presentes en un segundo conjunto especificado. Alternativamente, esta función aumenta el detalle de un conjunto de tuplas.|  
|[DrilldownMemberBottom &#40; MDX &#41;](../mdx/drilldownmemberbottom-mdx.md)|Aumenta el nivel de detalle de miembros de un conjunto especificado que están presentes en otro conjunto especificado, lo que limita el conjunto de resultados a un número específico de miembros. Alternativamente, esta función también aumenta el detalle de un conjunto de tuplas.|  
|[DrilldownMemberTop &#40; MDX &#41;](../mdx/drilldownmembertop-mdx.md)|Aumenta el nivel de detalle de miembros de un conjunto especificado que están presentes en otro conjunto especificado, lo que limita el conjunto de resultados a un número específico de miembros. Como alternativa, esta función aumenta el detalle de un conjunto de tuplas.|  
|[DrillupLevel &#40; MDX &#41;](../mdx/drilluplevel-mdx.md)|Reduce el detalle de los miembros de un conjunto por debajo de un nivel especificado.|  
|[DrillupMember &#40; MDX &#41;](../mdx/drillupmember-mdx.md)|Reduce el detalle de los miembros de un conjunto especificado presentes en un segundo conjunto especificado.|  
|[Excepto &#40; MDX &#41;](../mdx/except-mdx-function.md)|Encuentra la diferencia entre dos conjuntos, reteniendo opcionalmente los duplicados.|  
|[Existe &#40; MDX &#41;](../mdx/exists-mdx.md)|Devuelve el conjunto de miembros de un conjunto que existen con una o más tuplas de otros conjuntos.|  
|[Extracción &#40; MDX &#41;](../mdx/extract-mdx.md)|Devuelve un conjunto de tuplas a partir de elementos de dimensión extraídos.|  
|[Filtro &#40; MDX &#41;](../mdx/filter-mdx.md)|Devuelve el conjunto resultante de filtrar un determinado conjunto con una condición de búsqueda.|  
|[Generar &#40; MDX &#41;](../mdx/generate-mdx.md)|Aplica un conjunto a cada miembro de otro conjunto y a continuación combina los conjuntos resultantes mediante unión. Alternativamente, esta función devuelve una cadena concatenada que se creó evaluando una expresión de cadena en un conjunto.|  
|[Encabezado &#40; MDX &#41;](../mdx/head-mdx.md)|Devuelve el primer número de elementos especificado en un conjunto y retiene los duplicados.|  
|[Hierarchize &#40; MDX &#41;](../mdx/hierarchize-mdx.md)|Ordena los miembros de un conjunto en una jerarquía.|  
|[Intersect &#40; MDX &#41;](../mdx/intersect-mdx.md)|Devuelve la intersección de dos conjuntos de entrada; conservando opcionalmente los duplicados.|  
|[LastPeriods &#40; MDX &#41;](../mdx/lastperiods-mdx.md)|Devuelve un conjunto de miembros hasta un miembro determinado, éste inclusive.|  
|[Los miembros &#40; Conjunto de &#41; &#40; MDX &#41;](../mdx/members-set-mdx.md)|Devuelve el conjunto de miembros en una dimensión, nivel o jerarquía.|  
|[MTd &#40; MDX &#41;](../mdx/mtd-mdx.md)|Devuelve un conjunto de miembros del mismo nivel que un miembro determinado, empezando por el primer miembro del mismo nivel y acabando con el miembro en cuestión, de acuerdo con la restricción del nivel de año en la dimensión de tiempo.|  
|[NameToSet &#40; MDX &#41;](../mdx/nametoset-mdx.md)|Devuelve un conjunto que contiene el miembro especificado por una cadena con formato de MDX.|  
|[NonEmptyCrossjoin &#40; MDX &#41;](../mdx/nonemptycrossjoin-mdx.md)|Devuelve el producto cruzado de uno o más conjuntos de un conjunto, excluidas las tuplas vacías o sin datos de tabla de hechos asociada.|  
|[Orden &#40; MDX &#41;](../mdx/order-mdx.md)|Organiza los miembros de un conjunto especificado; opcionalmente preservando o rompiendo la jerarquía.|  
|[PeriodsToDate &#40; MDX &#41;](../mdx/periodstodate-mdx.md)|Devuelve un conjunto de miembros del mismo nivel que un miembro determinado, empezando por el primer miembro del mismo nivel y acabando con el miembro en cuestión, de acuerdo con la restricción del nivel especificado en la dimensión de tiempo.|  
|[QTD &#40; MDX &#41;](../mdx/qtd-mdx.md)|Devuelve un conjunto de miembros del mismo nivel que un miembro determinado, empezando por el primer miembro del mismo nivel y terminando con el miembro en cuestión, como restringida por la *trimestre* nivel en la dimensión de tiempo.|  
|[Elementos del mismo nivel &#40; MDX &#41;](../mdx/siblings-mdx.md)|Devuelve los miembros del mismo nivel que un miembro especificado, incluyendo el propio miembro.|  
|[StripCalculatedMembers &#40; MDX &#41;](../mdx/stripcalculatedmembers-mdx.md)|Devuelve un conjunto generado al eliminar miembros calculados de un conjunto especificado.|  
|[StrToSet &#40; MDX &#41;](../mdx/strtoset-mdx.md)|Devuelve el conjunto especificado por una cadena con formato de MDX.|  
|[Subconjunto &#40; MDX &#41;](../mdx/subset-mdx.md)|Devuelve un subconjunto de tuplas a partir de un conjunto especificado.|  
|[Final &#40; MDX &#41;](../mdx/tail-mdx.md)|Devuelve un subconjunto del final de un conjunto.|  
|[ToggleDrillState &#40; MDX &#41;](../mdx/toggledrillstate-mdx.md)|Alterna el estado de detalle de los miembros.|  
|[TopCount &#40; MDX &#41;](../mdx/topcount-mdx.md)|Ordena un conjunto de forma descendente y devuelve el número de elementos especificado con los valores más altos.|  
|[TopPercent &#40; MDX &#41;](../mdx/toppercent-mdx.md)|Ordena un conjunto de forma descendente y devuelve un conjunto de tuplas con los valores más altos con un total acumulado igual o inferior a un porcentaje especificado.|  
|[TopSum &#40; MDX &#41;](../mdx/topsum-mdx.md)|Ordena un conjunto y devuelve los elementos de nivel superior cuyo total acumulado sea igual o superior a un valor especificado.|  
|[Unión &#40; MDX &#41;](../mdx/union-mdx.md)|Devuelve la unión de dos conjuntos; opcionalmente conserva los duplicados.|  
|[Unorder, &#40; MDX &#41;](../mdx/unorder-mdx.md)|Quita cualquier orden impuesto sobre un conjunto especificado.|  
|[VisualTotals &#40; MDX &#41;](../mdx/visualtotals-mdx.md)|Devuelve un conjunto que se genera calculando de forma dinámica el total de miembros secundarios de un conjunto especificado; opcionalmente puede utilizar un patrón para el nombre del miembro primario en el conjunto de celdas resultante.|  
|[WTD &#40; MDX &#41;](../mdx/wtd-mdx.md)|Devuelve un conjunto de miembros del mismo nivel que un miembro determinado, empezando por el primer miembro del mismo nivel y acabando con el miembro en cuestión, de acuerdo con la restricción del nivel de semana en la dimensión de tiempo.|  
|[YTD &#40; MDX &#41;](../mdx/ytd-mdx.md)|Devuelve un conjunto de miembros del mismo nivel que un miembro determinado, empezando por el primer miembro del mismo nivel y terminando con el miembro en cuestión, como restringida por la *año* nivel en la dimensión de tiempo.|  
  
## <a name="string-functions"></a>Funciones de cadena  
  
|Función|Description|  
|--------------|-----------------|  
|[CalculationPassValue &#40;MDX&#41;](../mdx/calculationpassvalue-mdx.md)|Devuelve el valor de una expresión MDX evaluada sobre el paso de cálculo especificado de un cubo.|  
|[CoalesceEmpty &#40; MDX &#41;](../mdx/coalesceempty-mdx.md)|Fusiona en un número o en una cadena un valor de celda vacía, y devuelve el valor fusionado.|  
|[Generar &#40; MDX &#41;](../mdx/generate-mdx.md)|Aplica un conjunto a cada miembro de otro conjunto y a continuación combina los conjuntos resultantes mediante unión. Alternativamente, esta función devuelve una cadena concatenada que se creó evaluando una expresión de cadena en un conjunto.|  
|[IIf &#40; MDX &#41;](../mdx/iif-mdx.md)|Devuelve uno de los dos valores determinados por una prueba lógica.|  
|[LookupCube &#40; MDX &#41;](../mdx/lookupcube-mdx.md)|Devuelve el valor de una expresión MDX evaluada sobre otro cubo especificado en la misma base de datos.|  
|[MemberToStr &#40; MDX &#41;](../mdx/membertostr-mdx.md)|Devuelve una cadena con formato de MDX que corresponde a un miembro especificado.|  
|[Nombre de &#40; MDX &#41;](../mdx/name-mdx.md)|Devuelve el nombre de una dimensión, jerarquía, nivel o miembro.|  
|[Propiedades &#40; MDX &#41;](../mdx/properties-mdx.md)|Devuelve una cadena, o un valor con tipos muy marcados, que contiene un valor de propiedad de miembro.|  
|[SetToStr &#40; MDX &#41;](../mdx/settostr-mdx.md)|Devuelve una cadena con formato de MDX que corresponde a un conjunto especificado.|  
|[TupleToStr &#40; MDX &#41;](../mdx/tupletostr-mdx.md)|Devuelve una cadena con formato de MDX que corresponde a una tupla especificada.|  
|[UniqueName &#40; MDX &#41;](../mdx/uniquename-mdx.md)|Devuelve el nombre único de una dimensión, jerarquía, nivel o miembro especificado.|  
|[Nombre de usuario &#40; MDX &#41;](../mdx/username-mdx.md)|Devuelve el nombre de dominio y el nombre de usuario de la conexión actual.|  
  
## <a name="subcube-functions"></a>Funciones de subcubo  
  
|Función|Description|  
|--------------|-----------------|  
|[Esto &#40; MDX &#41;](../mdx/this-mdx.md)|Devuelve el subcubo actual.|  
|[Deja &#40; MDX &#41;](../mdx/leaves-mdx.md)|Devuelve el conjunto de miembros hoja en la dimensión, miembro o tupla especificada.|  
  
## <a name="tuple-functions"></a>funciones de tupla  
  
|Función|Description|  
|--------------|-----------------|  
|[Actual &#40; MDX &#41;](../mdx/current-mdx.md)|Devuelve la tupla actual de un conjunto durante la iteración.|  
|[Elemento &#40; Tupla &#41; &#40; MDX &#41;](../mdx/item-tuple-mdx.md)|Devuelve una tupla desde un conjunto.|  
|[Raíz &#40; MDX &#41;](../mdx/root-mdx.md)|Devuelve una tupla que consta de la **todos los** miembros de cada jerarquía de atributo en un cubo, dimensión o tupla.|  
|[StrToTuple &#40; MDX &#41;](../mdx/strtotuple-mdx.md)|Devuelve la tupla especificada por una cadena con formato de MDX.|  
  
## <a name="other-functions"></a>Otras funciones  
  
|Función|Description|  
|--------------|-----------------|  
|[Error &#40; MDX &#41;](../mdx/error-mdx.md)|Genera un error y puede, opcionalmente, proporcionar un mensaje de error especificado.|  
  
## <a name="see-also"></a>Vea también  
 [Referencia del lenguaje MDX &#40; MDX &#41;](../mdx/mdx-language-reference-mdx.md)  
  
  
