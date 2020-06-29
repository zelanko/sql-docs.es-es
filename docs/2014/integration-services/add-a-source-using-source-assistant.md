---
title: Agregar un origen mediante el Asistente de orígenes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5e850b7c-4b89-42ad-b0a6-d63ac7cc9568
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1b58b10508765580e0cffe9bd62099f3e2d69863
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439732"
---
# <a name="add-a-source-using-source-assistant"></a>Agregar un origen mediante el Asistente de orígenes
  En este tema se proporcionan los pasos para agregar un nuevo origen con el Asistente de orígenes y también se muestran las opciones disponibles en el cuadro de diálogo **Agregar nuevo origen** , que verá al arrastrar y colocar el Asistente de orígenes al Diseñador SSIS.  
  
### <a name="to-use-source-assistant-to-add-a-source"></a>Para utilizar el Asistente de orígenes para agregar un origen  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] al que desea agregar un componente de origen.  
  
2.  Arrastre el componente **Asistente de orígenes** desde el cuadro de herramientas de SSIS hasta la pestaña flujo de **datos** . Debería ver el cuadro de diálogo **Agregar nuevo origen** . En la siguiente sección se proporcionan detalles sobre las opciones disponibles en el cuadro de diálogo.  
  
3.  Seleccione el tipo de destino en la lista **Tipos** .  
  
4.  Seleccione un administrador de conexiones existente en la lista **administradores de conexiones** o seleccione **\<New>** para crear un nuevo administrador de conexiones.  
  
5.  Si selecciona un administrador de conexiones existente, haga clic **Aceptar** para cerrar el cuadro de diálogo **Agregar nuevo destino** . Debería ver el destino y los administradores de conexiones agregados al flujo de datos.  
  
6.  Si hace clic **\<New>** para crear un nuevo administrador de conexiones, debería ver un cuadro de diálogo **Administrador de conexiones** , que le permite especificar los parámetros de la conexión. Después de que finalice la creación del nuevo administrador de conexiones, verá el destino y el administrador de conexiones en el Diseñador SSIS.  
  
  
