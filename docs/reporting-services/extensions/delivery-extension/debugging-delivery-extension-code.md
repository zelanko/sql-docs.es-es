---
title: "Depurar código de extensión de entrega | Documentos de Microsoft"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- delivery extensions [Reporting Services], debugging
- debugging delivery extensions [Reporting Services]
- troubleshooting [Reporting Services], delivery extensions
ms.assetid: a7d959da-5005-4a50-aca7-2cef36aa9947
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: e2d2162167123c152cbbeb58739f25ee06ec692a
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="debugging-delivery-extension-code"></a>Depurar el código de extensión de entrega
  El [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] proporciona varias herramientas de depuración que pueden ayudarle a analizar el código de extensión de entrega y localizar errores en él. La herramienta más conveniente dependerá de lo que intente llevar a cabo. En este ejemplo se usa [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)].  
  
#### <a name="to-debug-your-delivery-extension-code"></a>Para depurar el código de extensión de entrega  
  
1.  Iniciar [!INCLUDE[vsOrcas](../../../includes/vsorcas-md.md)] y abra el proyecto de extensión de entrega.  
  
2.  Genere el proyecto e implemente el ensamblado de extensión de entrega y el archivo .pdb acompañante en el servidor de informes y el Administrador de informes. Para obtener más información acerca de la implementación, consulte [implementar una extensión de entrega](../../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md).  
  
3.  Si ha escrito una interfaz de usuario de suscripción para extender el Administrador de informes, ha abierto Internet Explorer y ha navegado al Administrador de informes mientras dejaba abierto el código de extensión de entrega en [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]. Si no tiene implementada una interfaz de usuario de suscripción para el Administrador de informes, simplemente abra la aplicación cliente desde la que llama a la extensión de entrega utilizando la API SOAP.  
  
4.  Navegue a [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] y al proyecto de extensión de entrega, y establezca algunos puntos de interrupción en el código.  
  
5.  Con el proyecto de extensión de entrega aún en la ventana activa, haga clic en **adjuntar al proceso** en el **depurar** menú.  
  
     El **adjuntar al proceso** abre el cuadro de diálogo.  
  
6.  En la lista de procesos, seleccione el proceso aspnet_wp.exe (o w3wp.exe, si la aplicación se implementa en IIS 6.0) y haga clic en **adjuntar**.  
  
7.  Defina una nueva suscripción mediante su extensión de entrega. Probablemente utilizará el Administrador de informes o la API SOAP. De esta forma se debería invocar el depurador y ejecutar el código correspondiente a sus puntos de interrupción.  
  
8.  Recorrer el código mediante el **F11** clave. Para obtener más información sobre cómo utilizar [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] para la depuración, vea la documentación de [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Implementar una extensión de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensión de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
