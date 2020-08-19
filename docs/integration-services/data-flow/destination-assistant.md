---
description: Asistente de destinos
title: Asistente de destinos | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.destinationassistant.f1
- sql13.DTS.DESIGNER.DESTINATIONASSIST.F1
ms.assetid: 10a40921-a2c2-4ac8-be28-311f8500fbf6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b47670e1830b7689231cdc87752ce6222faef5b3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425837"
---
# <a name="destination-assistant"></a>Asistente de destinos

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  El componente Asistente de destinos ayuda a crear un administrador de conexiones y componentes de destino. El componente está ubicado en la sección **Favoritos** del cuadro de herramientas de SSIS.  
  
> [!NOTE]  
>  El Asistente de destinos reemplaza el proyecto de conexiones de Integration Services y el asistente correspondiente.  

## <a name="add-a-destination-with-destination-assistant"></a>Agregar un destino mediante el Asistente de destinos
En este tema se proporcionan los pasos para agregar un nuevo destino mediante el Asistente de destinos y también se muestran las opciones disponibles en el cuadro de diálogo **Agregar nuevo destino** , que verá al arrastrar y colocar el Asistente de destinos en el Diseñador SSIS.  

1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] al que desea agregar un componente de destino.  
  
2.  Arrastre el componente **Asistente de destinos** desde el cuadro de herramientas de SSIS hasta la pestaña **Flujo de datos** . Debe ver el cuadro de diálogo **Agregar nuevo destino** . En la siguiente sección se proporcionan detalles sobre las opciones disponibles en el cuadro de diálogo.  
  
3.  Seleccione el tipo de destino en la lista **Tipos** .  
  
4.  Seleccione un administrador de conexiones existente en la lista **Administradores de conexiones** o seleccione **\<New>** para crear uno.  
  
5.  Si selecciona un administrador de conexiones existente, haga clic **Aceptar** para cerrar el cuadro de diálogo **Agregar nuevo destino** . Debería ver el destino y los administradores de conexiones agregados al flujo de datos.  
  
6.  Si hace clic en **\<New>** para crear un nuevo administrador de conexiones, aparecerá el cuadro de diálogo **Administrador de conexión**, que permite especificar parámetros para la conexión. Después de que finalice la creación del nuevo administrador de conexiones, verá el destino y el administrador de conexiones en el Diseñador SSIS. 
  
## <a name="add-new-destination-dialog-box"></a>Cuadro de diálogo Agregar nuevo destino
En la tabla siguiente se enumeran las opciones disponibles en el cuadro de diálogo **Agregar nuevo destino**.  
  
|Opción|Descripción|  
|------------|-----------------|  
|Tipos|Seleccione el tipo de destino al que desea conectarse.|  
|Administradores de conexión|Seleccione un administrador de conexiones existente o haga clic en **\<New>** para crear uno.|  
|Mostrar solo elementos instalados|Especifique si desea ver solo los destinos instalados.|  
|Aceptar|Haga clic para guardar los cambios y a abrir los cuadros de diálogo siguientes para configurar opciones adicionales.|  
