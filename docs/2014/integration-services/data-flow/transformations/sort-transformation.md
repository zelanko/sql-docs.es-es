---
title: Transformación Ordenar | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sorttrans.f1
helpviewer_keywords:
- Sort transformation
- descending sorts
- ascending sorts
- sorting data [Integration Services]
- multiple sorts
- duplicate data [Integration Services]
ms.assetid: 728c9351-84a8-4a89-be4d-d50d4adc04e0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: dba1f3598abb8877721ff77d3dabcc8af8e0b94a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62899902"
---
# <a name="sort-transformation"></a>Ordenar, transformación
  La transformación Ordenar ordena los datos de entrada en sentido ascendente o descendente, y copia los datos ordenados a la salida de transformación. Puede aplicar varias ordenaciones a una entrada; cada ordenación se identifica mediante un numeral que determina el criterio de ordenación. La columna con el número más bajo se ordenará primero, la columna con el segundo número más bajo se ordena a continuación, etc. Por ejemplo, si una columna denominada **CountryRegion** tiene un criterio de ordenación 1 y una columna denominada **Ciudad** tiene un criterio de ordenación 2, la salida se ordena por país o región y después por ciudad. Un número positivo indica que la ordenación es ascendente y un número negativo indica que la ordenación es descendente. Las columnas que no se están ordenadas tienen un criterio de ordenación de 0. Las columnas que no están seleccionadas para ordenar se copian automáticamente a la salida de transformación junto con las columnas ordenadas.  
  
 La transformación Ordenar incluye un conjunto de opciones de comparación para definir cómo controlará la transformación los datos de cadena de una columna. Para más información, consulte [Comparing String Data](../comparing-string-data.md).  
  
> [!NOTE]  
>  La transformación Ordenar no ordena los GUID en el mismo orden que la cláusula ORDER BY lo hace en Transact-SQL. Mientras que la transformación Ordenar ordena los GUID que se inician con 0-9 antes que los que se inician con A-F, la cláusula ORDER BY, tal y como se implementa en [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)], los ordena de otra manera. Para obtener más información, vea [ORDER BY &#40;cláusula de Transact-SQL&#41;](/sql/t-sql/queries/select-order-by-clause-transact-sql).  
  
 La transformación Ordenar también puede quitar filas duplicadas como parte de la ordenación. Las filas duplicadas son filas con los mismos criterios de ordenación. El valor del criterio de ordenación se genera a partir de las opciones de comparación de cadenas usadas, lo que implica que cadenas literales diferentes pueden tener los mismos criterios de ordenación. La transformación identifica filas en las columnas de entrada que tienen valores distintos pero un mismo criterio de ordenación que los duplicados.  
  
 La transformación Ordenar incluye la propiedad personalizada `MaximumThreads`, que se puede actualizar a través de una expresión de propiedad al cargar el paquete. Para más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../expressions/integration-services-ssis-expressions.md), [Usar expresiones de propiedad en paquetes](../../expressions/use-property-expressions-in-packages.md) y [Propiedades personalizadas de transformación](transformation-custom-properties.md).  
  
 Esta transformación tiene una entrada y una salida. No admite salidas de error.  
  
## <a name="configuration-of-the-sort-transformation"></a>Configuración de la transformación Ordenar  
 Puede establecer propiedades a través del Diseñador [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener información acerca de las propiedades que puede establecer en el cuadro de diálogo **Editor de transformación Ordenar** , vea [Sort Transformation Editor](../../sort-transformation-editor.md).  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](../../common-properties.md)  
  
-   [Propiedades personalizadas de transformación](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener más información sobre cómo establecer las propiedades del componente, vea [Establecer las propiedades de un componente de flujo de datos](../set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-content"></a>Contenido relacionado  
 Ejemplo, [SortDeDuplicateDelimitedString Custom SSIS Component](https://go.microsoft.com/fwlink/?LinkId=220821), en codeplex.com.  
  
## <a name="see-also"></a>Consulte también  
 [Flujo de datos](../data-flow.md)   
 [Transformaciones de Integration Services](integration-services-transformations.md)  
  
  
