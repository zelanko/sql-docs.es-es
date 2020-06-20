---
title: Transformación Muestreo de fila | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.rowsamplingtrans.f1
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
ms.openlocfilehash: 38ad000eee18256ef5a6dda6b64e0e5afc7054ac
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939356"
---
# <a name="row-sampling-transformation"></a>Muestreo de fila, transformación
  La transformación Muestreo de fila se usa para obtener un subconjunto seleccionado aleatoriamente de un conjunto de datos de entrada. Puede especificar el tamaño exacto del ejemplo de salida y especificar un valor de inicialización para el generador de números aleatorios.  
  
 Hay muchas aplicaciones para el muestreo aleatorio. Por ejemplo, una compañía que desea seleccionar aleatoriamente 50 empleados que recibirán los premios de una lotería podría aplicar la transformación Muestreo de fila a la base de datos de empleados para generar el número exacto de ganadores.  
  
 La transformación Muestreo de fila también es útil durante el desarrollo de paquetes para crear un conjunto de datos pequeño pero representativo. Puede probar la ejecución del paquete y la transformación de datos con datos representativos. Tardará menos tiempo, ya que usará una muestra aleatoria en lugar del conjunto de datos completo. Como el conjunto de datos de ejemplo utilizado por el paquete de prueba tiene siempre el mismo tamaño, al usar el subconjunto de ejemplo también resulta más fácil identificar posibles problemas de rendimiento del paquete.  
  
 Esta transformación es similar a la transformación Muestreo de porcentaje, que crea un conjunto de datos de ejemplo seleccionando un porcentaje de las filas de entrada. Consulte [Percentage Sampling Transformation](percentage-sampling-transformation.md).  
  
## <a name="configuring-the-row-sampling-transformation"></a>Configurar la transformación Muestreo de fila  
 La transformación Muestreo de fila crea un conjunto de datos de ejemplo seleccionando un número especificado de las filas de entrada de la transformación. Como la selección de filas de la entrada de transformación es aleatoria, la muestra resultante es representativa de la entrada. También puede especificar el valor de inicialización que usará el generador de números aleatorios; dicho valor afectará al modo en que la transformación seleccionará filas.  
  
 Si se utiliza el mismo valor de inicialización aleatorio en la misma entrada de la transformación, siempre se creará la misma salida de ejemplo. Si no se especifica un valor de inicialización, la transformación utilizará el contador del sistema operativo para crear el número aleatorio. Por tanto, puede usar el mismo valor de inicialización durante las pruebas, para comprobar los resultados de la transformación durante el desarrollo y las pruebas del paquete, y después cambiarlo por un valor de inicialización aleatorio cuando el paquete pase a producción.  
  
 La transformación Muestreo de fila incluye la propiedad personalizada `SamplingValue`. Esta propiedad se puede actualizar a través de una expresión de propiedad, al cargar el paquete. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../expressions/integration-services-ssis-expressions.md), [Usar expresiones de propiedad en paquetes](../../expressions/use-property-expressions-in-packages.md) y [Propiedades personalizadas de transformación](transformation-custom-properties.md).  
  
 Esta transformación tiene una entrada y dos salidas. No tiene ninguna salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información sobre las propiedades que puede establecer en el cuadro de diálogo **Editor de transformación Muestreo de fila**, vea [Editor de transformación Muestreo de fila &#40;página Muestreo&#41;](../../row-sampling-transformation-editor-sampling-page.md).  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](../../common-properties.md)  
  
-   [Propiedades personalizadas de transformación](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [Establecer las propiedades de un componente de flujo de datos](../set-the-properties-of-a-data-flow-component.md)  
  
  
