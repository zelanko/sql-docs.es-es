---
title: Transformación Muestreo de fila | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.rowsamplingtrans.f1
- sql13.DTS.DESIGNER.ROWSAMPLINGTRANSFORMATION.COLUMNS.F1
- sql13.dts.designer.rowsamplingtransformation.f1
helpviewer_keywords:
- sampling seeds [Integration Services]
- random seeds
- random sampling
- sample data sets [Integration Services]
- Row Sampling transformation
- packages [Integration Services], samples
- datasets [Integration Services], sample
ms.assetid: b6caafd3-30b2-4368-82af-a44611d4cd39
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e2964300e2990721afe920c0e418a220fe0b1a22
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/20/2019
ms.locfileid: "58271940"
---
# <a name="row-sampling-transformation"></a>Muestreo de fila, transformación
  La transformación Muestreo de fila se usa para obtener un subconjunto seleccionado aleatoriamente de un conjunto de datos de entrada. Puede especificar el tamaño exacto del ejemplo de salida y especificar un valor de inicialización para el generador de números aleatorios.  
  
 Hay muchas aplicaciones para el muestreo aleatorio. Por ejemplo, una compañía que desea seleccionar aleatoriamente 50 empleados que recibirán los premios de una lotería podría aplicar la transformación Muestreo de fila a la base de datos de empleados para generar el número exacto de ganadores.  
  
 La transformación Muestreo de fila también es útil durante el desarrollo de paquetes para crear un conjunto de datos pequeño pero representativo. Puede probar la ejecución del paquete y la transformación de datos con datos representativos. Tardará menos tiempo, ya que usará una muestra aleatoria en lugar del conjunto de datos completo. Como el conjunto de datos de ejemplo utilizado por el paquete de prueba tiene siempre el mismo tamaño, al usar el subconjunto de ejemplo también resulta más fácil identificar posibles problemas de rendimiento del paquete.  
  
 Esta transformación es similar a la transformación Muestreo de porcentaje, que crea un conjunto de datos de ejemplo seleccionando un porcentaje de las filas de entrada. Consulte [Percentage Sampling Transformation](../../../integration-services/data-flow/transformations/percentage-sampling-transformation.md).  
  
## <a name="configuring-the-row-sampling-transformation"></a>Configurar la transformación Muestreo de fila  
 La transformación Muestreo de fila crea un conjunto de datos de ejemplo seleccionando un número especificado de las filas de entrada de la transformación. Como la selección de filas de la entrada de transformación es aleatoria, la muestra resultante es representativa de la entrada. También puede especificar el valor de inicialización que usará el generador de números aleatorios; dicho valor afectará al modo en que la transformación seleccionará filas.  
  
 Si se utiliza el mismo valor de inicialización aleatorio en la misma entrada de la transformación, siempre se creará la misma salida de ejemplo. Si no se especifica un valor de inicialización, la transformación utilizará el contador del sistema operativo para crear el número aleatorio. Por tanto, puede usar el mismo valor de inicialización durante las pruebas, para comprobar los resultados de la transformación durante el desarrollo y las pruebas del paquete, y después cambiarlo por un valor de inicialización aleatorio cuando el paquete pase a producción.  
  
 La transformación Muestreo de fila incluye la propiedad personalizada **SamplingValue** . Esta propiedad se puede actualizar a través de una expresión de propiedad, al cargar el paquete. Para obtener más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Usar expresiones de propiedad en paquetes](../../../integration-services/expressions/use-property-expressions-in-packages.md) y [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Esta transformación tiene una entrada y dos salidas. No tiene ninguna salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para obtener más información sobre cómo establecer propiedades, vea.  
  
## <a name="row-sampling-transformation-editor-sampling-page"></a>Editor de transformación Muestreo de fila (página Muestreo)
  Use el cuadro de diálogo **Editor de transformación Muestreo de fila** para dividir una parte de una entrada en un ejemplo que utilice un número especificado de filas. La transformación divide la entrada en dos salidas independientes.  
  
### <a name="options"></a>Opciones  
 **Número de filas**  
 Especifique el número de filas de la entrada que se utilizarán como ejemplo.  
  
 Puede especificar el valor de esta propiedad con una expresión de propiedad.  
  
 **Nombre de salida de ejemplo**  
 Proporcione un nombre único para la salida que incluirá las filas de ejemplo. El nombre que indique se mostrará en el Diseñador SSIS.  
  
 **Nombre de salida no seleccionado**  
 Proporcione un nombre único para la salida que contendrá las filas excluidas de ejemplo. El nombre que indique se mostrará en el Diseñador SSIS.  
  
 **Utilizar el valor de inicialización aleatorio siguiente**  
 Especifique el valor de inicialización del ejemplo para el generador de números aleatorios que utiliza la transformación para crear un ejemplo. Esto solamente se recomienda para desarrollo y pruebas. La transformación utiliza el contador de Microsoft Windows como valor de inicialización si no se especifica un valor de inicialización aleatorio.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
  
