---
title: Transformación Recuento de filas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.rowcounttrans.f1
helpviewer_keywords:
- updating variables
- Row Count transformation
- number of rows
- variables [Integration Services], updating
- counting rows
ms.assetid: b68293b9-a68c-40be-9d81-77342da1be29
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4db63681f489b0f375846272b7093545eb8fefa6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65725930"
---
# <a name="row-count-transformation"></a>Recuento de filas, transformación

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La transformación Recuento de filas cuenta las filas a medida que pasan por un flujo de datos y almacena el recuento final en una variable.  
  
 A [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] puede usar recuentos de filas para actualizar las variables utilizadas en scripts, expresiones y expresiones de propiedades. (Por ejemplo, la variable que almacena el número de filas puede actualizar el texto de un mensaje de correo electrónico para incluir el número de filas). La variable que se va a utilizar en la transformación Recuento de filas debe existir ya y debe estar dentro del ámbito de la tarea Flujo de datos a la que pertenece el flujo de datos con la transformación Recuento de filas.  
  
 La transformación almacena el valor del recuento de filas en la variable únicamente después de que la última fila ya ha pasado a través de ella. Por lo tanto, el valor de la variable no está actualizado en el momento en que el valor actualizado se va a usar en el flujo de datos que contiene la transformación Recuento de filas. Puede usar la variable actualizada en un flujo de datos independiente.  
  
 Esta transformación tiene una entrada y una salida. No admite una salida de error.  
  
## <a name="configuration-of-the-row-count-transformation"></a>Configuración de la transformación Recuento de filas  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o mediante programación.  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Propiedades personalizadas de transformación](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener más información sobre cómo establecer las propiedades de este componente, vea [Establecer las propiedades de un componente de flujo de datos](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Consulte también  
 [Variables de Integration Services &#40;SSIS&#41;](../../../integration-services/integration-services-ssis-variables.md)   
 [Flujo de datos](../../../integration-services/data-flow/data-flow.md)   
 [Transformaciones de Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
