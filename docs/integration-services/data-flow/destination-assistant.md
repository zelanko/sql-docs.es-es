---
title: Asistente de destinos | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.destinationassistant.f1
- sql13.DTS.DESIGNER.DESTINATIONASSIST.F1
ms.assetid: 10a40921-a2c2-4ac8-be28-311f8500fbf6
caps.latest.revision: "13"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 21ce9dc332f5a31fa95ea57e5cbe63a2757f198a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="destination-assistant"></a>Asistente de destinos
  El componente Asistente de destinos ayuda a crear un administrador de conexiones y componentes de destino. El componente está ubicado en la sección **Favoritos** del cuadro de herramientas de SSIS.  
  
> [!NOTE]  
>  El Asistente de destinos reemplaza el proyecto de conexiones de Integration Services y el asistente correspondiente.  

## <a name="add-a-destination-with-destination-assistant"></a>Agregar un destino mediante el Asistente de destinos
En este tema se proporcionan los pasos para agregar un nuevo destino mediante el Asistente de destinos y también se muestran las opciones disponibles en el cuadro de diálogo **Agregar nuevo destino** , que verá al arrastrar y colocar el Asistente de destinos en el Diseñador SSIS.  

1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] al que desea agregar un componente de destino.  
  
2.  Arrastre el componente **Asistente de destinos** desde el cuadro de herramientas de SSIS hasta la pestaña **Flujo de datos** . Debe ver el cuadro de diálogo **Agregar nuevo destino** . En la siguiente sección se proporcionan detalles sobre las opciones disponibles en el cuadro de diálogo.  
  
3.  Seleccione el tipo de destino en la lista **Tipos** .  
  
4.  Seleccione un administrador de conexiones existente en la lista **Administradores de conexiones** o seleccione **\<Nuevo>** para crear un administrador de conexiones.  
  
5.  Si selecciona un administrador de conexiones existente, haga clic **Aceptar** para cerrar el cuadro de diálogo **Agregar nuevo destino** . Debería ver el destino y los administradores de conexiones agregados al flujo de datos.  
  
6.  Si hace clic en **\<Nuevo>** para crear un administrador de conexiones, verá el cuadro de diálogo **Administrador de conexiones**, que permite especificar los parámetros de la conexión. Después de que finalice la creación del nuevo administrador de conexiones, verá el destino y el administrador de conexiones en el Diseñador SSIS. 
  
## <a name="add-new-destination-dialog-box"></a>Cuadro de diálogo Agregar nuevo destino
En la tabla siguiente se enumeran las opciones disponibles en el cuadro de diálogo **Agregar nuevo destino**.  
  
|Opción|Description|  
|------------|-----------------|  
|Tipos|Seleccione el tipo de destino al que desea conectarse.|  
|Administradores de conexión|Seleccione un administrador de conexiones existente o haga clic en **\<Nuevo>** para crear uno.|  
|Mostrar solo elementos instalados|Especifique si desea ver solo los destinos instalados.|  
|Aceptar|Haga clic para guardar los cambios y a abrir los cuadros de diálogo siguientes para configurar opciones adicionales.|  
