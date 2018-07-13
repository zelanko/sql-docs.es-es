---
title: Eventos registrados por el servicio Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- service [Integration Services], events
- events [Integration Services], service
- Integration Services service, events
ms.assetid: d4122dcf-f16f-47a0-93a2-ffa3d0d4f9cf
caps.latest.revision: 18
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7a784b1ae955d66db9cccae24b6ccaa543fa9597
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37164856"
---
# <a name="events-logged-by-the-integration-services-service"></a>Eventos registrados por el servicio Integration Services
  El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] registra diversos mensajes en el registro de eventos de aplicación de Windows. El servicio registra estos mensajes cuando el servicio se inicia, cuando se detiene y cuando se producen ciertos problemas.  
  
 Este tema proporciona información sobre los mensajes de eventos comunes que el servicio registra en el registro de eventos de aplicación. El servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] registra todos los mensajes descritos en este tema con un origen del evento de SQLISService.  
  
 Para obtener información general sobre el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vea [Servicio Integration Services &#40;servicio SSIS&#41;](integration-services-service-ssis-service.md).  
  
## <a name="messages-about-the-status-of-the-service"></a>Mensajes sobre el estado del servicio  
 Cuando selecciona [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para la instalación, el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se instala y se inicia, y el tipo de inicio del servicio se establece como automático.  
  
|Identificador del evento|Nombre simbólico|Texto|Notas|  
|--------------|-------------------|----------|-----------|  
|256|DTS_MSG_SERVER_STARTING|Iniciando el Servicio [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] .|El servicio está a punto de iniciarse.|  
|257|DTS_MSG_SERVER_STARTED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] Se ha iniciado el servicio  de.|El servicio se ha iniciado.|  
|260|DTS_MSG_SERVER_START_FAILED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] .%nError:%1|El servicio no se ha podido iniciar. Esta imposibilidad de iniciarse puede deberse a una instalación dañada o a una cuenta de servicio inapropiada.|  
|258|DTS_MSG_SERVER_STOPPING|Deteniendo el servicio [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] .%n%nDetener todos los paquetes en ejecución al salir:%1|El servicio se está deteniendo, y si se configura el servicio para ello, detendrá todos los paquetes en ejecución. Puede establecer un valor de verdadero o falso en el archivo de configuración que determina si el servicio detiene los paquetes en ejecución cuando el propio servicio se detiene. El mensaje para este evento incluye el valor de esta configuración.|  
|259|DTS_MSG_SERVER_STOPPED|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] .%nVersión de servidor %1|El servicio se ha detenido.|  
  
## <a name="messages-about-the-configuration-file"></a>Mensajes sobre el archivo de configuración  
 La configuración para el servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se almacena en un archivo XML que se puede modificar. Para obtener más información, vea [Configurar el servicio Integration Services &#40;servicio SSIS&#41;](../configuring-the-integration-services-service-ssis-service.md).  
  
|Identificador del evento|Nombre simbólico|Texto|Notas|  
|--------------|-------------------|----------|-----------|  
|274|DTS_MSG_SERVER_MISSING_CONFIG_REG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] : %nLa configuración del Registro que especifica el archivo de configuración no existe. %nIntentando cargar el archivo de configuración.|La entrada del Registro que contiene la ruta de acceso del archivo de configuración no existe o esta vacía.|  
|272|DTS_MSG_SERVER_MISSING_CONFIG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] no existe.%nCargando la configuración predeterminada.|El archivo de configuración no existe en la ubicación especificada.|  
|273|DTS_MSG_SERVER_BAD_CONFIG|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] es incorrecto.%nError al leer el archivo de configuración: %1%n%nCargando el servidor con la configuración predeterminada.|El archivo de configuración no se puede leer o no es válido. Este error puede ser el resultado de un error de sintaxis XML en el archivo.|  
  
## <a name="other-messages"></a>Otros mensajes  
  
|Identificador del evento|Nombre simbólico|Texto|Notas|  
|--------------|-------------------|----------|-----------|  
|336|DTS_MSG_SERVER_STOPPING_PACKAGE|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] deteniendo el paquete en ejecución.%nId. de instancia del paquete: %1%nId. del paquete: %2%nNombre del paquete: %3%nDescripción del paquete: %4%nPaquete iniciado por: %5.|El servicio está intentando detener un paquete en ejecución. Puede supervisar y detener los paquetes en ejecución en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para obtener información sobre cómo administrar paquetes en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], vea [Administración de paquetes &#40;servicio SSIS&#41;](package-management-ssis-service.md).|  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener información sobre cómo ver las entradas de registro, vea [Ver entradas del registro en la ventana Registrar eventos](../view-log-entries-in-the-log-events-window.md).  
  
## <a name="see-also"></a>Vea también  
 [Eventos registrados por un paquete de Integration Services](../performance/events-logged-by-an-integration-services-package.md)  
  
  
