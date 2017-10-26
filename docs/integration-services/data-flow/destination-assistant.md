---
title: El Asistente de destinos | Documentos de Microsoft
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
- sql13.dts.designer.destinationassistant.f1
- sql13.DTS.DESIGNER.DESTINATIONASSIST.F1
ms.assetid: 10a40921-a2c2-4ac8-be28-311f8500fbf6
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: aebe1dfa1046bddfa86e48aecdd68930caf3285c
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="destination-assistant"></a>Asistente de destinos
  El componente Asistente de destinos ayuda a crear un administrador de conexiones y componentes de destino. El componente está ubicado en la sección **Favoritos** del cuadro de herramientas de SSIS.  
  
> [!NOTE]  
>  El Asistente de destinos reemplaza el proyecto de conexiones de Integration Services y el asistente correspondiente.  

## <a name="add-a-destination-with-destination-assistant"></a>Agregue un destino con el Asistente de destino
En este tema se proporcionan los pasos para agregar un nuevo destino mediante el Asistente de destinos y también se muestran las opciones disponibles en el cuadro de diálogo **Agregar nuevo destino** , que verá al arrastrar y colocar el Asistente de destinos en el Diseñador SSIS.  

1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] al que desea agregar un componente de destino.  
  
2.  Arrastre el componente **Asistente de destinos** desde el cuadro de herramientas de SSIS hasta la pestaña **Flujo de datos** . Debe ver el cuadro de diálogo **Agregar nuevo destino** . En la siguiente sección se proporcionan detalles sobre las opciones disponibles en el cuadro de diálogo.  
  
3.  Seleccione el tipo de destino en la lista **Tipos** .  
  
4.  Seleccione un administrador de conexiones existente en el **administradores de conexión** lista o seleccione  **\<nuevo >** para crear una nueva conexión de administrador.  
  
5.  Si selecciona un administrador de conexiones existente, haga clic **Aceptar** para cerrar el cuadro de diálogo **Agregar nuevo destino** . Debería ver el destino y los administradores de conexiones agregados al flujo de datos.  
  
6.  Si hace clic en  **\<nuevo >** para crear una nueva conexión de administrador, debería ver un **Connection Manager** cuadro de diálogo que le permite especificar parámetros para la conexión. Después de que finalice la creación del nuevo administrador de conexiones, verá el destino y el administrador de conexiones en el Diseñador SSIS. 
  
## <a name="add-new-destination-dialog-box"></a>Agregar cuadro de diálogo nuevo destino
En la tabla siguiente se enumera las opciones disponibles en la **Agregar nuevo destino** cuadro de diálogo.  
  
|Opción|Description|  
|------------|-----------------|  
|Tipos|Seleccione el tipo de destino al que desea conectarse.|  
|Administradores de conexión|Seleccione un administrador de conexiones existente o haga clic en  **\<nuevo >** para crear una nueva conexión de administrador.|  
|Mostrar solo elementos instalados|Especifique si desea ver solo los destinos instalados.|  
|Aceptar|Haga clic para guardar los cambios y a abrir los cuadros de diálogo siguientes para configurar opciones adicionales.|  

