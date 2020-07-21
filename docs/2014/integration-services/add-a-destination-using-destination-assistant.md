---
title: Agregar un destino mediante el Asistente de destino | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 747a0de0-3c2f-4d31-a692-7111fc0911d8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cd36828a7bab7fb33b86765f9f064b6406a17a9a
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439762"
---
# <a name="add-a-destination-using-destination-assistant"></a>Agregar un destino mediante el Asistente de destinos
  En este tema se proporcionan los pasos para agregar un nuevo destino mediante el Asistente de destinos y también se muestran las opciones disponibles en el cuadro de diálogo **Agregar nuevo destino** , que verá al arrastrar y colocar el Asistente de destinos en el Diseñador SSIS.  
  
### <a name="to-use-destination-assistant-to-add-a-destination"></a>Para utilizar el Asistente de destinos para agregar un destino  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] al que desea agregar un componente de destino.  
  
2.  Arrastre el componente **Asistente de destinos** desde el cuadro de herramientas de SSIS hasta la pestaña flujo de **datos** . Debería ver el cuadro de diálogo **Agregar nuevo destino** . En la siguiente sección se proporcionan detalles sobre las opciones disponibles en el cuadro de diálogo.  
  
3.  Seleccione el tipo de destino en la lista **Tipos** .  
  
4.  Seleccione un administrador de conexiones existente en la lista **administradores de conexiones** o seleccione **\<New>** para crear un nuevo administrador de conexiones.  
  
5.  Si selecciona un administrador de conexiones existente, haga clic **Aceptar** para cerrar el cuadro de diálogo **Agregar nuevo destino** . Debería ver el destino y los administradores de conexiones agregados al flujo de datos.  
  
6.  Si hace clic **\<New>** para crear un nuevo administrador de conexiones, debería ver un cuadro de diálogo **Administrador de conexiones** , que le permite especificar los parámetros de la conexión. Después de que finalice la creación del nuevo administrador de conexiones, verá el destino y el administrador de conexiones en el Diseñador SSIS.  
  
  
