---
title: Editor de origen de SAP BW (página Administrador de conexiones) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sapbwsource.connection.f1
ms.assetid: 2a6dc531-85ca-43c5-a65f-3ad3f7d537c4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 52972f7b21a9eb7ff2fa0059e8d52848e8cc9ab4
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86917849"
---
# <a name="sap-bw-source-editor-connection-manager-page"></a>Editor de origen de SAP BW (página Administrador de conexiones)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Use la página **Administrador de conexiones** del cuadro de diálogo **Editor de origen de SAP BW** para seleccionar el administrador de conexiones de SAP BW para el origen de SAP BW. En esta página, puede seleccionar el modo de ejecución y los parámetros para extraer los datos del sistema SAP Netweaver BW.  
  
 Para obtener más información sobre el componente de origen de SAP BW de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW, vea [Origen de SAP BW](../../integration-services/data-flow/sap-bw-source.md).  
  
> [!IMPORTANT]  
>  La documentación de Microsoft Connector 1.1 for SAP BW da por supuesto que se está familiarizado con el entorno SAP Netweaver BW. Para obtener más información acerca de SAP Netweaver BW, o sobre cómo configurar los objetos y los procesos de SAP Netweaver BW, vea la documentación de SAP.  
  
> [!IMPORTANT]  
>  La extracción de datos de SAP Netweaver BW requiere una licencia SAP adicional. Póngase en contacto con SAP para comprobar estos requisitos.  
  
 **Para abrir la página Administrador de conexiones**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el origen de SAP BW.  
  
2.  En la pestaña **Flujo de datos** , haga doble clic en el origen de SAP BW.  
  
3.  En **Editor de origen de SAP BW**, haga clic en **Administrador de conexiones** para abrir la página **Administrador de conexiones** del editor.  
  
## <a name="static-options"></a>Opciones estáticas  
  
> [!NOTE]  
>  Si no conoce todos los valores necesarios para configurar el origen, puede que tenga que ponerse en contacto con el administrador de SAP.  
  
 **Administrador de conexiones de SAP BW**  
 Seleccione un administrador de conexiones de la lista o cree una conexión haciendo clic en **Nuevo**.  
  
 **Nuevo**  
 Cree un administrador de conexiones con el cuadro de diálogo **Administrador de conexiones de SAP BW** .  
  
 Para obtener más información sobre este cuadro de diálogo, vea [SAP BW Connection Manager Editor](../../integration-services/connection-manager/sap-bw-connection-manager-editor.md).  
  
 **Destino OHS**  
 Permite seleccionar el destino del servicio de concentrador abierto (OHS) que se usará para extraer los datos del origen.  
  
 **Modo de ejecución**  
 Permite especificar el método para la extracción de datos desde el origen.  
  
|Opción|Descripción|  
|------------|-----------------|  
|**P -Desencadenar cadena de procesos**|Desencadene una cadena de procesos. En este caso, el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inicia el proceso de extracción.|  
|**W - Esperar notificación**|Permite esperar para recibir la notificación del sistema SAP Netweaver BW para comenzar a extraer datos. En este caso, el sistema SAP Netweaver BW inicia el proceso de extracción.|  
|**E - Extraer únicamente**|Recupere los datos asociados a un identificador de solicitud determinado. En este caso, el sistema SAP Netweaver BW ha extraído ya los datos a una tabla interna y el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] solo lee los datos.|  
  
 **Versión preliminar**  
 Permite abrir el cuadro de diálogo **Vista previa** , donde podrá obtener una vista previa de los resultados. Para más información, consulte [Preview](../../integration-services/data-flow/preview.md).  
  
> [!IMPORTANT]  
>  La opción de **Vista previa** , que está disponible en la página de **Administrador de conexiones** del editor de origen de SAP BW, extrae los datos. Si ha configurado SAP Netweaver BW para extraer solamente los datos que han cambiado desde la extracción anterior, si selecciona **Vista previa** , excluirá datos de la vista previa de la extracción siguiente.  
  
 Al hacer clic en **Vista previa**, también se abre el cuadro de diálogo **Registro de solicitudes** . Puede usar este cuadro de diálogo para ver los eventos que se registran durante la solicitud que se efectúa al sistema SAP Netweaver BW sobre datos de ejemplo. Para más información, consulte [Request Log](../../integration-services/data-flow/request-log.md).  
  
## <a name="execution-mode-dynamic-options"></a>Opciones dinámicas del modo de ejecución  
  
> [!NOTE]  
>  Si no conoce todos los valores necesarios para configurar el origen, puede que tenga que ponerse en contacto con el administrador de SAP.  
  
### <a name="execution-mode--p---trigger-process-chain"></a>Modo de ejecución = P - Desencadenar cadena de procesos  
  
#### <a name="rfc-destination-options"></a>Opciones de destino RFC  
 No es necesario que conozca y especifique estos valores previamente. Utilice el botón de **Buscar** para buscar y seleccionar el destino RFC adecuado. Después de seleccionar un destino RFC, el componente especifica los valores adecuados para estas opciones.  
  
 **Host de puerta de enlace**  
 Permite escribir el nombre del servidor o la dirección IP del host de puerta de enlace. Normalmente, el nombre o la dirección IP es el mismo que el del servidor de aplicaciones SAP.  
  
 **Servicio de puerta de enlace**  
 Permite escribir el nombre del servicio de puerta de enlace, en formato **sapgwNN**, donde **NN** es el número de sistema.  
  
 **Id. de programa**  
 Permite escribir el identificador de programa asociado al destino RFC.  
  
 **Buscar**  
 Permite buscar el destino RFC con el cuadro de diálogo **Buscar destino RFC** . Para obtener más información sobre este cuadro de diálogo, vea [Look Up RFC Destination](../../integration-services/data-flow/look-up-rfc-destination.md).  
  
#### <a name="process-chain-options"></a>Opciones de la cadena de procesos  
 No es necesario que conozca y especifique estos valores previamente. Use el botón de **Buscar** para buscar y seleccionar la cadena de procesos adecuada. Después de seleccionar una cadena de procesos, el componente especifica los valores adecuados para la opción.  
  
 **Cadena de procesos**  
 Permite escribir el nombre de la cadena de procesos que va a desencadenar el origen.  
  
 **Buscar**  
 Permite buscar la cadena de procesos con el cuadro de diálogo **Buscar cadena de procesos** . Para obtener más información sobre este cuadro de diálogo, vea [Look Up Process Chain](../../integration-services/data-flow/look-up-process-chain.md).  
  
### <a name="execution-mode--w---wait-for-notify"></a>Modo de ejecución = W - Esperar notificación  
  
#### <a name="rfc-destination-options"></a>Opciones de destino RFC  
 No es necesario que conozca y especifique estos valores previamente. Utilice el botón de **Buscar** para buscar y seleccionar el destino RFC adecuado. Después de seleccionar un destino RFC, el componente especifica los valores adecuados para las opciones.  
  
 **Host de puerta de enlace**  
 Permite escribir el nombre del servidor o la dirección IP del host de puerta de enlace. Normalmente, el nombre o la dirección IP es el mismo que el del servidor de aplicaciones SAP.  
  
 **Servicio de puerta de enlace**  
 Permite escribir el nombre del servicio de puerta de enlace, en formato **sapgwNN**, donde **NN** es el número de sistema.  
  
 **Id. de programa**  
 Permite escribir el identificador de programa asociado al destino RFC.  
  
 **Buscar**  
 Permite buscar el destino RFC con el cuadro de diálogo **Buscar destino RFC** . Para obtener más información sobre este cuadro de diálogo, vea [Look Up RFC Destination](../../integration-services/data-flow/look-up-rfc-destination.md).  
  
### <a name="execution-mode--e---extract-only"></a>Modo de ejecución = E - Extraer únicamente  
 **Id. de solicitud**  
 Permite escribir el identificador de solicitud asociado a la extracción.  
  
## <a name="see-also"></a>Consulte también  
 [Editor de origen de SAP BW &#40;página Columnas&#41;](../../integration-services/data-flow/sap-bw-source-editor-columns-page.md)   
 [Editor de origen de SAP BW &#40;página Salida de error&#41;](../../integration-services/data-flow/sap-bw-source-editor-error-output-page.md)   
 [Editor de origen de SAP BW &#40;página Opciones avanzadas&#41;](../../integration-services/data-flow/sap-bw-source-editor-advanced-page.md)   
 [Ayuda F1 de Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
