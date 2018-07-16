---
title: Agregar un destino mediante el Asistente de destinos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 747a0de0-3c2f-4d31-a692-7111fc0911d8
caps.latest.revision: 4
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5251cd85dd24de18e582875c0a6c0100ae3fffcc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37246785"
---
# <a name="add-a-destination-using-destination-assistant"></a>Agregar un destino mediante el Asistente de destinos
  En este tema se proporcionan los pasos para agregar un nuevo destino mediante el Asistente de destinos y también se muestran las opciones disponibles en el cuadro de diálogo **Agregar nuevo destino**, que verá al arrastrar y colocar el Asistente de destinos en el Diseñador SSIS.  
  
### <a name="to-use-destination-assistant-to-add-a-destination"></a>Para utilizar el Asistente de destinos para agregar un destino  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] al que desea agregar un componente de destino.  
  
2.  Arrastre el componente **Asistente de destinos** desde el cuadro de herramientas de SSIS hasta la pestaña **Flujo de datos** . Debe ver el cuadro de diálogo **Agregar nuevo destino** . En la siguiente sección se proporcionan detalles sobre las opciones disponibles en el cuadro de diálogo.  
  
3.  Seleccione el tipo de destino en la lista **Tipos** .  
  
4.  Seleccione un administrador de conexiones existente en la lista **Administradores de conexiones** o seleccione **\<Nuevo>** para crear un administrador de conexiones.  
  
5.  Si selecciona un administrador de conexiones existente, haga clic **Aceptar** para cerrar el cuadro de diálogo **Agregar nuevo destino** . Debería ver el destino y los administradores de conexiones agregados al flujo de datos.  
  
6.  Si hace clic en **\<Nuevo>** para crear un administrador de conexiones, verá el cuadro de diálogo **Administrador de conexiones**, que permite especificar los parámetros de la conexión. Después de que finalice la creación del nuevo administrador de conexiones, verá el destino y el administrador de conexiones en el Diseñador SSIS.  
  
  
