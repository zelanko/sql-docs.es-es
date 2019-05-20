---
title: Asistente de orígenes | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sourceassistant.f1
- sql13.dts.designer.addNewSource.f1
ms.assetid: 5ca9d821-7d61-4727-9133-5f9cb485c7f3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 93bbfcc8b76fe6fe1028b5b13395e0a88a6b359a
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65726362"
---
# <a name="source-assistant"></a>Asistente de orígenes

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  El componente Asistente de orígenes ayuda a crear un componente de origen y un administrador de conexiones. El componente está ubicado en la sección **Favoritos** del cuadro de herramientas de SSIS.  
  
> [!NOTE]  
>  El Asistente de orígenes reemplaza el proyecto de conexiones de Integration Services y el asistente correspondiente.  
  
## <a name="add-a-source-with-source-assistant"></a>Agregar un origen con Asistente de orígenes
En esta sección se proporcionan los pasos para agregar un nuevo origen con el Asistente de orígenes y también se muestran las opciones disponibles en el cuadro de diálogo **Agregar nuevo origen**, que verá al arrastrar y colocar el Asistente de orígenes en el Diseñador SSIS.  

1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] al que desea agregar un componente de origen.  
  
2.  Arrastre el componente **Asistente de orígenes** desde el cuadro de herramientas de SSIS hasta la pestaña **Flujo de datos** . Debe ver el cuadro de diálogo **Agregar nuevo origen** . En la siguiente sección se proporcionan detalles sobre las opciones disponibles en el cuadro de diálogo.  
  
3.  Seleccione el tipo de destino en la lista **Tipos** .  
  
4.  Seleccione un administrador de conexiones existente en la lista **Administradores de conexiones** o seleccione **\<Nuevo>** para crear un administrador de conexiones.  
  
5.  Si selecciona un administrador de conexiones existente, haga clic **Aceptar** para cerrar el cuadro de diálogo **Agregar nuevo destino** . Debería ver el destino y los administradores de conexiones agregados al flujo de datos.  
  
6.  Si hace clic en **\<Nuevo>** para crear un administrador de conexiones, verá el cuadro de diálogo **Administrador de conexiones**, que permite especificar los parámetros de la conexión. Después de que finalice la creación del nuevo administrador de conexiones, verá el destino y el administrador de conexiones en el Diseñador SSIS.  

## <a name="add-new-source-dialog-box"></a>Cuadro de diálogo Agregar nuevo origen
En la tabla siguiente se enumeran las opciones disponibles en el cuadro de diálogo **Agregar nuevo origen**.  
  
|Opción|Descripción|  
|------------|-----------------|  
|Tipos|Seleccione el tipo de origen al que desea conectarse.|  
|Administradores de conexión|Seleccione un administrador de conexiones existente o haga clic en **\<Nuevo>** para crear uno.|  
|Mostrar solo elementos instalados|Especifique si desea ver solo los orígenes instalados.|  
|Aceptar|Haga clic para guardar los cambios y a abrir los cuadros de diálogo siguientes para configurar opciones adicionales.| 
  
