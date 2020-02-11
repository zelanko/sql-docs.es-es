---
title: Asistente para clasificar (complementos de minería de datos para Excel) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66087932"
---
# <a name="classify-wizard-data-mining-add-ins-for-excel"></a>Asistente para clasificación (Complementos de minería de datos para Excel)
  ![Asistente para clasificación, cinta de opciones Minería de datos](media/dmc-classify.gif "Asistente para clasificación, cinta de opciones Minería de datos")  
  
 El Asistente para **clasificar** le ayuda a generar un modelo de clasificación basado en los datos existentes en una tabla de Excel, un intervalo de Excel o un origen de datos externo.  
  
 Un modelo de clasificación extrae patrones de los datos que indican similitudes y permiten realizar predicciones basadas en las agrupaciones de valores. Por ejemplo, un modelo de clasificación podría utilizarse para predecir el riesgo en función de los patrones de ingresos o gastos.  
  
## <a name="using-the-classify-wizard"></a>Usar el Asistente para clasificar  
  
1.  En la cinta de opciones **minería de datos** , haga clic en **clasificar**y, a continuación, en **siguiente**.  
  
2.  En la página **seleccionar datos de origen** , elija los datos que desea analizar.  
  
     Este asistente admite varios tipos de datos: tablas de Excel, rangos de Excel y orígenes de datos externos. Con datos externos, puede agregarlos a Excel o elegir un conjunto de tablas o vistas de un origen de datos de Analysis Services. También puede agregar tablas y cambiar columnas para crear orígenes de datos ad hoc.  
  
3.  En la página **clasificación** , elija la columna que desea clasificar.  
  
     Revise las columnas de la lista, **las columnas de entrada**y anule la selección de las columnas que tengan valores únicos y, por tanto, no resulten útiles para crear patrones, como números de identificación, nombres de clientes, etc. También debe quitar las columnas que básicamente dupliquen la columna clasificable.  
  
     Por ejemplo, si está clasificando la predicción de la categoría de un producto, debe excluir el campo de subcategoría si hay una regla de negocios conocida o la fortaleza de esa regla podría impedir que se detectaran otras correlaciones.  
  
4.  Opcionalmente, haga clic en **parámetros** para cambiar los parámetros del algoritmo y personalizar el comportamiento del modelo de agrupación en clústeres.  
  
5.  En la página **dividir datos en conjuntos de entrenamiento y de prueba** , especifique la cantidad de datos que se van a conservar para las pruebas. El resto se utiliza siempre para entrenar el modelo.  
  
     La configuración predeterminada es tener un 30 % de datos de prueba y un 70 % de datos de entrenamiento.  
  
6.  En la página **Finalizar** , proporcione un nombre descriptivo para el conjunto de datos y el modelo, y establezca las siguientes opciones que controlan cómo se trabaja con el modelo terminado:  
  
    -   **Examinar modelo**. Cuando se selecciona esta opción, en cuanto el asistente finaliza el procesamiento del modelo, se abre una ventana **examinar** para ayudarle a explorar los resultados. El contenido del visor depende del tipo de modelo que creó. Para obtener más información, vea [examinar un modelo de árboles de decisión](browsing-a-decision-trees-model.md) y [examinar un modelo de red neuronal](browsing-a-neural-network-model.md).  
  
    -   **Habilitar la obtención de detalles**. Seleccione esta opción para ver los datos subyacentes desde el modelo terminado. Esta opción solo está disponible si se crea un modelo de árbol de decisión.  
  
    -   **Usar modelo temporal**. Si selecciona esta opción, el modelo no se guardará en el servidor. Se eliminan los modelos temporales al cerrar Excel.  
  
## <a name="more-about-classification-models"></a>Más información sobre los modelos de clasificación  
 En el cuadro de diálogo **parámetros de algoritmo** , también puede elegir el método de clasificación entre estos algoritmos que se proporcionan en Analysis Services:  
  
-   Árbol de decisión de Microsoft  
  
-   Regresión logística de Microsoft  
  
-   Bayes naive de Microsoft  
  
-   Red neuronal de Microsoft  
  
 Aunque los algoritmos podrían producir resultados similares, analizan los datos de forma diferente, por lo que recomendamos probar varios y comparar los resultados. El método predeterminado es Árboles de decisión de Microsoft.  
  
 En la lista de **parámetros** , puede cambiar las opciones avanzadas, que dependen del tipo de algoritmo que elija. Los parámetros de cada algoritmo se describen con más detalle en los Libros en pantalla de SQL Server.  
  
 [Referencia técnica del algoritmo de árboles de decisión de Microsoft](data-mining/microsoft-decision-trees-algorithm-technical-reference.md)  
  
 [Referencia técnica del algoritmo de regresión logística de Microsoft](data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)  
  
 [Referencia técnica del algoritmo Bayes naive de Microsoft](data-mining/microsoft-naive-bayes-algorithm-technical-reference.md)  
  
 [Referencia técnica del algoritmo de red neuronal de Microsoft](data-mining/microsoft-neural-network-algorithm-technical-reference.md)  
  
### <a name="requirements"></a>Requisitos  
 Para usar el Asistente para **clasificar** , debe estar conectado a [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] una base de datos de. Para obtener información sobre cómo crear una conexión, vea [conectarse a los datos de origen &#40;cliente de minería de datos para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
## <a name="see-also"></a>Consulte también  
 [Crear un modelo de minería de datos](creating-a-data-mining-model.md)  
  
  
