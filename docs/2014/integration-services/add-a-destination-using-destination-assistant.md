---
title: Agregar un destino mediante el Asistente de destinos | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 747a0de0-3c2f-4d31-a692-7111fc0911d8
caps.latest.revision: 4
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 88d942ea38004d6d4085b73a4f2967a9a2e68705
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201432"
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
  
  