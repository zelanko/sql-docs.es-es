---
title: Buscar destino RFC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: db9404d8-4c42-45e5-a100-c7a84b056109
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4badd9c961f5a0d7ca2d3e32185a7ab742628d97
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62901793"
---
# <a name="look-up-rfc-destination"></a>Buscar destino RFC
  Use el cuadro de diálogo **Buscar destino RFC** para buscar un destino RFC que se haya definido en el sistema de SAP Netweaver BW. Cuando aparezca la lista de destinos RFC disponibles, seleccione el destino que desee y el componente rellenará las opciones asociadas a los valores necesarios.  
  
 El origen y el destino de SAP BW utilizan el cuadro de diálogo **Buscar destino RFC** . Para más información sobre estos componentes de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW, vea [Origen de SAP BW](sap-bw-source.md) y [Destino de SAP BW](sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  La documentación de Microsoft Connector 1.1 for SAP BW da por supuesto que se está familiarizado con el entorno SAP Netweaver BW. Para obtener más información acerca de SAP Netweaver BW, o sobre cómo configurar los objetos y los procesos de SAP Netweaver BW, vea la documentación de SAP.  
  
 **Para abrir el cuadro de diálogo Buscar destino RFC**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el origen o destino de SAP BW.  
  
2.  En la pestaña **Flujo de datos** , haga doble clic en el origen o destino de SAP BW.  
  
3.  En **Editor de origen SAP BW** o **Editor de destino de SAP BW**, haga clic en **Administrador de conexiones** para abrir la página **Administrador de conexiones** del editor.  
  
4.  En la página **Administrador de conexiones** , en el cuadro del grupo **Destino RFC** , haga clic en **Buscar** para mostrar el cuadro de diálogo **Buscar destino RFC** .  
  
     En el **Editor de origen de SAP BW**, el cuadro del grupo **Destino RFC** solo aparece si el valor de **Modo de ejecución** es **P - Desencadenar cadena de procesos** o **W - Esperar notificación**.  
  
## <a name="options"></a>Opciones  
 **Destino**  
 Permite ver el nombre del destino RFC que se haya definido en el sistema de SAP Netweaver BW.  
  
 **Host de puerta de enlace**  
 Permite ver el nombre del servidor o la dirección IP del host de puerta de enlace. Normalmente, el nombre o la dirección IP es el mismo que el del servidor de aplicaciones SAP.  
  
 **Servicio de puerta de enlace**  
 Vea el nombre del servicio de puerta de enlace, con el formato `sapgwNN`, donde `NN` es el número del sistema.  
  
 **Id. de programa**  
 Permite ver el identificador de programa asociado al destino RFC.  
  
## <a name="see-also"></a>Vea también  
 [Editor de origen de SAP BW &#40;página Administrador de conexiones&#41;](sap-bw-source-editor-connection-manager-page.md)   
 [Editor de destino de SAP BW &#40;página Administrador de conexiones&#41;](sap-bw-destination-editor-connection-manager-page.md)   
 [Ayuda F1 de Microsoft Connector 1.1 for SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
