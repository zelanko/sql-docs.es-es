---
title: Clasificar (complementos de minería de datos para Excel de datos) del Asistente | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data modeling [data mining]
- classification [data mining]
ms.assetid: 409c5076-c4c3-4f09-8f30-d3297df45f13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a62d937a733ea41b85a83224a043ff4ad7ecdd29
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66087932"
---
# <a name="classify-wizard-data-mining-add-ins-for-excel"></a>Asistente para clasificación (Complementos de minería de datos para Excel)
  ![Asistente para clasificar en la cinta de opciones minería de datos](media/dmc-classify.gif "Asistente para clasificar en la cinta de opciones minería de datos")  
  
 El **clasificar** asistente le ayuda a crear un modelo de clasificación basado en datos existentes en una tabla de Excel, un rango de Excel o un origen de datos externo.  
  
 Un modelo de clasificación extrae patrones de los datos que indican similitudes y permiten realizar predicciones basadas en las agrupaciones de valores. Por ejemplo, un modelo de clasificación podría utilizarse para predecir el riesgo en función de los patrones de ingresos o gastos.  
  
## <a name="using-the-classify-wizard"></a>Usar el Asistente para clasificar  
  
1.  En el **minería de datos** la cinta de opciones, haga clic en **clasificar**y, a continuación, haga clic en **siguiente**.  
  
2.  En el **seleccionar datos de origen** página, elija los datos que se va a analizar.  
  
     Este asistente admite varios tipos de datos: Las tablas de Excel, rangos de Excel y orígenes de datos externos. Con datos externos, puede agregarlos a Excel o elegir un conjunto de tablas o vistas de un origen de datos de Analysis Services. También puede agregar tablas y cambiar columnas para crear orígenes de datos ad hoc.  
  
3.  En el **clasificación** página, elija la columna que desea clasificar.  
  
     Revise las columnas en la lista, **columnas de entrada**y anule la selección de todas las columnas que tienen valores únicos y, por tanto, no son útiles para la creación de patrones, como números de identificación, nombres de cliente y así sucesivamente. También debe quitar las columnas que básicamente dupliquen la columna clasificable.  
  
     Por ejemplo, si está clasificando la predicción de la categoría de un producto, debe excluir el campo de subcategoría si hay una regla de negocios conocida o la fortaleza de esa regla podría impedir que se detectaran otras correlaciones.  
  
4.  Si lo desea, haga clic en **parámetros** para cambiar los parámetros del algoritmo y personalizar el comportamiento del modelo de agrupación en clústeres.  
  
5.  En el **dividir los datos en conjuntos de prueba y entrenamiento** , especifique la cantidad de datos son suficientes para las pruebas. El resto se utiliza siempre para entrenar el modelo.  
  
     La configuración predeterminada es tener un 30 % de datos de prueba y un 70 % de datos de entrenamiento.  
  
6.  En el **finalizar** página, proporcione un nombre descriptivo para el conjunto de datos y el modelo y establecer las siguientes opciones que controlan cómo trabajar con el modelo terminado:  
  
    -   **Examinar modelo**. Cuando se selecciona esta opción, tan pronto como el asistente finaliza el procesamiento del modelo, se abre un **examinar** ventana que le ayudarán a explorar los resultados. El contenido del visor depende del tipo de modelo que creó. Para obtener más información, consulte [examinar un modelo de árboles de decisión](browsing-a-decision-trees-model.md) y [examinar un modelo de red neuronal](browsing-a-neural-network-model.md).  
  
    -   **Habilitar obtención de detalles**. Seleccione esta opción para ver los datos subyacentes desde el modelo terminado. Esta opción solo está disponible si se crea un modelo de árbol de decisión.  
  
    -   **Usar modelo temporal**. Si selecciona esta opción, el modelo no se guardará en el servidor. Se eliminan los modelos temporales al cerrar Excel.  
  
## <a name="more-about-classification-models"></a>Más información sobre los modelos de clasificación  
 En el **parámetros de algoritmo** cuadro de diálogo, también puede elegir el método de clasificación entre estos algoritmos proporcionados en Analysis Services:  
  
-   Árbol de decisión de Microsoft  
  
-   Regresión logística de Microsoft  
  
-   Bayes naive de Microsoft  
  
-   Red neuronal de Microsoft  
  
 Aunque los algoritmos podrían producir resultados similares, analizan los datos de forma diferente, por lo que recomendamos probar varios y comparar los resultados. El método predeterminado es Árboles de decisión de Microsoft.  
  
 En el **parámetros** lista, puede cambiar las opciones avanzadas, que dependen del tipo de algoritmo que elija. Los parámetros de cada algoritmo se describen con más detalle en los Libros en pantalla de SQL Server.  
  
 [Referencia técnica del algoritmo de árboles de decisión de Microsoft](data-mining/microsoft-decision-trees-algorithm-technical-reference.md)  
  
 [Referencia técnica del algoritmo de regresión logística de Microsoft](data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)  
  
 [Referencia técnica del algoritmo Bayes naive de Microsoft](data-mining/microsoft-naive-bayes-algorithm-technical-reference.md)  
  
 [Referencia técnica del algoritmo de red neuronal de Microsoft](data-mining/microsoft-neural-network-algorithm-technical-reference.md)  
  
### <a name="requirements"></a>Requisitos  
 Para usar el **clasificar** asistente, debe estar conectado a un [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] base de datos. Para obtener información sobre cómo crear una conexión, consulte [conectarse a los datos de origen &#40;cliente de minería de datos para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
## <a name="see-also"></a>Vea también  
 [Crear un modelo de minería de datos](creating-a-data-mining-model.md)  
  
  
