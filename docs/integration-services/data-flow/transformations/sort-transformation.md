---
title: Transformación Ordenar | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sorttrans.f1
- sql13.dts.designer.sorttransformation.f1
helpviewer_keywords:
- Sort transformation
- descending sorts
- ascending sorts
- sorting data [Integration Services]
- multiple sorts
- duplicate data [Integration Services]
ms.assetid: 728c9351-84a8-4a89-be4d-d50d4adc04e0
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bfcf99a28a847097d943495c205d7d894bb388ea
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47658473"
---
# <a name="sort-transformation"></a>Ordenar, transformación
  La transformación Ordenar ordena los datos de entrada en sentido ascendente o descendente, y copia los datos ordenados a la salida de transformación. Puede aplicar varias ordenaciones a una entrada; cada ordenación se identifica mediante un numeral que determina el criterio de ordenación. La columna con el número más bajo se ordenará primero, la columna con el segundo número más bajo se ordena a continuación, etc. Por ejemplo, si una columna denominada **CountryRegion** tiene un criterio de ordenación 1 y una columna denominada **Ciudad** tiene un criterio de ordenación 2, la salida se ordena por país o región y después por ciudad. Un número positivo indica que la ordenación es ascendente y un número negativo indica que la ordenación es descendente. Las columnas que no se están ordenadas tienen un criterio de ordenación de 0. Las columnas que no están seleccionadas para ordenar se copian automáticamente a la salida de transformación junto con las columnas ordenadas.  
  
 La transformación Ordenar incluye un conjunto de opciones de comparación para definir cómo controlará la transformación los datos de cadena de una columna. Para más información, consulte [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).  
  
> [!NOTE]  
>  La transformación Ordenar no ordena los GUID en el mismo orden que la cláusula ORDER BY lo hace en Transact-SQL. Mientras que la transformación Ordenar ordena los GUID que se inician con 0-9 antes que los que se inician con A-F, la cláusula ORDER BY, tal y como se implementa en [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)], los ordena de otra manera. Para obtener más información, vea [ORDER BY &#40;cláusula de Transact-SQL&#41;](../../../t-sql/queries/select-order-by-clause-transact-sql.md).  
  
 La transformación Ordenar también puede quitar filas duplicadas como parte de la ordenación. Las filas duplicadas son filas con los mismos criterios de ordenación. El valor del criterio de ordenación se genera a partir de las opciones de comparación de cadenas usadas, lo que implica que cadenas literales diferentes pueden tener los mismos criterios de ordenación. La transformación identifica filas en las columnas de entrada que tienen valores distintos pero un mismo criterio de ordenación que los duplicados.  
  
 La transformación Ordenar incluye la propiedad personalizada **MaximumThreads** , que se puede actualizar a través de una expresión de propiedad al cargar el paquete. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Usar expresiones de propiedad en paquetes](../../../integration-services/expressions/use-property-expressions-in-packages.md) y [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Esta transformación tiene una entrada y una salida. No admite salidas de error.  
  
## <a name="configuration-of-the-sort-transformation"></a>Configuración de la transformación Ordenar  
 Puede establecer propiedades a través del Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener más información sobre cómo establecer las propiedades del componente, vea [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-content"></a>Contenido relacionado  
 Ejemplo, [SortDeDuplicateDelimitedString Custom SSIS Component](http://go.microsoft.com/fwlink/?LinkId=220821), en codeplex.com.  
  
## <a name="sort-transformation-editor"></a>Editor de transformación Ordenar
  Use el cuadro de diálogo **Editor de transformación Ordenar** para seleccionar las columnas que desea ordenar, establecer el orden y especificar si deben quitarse los duplicados.  
  
### <a name="options"></a>Opciones  
 **Columnas de entrada disponibles**  
 Active las casillas de las columnas que desea ordenar.  
  
 **Nombre**  
 Muestra el nombre de todas las columnas de entrada disponibles.  
  
 **Paso a través**  
 Permite indicar si la columna debe incluirse en la salida ordenada.  
  
 **Columna de entrada**  
 Seleccione de la lista de entradas disponibles las columnas para cada fila. Las selecciones se reflejan en las casillas activadas en la tabla **Columnas de entrada disponibles** .  
  
 **Alias de salida**  
 Escriba un alias para cada columna de salida. El nombre predeterminado es el de la columna de entrada, pero puede elegir cualquier nombre descriptivo único.  
  
 **Tipo de orden**  
 Permite indicar si la ordenación seguirá un orden ascendente o descendente.  
  
 **Criterio de ordenación**  
 Permite indicar el orden en que deben ordenarse las columnas. Esta característica debe establecerse manualmente para cada columna.  
  
 **Marcas de comparación**  
 Para más información sobre las opciones de comparación de cadenas, vea [Comparar datos de cadena](../../../integration-services/data-flow/comparing-string-data.md).  
  
 **Quitar filas con valores de ordenación duplicados**  
 Permite indicar si la transformación copia filas duplicadas en la salida o crea una única entrada para todos los duplicados utilizando las opciones de comparación de cadenas especificadas.  
  
## <a name="see-also"></a>Ver también  
 [Flujo de datos](../../../integration-services/data-flow/data-flow.md)   
 [Transformaciones de Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
