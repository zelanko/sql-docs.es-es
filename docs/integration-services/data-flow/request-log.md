---
title: Registro de solicitudes | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: data-flow
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 165d3833-0493-490c-9f63-8a134a7fafb8
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1e2d3ea8253e3bc999168d5890fe3de23e34eaaa
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="request-log"></a>Registro de solicitudes
  Use el cuadro de diálogo **Registro de solicitudes** para ver los eventos que se registran durante la solicitud que se efectúa al sistema SAP Netweaver BW sobre datos de ejemplo. Esta información puede ser útil si tiene que solucionar problemas en la configuración del origen de SAP BW.  
  
 Para obtener más información sobre el componente de origen de SAP BW de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW, vea [Origen de SAP BW](../../integration-services/data-flow/sap-bw-source.md).  
  
> [!IMPORTANT]  
>  La documentación de Microsoft Connector 1.1 for SAP BW da por supuesto que se está familiarizado con el entorno SAP Netweaver BW. Para obtener más información acerca de SAP Netweaver BW, o sobre cómo configurar los objetos y los procesos de SAP Netweaver BW, vea la documentación de SAP.  
  
> [!IMPORTANT]  
>  La extracción de datos de SAP Netweaver BW requiere una licencia SAP adicional. Póngase en contacto con SAP para comprobar estos requisitos.  
  
 **Para abrir el cuadro de diálogo Registro de solicitudes**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el origen de SAP BW.  
  
2.  En la pestaña **Flujo de datos** , haga doble clic en el origen de SAP BW.  
  
3.  En **Editor de origen de SAP BW**, haga clic en **Administrador de conexiones** para abrir la página **Administrador de conexiones** del editor.  
  
4.  Después de configurar el origen de SAP BW, haga clic en **Vista previa** para obtener una vista previa de los eventos del cuadro de diálogo **Registro de solicitudes** .  
  
    > [!NOTE]  
    >  Al hacer clic en **Vista previa** , también se abre el cuadro de diálogo **Vista previa** . Para obtener más información sobre este cuadro de diálogo, vea [Preview](../../integration-services/data-flow/preview.md).  
  
## <a name="options"></a>Opciones  
 **Time**  
 Muestra la hora en la que se ha registrado el evento.  
  
 **Tipo**  
 Muestra el tipo de evento que se ha registrado. En la tabla siguiente se enumeran los tipos de evento posibles.  
  
|Valor|Description|  
|-----------|-----------------|  
|S|Mensaje de correcto.|  
|E|Mensaje de error|  
|W|Mensaje de advertencia.|  
|I|Mensaje informativo.|  
|Un|Se anuló la operación.|  
  
 **de mensaje**  
 Muestra el texto del mensaje asociado al evento registrado.  
  
## <a name="see-also"></a>Ver también  
 [Editor de origen de SAP BW &#40;página Administrador de conexiones&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [Ayuda F1 de Microsoft Connector for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
