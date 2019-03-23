---
title: Registro de solicitudes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 165d3833-0493-490c-9f63-8a134a7fafb8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 521d40529501d761b8e50300c16a816284109695
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58384523"
---
# <a name="request-log"></a>Registro de solicitudes
  Use el cuadro de diálogo **Registro de solicitudes** para ver los eventos que se registran durante la solicitud que se efectúa al sistema SAP Netweaver BW sobre datos de ejemplo. Esta información puede ser útil si tiene que solucionar problemas en la configuración del origen de SAP BW.  
  
 Para obtener más información sobre el componente de origen de SAP BW de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW, vea [Origen de SAP BW](sap-bw-source.md).  
  
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
    >  Al hacer clic en **Vista previa** , también se abre el cuadro de diálogo **Vista previa** . Para obtener más información sobre este cuadro de diálogo, vea [Preview](preview.md).  
  
## <a name="options"></a>Opciones  
 **Time**  
 Muestra la hora en la que se ha registrado el evento.  
  
 **Tipo**  
 Muestra el tipo de evento que se ha registrado. En la tabla siguiente se enumeran los tipos de evento posibles.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|S|Mensaje de correcto.|  
|E|Mensaje de error|  
|W|Mensaje de advertencia.|  
|I|Mensaje informativo.|  
|A|Se anuló la operación.|  
  
 **de mensaje**  
 Muestra el texto del mensaje asociado al evento registrado.  
  
## <a name="see-also"></a>Vea también  
 [Editor de origen de SAP BW &#40;página Administrador de conexiones&#41;](sap-bw-source-editor-connection-manager-page.md)   
 [Ayuda F1 de Microsoft Connector 1.1 for SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
