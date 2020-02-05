---
title: Transformación Muestreo de porcentaje | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.percentagesamplingtrans.f1
- sql13.dts.designer.percentagesamplingtransformation.f1
helpviewer_keywords:
- testing mining models
- sampling seeds [Integration Services]
- data mining [Analysis Services], sample data sets
- Percentage Sampling transformation
- sample data sets [Integration Services]
- datasets [Integration Services], sample
- training mining models
ms.assetid: 59767e52-f732-4b3f-8602-be50d0a64ef2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c51d65dabef5efa4de7ecb4c62b633e62ed0b082
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "71297890"
---
# <a name="percentage-sampling-transformation"></a>Muestreo de porcentaje, transformación

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La transformación Muestreo de porcentaje crea un conjunto de datos de muestra seleccionando un porcentaje de las filas de entrada de transformación. El conjunto de datos de muestra es una selección aleatoria de filas de la entrada de transformación, de forma que la muestra resultante sea representativa de la entrada.  
  
> [!NOTE]  
>  Además del porcentaje especificado, la transformación Muestreo de porcentaje utiliza un algoritmo para determinar si se debe incluir una fila en la salida de ejemplo. Esto significa que el número de filas de la salida de ejemplo podría no reflejar exactamente el porcentaje especificado. Por ejemplo, si especifica 10% para un conjunto de datos de entrada que tiene 25.000 filas, no se generará una muestra con exactamente 2.500 filas; la muestra puede tener unas pocas filas más o menos.  
  
 La transformación Muestreo de porcentaje es especialmente útil para la minería de datos. Utilizando esta transformación, puede dividir de forma aleatoria un conjunto de datos en dos conjuntos de datos: uno para el entrenamiento del modelo de minería de datos y otro para probar el modelo.  
  
 La transformación Muestreo de porcentaje también es útil para crear conjuntos de datos de ejemplo de desarrollo de paquetes. Si aplica la transformación Muestreo de porcentaje a un flujo de datos, puede reducir uniformemente el tamaño de los conjuntos de datos conservando sus características. El paquete de prueba podrá ejecutarse más rápido porque utilizará un conjunto de datos pequeño, pero representativo.  
  
## <a name="configuration-the-percentage-sampling-transformation"></a>Configuración de la transformación Muestreo de porcentaje  
 Puede especificar un valor de inicialización de muestreo para modificar el comportamiento del generador de números aleatorios utilizado por la transformación para seleccionar filas. Si se usa el mismo valor de inicialización de muestreo, la transformación siempre creará la misma salida de ejemplo. Si no se especifica un valor de inicialización, la transformación utilizará el contador del sistema operativo para crear el número aleatorio. Por tanto, puede elegir usar un valor de inicialización estándar cuando desee comprobar los resultados de la transformación durante el desarrollo y las pruebas de un paquete, y después usar un valor de inicialización aleatorio cuando el paquete pase a producción.  
  
 Esta transformación es similar a la transformación Muestreo de fila, que crea a conjunto de datos de ejemplo seleccionando un número especificado de filas de entrada. Para más información, consulte [Row Sampling Transformation](../../../integration-services/data-flow/transformations/row-sampling-transformation.md).  
  
 La transformación Muestreo de porcentaje incluye la propiedad personalizada **SamplingValue** . Esta propiedad se puede actualizar a través de una expresión de propiedad, al cargar el paquete. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Usar expresiones de propiedad en paquetes](../../../integration-services/expressions/use-property-expressions-in-packages.md) y [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 La transformación tiene una entrada y dos salidas. No admite una salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Para más información sobre cómo establecer propiedades, vea [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="percentage-sampling-transformation-editor"></a>Editor de transformación Muestreo de porcentaje
  Use el cuadro de diálogo **Editor de transformación Muestreo de porcentaje** para dividir parte de una entrada en un ejemplo utilizando un porcentaje de filas especificado. La transformación divide la entrada en dos salidas independientes.  
  
### <a name="options"></a>Opciones  
 **Porcentaje de filas**  
 Especifique el porcentaje de filas de la entrada que se utilizarán como ejemplo.  
  
 Puede especificar el valor de esta propiedad con una expresión de propiedad.  
  
 **Nombre de salida de ejemplo**  
 Proporcione un nombre único para la salida que incluirá las filas de ejemplo. El nombre proporcionado se mostrará en el Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .  
  
 **Nombre de salida no seleccionado**  
 Proporcione un nombre único para la salida que contendrá las filas excluidas de ejemplo. El nombre proporcionado se mostrará en el Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .  
  
 **Utilizar el valor de inicialización aleatorio siguiente**  
 Especifique el valor de inicialización del ejemplo para el generador de números aleatorios que utiliza la transformación para crear un ejemplo. Esto solamente se recomienda para desarrollo y pruebas. La transformación utiliza el contador de Microsoft Windows si no se especifica el valor de inicialización.  
  
  
