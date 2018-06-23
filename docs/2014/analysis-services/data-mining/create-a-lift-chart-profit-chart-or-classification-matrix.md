---
title: Crear un gráfico de elevación, un gráfico de beneficios o una matriz de clasificación | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Mining Accuracy Chart [Analysis Services], mining structures
ms.assetid: aa3d052f-58a9-4417-8e7a-5e6feb562af0
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f4538b84c5dcda3ef5c29d191e8e2dcf78c39442
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106235"
---
# <a name="create-a-lift-chart-profit-chart-or-classification-matrix"></a>Crear un gráfico de mejora respecto al modelo predictivo, un gráfico de beneficios o una matriz de clasificación
  Puede crear un gráfico de precisión para un modelo de minería de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] siguiendo cinco pasos básicos:  
  
-   Seleccione la estructura de minería de datos que contiene los modelos de minería de datos que desea comparar.  
  
-   Seleccione los modelos de minería de datos que desea agregar al gráfico.  
  
-   Especifique el origen de datos de pruebas que se ha de utilizar al generar el gráfico.  
  
-   Elija el tipo de gráfico.  
  
-   Configure las opciones de gráfico.  
  
 Estos pasos básicos son los mismos para el gráfico de elevación, el gráfico de beneficios y la matriz de clasificación. Los procedimientos siguientes describen los pasos necesarios para configurar las opciones de gráfico básicas para estos tipos de gráfico. Para obtener más información sobre cómo crear un informe de validación cruzada, vea [Medidas en el informe de validación cruzada](measures-in-the-cross-validation-report.md).  
  
### <a name="open-the-mining-structure-in-the-accuracy-chart-designer"></a>Abrir la estructura de minería de datos en el Diseñador de gráficos de precisión  
  
1.  Abra el Diseñador de minería de datos de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  En el Explorador de soluciones, haga doble clic en la estructura que contiene el modelo o los modelos de minería de datos.  
  
3.  Haga clic en la pestaña **Gráfico de precisión de minería de datos** .  
  
### <a name="select-mining-models-for-inclusion-in-the-chart"></a>Seleccionar los modelos de minería de datos para incluirlos en el gráfico  
  
1.  En la pestaña **Gráfico de precisión de minería de datos** del Diseñador de minería de datos de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], haga clic en la pestaña **Selección de entrada** .  
  
     La lista muestra todos los modelos de la estructura actual que tienen el mismo atributo de predicción.  
  
2.  Seleccione el cuadro **Mostrar** para cada uno de los modelos que desea incluir en el gráfico.  
  
3.  Haga clic en el cuadro de texto **Nombre de columna de predicción** y seleccione el nombre de una columna de predicción en la lista. Todos los modelos que ponga en el gráfico deben tener la misma columna de predicción.  
  
4.  Si compara dos modelos y las columnas de predicción tienen valores o tipos de datos diferentes, desactive la casilla **Sincronizar valores y columnas de predicción** para forzar la comparación.  
  
    > [!NOTE]  
    >  Si está activada la casilla **Sincronizar valores y columnas de predicción** , Analysis Services analiza los datos de las columnas de predicción del modelo y los datos de pruebas, e intenta buscar la mejor coincidencia. Por consiguiente, no desactive la casilla a menos que sea absolutamente necesario forzar una comparación de las columnas.  
  
5.  Haga clic en el cuadro de texto **Valor de predicción** y seleccione un valor en la lista. Si la columna de predicción es un tipo de datos continuo, debe escribir un valor en el cuadro de texto.  
  
     Para obtener más información, vea [Elija la columna que se va a utilizar para probar un modelo de minería de datos](choose-the-column-to-use-for-testing-a-mining-model.md).  
  
### <a name="select-testing-data"></a>Seleccionar los datos de pruebas  
  
1.  En la pestaña **Selección de entrada** de la pestaña **Gráfico de precisión de minería de datos** , especifique el origen de los datos que utilizará para generar el gráfico seleccionando una de las opciones del grupo **Seleccionar un conjunto de datos para usarlo en un gráfico de precisión**.  
  
    -   Seleccione la opción **Usar casos de pruebas de modelo de minería de datos**si desea utilizar el subconjunto de casos definido por la intersección de los casos de prueba de la estructura de minería de datos y los filtros que se hayan aplicado durante la creación del modelo.  
  
    -   Seleccione la opción **Usar casos de pruebas de estructura de minería de datos**para utilizar el conjunto completo de casos de prueba que se definieron como parte del conjunto de datos de exclusión de las estructuras de minería de datos.  
  
    -   Seleccione la opción **Especificar otro conjunto de datos**si desea utilizar datos externos.  El conjunto de datos debe estar disponible como vista del origen de datos.   Haga clic en el botón Examinar (**…**) para elegir las tablas de datos que quiere usar en el gráfico de precisión. Para más información, consulte [Choose and Map Model Testing Data](choose-and-map-model-testing-data.md).  
  
         Si está utilizando un conjunto de datos externos, opcionalmente puede filtrar el conjunto de datos de entrada. Para obtener más información, vea [Aplicar filtros a los datos de prueba del modelo](apply-filters-to-model-testing-data.md).  
  
> [!NOTE]  
>  No puede crear un filtro para los casos de prueba del modelo ni para los casos de prueba de la estructura de minería de datos de la pestaña **Selección de entrada** . Para crear un filtro en el modelo de minería de datos, modifique la propiedad Filter del modelo. Para obtener más información, vea [Aplicar un filtro a un modelo de minería de datos](apply-a-filter-to-a-mining-model.md).  
  
### <a name="configure-chart-settings-and-generate-the-chart"></a>Configurar los valores del gráfico y generarlo  
  
1.  En la pestaña **Gráfico de precisión de minería de datos** , haga clic en la pestaña correspondiente al gráfico que desea crear.  
  
2.  Para un **gráfico de mejora respecto al modelo predictivo**, haga clic en la pestaña **Gráfico de elevación** . El gráfico se genera automáticamente basándose en el modelo, los atributos de predicción y los datos de entrada que acaba de seleccionar.  
  
3.  Para una **matriz de clasificación**, haga clic en la pestaña **Matriz de clasificación** . No es necesario ningún valor más; el gráfico se genera automáticamente basándose en los datos de entrada y en el modelo seleccionado.  
  
4.  Para un **gráfico de beneficios**, primero haga clic en la pestaña **Gráfico de elevación** . Después, en la lista desplegable **Tipo de gráfico** , seleccione **Gráfico de beneficios**.  
  
     Escriba los valores siguientes en el cuadro de diálogo **Configuración del gráfico de beneficios** .  
  
     **Población**  
     El número de casos del conjunto de datos que desea utilizar al crear el gráfico de elevación.  
  
     El modelo siempre elige los casos en orden de probabilidad decreciente; es decir, si se están evaluando clientes potenciales y elige un número que representa solo la mitad de los registros de la base de datos de clientes, el modelo medirá la exactitud en el subconjunto de casos que mejor se ajustan al modelo.  
  
     Esto se debe a que cuando use el modelo para generar un envío de correo directo o crear una campaña, utilizará la probabilidad de predicción asociada a cada caso para destinarlo solo a los clientes que tengan la mayor probabilidad de dar una respuesta favorable.  
  
     **Costo fijo**  
     Costo fijo asociado con el problema de la empresa.  
  
     Si se tratara de una solución de envío de correo directo, el costo fijo podría representar una tarifa por la configuración de la impresora que abarcara el costo inicial de preparar el envío de correo promocional.  
  
     Este costo se aplica una vez a toda la población de destino.  
  
     **Costo individual**  
     Costos adicionales al costo fijo y que se pueden asociar con cada contacto con el cliente. Por ejemplo, podría especificar el costo del franqueo para un envío de correo promocional o el costo de la realización de llamadas telefónicas.  
  
     Este costo debe ser el mismo para toda la población de destino. Cada valor se multiplica por el número de casos que constituyen el destino.  
  
     **Ingresos por individuo**  
     Cantidad de ingresos asociados con cada venta realizada con éxito.  
  
## <a name="see-also"></a>Vea también  
 [Gráfico de elevación &#40;Analysis Services: minería de datos&#41;](lift-chart-analysis-services-data-mining.md)   
 [Matriz de clasificación &#40;Analysis Services: minería de datos&#41;](classification-matrix-analysis-services-data-mining.md)  
  
  