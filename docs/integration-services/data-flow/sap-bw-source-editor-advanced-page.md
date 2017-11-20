---
title: "Editor de origen de SAP BW (página avanzadas) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.sapbwsource.advanced.f1
ms.assetid: 44f3c991-9e8f-4126-a9a2-2d9da779fb11
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ac7757987c169f803f3b0adda7f27c94f090d7db
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="sap-bw-source-editor-advanced-page"></a>Editor de origen de SAP BW (página Avanzadas)
  Use la página **Avanzadas** del **Editor de origen de SAP BW** para especificar la regla de conversión de cadenas y el tiempo de espera, así como para restablecer el estado de un determinado identificador de solicitud.  
  
 Para más información sobre el componente de origen de SAP BW de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW, vea [Origen de SAP BW](../../integration-services/data-flow/sap-bw-source.md).  
  
> [!IMPORTANT]  
>  La documentación de Microsoft Connector 1.1 for SAP BW da por supuesto que se está familiarizado con el entorno SAP Netweaver BW. Para obtener más información acerca de SAP Netweaver BW, o sobre cómo configurar los objetos y los procesos de SAP Netweaver BW, vea la documentación de SAP.  
  
> [!IMPORTANT]  
>  La extracción de datos de SAP Netweaver BW requiere una licencia SAP adicional. Póngase en contacto con SAP para comprobar estos requisitos.  
  
 **Para abrir la página Administrador de conexiones**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el origen de SAP BW.  
  
2.  En la pestaña **Flujo de datos** , haga doble clic en el origen de SAP BW.  
  
3.  En **Editor de origen de SAP BW**, haga clic en **Opciones avanzadas** para abrir la página **Opciones avanzadas** del editor.  
  
## <a name="options"></a>Opciones  
  
> [!NOTE]  
>  Si no conoce todos los valores necesarios para configurar el origen, puede que tenga que ponerse en contacto con el administrador de SAP.  
  
 **Conversión de cadenas**  
 Permite especificar la regla que se va a aplicar en la conversión de cadenas.  
  
|Opción|Description|  
|------------|-----------------|  
|**Conversión de cadena automática**|Permite convertir todas las cadenas a **nvarchar** cuando el sistema SAP Netweaver BW es un sistema de Unicode. Si no es así, convierte todas las cadenas a **varchar**.|  
|**Convertir cadenas a varchar**|Permite convertir todas las cadenas a **varchar**.|  
|**Convertir cadenas a nvarchar**|Permite convertir todas las cadenas a **nvarchar**.|  
  
 **Tiempo de espera en segundos**  
 Permite especificar el número máximo de segundos que debe esperar el origen.  
  
> [!NOTE]  
>  Esta opción solo es válida si ha seleccionado **W - Esperar notificación** como el valor de **Modo de ejecución** en la página **Administrador de conexiones** del editor. Para más información, vea [Editor de origen de SAP BW &#40;página Administrador de conexiones&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md).  
  
 **Id. de solicitud**  
 Permite especificar el identificador de solicitud cuyo estado quiere restablecer a “G - Verde” al hacer clic en **Restablecer**.  
  
 **Restablecer**  
 Permite restablecer el estado del identificador de solicitud especificado a “G - Verde”, después de solicitarle la confirmación. Esto puede resultar útil en caso de que se produzcan problemas y el sistema SAP Netweaver BW haya marcado la solicitud con un estado de amarillo o rojo.  
  
## <a name="see-also"></a>Vea también  
 [Editor de origen de SAP BW &#40;página Administrador de conexiones&#41;](../../integration-services/data-flow/sap-bw-source-editor-connection-manager-page.md)   
 [Editor de origen de SAP BW &#40; Página columnas &#41;](../../integration-services/data-flow/sap-bw-source-editor-columns-page.md)   
 [Editor de origen de SAP BW &#40; Página de salida de error &#41;](../../integration-services/data-flow/sap-bw-source-editor-error-output-page.md)   
 [Ayuda F1 de Microsoft Connector 1.1 for SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  

