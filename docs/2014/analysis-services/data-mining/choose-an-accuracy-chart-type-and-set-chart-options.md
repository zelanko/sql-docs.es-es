---
title: Elegir un tipo de gráfico de precisión y establecer las opciones del gráfico | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Mining Accuracy Chart [Analysis Services]
- mining models [Analysis Services], validating
- classification accuracy [data mining]
- accuracy testing [data mining]
ms.assetid: bd24dd4a-624f-478a-9c94-b1361e857680
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6d9f375eb2d55c396000b7c2d7a14614153861e6
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66085823"
---
# <a name="choose-an-accuracy-chart-type-and-set-chart-options"></a>Elegir un tipo de gráfico de precisión y establecer las opciones del gráfico
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proporciona varios métodos para determinar la validez de los modelos de minería de datos. El tipo de gráfico de precisión que puede crear para cada modelo o estructura depende de estos factores:  
  
-   El tipo de algoritmo utilizado para crear el modelo  
  
-   El tipo de datos del atributo de predicción.  
  
-   El número de atributos de predicción que medir  
  
 En este tema se proporciona información general de los diferentes gráficos de precisión.  
  
 **Nota** Los gráficos y sus definiciones no se guardan. Si cierra la ventana que contiene un gráfico, debe volverlo a crear.  
  
## <a name="accuracy-chart-types"></a>Tipos de gráficos de precisión  
 Según el tipo de gráfico que elija, puede seguir configurando las opciones, examinar el gráfico o copiarlo en el Portapapeles y trabajar con los datos en Excel.  
  
#### <a name="lift-chart"></a>Gráfico de elevación  
 Después de configurar las opciones para los modelos y los datos de prueba, haga clic en la pestaña **Gráfico de elevación** para ver los resultados. También puede copiar el gráfico en el Portapapeles o ver detalles de puntos de datos o líneas de tendencia individuales en la Leyenda de minería de datos.  
  
#### <a name="profit-chart"></a>Gráfico de beneficios  
 Después de configurar las opciones de los modelos y los datos de prueba, haga clic en la pestaña **Gráfico de elevación** , seleccione **Gráfico de beneficios** en la lista **Tipo de gráfico** para establecer las opciones del gráfico de beneficios y, a continuación, haga clic en **Aceptar** para ver los resultados.  
  
 Puede utilizar el cuadro de diálogo **Configuración del gráfico de beneficios** tantas veces como desee para probar opciones de costo diferentes y volver a mostrar el gráfico. La Leyenda de minería de datos contiene información detallada sobre las ventajas estimadas de cada modelo. También puede copiar el gráfico y el contenido de la Leyenda de minería de datos en el Portapapeles para trabajar con ellos en Excel.  
  
#### <a name="scatter-plot"></a>Gráfico de dispersión  
 Si ha seleccionado el tipo adecuado de modelo, al hacer clic en la pestaña **Gráfico de elevación** , el tipo de gráfico se establece automáticamente en **Gráfico de dispersión** y se muestra un gráfico de dispersión. No se puede realizar ninguna otra configuración. También puede copiar el gráfico en el Portapapeles y pegarlo como un gráfico en Excel u otra aplicación.  
  
#### <a name="classification-matrix"></a>Matriz de clasificación  
 En una matriz de clasificación, utilice la pestaña **Selección de entrada** para elegir los modelos y los datos de prueba y, a continuación, haga clic en la pestaña **Matriz de clasificación** para ver los resultados.  
  
 El contenido de una matriz de clasificación es el mismo para todos los tipos de modelo y no se puede configurar. Puede copiar los datos del gráfico en el Portapapeles y, a continuación, trabajar con ellos en Excel.  
  
#### <a name="cross-validation-report"></a>Informe de validación cruzada  
 En un informe de validación cruzada, después de seleccionar una estructura o un modelo de minería de datos en el Explorador de soluciones, haga clic en la pestaña **Validación cruzada** , configure todas las opciones correspondientes y, después, haga clic **Obtener resultados** para generar el informe. No se puede realizar ninguna otra configuración.  
  
 El formato del informe de validación cruzada es el mismo para todos los tipos de modelo y no se puede configurar. Sin embargo, el contenido del informe difiere según sea el tipo de modelo que se esté analizando y el tipo de datos del atributo de predicción. También puede copiar los resultados del informe en el Portapapeles y trabajar con ellos en Excel.  
  
  
