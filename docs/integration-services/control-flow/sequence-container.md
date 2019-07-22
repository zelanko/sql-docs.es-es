---
title: Contenedor de secuencias | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sequencecontainer.f1
helpviewer_keywords:
- Sequence container
- grouping control flows
- containers [Integration Services], Sequence
- subset control flow [Integration Services]
ms.assetid: 7731f91e-b8b3-4d96-a0d9-73f568547cb3
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 38f22a3e65822300eb0a585ed2339a10d7bb349f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68011332"
---
# <a name="sequence-container"></a>contenedor de secuencias

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  El contenedor de secuencias define un flujo de control que es un subconjunto del flujo de control de paquete. Los contenedores de secuencias agrupan el paquete en varios flujos de control independientes, cada uno con una o varias tareas y contenedores que se ejecutan en el flujo de control global del paquete.  
  
 El contenedor de secuencias puede incluir varias tareas, además de otros contenedores. Agregar tareas y contenedores a un contenedor de secuencias es similar a agregarlas a un paquete, salvo que se arrastran las tareas y contenedores al contenedor de secuencias en lugar de al contenedor de paquetes. Si el contenedor de secuencias incluye más de una tarea o contenedor, puede conectarlos mediante restricciones de precedencia, tal como se hace en un paquete. Para más información, consulte [Precedence Constraints](../../integration-services/control-flow/precedence-constraints.md).  
  
 El uso de un contenedor de secuencias ofrece muchas ventajas:  
  
-   Permite deshabilitar grupos de tareas para centrar la depuración en un subconjunto del flujo de control del paquete.  
  
-   Permite administrar propiedades en varias tareas de una ubicación estableciendo propiedades en un contenedor de secuencias en lugar de hacerlo en las tareas individuales.  
  
     Por ejemplo, puede establecer la propiedad **Disable** del contenedor de secuencias en **True** para deshabilitar todas las tareas y contenedores en el contenedor de secuencias.  
  
-   Proporciona un ámbito para variables usadas por un grupo de tareas y contenedores relacionados.  
  
-   Permite agrupar muchas tareas de modo que se puedan administrar más fácilmente mediante la contracción y expansión del contenedor de secuencias.  
  
     También puede crear grupos de tareas, que se expanden y contraen mediante el cuadro **Grupo** . Pero el cuadro **Grupo** es una característica de tiempo de diseño que no tiene propiedades o comportamiento de tiempo de ejecución. Para obtener más información, vea [Agrupar o desagrupar componentes](../../integration-services/group-or-ungroup-components.md)  
  
-   Permite establecer un atributo de transacción en el contenedor de secuencias para definir una transacción para un subconjunto del flujo de control del paquete. De esta manera, puede administrar las transacciones en mayor detalle.  
  
     Por ejemplo, si un contenedor de secuencias incluye dos tareas relacionadas, una tarea que elimina datos de una tabla y otra tarea que inserta datos en una tabla, puede configurar una transacción para garantizar que se revierta la acción de eliminación si la acción de inserción no se ejecuta correctamente. Para obtener más información, consulte [Transacciones de Integration Services](../../integration-services/integration-services-transactions.md).  
  
## <a name="configuration-of-the-sequence-container"></a>Configuración del contenedor de secuencias  
 El contenedor de secuencias no tiene interfaz de usuario personalizada y solo se puede configurar en la ventana **Propiedades** de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o mediante programación.  
  
 Para obtener más información sobre cómo establecer estas propiedades mediante programación, vea la documentación de la clase **T:Microsoft.SqlServer.Dts.Runtime.Sequence** en la Guía del desarrollador.  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener información sobre cómo establecer las propiedades del componente en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], vea [Establecer las propiedades de tareas o contenedores](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b).  
  
## <a name="see-also"></a>Consulte también  
 [Agregar o eliminar tareas o contenedores en un flujo de control](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [Conectar tareas y contenedores mediante una restricción de precedencia predeterminada](https://msdn.microsoft.com/library/8f31f15f-98ff-4c35-b41f-8b8cfd148d75)   
 [Contenedores de Integration Services](../../integration-services/control-flow/integration-services-containers.md)  
  
  
