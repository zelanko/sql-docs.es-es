---
title: Transformación Multidifusión | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.multicasttrans.f1
helpviewer_keywords:
- multiple outputs
- Multicast transformation
- datasets [Integration Services], multiple outputs
- multiple transformations
ms.assetid: 32194784-1684-40cd-9f91-1aba4d8360d3
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7b5c0a38c966c89f426a213f302b45c390b77cfe
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437612"
---
# <a name="multicast-transformation"></a>Multidifusión, transformación
  La transformación Multidifusión distribuye su entrada en una o más salidas. Esta transformación es similar a la transformación División condicional. Ambas transformaciones dirigen una entrada a varias salidas. La diferencia entre las dos es que la transformación Multidifusión dirige cada fila a cada salida, mientras que la División condicional dirige una fila a una sola salida. Para más información, consulte [Conditional Split Transformation](conditional-split-transformation.md).  
  
 Para configurar la transformación Multidifusión, debe agregar salidas.  
  
 Un paquete puede crear copias lógicas de datos mediante la transformación Multidifusión. Esta capacidad resulta útil cuando el paquete tiene que aplicar varios conjuntos de transformaciones a los mismos datos. Por ejemplo, cuando se agrega una copia de los datos y solo se carga la información de resumen en su destino, mientras otra copia de los datos se extiende con valores de búsqueda y columnas derivadas antes de cargarla en su destino.  
  
 Esta transformación tiene una entrada y varias salidas. No admite una salida de error.  
  
## <a name="configuration-of-the-multicast-transformation"></a>Configuración de la transformación Multidifusión  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información acerca de las propiedades que puede establecer en el cuadro de diálogo **Editor de transformación Multidifusión** , vea [Multicast Transformation Editor](../../multicast-transformation-editor.md).  
  
 Para obtener información acerca de las propiedades que puede establecer mediante programación, vea [Common Properties](../../common-properties.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 Para más información sobre cómo establecer las propiedades de este componente, vea [Establecer las propiedades de un componente de flujo de datos](../set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Consulte también  
 [Flujo de datos](../data-flow.md)   
 [Transformaciones de Integration Services](integration-services-transformations.md)  
  
  
