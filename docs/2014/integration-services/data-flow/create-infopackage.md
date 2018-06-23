---
title: Crear InfoPackage | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9cd4a848-409f-4681-a390-1c49a2aadbd7
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 25ecfabc0f48b2cc34c723e4052d89da5d7e29dc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198961"
---
# <a name="create-infopackage"></a>Crear InfoPackage
  Use el cuadro de diálogo **Crear nuevo InfoPackage** para crear un nuevo InfoPackage en el sistema SAP Netweaver BW.  
  
 Puede abrir el cuadro de diálogo **Crear InfoPackage** desde la página **Administrador de conexiones** del **Editor de destino de SAP BW**. Para más información acerca del destino de SAP BW, consulte [SAP BW Destination](sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  La documentación de Microsoft Connector 1.1 for SAP BW da por supuesto que se está familiarizado con el entorno SAP Netweaver BW. Para obtener más información acerca de SAP Netweaver BW, o sobre cómo configurar los objetos y los procesos de SAP Netweaver BW, vea la documentación de SAP.  
  
 **Para abrir el cuadro de diálogo Crear InfoPackage**  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contiene el destino SAP BW.  
  
2.  En la pestaña **Flujo de datos** , haga doble clic en el destino de SAP BW.  
  
3.  En **Editor de destino SAP BW**, haga clic en **Administrador de conexiones** para abrir la página **Administrador de conexiones** del editor.  
  
4.  En la página **Administrador de conexiones** , en el cuadro del grupo **Crear objetos de SAP BW** , seleccione **InfoPackage**y, a continuación, haga clic en **Crear**.  
  
## <a name="options"></a>Opciones  
 **InfoSource**  
 Permite escribir el nombre del InfoSource en el que se va a basar el nuevo InfoPackage.  
  
 **Descripción breve**  
 Permite escribir una descripción para el nuevo InfoPackage.  
  
 **Sistema de origen**  
 Permite seleccionar el sistema origen con el que se va asociar el nuevo InfoPackage.  
  
 **Atributos**  
 Permite indicar que el InfoPackage cargará los datos del atributo.  
  
 **Textos**  
 Permite indicar que el InfoPackage cargará los datos de texto.  
  
 **Transaction**  
 Permite indicar que el InfoPackage cargará los datos de transacciones.  
  
 **Guardar y activar**  
 Permite guardar y activar el nuevo InfoPackage.  
  
## <a name="see-also"></a>Vea también  
 [Microsoft Connector 1.1 for SAP BW F1 Ayuda](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  