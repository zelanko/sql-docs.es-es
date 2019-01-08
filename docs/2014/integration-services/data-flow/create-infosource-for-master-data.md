---
title: Crear InfoSource para datos maestros | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b52a9a89-8380-4a02-8a83-dcfb46ae860e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0b9460ee16c73d5bf61fdfab1f67a796d5b033c1
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52793566"
---
# <a name="create-infosource-for-master-data"></a>Crear InfoSource para datos maestros
  Use el cuadro de diálogo **Crear InfoSource para los datos maestros** para crear un InfoSource nuevo para los datos maestros en el sistema SAP Netweaver BW.  
  
 Puede abrir el cuadro de diálogo **Crear InfoSource para los datos maestros** desde la página **Administrador de conexiones** del **Editor de destino de SAP BW**. Para más información acerca del destino de SAP BW, consulte [SAP BW Destination](sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  La documentación de Microsoft Connector 1.1 for SAP BW da por supuesto que se está familiarizado con el entorno SAP Netweaver BW. Para obtener más información acerca de SAP Netweaver BW, o sobre cómo configurar los objetos y los procesos de SAP Netweaver BW, vea la documentación de SAP.  
  
 **Para abrir el cuadro de diálogo Crear InfoSource para los datos maestros**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el destino SAP BW.  
  
2.  En la pestaña **Flujo de datos** , haga doble clic en el destino de SAP BW.  
  
3.  En **Editor de destino SAP BW**, haga clic en **Administrador de conexiones** para abrir la página **Administrador de conexiones** del editor.  
  
4.  En la página **Administrador de conexiones** , en el cuadro del grupo **Crear objetos de SAP BW** , seleccione **InfoSource**y, a continuación, haga clic en **Crear**.  
  
5.  En el cuadro de diálogo **Crear InfoSource** , seleccione **Datos maestros**y, a continuación, haga clic en **Aceptar**.  
  
## <a name="options"></a>Opciones  
 **Nombre de InfoObject**  
 Permite escribir el nombre del InfoObject en el que se va a basar el nuevo InfoSource.  
  
 **Buscar**  
 Permite buscar el InfoObject. Esta opción abre el cuadro de diálogo **Buscar InfoObject** , donde podrá seleccionar el InfoObject. Para obtener más información sobre este cuadro de diálogo, vea [Look Up InfoObject](look-up-infoobject.md).  
  
 Después de seleccionar un InfoObject, el componente rellena el cuadro de texto **Nombre de InfoObject** con el nombre del InfoObject seleccionado.  
  
 **Nueva**  
 Permite crear un nuevo InfoObject. Esta opción abre el cuadro de diálogo **Crear nuevo InfoObject**, donde podrá crear el InfoObject nuevo. Para obtener más información sobre este cuadro de diálogo, vea [Create New InfoObject](create-new-infoobject.md).  
  
 Después de crear un InfoObject, el componente rellena el cuadro de texto **Nombre de InfoObject** con el nombre del InfoObject nuevo.  
  
 **Descripción breve**  
 Permite escribir una descripción breve para el nuevo InfoSource.  
  
 **Descripción larga**  
 Permite escribir una descripción larga para el nuevo InfoSource.  
  
 **Sistema de origen**  
 Permite seleccionar el sistema de origen que se va a asociar al InfoSource.  
  
 **Aplicación**  
 Permite escribir el nombre de la aplicación que se va a asociar al nuevo InfoSource.  
  
 **Atributos**  
 Permite indicar que los datos maestros están compuestos de atributos.  
  
 **Textos**  
 Permite indicar que los datos maestros están compuestos de atributos.  
  
 **Guardar y activar**  
 Permite guardar y activar el nuevo InfoSource.  
  
## <a name="see-also"></a>Vea también  
 [Crear InfoSource](create-infosource.md)   
 [Ayuda F1 de Microsoft Connector 1.1 for SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
