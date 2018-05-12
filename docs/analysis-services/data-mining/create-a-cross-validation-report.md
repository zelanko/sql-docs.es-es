---
title: Crear un informe de validación cruzada | Documentos de Microsoft
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 88d3af205a1e92ac07a4c841c80f2abea463de9b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="create-a-cross-validation-report"></a>Crear un informe de validación cruzada
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Este tema le guía a través del proceso de creación de un informe de validación cruzada utilizando la pestaña Gráfico de precisión del Diseñador de minería de datos. Para obtener información general sobre el aspecto de un informe de validación cruzada y sobre las medidas estadísticas que se incluyen en este, vea [Validación cruzada &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/cross-validation-analysis-services-data-mining.md).  
  
 Un informe de validación cruzada es totalmente diferente de un gráfico de precisión, como un gráfico de mejora respecto al modelo predictivo o una matriz de clasificación.  
  
-   La validación cruzada evalúa la distribución global de los datos utilizados en un modelo o una estructura; por lo tanto, no es necesario especificar un conjunto de datos de pruebas. La validación cruzada utiliza siempre únicamente los datos originales que se utilizaron para entrenar al modelo o a la estructura de minería de datos.  
  
-   Este tipo de validación solo se puede realizar con respecto a un único resultado de predicción. Si la estructura admite modelos con atributos de predicción diferentes, deberá crear informes independientes para cada resultado de predicción.  
  
-   Solo los modelos que se relacionan con la estructura seleccionada actualmente están disponibles para la validación cruzada.  
  
-   Si la estructura que está seleccionada actualmente admite una combinación de modelos de agrupación en clústeres y de no agrupación en clústeres, al hacer clic en **Obtener resultados**, el procedimiento almacenado de validación cruzada cargará automáticamente los modelos que tengan la misma columna predicha y omitirá los modelos de agrupación en clústeres que no compartan el mismo atributo de predicción.  
  
-   Solo podrá crear un informe de validación cruzada en un modelo de agrupación en clústeres que no tenga un atributo de predicción si la estructura de minería de datos no admite ningún otro atributo de predicción.  
  
### <a name="select-a-mining-structure"></a>Seleccionar una estructura de minería de datos  
  
1.  Abra el Diseñador de minería de datos de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  En el Explorador de soluciones, abra la base de datos que contiene la estructura o el modelo para el que desea crear un informe.  
  
3.  Haga doble clic en la estructura de minería de datos para abrir la estructura y sus modelos relacionados en el Diseñador de minería de datos.  
  
4.  Haga clic en la pestaña **Gráfico de precisión de minería de datos** .  
  
5.  Haga clic en la pestaña **Validación cruzada** .  
  
### <a name="set-cross-validation-options"></a>Establecer opciones de validación cruzada  
  
1.  En la pestaña **Validación cruzada** , en **Recuento de plegamientos**, haga clic en la flecha abajo para seleccionar un número entre 1 y 10. El valor predeterminado es 10.  
  
     El **Recuento de plegamientos** representa el número de particiones que se creará dentro del conjunto de datos original. Si establece Recuento de plegamientos en 1, el conjunto de entrenamiento se utilizará sin particiones.  
  
2.  En **Atributo de destino**, haga clic en la flecha abajo y seleccione una columna en la lista. Si el modelo es un modelo de agrupación en clústeres, seleccione **#Cluster** para indicar que el modelo no tiene un atributo de predicción. Tenga en cuenta que el valor **#Cluster**solo estará disponible si la estructura de minería de datos no admite otros tipos de atributos de predicción.  
  
     Puede seleccionar solo un atributo de predicción para cada informe. De forma predeterminada, todos los modelos relacionados que tienen el mismo atributo de predicción se incluyen en el informe.  
  
3.  En **Máximo de casos**, escriba un número que sea suficientemente grande para proporcionar una muestra representativa de datos cuando los datos se dividen entre el número especificado de plegamientos. Si el número es mayor que el recuento de casos en el conjunto de entrenamiento del modelo, se utilizarán todos los casos.  
  
     Si el conjunto de datos de entrenamiento es muy grande, al establecer el valor de **Máximo de casos** se limita el número total de casos procesados y se permite que el informe finalice más rápidamente. Pero no establezca el valor de **Máximo de casos** en un valor demasiado bajo, ya que es posible que no haya datos suficientes para la validación cruzada.  
  
4.  Si lo desea, en **Estado de destino**, escriba el valor del atributo de predicción que desea modelar. Por ejemplo, si la columna [Bike Buyer] tiene dos valores posibles, 1 (Sí) y 2 (No), puede especificar el valor 1 para evaluar la exactitud del modelo solo para el resultado deseado.  
  
    > [!NOTE]  
    >  Si no especifica un valor, la opción **Umbral de destino** no estará disponible y el modelo se evaluará para todos los valores posibles del atributo de predicción.  
  
5.  Opcionalmente, en **Umbral de destino**, escriba un número decimal comprendido entre 0 y 1 para especificar la probabilidad mínima que una predicción debe tener para que se considere que es precisa.  
  
     Para más información sobre cómo establecer los umbrales de probabilidad, vea [Medidas en el informe de validación cruzada](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md).  
  
6.  Haga clic en **Obtener resultados**.  
  
### <a name="print-the-cross-validation-report"></a>Imprimir el informe de validación cruzada  
  
1.  Haga clic con el botón derecho en la pestaña **Validación cruzada** del informe completado.  
  
2.  En el menú contextual, seleccione **Imprimir** o **Vista previa de impresión** para revisar el informe primero.  
  
### <a name="create-a-copy-of-the-report-in-microsoft-excel"></a>Crear una copia del informe en Microsoft Excel  
  
1.  Haga clic con el botón derecho en la pestaña **Validación cruzada** del informe completado.  
  
2.  En el menú contextual, seleccione **Seleccionar todo**.  
  
3.  Haga clic con el botón derecho en el texto seleccionado y, después, haga clic en **Copiar**.  
  
4.  Pegue la selección en un libro de Excel abierto. Si utiliza la opción **Pegar** , el informe se pega en Excel como HTML, con lo que se conserva el formato de filas y columnas. Si pega el informe con las opciones de **Pegado especial** para texto o texto Unicode, el informe se pegará con un formato delimitado por filas.  
  
## <a name="see-also"></a>Vea también  
 [Medidas en el informe de validación cruzada](../../analysis-services/data-mining/measures-in-the-cross-validation-report.md)  
  
  
