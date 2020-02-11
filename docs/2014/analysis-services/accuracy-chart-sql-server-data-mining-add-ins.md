---
title: Gráfico de precisión (complementos de minería de datos de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- accuracy chart
- mining models, validating
- mining models, charting
- lift chart
- mining models, testing
- lift [data mining]
ms.assetid: 303973b4-71c0-4cfc-b7bc-92218b52509d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ebe159aed7b27bf00ef47a110de1c7ec5ee70adb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66062987"
---
# <a name="accuracy-chart-sql-server-data-mining-add-ins"></a>Gráfico de precisión (Complementos de minería de datos de SQL Server)
  ![Botón Gráfico de precisión de la cinta Minería de datos](media/dmc-accchart.gif "Botón Gráfico de precisión de la cinta Minería de datos")  
  
 Un gráfico de precisión permite aplicar un modelo a un conjunto de datos nuevo y, a continuación, evaluar su rendimiento. El gráfico de precisión creado por este asistente es un *gráfico de elevación*, que es un tipo de gráfico que se usa con frecuencia para medir la precisión de un modelo de minería de datos. Este tipo de gráfico de precisión muestra una representación gráfica de la mejora obtenida al usar el modelo de minería de datos especificado en comparación con predicciones aleatorias y con el caso ideal de que el cien por cien de esas predicciones fuera correcto. Puede comparar varios modelos dentro de un único gráfico.  
  
## <a name="example"></a>Ejemplo  
 Pongámonos en el caso de que el departamento de marketing de Adventure Works Cycles desee crear una campaña de correo directo. Por las campañas anteriores, saben que el índice de respuesta típico es de un 10 por ciento. Tienen una lista de 10.000 clientes potenciales almacenada en una tabla de la base de datos. Basándose en el índice típico de respuesta, pueden esperar que respondan 1.000 clientes.  
  
 No obstante, dado que sólo se pueden permitir el envío de un anuncio a 5.000 clientes, el departamento de marketing emplea un modelo de minería de datos para dirigirse a los 5.000 clientes que es más probable que respondan.  
  
 Si la empresa selecciona aleatoriamente 5.000 clientes, es de esperar tan sólo 500 respuestas positivas, ya que generalmente sólo responde el 10 por ciento. La línea aleatoria del gráfico de elevación representa este escenario.  
  
 Sin embargo, si el departamento de marketing usara un modelo de minería de datos para realizar el envío de correo y este modelo fuera perfecto, la empresa podría enviar un anuncio a los 1.000 clientes potenciales recomendados por el modelo y aspirar a recibir 1.000 respuestas. La línea ideal del gráfico de elevación representa este escenario.  
  
## <a name="using-the-accuracy-chart-wizard"></a>Usar el Asistente para gráfico de precisión  
 Para crear un gráfico de precisión, debe hacer referencia a una estructura de minería de datos existente. Puede medir la precisión de varios modelos que estén basados en esa estructura, siempre y cuando predigan lo mismo.  
  
 Si no está seguro de qué estructuras están disponibles, puede examinar el servidor. Para obtener más información, vea [examinar modelos en Excel &#40;SQL Server complementos de minería de datos&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md).  
  
#### <a name="to-create-an-accuracy-chart"></a>Para crear un gráfico de precisión  
  
1.  Haga clic en la cinta de opciones **cliente de minería de datos** .  
  
2.  En el grupo **precisión y validación** , haga clic en **gráfico de precisión**.  
  
3.  En el cuadro de diálogo **seleccionar estructura o modelo** , elija el modelo que desea evaluar. Haga clic en **Next**.  
  
    > [!NOTE]  
    >  Debe seleccionar un modelo que coincida con los datos que desea probar.  
  
4.  En el cuadro de diálogo especificar columna que se va a predecir **y valor que se va a predecir** , elija la columna que desea predecir y, si es necesario, un valor de destino. Haga clic en **Next**.  
  
     Por ejemplo, en el ejemplo anterior, puede seleccionar la columna que modela la respuesta del cliente y especificar el valor de destino como "Probably Will Buy".  
  
    > [!NOTE]  
    >  No es posible predecir un valor continuo. Sin embargo, se puede discretizar la columna si separa los valores en intervalos discretos. Esto debe hacerse antes de crear el modelo de minería de datos.  
  
5.  En el cuadro de diálogo **seleccionar datos de origen** , especifique el origen de los datos que pasará a través del modelo para crear una predicción.  
  
6.  Si utiliza un origen de datos externo, y no los datos de prueba que se almacenan con el modelo, en el cuadro de diálogo **especificar relaciones** , asigne las columnas de los nuevos datos de origen a las columnas utilizadas en el modelo de minería de datos.  
  
     Si los nombres de las columnas son similares, el asistente hará la asignación automáticamente. Aunque algunas columnas de los datos de entrada pueden ser irrelevantes para el análisis y pueden omitirse, otras son necesarias para que el modelo de minería de datos procese la entrada. Dichas columnas pueden incluir un identificador de transacción, el valor de destino, o pueden ser columnas usadas para la predicción. Si no asigna una columna necesaria, el asistente mostrará un mensaje de advertencia.  
  
7.  Haga clic en **Finalizar**  
  
     El asistente crea un informe que incluye el gráfico de elevación y los datos subyacentes.  
  
### <a name="requirements"></a>Requisitos  
 Si se va a predecir un valor discreto, es necesario seleccionar el valor de destino que se desea predecir. Por ejemplo, si los datos se han clasificado con una respuesta "Yes: Buy" como 1 y "No: Do Not Buy" como 2, es necesario especificar 1 ó 2 como valores de predicción. Sin embargo, si se desea predecir un intervalo de valores, sólo es posible comparar dos valores a la vez. Por ejemplo, si se desea predecir una puntuación superior a 5, quizás sea necesario cambiar las etiquetas de los datos de origen y crear un nuevo modelo que separe los resultados en dos conjuntos: aquellos mayores que 5 y aquellos menores que 5. A continuación, puede comparar la precisión de esos dos grupos.  
  
## <a name="understanding-accuracy"></a>Descripción de la precisión  
 Puede crear dos tipos de gráficos, uno en el que especifique un estado de la columna de predicción y otro en el que no especifique el estado.  
  
 Si especifica el estado de la columna de predicción, el eje X del gráfico representa el porcentaje del conjunto de datos de prueba que se usa para comparar las predicciones. El eje Y del gráfico representa el porcentaje de valores que se predicen que tendrán el estado especificado.  
  
 Si no especifica el estado de la columna de predicción, el gráfico muestra la precisión del modelo para todas las predicciones posibles.  
  
 Para obtener más información acerca del funcionamiento de los gráficos de elevación y del cálculo de la precisión basado en las líneas de predicción aleatorias e ideales, vea el tema "Gráfico de elevación" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Validar modelos y usar modelos para la predicción &#40;complementos de minería de datos para Excel&#41;](validating-models-and-using-models-for-prediction-data-mining-add-ins-for-excel.md)  
  
  
