---
title: "Transformación multidifusión | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.multicasttrans.f1
helpviewer_keywords:
- multiple outputs
- Multicast transformation
- datasets [Integration Services], multiple outputs
- multiple transformations
ms.assetid: 32194784-1684-40cd-9f91-1aba4d8360d3
caps.latest.revision: 45
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8619a0ed02ffc73126eb151f4a83a0b6b24c4be8
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="multicast-transformation"></a>Multidifusión, transformación
  La transformación Multidifusión distribuye su entrada en una o más salidas. Esta transformación es similar a la transformación División condicional. Ambas transformaciones dirigen una entrada a varias salidas. La diferencia entre las dos es que la transformación Multidifusión dirige cada fila a cada salida, mientras que la División condicional dirige una fila a una sola salida. Para más información, consulte [Conditional Split Transformation](../../../integration-services/data-flow/transformations/conditional-split-transformation.md).  
  
 Para configurar la transformación Multidifusión, debe agregar salidas.  
  
 Un paquete puede crear copias lógicas de datos mediante la transformación Multidifusión. Esta capacidad resulta útil cuando el paquete tiene que aplicar varios conjuntos de transformaciones a los mismos datos. Por ejemplo, cuando se agrega una copia de los datos y solo se carga la información de resumen en su destino, mientras otra copia de los datos se extiende con valores de búsqueda y columnas derivadas antes de cargarla en su destino.  
  
 Esta transformación tiene una entrada y varias salidas. No admite una salida de error.  
  
## <a name="configuration-of-the-multicast-transformation"></a>Configuración de la transformación Multidifusión  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el cuadro de diálogo **Editor de transformación Multidifusión** , vea [Multicast Transformation Editor](../../../integration-services/data-flow/transformations/multicast-transformation-editor.md).  
  
 Para obtener información acerca de las propiedades que puede establecer mediante programación, vea [Common Properties](http://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796).  
  
## <a name="related-tasks"></a>Tareas relacionadas  
 Para más información sobre cómo establecer las propiedades de este componente, vea [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Vea también  
 [Flujo de datos](../../../integration-services/data-flow/data-flow.md)   
 [Transformaciones de Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
