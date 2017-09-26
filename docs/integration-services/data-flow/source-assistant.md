---
title: Asistente de origen | Documentos de Microsoft
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
- sql13.dts.designer.sourceassistant.f1
- sql13.dts.designer.addNewSource.f1
ms.assetid: 5ca9d821-7d61-4727-9133-5f9cb485c7f3
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 9b7406edf9f7234db739730473772d77c42399ec
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="source-assistant"></a>Asistente de orígenes
  El componente Asistente de orígenes ayuda a crear un componente de origen y un administrador de conexiones. El componente está ubicado en la sección **Favoritos** del cuadro de herramientas de SSIS.  
  
> [!NOTE]  
>  El Asistente de orígenes reemplaza el proyecto de conexiones de Integration Services y el asistente correspondiente.  
  
## <a name="add-a-source-with-source-assistant"></a>Agregar un origen con el Asistente de origen
En esta sección se explica cómo agregar un nuevo origen mediante el Asistente de origen y también se enumeran las opciones que están disponibles en la **Agregar nuevo origen de** cuadro de diálogo, que verá al arrastrar y colocar el Asistente de origen en el Diseñador SSIS.  

1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] al que desea agregar un componente de origen.  
  
2.  Arrastre el componente **Asistente de orígenes** desde el cuadro de herramientas de SSIS hasta la pestaña **Flujo de datos** . Debe ver el cuadro de diálogo **Agregar nuevo origen** . En la siguiente sección se proporcionan detalles sobre las opciones disponibles en el cuadro de diálogo.  
  
3.  Seleccione el tipo de destino en la lista **Tipos** .  
  
4.  Seleccione un administrador de conexiones existente en el **administradores de conexión** lista o seleccione ** \<nuevo >** para crear una nueva conexión de administrador.  
  
5.  Si selecciona un administrador de conexiones existente, haga clic **Aceptar** para cerrar el cuadro de diálogo **Agregar nuevo destino** . Debería ver el destino y los administradores de conexiones agregados al flujo de datos.  
  
6.  Si hace clic en ** \<nuevo >** para crear una nueva conexión de administrador, debería ver un **Connection Manager** cuadro de diálogo que le permite especificar parámetros para la conexión. Después de que finalice la creación del nuevo administrador de conexiones, verá el destino y el administrador de conexiones en el Diseñador SSIS.  

## <a name="add-new-source-dialog-box"></a>Agregar cuadro de diálogo nuevo origen
En la tabla siguiente se enumera opciones disponibles en la **Agregar nuevo origen de** cuadro de diálogo.  
  
|Opción|Description|  
|------------|-----------------|  
|Tipos|Seleccione el tipo de origen al que desea conectarse.|  
|Administradores de conexión|Seleccione un administrador de conexiones existente o haga clic en ** \<nuevo >** para crear una nueva conexión de administrador.|  
|Mostrar solo elementos instalados|Especifique si desea ver solo los orígenes instalados.|  
|Aceptar|Haga clic para guardar los cambios y a abrir los cuadros de diálogo siguientes para configurar opciones adicionales.| 
  
