---
title: Estimación (complementos de minería de datos para Excel de datos) del Asistente | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data modeling [data mining]
- estimation
ms.assetid: 7f2b1d5f-c9b3-4939-b35a-34ae099af15f
caps.latest.revision: 23
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6e81ee7d3ff6115cbec5774d8c139c0d9933afb0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37231997"
---
# <a name="estimate-wizard-data-mining-add-ins-for-excel"></a>Asistente para estimación (Complementos de minería de datos para Excel)
  ![Asistente para estimación en la cinta de opciones minería de datos](media/dmc-estimate.gif "Asistente para estimación en la cinta de opciones minería de datos")  
  
 El **estimación** asistente le ayuda a crear un modelo de estimación. Un modelo de estimación extrae patrones de los datos y usa los patrones para predecir los factores que afectan a los resultados.  
  
 La estimación se utiliza para predecir los resultados numéricos. Por ejemplo, si la columna de destino contiene las tasas de aprobados de varios centros escolares, expresadas como porcentaje, podría analizar factores que potencialmente aumentan o disminuyen dicha tasa, como el número de alumnos por centro, la proporción entre alumnos y profesores, y el número de profesores.  
  
## <a name="using-the-estimate-data-wizard"></a>Usar el Asistente para estimación de datos  
  
1.  En el **minería de datos** la cinta de opciones, haga clic en **estimación**.  
  
2.  En el **seleccionar datos de origen** cuadro de diálogo, seleccione los datos de origen que desea usar. Puede usar los datos en un Excel **tabla**, un Excel **rango de datos**, o desde un **origen de datos externo**.  
  
     Si utiliza un origen de datos externo, puede crear vistas personalizadas o consultas y guardarlas como un origen de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
3.  En el **estimación** cuadro de diálogo, seleccione el **columna para analizar**.  
  
     La columna de destino debe contener datos numéricos continuos.  
  
4.  Seleccione columnas que se va a utilizar como entrada al comprobar la **columnas de entrada** casilla de verificación.  
  
     Estas columnas se usarán para crear los patrones. Debe excluir del análisis las columnas que no sean útiles, como las que contienen números de identificador o datos irrelevantes.  
  
5.  El **estimación** asistente selecciona el algoritmo óptimo para el conjunto de datos. Sin embargo, puede hacer clic en **parámetros** para abrir el **parámetros de algoritmo** cuadro de diálogo y establecer las opciones avanzadas.  
  
6.  Si los datos son numéricos y puede usar el método de regresión lineal de Microsoft, puede comprobar el **regresor** cuadro para cualquier columna numérica que sepa (o sospeche) que está correlacionada con el valor de predicción.  
  
     El algoritmo comprobará entonces los valores de esa columna para determinar si afectan a los resultados. Si no está seguro, haga clic en **sugerir** y el algoritmo se pruebe todas las columnas y detectar automáticamente los mejores valores deben usar como regresores.  
  
    > [!NOTE]  
    >  Para crear una estimación, se necesita un regresor. El asistente siempre recomienda el mejor regresor basándose en un análisis inicial de los datos. Por consiguiente, si no está seguro, es mejor que acepte las selecciones recomendadas.  
  
7.  En el **dividir los datos en conjuntos de prueba y entrenamiento** , especifique si desea crear un pequeño subconjunto de los datos de prueba.  
  
8.  En el **finalizar** página, proporcione los nombres de la nueva estructura de minería de datos y el modo de minería de datos o acepte los nombres predeterminados que se proporcionan.  
  
9. Establezca las opciones para usar el modelo.  
  
    -   Seleccione **examinar** para abrir inmediatamente el modelo en un visor.  
  
         Este visor gráfico muestra un gráfico de red de dependencias y el árbol de decisión generado por el algoritmo. Si examina esta información, entenderá mejor los factores que contribuyen a los valores estimados.  
  
    -   Seleccione **Habilitar obtención de detalles** para permitir que los usuarios de su análisis ver los datos subyacentes.  
  
         Esta opción solo está disponible si utiliza algoritmos de regresión lineal o de árboles de decisión.  
  
    -   **Usar modelo temporal**. Si selecciona esta opción, el modelo no se guardará en el servidor. Se eliminan los modelos temporales al cerrar Excel.  
  
## <a name="more-about-estimation-models"></a>Más información sobre los modelos de estimación  
 El **estimación** asistente admite el uso de cualquiera de los algoritmos siguientes:  
  
-   Algoritmo de árboles de decisión de Microsoft  
  
-   Algoritmo de regresión lineal de Microsoft  
  
-   Algoritmo de regresión logística de Microsoft  
  
-   Algoritmo de red Neural Microsoft  
  
 En el **parámetros de algoritmo** cuadro de diálogo, puede establecer opciones avanzadas adicionales, según el algoritmo que eligió. Para obtener información sobre las opciones de cada algoritmo, vea estos temas en los Libros en pantalla de SQL Server:  
  
 [Referencia técnica del algoritmo de árboles de decisión de Microsoft](data-mining/microsoft-decision-trees-algorithm-technical-reference.md)  
  
 [Referencia técnica del algoritmo de regresión lineal de Microsoft](data-mining/microsoft-linear-regression-algorithm-technical-reference.md)  
  
 [Referencia técnica del algoritmo de regresión logística de Microsoft](data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)  
  
 [Referencia técnica del algoritmo de red neuronal de Microsoft](data-mining/microsoft-neural-network-algorithm-technical-reference.md)  
  
### <a name="requirements"></a>Requisitos  
 Para usar el Asistente para estimación de datos, debe estar conectado a una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Para obtener información sobre cómo crear una conexión, consulte [conectarse a los datos de origen &#40;cliente de minería de datos para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
 Para usar el algoritmo de estimación, el resultado que está intentando predecir debería expresarse como un valor numérico, como una moneda, cantidad de ventas, fecha u hora.  
  
## <a name="see-also"></a>Vea también  
 [Creación de un modelo de minería de datos](creating-a-data-mining-model.md)   
 [Tutorial del diagrama de árbol de decisión &#40;complementos de minería de datos&#41;](decision-tree-diagram-walkthrough-data-mining-add-ins.md)  
  
  
