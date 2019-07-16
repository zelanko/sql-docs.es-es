---
title: Los valores que faltan (Analysis Services - minería de datos) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 662fdd55fc5929fe56734b9894bf971962ff2a7b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "68182604"
---
# <a name="missing-values-analysis-services---data-mining"></a>Valores ausentes (Analysis Services - Minería de datos)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Controlar los  *valores ausentes* correctamente constituye una parte importante del modelado eficiente. En esta sección se explica qué son los valores ausentes, y se describen las características proporcionadas en [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para trabajar con valores ausentes al generar estructuras y modelos de minería de datos.  
  
## <a name="definition-of-missing-values-in-data-mining"></a>Definición de los valores ausentes en la minería de datos  
 Un valor ausente puede tener distintos significados. Es posible que el campo no fuera aplicable, que el evento no se produjera o que los datos no estuvieran disponibles. También puede deberse a que la persona que escribió los datos no conocía el valor correcto, o no se preocupó de rellenar un campo.  
  
 Sin embargo, hay muchos escenarios de minería de datos en los que los valores ausentes proporcionan información importante. El significado de los valores ausentes depende en gran parte del contexto. Por ejemplo, un valor de fecha ausente en una lista de facturas tiene un significado sustancialmente diferente de la ausencia de una fecha en la columna que indica la fecha de contratación de un empleado. Generalmente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] trata los valores ausentes como informativos y ajusta las probabilidades para incorporarlos en sus cálculos. De esta forma, puede asegurarse de que los modelos están equilibrados y no dan demasiada importancia a los casos existentes.  
  
 Por consiguiente, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proporciona dos mecanismos totalmente distintos para administrar y calcular los valores ausentes. El primer método controla la administración de los valores NULL en el nivel de la estructura de minería de datos. La implementación del segundo método difiere para cada algoritmo, pero normalmente define cómo se procesan y cuentan los valores ausentes en los modelos que admiten valores NULL.  
  
## <a name="specifying-handling-of-nulls"></a>Especificar la administración de los valores NULL  
 Los valores ausentes pueden estar representados en el origen de datos de varias maneras: como valores NULL, como celdas vacías en una hoja de cálculo, como el valor N/D u otro código similar, o como un valor artificial, por ejemplo 9999. Sin embargo, en la minería de datos, solo los valores NULL se consideran valores ausentes. Si los datos contienen valores de marcador de posición en lugar de valores NULL, dichos valores pueden afectar a los resultados del modelo, por lo que deberá reemplazarlos por valores NULL o bien deducir los valores correctos si es posible. Existen diversas herramientas que puede usar para deducir y rellenar los valores adecuados, como la transformación Búsqueda o la tarea de generación de perfiles de datos en SQL Server Integration Services, o la herramienta Rellenar desde ejemplo incluida en los complementos de minería de datos para Excel.  
  
 Si la tarea que está modelando especifica que una columna nunca tiene que tener valores ausentes, necesita aplicar la marca de modelado **NOT_NULL** a la columna al definir la estructura de minería de datos. Esta marca indica que se debe producir un error en el procesamiento si un caso no tiene un valor adecuado. Si se produce este error al procesar un modelo, puede registrarlo y tomar las medidas necesarias para corregir los datos que se proporcionan al modelo.  
  
## <a name="calculation-of-the-missing-state"></a>Cálculo del estado ausente  
 Para el algoritmo de minería de datos, los valores ausentes son informativos. En las tablas de casos, **Missing** es un estado tan válido como cualquier otro. Es más, un modelo de minería de datos puede usar otros valores para predecir la ausencia de un valor. En otras palabras, la ausencia de un valor no es un error.  
  
 Cuando se crea un modelo de minería de datos, se agrega automáticamente un estado **Missing** a dicho modelo para todas las columnas discretas. Por ejemplo, si la columna de entrada [Sexo] contiene dos valores posibles (Hombre y Mujer), automáticamente se agrega un tercer valor para representar el valor **Missing** y en el histograma que muestra la distribución de todos los valores de la columna siempre se incluirá el recuento de los casos con valores **Missing** . Si en la columna Sexo no hay ningún valor ausente, el histograma muestra que el estado Missing aparece en 0 casos.  
  
 La inclusión del estado **Missing** de forma predeterminada está justificada si cree probable que los datos no dispongan de ejemplos de todos los valores posibles y no desea que el modelo excluya la posibilidad solo porque no existe ningún ejemplo en los datos. Por ejemplo, si los datos de ventas de una tienda muestran que todos los clientes que compraron un determinado producto resultaron ser mujeres, probablemente no desee crear un modelo que prediga que únicamente las mujeres podrán adquirir el producto. En su lugar, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] agrega un marcador de posición para el valor desconocido adicional, denominado **Missing**, que permitiría alojar otros posibles estados.  
  
 Por ejemplo, la tabla siguiente muestra la distribución de valores para el nodo (Todos) del modelo de árbol de decisión creado para el tutorial de Bike Buyer. En el ejemplo, la columna [Bike Buyer] es el atributo de predicción, donde 1 indica "Sí" y 0 indica "No".  
  
|Valor|Casos|  
|-----------|-----------|  
|0|9296|  
|1|9098|  
|Missing|0|  
  
 Esta distribución muestra que aproximadamente la mitad de los clientes han comprado una bicicleta, y la otra mitad no lo ha hecho. Este conjunto de datos específico es muy limpio y, por lo tanto, cada caso tiene un valor en la columna [Bike Buyer] y el número de valores **Missing** es 0. Pero, si un caso tuviera un valor NULL en el campo [Bike Buyer], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] consideraría esa fila como un caso con un valor **Missing** .  
  
 Si la entrada es una columna continua, el modelo tabula dos posibles estados del atributo: **Existente** y **falta**. En otras palabras, o la columna contiene un valor de algún tipo de datos numéricos o no contiene ningún valor. Para los casos que tienen un valor, el modelo calcula la media, la desviación estándar y otras estadísticas significativas. Para los casos que no tienen ningún valor, el modelo proporciona un recuento de los valores **Missing** y ajusta las predicciones de la forma apropiada. El método para ajustar la predicción difiere dependiendo del algoritmo y se describe en la sección siguiente.  
  
> [!NOTE]  
>  Para los atributos de una tabla anidada, los valores ausentes no son informativos. Por ejemplo, si un cliente no ha comprado un producto, la tabla anidada **Productos** no tendrá ninguna fila para dicho producto y el modelo de minería no creará ningún atributo para el producto ausente. Sin embargo, si le interesan los clientes que no han comprado determinados productos, puede crear un modelo cuyo filtro esté basado en la inexistencia de los productos en la tabla anidada, usando para ello una instrucción NOT EXISTS en el filtro del modelo. Para más información, vea [Aplicar un filtro a un modelo de minería de datos](../../analysis-services/data-mining/apply-a-filter-to-a-mining-model.md).  
  
## <a name="adjusting-probability-for-missing-states"></a>Ajustar la probabilidad para los estados ausentes  
 Además de contar los valores, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] calcula la probabilidad de cualquier valor en el conjunto de datos. Esto también se aplica al valor **Missing** . Por ejemplo, la tabla siguiente muestra las probabilidades para los casos del ejemplo anterior:  
  
|Valor|Casos|Probabilidad|  
|-----------|-----------|-----------------|  
|0|9296|50,55 %|  
|1|9098|49,42 %|  
|Missing|0|0,03 %|  
  
 Puede parecer extraño que la probabilidad del valor **Missing** sea 0,03%, cuando el número de casos es 0. En realidad, este comportamiento forma parte del diseño y representa un ajuste que permite al modelo administrar correctamente los valores desconocidos.  
  
 En general, la probabilidad se calcula dividiendo los casos favorables entre todos los casos posibles. En este ejemplo, el algoritmo calcula la suma de los casos que cumplen una condición determinada ([Bike Buyer] = 1 o [Bike Buyer] = 0) y divide ese número entre el recuento total de filas. Sin embargo, para representar los casos **Missing** , se suma 1 al número de casos posibles. Como resultado, la probabilidad para el caso desconocido ya no es cero, sino un número muy pequeño, lo que indica que el estado es simplemente improbable, no imposible.  
  
 La suma de este pequeño valor para **Missing** no cambia el resultado del elemento de predicción; sin embargo, mejora el modelado en escenarios donde los datos históricos no contemplan todos los resultados posibles.  
  
> [!NOTE]  
>  Los proveedores de minería de datos difieren en la forma de administrar los valores ausentes. Por ejemplo, algunos proveedores dan por hecho que los datos ausentes en una columna anidada constituyen una representación dispersa, pero que esos mismos datos en una columna no anidada están ausentes de forma aleatoria.  
  
 Si está seguro de que en los datos se especifican todos los resultados y desea evitar que se ajusten las probabilidades, deberá establecer la marca de modelado NOT_NULL en la columna de la estructura de minería de datos.  
  
> [!NOTE]  
>  Cada algoritmo, incluidos los algoritmos personalizados que pudiera haber obtenido de un complemento de terceros, puede administrar los valores ausentes de forma distinta.  
  
### <a name="special-handling-of-missing-values-in-decision-tree-models"></a>Administrar de manera especial los valores ausentes en los modelos de árbol de decisión  
 El algoritmo de árboles de decisión de Microsoft calcula las probabilidades para los valores ausentes de manera diferente que otros algoritmos. En lugar de limitarse a agregar 1 al número total de casos, el algoritmo de árboles de decisión se ajusta para el estado **Missing** usando una fórmula algo diferente.  
  
 En un modelo de árbol de decisión, la probabilidad del estado **Missing** se calcula de la forma siguiente:  
  
 ProbabilidadEstado = (ProbabilidadNodoAnterior) * (SoporteEstado + 1) / (SoporteNodo + TotalEstados)  
  
El algoritmo de árboles de decisión proporciona un ajuste adicional que ayuda al algoritmo a compensar la presencia de filtros en el modelo, lo que puede provocar muchos Estados durante el proceso de entrenamiento.  
  
 En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], si un estado está presente durante el proceso de entrenamiento pero el soporte es cero en un nodo determinado, se realiza el ajuste estándar. Sin embargo, si un estado nunca aparece durante el proceso de entrenamiento, el algoritmo establece la probabilidad exactamente en cero. Este ajuste no solo se aplica al estado **Missing** , sino también a los otros estados que existen en los datos de entrenamiento, pero que tienen un soporte cero como resultado del filtrado de modelos.  
  
 Este ajuste adicional da como resultado la fórmula siguiente:  
  
 StateProbability = 0,0 si el estado tiene 0 como admisión en el conjunto de aprendizaje  
  
 ProbabilidadEstado ELSE = (ProbabilidadNodoAnterior) * (SoporteEstado + 1) / (SoporteNodo + TotalEstadosConSoporteDistintoCero)  
  
 El efecto neto de este ajuste es mantener la estabilidad del árbol.  
  
## <a name="related-tasks"></a>Related Tasks  
 En los siguientes temas se proporciona más información acerca de cómo administrar los valores ausentes.  
  
|Tareas|Vínculos|  
|-----------|-----------|  
|Agregar marcas a columnas del modelo individuales para controlar la administración de los valores ausentes|[Ver o cambiar marcas de modelado &#40;minería de datos&#41;](../../analysis-services/data-mining/view-or-change-modeling-flags-data-mining.md)|  
|Establecer propiedades en un modelo de minería de datos para controlar la administración de los valores ausentes|[Cambiar las propiedades de un modelo de minería de datos](../../analysis-services/data-mining/change-the-properties-of-a-mining-model.md)|  
|Obtenga información acerca de cómo especificar las marcas de modelado en DMX|[Marcas de modelado &#40;DMX&#41;](../../dmx/modeling-flags-dmx.md)|  
|Modificar la forma en la que la estructura de minería de datos administra los valores ausentes|[Cambiar las propiedades de una estructura de minería de datos](../../analysis-services/data-mining/change-the-properties-of-a-mining-structure.md)|  
  
## <a name="see-also"></a>Vea también  
 [Contenido del modelo de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-model-content-analysis-services-data-mining.md)   
 [Marcas de modelado &#40;Minería de datos&#41;](../../analysis-services/data-mining/modeling-flags-data-mining.md)  
  
  
