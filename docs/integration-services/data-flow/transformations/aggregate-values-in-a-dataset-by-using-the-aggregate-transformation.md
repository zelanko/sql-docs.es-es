---
title: Agregar valores en un conjunto de datos mediante la transformación Agregado | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Aggregate transformation [Integration Services]
- aggregate values [Integration Services]
- datasets [Integration Services], aggregate values
ms.assetid: 01b81c0f-d5e0-483b-81b2-73800a6945ac
author: janinezhang
ms.author: janinez
ms.openlocfilehash: f3e4a41f3fef4cb8b8d64de6015c5e3011490d3a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019532"
---
# <a name="aggregate-values-in-a-dataset-by-using-the-aggregate-transformation"></a>Agregar valores en un conjunto de datos mediante la transformación Agregado

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Para agregar y configurar una transformación Agregado, el paquete ya debe incluir por lo menos una tarea Flujo de datos y un origen.  
  
### <a name="to-aggregate-values-in-a-dataset"></a>Para agregar valores en un conjunto de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] que contiene el paquete que desea.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  Haga clic en la pestaña **Flujo de datos** y, a continuación, desde el **Cuadro de herramientas**, arrastre la transformación Agregado a la superficie de diseño.  
  
4.  Conecte la transformación Agregado al flujo de datos arrastrando el conector desde un origen o una transformación anterior a la transformación Agregado.  
  
5.  Haga doble clic en la transformación.  
  
6.  En el cuadro de diálogo **Editor de transformación Agregado** , haga clic en la pestaña **Agregaciones** .  
  
7.  En la lista **Columnas de entrada disponibles** , active la casilla situada junto a las columnas en las que desea agregar valores. Las columnas seleccionadas aparecen en la tabla.  
  
    > [!NOTE]  
    >  Puede seleccionar una columna muchas veces, aplicando varias transformaciones a la columna. Para identificar de manera exclusiva las agregaciones, se anexa un número al nombre predeterminado del alias de salida de la columna.  
  
8.  Opcionalmente, modifique el valor en las columnas **Alias de salida** .  
  
9. Para cambiar la operación de agregación predeterminada, **GROUP BY**, seleccione otra operación en la lista **Operación** .  
  
10. Para cambiar la comparación predeterminada, seleccione las marcas de comparación individuales enumeradas en la columna **Marcas de comparación** . De forma predeterminada, una comparación omite la distinción entre mayúsculas y minúsculas, el tipo de kana, los caracteres sin espacio y el ancho de caracteres.  
  
11. Opcionalmente, para la agregación **Count distinct** , especifique un número exacto de valores distintos en la columna **Claves Count Distinct** , o seleccione un recuento aproximado en la columna **Escala Count Distinct** .  
  
    > [!NOTE]  
    >  Al proporcionar el número de valores distintos, sea exacto o aproximado, se optimiza el rendimiento, dado que la transformación puede asignar previamente una cantidad apropiada de memoria para realizar el trabajo.  
  
12. Opcionalmente, haga clic en **Avanzado** y actualice el nombre de la salida de transformación Agregado. Si las agregaciones incluyen una operación **Group By** , puede seleccionar un recuento aproximado de los valores de las claves de agrupación en la columna **Escala de claves** , o especificar un número exacto de valores de claves de agrupación en la columna **Claves** .  
  
    > [!NOTE]  
    >  Al proporcionar el número de valores distintos, sea exacto o aproximado, se optimiza el rendimiento, dado que la transformación puede asignar previamente una cantidad apropiada de memoria para realizar el trabajo.  
  
    > [!NOTE]  
    >  Las opciones **Escala de claves** y **Claves** se excluyen mutuamente. Si escribe valores en ambas columnas, se utiliza el valor más grande en **Escala de claves** o en **Claves** .  
  
13. También puede hacer clic en la pestaña **Avanzado** y establecer los atributos que se aplican a la optimización de todas las operaciones que realiza la transformación Agregado.  
  
14. Haga clic en **Aceptar**.  
  
15. Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
## <a name="see-also"></a>Consulte también  
 [Transformación Agregado](../../../integration-services/data-flow/transformations/aggregate-transformation.md)   
 [Transformaciones de Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Rutas de Integration Services](../../../integration-services/data-flow/integration-services-paths.md)   
 [Tarea Flujo de datos](../../../integration-services/control-flow/data-flow-task.md)  
  
  
