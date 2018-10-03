---
title: Examinar un modelo Bayes Naive | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: f9160b48-3beb-439c-9694-f084e1afa625
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bdc6b3aa34ae3d2a75e78fe70862d3186c959f82
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48223315"
---
# <a name="browsing-a-naive-bayes-model"></a>Examinar un modelo Bayes naive
  Al abrir un modelo de Naïve Bayes con **examinar**, el modelo se muestra en un visor interactivo con cuatro paneles diferentes. El visor se usa para explorar las correlaciones y obtener información sobre el modelo y los datos subyacentes.  
  
-   [Red de dependencias](#bkmk_DepNet)  
  
-   [Perfiles del atributo](#bkmk_AttProf)  
  
-   [Características del atributo](#bkmk_AttChar)  
  
-   [Distinción del atributo](#bkmk_AttDisc)  
  
##  <a name="BKMK_Tabs"></a> Explorar el modelo  
 El visor tiene por objeto ayudarle a explorar la interacción entre los atributos de entrada y los atributos de salida (las entradas y variables dependientes) que se detectaron mediante el modelo Bayes naive de [!INCLUDE[msCoName](../includes/msconame-md.md)].  
  
 Si desea experimentar con el Visor Naïve Bayes, utilice el [Asistente para clasificar &#40;complementos minería de datos para Excel&#41; ](classify-wizard-data-mining-add-ins-for-excel.md) asistente en la cinta de opciones minería de datos, haga clic en el **avanzadas** y cambie el algoritmo que se utiliza el algoritmo Naïve Bayes  
  
 Para estos ejemplos, se usan los datos de origen en el libro de ejemplo y agrupa la columna **Yearly Income**, en cinco grupos de ingresos, desde **Very Low** a **muy alto**. Posteriormente, el modelo Bayes naive analiza los factores en correlación con cada categoría de ingresos.  
  
###  <a name="bkmk_DepNet"></a> Red de dependencias  
 Es la primera ventana que usará el **red de dependencias**. Muestra de un solo vistazo las entradas que están estrechamente correlacionadas con el resultado seleccionado.  
  
 ![red de dependencias en Visor Bayes Naive](media/dm13-nb.gif "red de dependencias en Visor Bayes Naive")  
  
##### <a name="explore-the-dependency-network"></a>Explorar la red de dependencias  
  
1.  En primer lugar, haga clic en el resultado de destino, **Yearly Income**, que se representa como un nodo en el gráfico.  
  
     Los nodos resaltados que rodean la variable de destino son los que se correlacionan estadísticamente con este resultado. Use la leyenda en la parte inferior del visor para entender la naturaleza de la relación.  
  
2.  Haga clic en el control deslizante a la izquierda del visor y arrástrelo hacia abajo.  
  
     Este control filtra las variables independientes según la importancia de las dependencias. Cuando desplace el control deslizante hacia abajo, solamente permanecen en el gráfico los vínculos de mayor importancia.  
  
3.  Una vez haya filtrado el gráfico, haga clic en el botón, **Copiar vista del gráfico**. A continuación, seleccione una hoja de cálculo de Excel y presione Ctrl+V.  
  
     Esta opción copia la vista seleccionada, incluidos los filtros y lo que se ha resaltado.  
  
 [Volver al principio](#BKMK_Tabs)  
  
###  <a name="bkmk_AttProf"></a> Perfiles del atributo  
 El **perfiles del atributo** windows le proporciona una indicación visual de cómo todas las demás variables se relacionan con los resultados individuales.  
  
##### <a name="explore-the-profiles"></a>Explorar los perfiles  
  
1.  Para ocultar algunos valores de forma que pueda comparar los resultados con mayor facilidad, haga clic en el encabezado de columna y arrástrelo a otra columna.  
  
     ![atributo de perfiles en Visor Bayes Naive](media/dm13-nb-attprof.gif "atributo perfiles en Visor Bayes Naive")  
  
2.  Haga clic en cualquier celda para ver la distribución de valores en el **leyenda de minería de datos**.  
  
     Como los atributos asociados a los distintos resultados se muestran visualmente, es fácil identificar correlaciones interesantes, como por ejemplo, la forma en que se distribuyen los ingresos por región.  
  
3.  Para obtener los datos subyacentes de esta vista, haga clic en **copiar a Excel**. Una tabla se genera en una hoja de cálculo nueva que muestra las correlaciones entre atributos y resultados individuales. En esta tabla de Excel puede ocultar o filtrar columnas fácilmente.  
  
 [Volver al principio](#BKMK_Tabs)  
  
###  <a name="bkmk_AttChar"></a> Características del atributo  
 El **características del atributo** vista es útil para revisión en profundidad de una variable de resultado determinado y los factores que contribuyen.  
  
 ![atributo de características en Visor Bayes Naive](media/dm13-nb-viewer.gif "atributo características en Visor Bayes Naive")  
  
##### <a name="explore-the-attribute-characteristics"></a>Explorar las características del atributo  
  
1.  Haga clic en **valor** y seleccione un elemento de la **valor**.  
  
     Al seleccionar un resultado de destino, el gráfico se actualiza para mostrar los factores más estrechamente asociados a los resultados, ordenados según su importancia.  
  
     Tenga en cuenta que si crea un modelo con el [analizar Influenciadores clave &#40;herramientas de análisis de tabla para Excel&#41; ](analyze-key-influencers-table-analysis-tools-for-excel.md) opción, puede crear modelos que tienen más de un atributo de predicción. Sin embargo, el resto de los asistentes de los complementos de minería de datos le limitarán a un solo atributo de predicción.  
  
2.  Haga clic en **copiar a Excel** para crear una tabla, en una nueva hoja de cálculo, enumerar las puntuaciones para todos los atributos que están relacionados con el resultado de destino seleccionado.  
  
 [Volver al principio](#BKMK_Tabs)  
  
###  <a name="bkmk_AttDisc"></a> Distinción del atributo  
 El **distinción del atributo** vista le ayuda a comparar dos resultados, o uno de los resultados frente a todos los demás resultados.  
  
 ![atributo de discriminación en Visor Bayes Naive](media/dm13-nb-attdisc.gif "atributo discriminación en Visor Bayes Naive")  
  
##### <a name="explore-attribute-discrimination"></a>Explorar la distinción del atributo  
  
1.  Use los controles, **valor 1** y **valor 2**, para seleccionar los resultados que desea comparar.  
  
     Por ejemplo, en este modelo había ciertos atributos interesantes en el grupo de ingresos bajos, por lo que se seleccionó el grupo de ingresos más bajo en la primera lista desplegable y elija **todos los demás Estados** en la segunda lista desplegable.  
  
     Los atributos se ordenan por orden de importancia (se calcula en función de los datos de entrenamiento). Por tanto, el empleo es el factor más estrechamente correlacionado con los ingresos (al menos para el primer grupo de destino).  
  
     Para ver las cifras exactas, haga clic en la barra coloreada y ver el **leyenda de minería de datos**.  
  
2.  Observe que los ingresos más bajos también se correlacionan con la región Europa.  
  
     El modelo de Bayes naive no admite la obtención de detalles; sin embargo, si quisiera investigar los casos asociados a este grupo de resultados, puede utilizar una consulta. Para obtener información acerca de las consultas en este tipo de modelo, vea [ejemplos de consultas de modelo de Bayes Naive](data-mining/naive-bayes-model-query-examples.md).  
  
 [Volver al principio](#BKMK_Tabs)  
  
## <a name="see-also"></a>Vea también  
 [Examinar modelos en Excel &#40;complementos de minería de datos de SQL Server&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)  
  
  
