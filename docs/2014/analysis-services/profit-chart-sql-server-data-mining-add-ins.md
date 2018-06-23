---
title: (Datos de SQL Server a los complementos de minería de datos) del gráfico de beneficios | Documentos de Microsoft
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- accuracy chart
- profit chart
- mining models, charting
- mining models, testing
ms.assetid: 5c902543-4da9-4db3-99d5-4ce04c43d7ef
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c78d1f477b878b2ddf78e3c5446e46c249ffcb62
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106246"
---
# <a name="profit-chart-sql-server-data-mining-add-ins"></a>Gráfico de beneficios (Complementos de minería de datos de SQL Server)
  ![Botón gráfico de beneficios en la cinta de opciones de minería de datos](media/dmc-profitchart.gif "botón gráfico de beneficios en la cinta de opciones de minería de datos")  
  
 Un gráfico de beneficios muestra el incremento estimado de beneficios relacionado con el uso de un modelo de minería de datos para determinar con qué clientes debe ponerse en contacto una empresa en un escenario empresarial. El eje Y del gráfico representa el beneficio, en tanto que el eje X representa el porcentaje de la población con la que la empresa se ha puesto en contacto. Un gráfico de beneficios típico muestra un incremento en los beneficios hasta un determinado punto, después del cual los beneficios disminuyen a medida que crece la población con la que se entra en contacto.  
  
## <a name="configuring-the-profit-chart"></a>Configurar el gráfico de beneficios  
 Mientras que el gráfico de precisión evalúa sólo la probabilidad de que las predicciones sean correctas o incorrectas, el gráfico de beneficios incorpora datos reales sobre las consecuencias de actuar en función de una predicción. Esto se consigue teniendo en cuenta los factores siguientes, que se especifican al ejecutar el asistente:  
  
-   **Población**  
  
     Número de casos del conjunto de datos que se utiliza para crear el gráfico de elevación. Por ejemplo, el número de clientes potenciales.  
  
-   **Costo fijo**  
  
     Costo fijo asociado con el problema de la empresa. Si se calculase para una solución de correo directo, el costo no dependería de variables como el número de llamadas telefónicas o el número de envíos de correo promocional.  
  
-   **Costo individual**  
  
     Costos adicionales al costo fijo y que se pueden asociar con cada contacto con el cliente. Por ejemplo, el correo promocional o las llamadas de teléfono.  
  
-   **Ingresos por individuo**  
  
     Cantidad de ingresos asociados con cada venta realizada con éxito.  
  
## <a name="using-the-profit-chart-wizard"></a>Usar el Asistente para gráfico de beneficios  
 Para crear un gráfico de beneficios, se debe hacer referencia a un modelo de minería de datos existente. Puede examinar los modelos para encontrar uno que coincida con sus datos, haga clic en **administrar modelos** o **examinar** para ver detalles sobre el algoritmo que se usó y las columnas en el modelo de minería de datos.  
  
 Para obtener más información, consulte [examinar modelos en Excel &#40;complementos de minería de datos de SQL Server&#41; ](browsing-models-in-excel-sql-server-data-mining-add-ins.md) y [administrar modelos &#40;complementos de minería de datos de SQL Server&#41;](manage-models-sql-server-data-mining-add-ins.md).  
  
#### <a name="to-create-a-profit-chart"></a>Para crear un gráfico de beneficios  
  
1.  Seleccione un modelo existente.  
  
2.  Especifique la columna que desea predecir y, si es necesario, un valor de destino.  
  
3.  Seleccione los datos de origen, que son los datos que se pasarán a través del modelo para crear una predicción. No deben ser los mismos datos que se usaron para crear el modelo.  
  
4.  Asigne las columnas de los nuevos datos (de origen) a las columnas utilizadas en el modelo de minería de datos. Si los nombres de las columnas son similares, el asistente hará la asignación automáticamente.  
  
5.  Especifique la información de costo que requiere el asistente: el costo fijo, el costo individual, la población y los ingresos esperados.  
  
6.  Si lo desea, puede escribir una serie de costos gradual (haga clic en el botón Examinar **(...)**  botón). Por ejemplo, una campaña de correo puede ser más económica a medida que aumenta el número de elementos enviados, por lo que puede especificarse un costo diferente en función del número de elementos, y el asistente ajustará automáticamente los costos para cada tamaño de muestra.  
  
7.  El asistente crea un gráfico que incluye el análisis de costos y beneficios para el modelo.  
  
### <a name="requirements"></a>Requisitos  
 Si se va a predecir un valor numérico discreto, debe seleccionarse el valor de destino exacto que se desea predecir.  
  
## <a name="understanding-the-profit-chart"></a>Descripción del gráfico de beneficios  
 El gráfico de beneficios contiene una línea vertical gris que puede desplazar haciendo clic en una ubicación del gráfico. El **leyenda de minería de datos** muestra una puntuación, la población correcta y la probabilidad de predicción que están asociados a la ubicación de la línea gris en el gráfico. Si selecciona el punto máximo de beneficios en el gráfico utilizando la línea gris, puede usar el valor de probabilidad de predicción para determinar un umbral de probabilidad para el contacto con un cliente.  
  
 Por ejemplo, si el máximo de la curva de beneficios está en el 55 por ciento de la población y la probabilidad de predicción asociada es del 20 por ciento, esto indica que para conseguir los máximos beneficios sólo debe ponerse en contacto con aquellos clientes cuya respuesta se predice con una probabilidad del 20 por ciento o superior.  
  
## <a name="see-also"></a>Vea también  
 [Validar modelos y usar modelos para la predicción &#40;datos complementos de minería de datos para Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)  
  
  