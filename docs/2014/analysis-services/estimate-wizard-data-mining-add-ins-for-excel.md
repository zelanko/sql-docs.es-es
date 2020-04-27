---
title: Asistente para estimación (complementos de minería de datos para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data modeling [data mining]
- estimation
ms.assetid: 7f2b1d5f-c9b3-4939-b35a-34ae099af15f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9b7ffc1b77d90946a119dc462da2057cf3fe4988
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66081252"
---
# <a name="estimate-wizard-data-mining-add-ins-for-excel"></a>Asistente para estimación (Complementos de minería de datos para Excel)
  ![Asistente para estimación, cinta de opciones Minería de datos](media/dmc-estimate.gif "Asistente para estimación, cinta de opciones Minería de datos")  
  
 El Asistente para **estimación** le ayuda a crear un modelo de estimación. Un modelo de estimación extrae patrones de los datos y usa los patrones para predecir los factores que afectan a los resultados.  
  
 La estimación se utiliza para predecir los resultados numéricos. Por ejemplo, si la columna de destino contiene las tasas de aprobados de varios centros escolares, expresadas como porcentaje, podría analizar factores que potencialmente aumentan o disminuyen dicha tasa, como el número de alumnos por centro, la proporción entre alumnos y profesores, y el número de profesores.  
  
## <a name="using-the-estimate-data-wizard"></a>Usar el Asistente para estimación de datos  
  
1.  En la cinta de opciones **minería de datos** , haga clic en **estimar**.  
  
2.  En el cuadro de diálogo **seleccionar datos de origen** , seleccione los datos de origen que se van a utilizar. Puede utilizar los datos de una **tabla**de Excel, un **intervalo de datos**de Excel o un **origen de datos externo**.  
  
     Si utiliza un origen de datos externo, puede crear vistas personalizadas o consultas y guardarlas como un origen de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
3.  En el cuadro de diálogo **estimación** , seleccione la **columna que se va a analizar**.  
  
     La columna de destino debe contener datos numéricos continuos.  
  
4.  Seleccione las columnas que desea usar como entrada activando la casilla **columnas de entrada** .  
  
     Estas columnas se usarán para crear los patrones. Debe excluir del análisis las columnas que no sean útiles, como las que contienen números de identificador o datos irrelevantes.  
  
5.  El Asistente para **estimación** selecciona el algoritmo óptimo para el conjunto de datos. Sin embargo, puede hacer clic en **parámetros** para abrir el cuadro de diálogo **parámetros de algoritmo** y establecer opciones avanzadas.  
  
6.  Si los datos son numéricos y puede usar el método de regresión lineal de Microsoft, puede activar el cuadro **regresor** para cualquier columna numérica que sepa (o sospeche) que se va a correlacionar con el valor de predicción.  
  
     El algoritmo comprobará entonces los valores de esa columna para determinar si afectan a los resultados. Si no está seguro, haga clic en **sugerir** y el algoritmo probará todas las columnas y detecte automáticamente los mejores valores que se usarán como regresores.  
  
    > [!NOTE]  
    >  Para crear una estimación, se necesita un regresor. El asistente siempre recomienda el mejor regresor basándose en un análisis inicial de los datos. Por consiguiente, si no está seguro, es mejor que acepte las selecciones recomendadas.  
  
7.  En la página **dividir datos en conjuntos de entrenamiento y de prueba** , especifique si desea crear un pequeño subconjunto de los datos para las pruebas.  
  
8.  En la página **Finalizar** , proporcione nombres para la nueva estructura de minería de datos y el modo de minería de datos, o acepte los nombres predeterminados que se proporcionan.  
  
9. Establezca las opciones para usar el modelo.  
  
    -   Seleccione **examinar** para abrir inmediatamente el modelo en un visor.  
  
         Este visor gráfico muestra un gráfico de red de dependencias y el árbol de decisión generado por el algoritmo. Si examina esta información, entenderá mejor los factores que contribuyen a los valores estimados.  
  
    -   Seleccione **Habilitar obtención de detalles** para permitir que los usuarios de su análisis vean los datos subyacentes.  
  
         Esta opción solo está disponible si utiliza algoritmos de regresión lineal o de árboles de decisión.  
  
    -   **Usar modelo temporal**. Si selecciona esta opción, el modelo no se guardará en el servidor. Se eliminan los modelos temporales al cerrar Excel.  
  
## <a name="more-about-estimation-models"></a>Más información sobre los modelos de estimación  
 El Asistente para **estimación** admite el uso de cualquiera de los siguientes algoritmos:  
  
-   Algoritmo de árbol de decisión de Microsoft  
  
-   Algoritmo de regresión lineal de Microsoft  
  
-   Algoritmo de regresión logística de Microsoft  
  
-   Algoritmo de red neuronal de Microsoft  
  
 En el cuadro de diálogo **parámetros de algoritmo** , puede establecer opciones avanzadas adicionales, en función del algoritmo que elija. Para obtener información sobre las opciones de cada algoritmo, vea estos temas en los Libros en pantalla de SQL Server:  
  
 [Referencia técnica del algoritmo de árboles de decisión de Microsoft](data-mining/microsoft-decision-trees-algorithm-technical-reference.md)  
  
 [Referencia técnica del algoritmo de regresión lineal de Microsoft](data-mining/microsoft-linear-regression-algorithm-technical-reference.md)  
  
 [Referencia técnica del algoritmo de regresión logística de Microsoft](data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)  
  
 [Referencia técnica del algoritmo de red neuronal de Microsoft](data-mining/microsoft-neural-network-algorithm-technical-reference.md)  
  
### <a name="requirements"></a>Requisitos  
 Para usar el Asistente para estimación de datos, debe estar conectado a una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Para obtener información sobre cómo crear una conexión, vea [conectarse a los datos de origen &#40;cliente de minería de datos para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
 Para usar el algoritmo de estimación, el resultado que está intentando predecir debería expresarse como un valor numérico, como una moneda, cantidad de ventas, fecha u hora.  
  
## <a name="see-also"></a>Consulte también  
 [Crear un modelo de minería de datos](creating-a-data-mining-model.md)   
 [Tutorial del diagrama de árbol de decisión &#40;complementos de minería de datos&#41;](decision-tree-diagram-walkthrough-data-mining-add-ins.md)  
  
  
