---
title: Transformación Multidifusión | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.multicasttrans.f1
- sql13.dts.designer.multicasttransformation.f1
helpviewer_keywords:
- multiple outputs
- Multicast transformation
- datasets [Integration Services], multiple outputs
- multiple transformations
ms.assetid: 32194784-1684-40cd-9f91-1aba4d8360d3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6fca2fd4670fae2838eb0512c68483024bdb4dee
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "71297840"
---
# <a name="multicast-transformation"></a>Multidifusión, transformación

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La transformación Multidifusión distribuye su entrada en una o más salidas. Esta transformación es similar a la transformación División condicional. Ambas transformaciones dirigen una entrada a varias salidas. La diferencia entre las dos es que la transformación Multidifusión dirige cada fila a cada salida, mientras que la División condicional dirige una fila a una sola salida. Para más información, consulte [Conditional Split Transformation](../../../integration-services/data-flow/transformations/conditional-split-transformation.md).  
  
 Para configurar la transformación Multidifusión, debe agregar salidas.  
  
 Un paquete puede crear copias lógicas de datos mediante la transformación Multidifusión. Esta capacidad resulta útil cuando el paquete tiene que aplicar varios conjuntos de transformaciones a los mismos datos. Por ejemplo, cuando se agrega una copia de los datos y solo se carga la información de resumen en su destino, mientras otra copia de los datos se extiende con valores de búsqueda y columnas derivadas antes de cargarla en su destino.  
  
 Esta transformación tiene una entrada y varias salidas. No admite una salida de error.  
  
## <a name="configuration-of-the-multicast-transformation"></a>Configuración de la transformación Multidifusión  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener información acerca de las propiedades que puede establecer mediante programación, vea [Common Properties](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796).  
  
## <a name="related-tasks"></a>Related Tasks  
 Para más información sobre cómo establecer las propiedades de este componente, vea [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="multicast-transformation-editor"></a>Editor de trasformación Multidifusión
  Use el cuadro de diálogo **Editor de transformación Multidifusión** para ver y establecer las propiedades de cada salida de la transformación.  
  
### <a name="options"></a>Opciones  
 **Salidas**  
 Seleccione una salida de la izquierda para ver sus propiedades en la tabla de la derecha.  
  
 **Propiedades**  
 Todas las propiedades que se muestran para la salida son de solo lectura, excepto **Nombre** y **Descripción**.  
  
## <a name="see-also"></a>Consulte también  
 [Flujo de datos](../../../integration-services/data-flow/data-flow.md)   
 [Transformaciones de Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
