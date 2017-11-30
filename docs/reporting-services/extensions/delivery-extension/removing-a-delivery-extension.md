---
title: "Quitar una extensión de entrega | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- removing delivery extensions
- deleting delivery extensions
- delivery extensions [Reporting Services], removing
ms.assetid: dcb7caf2-d19a-4bc5-afb3-2b61ad11cac5
caps.latest.revision: "31"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: fa353bad5d7ba36330aca71fcb0d329ff0c606a6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="removing-a-delivery-extension"></a>Quitar una extensión de entrega
  Para quitar una extensión de entrega de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], basta con quitar el elemento **Extension** para la extensión de entrega del archivo de configuración. Después de quitar la información de configuración, la extensión de entrega deja de estar disponible en el servidor de informes.  
  
 Cuando el elemento **Extension** correspondiente de la extensión de entrega se quita del archivo de configuración, ya no está registrado en el servidor de informes. El servidor de informes quita la entrada de la lista de extensiones de entrega y desactiva cualquier suscripción que use esa extensión de entrega. Cuando una extensión de entrega se quita, los usuarios ya no pueden seleccionarla como un método de notificación.  
  
## <a name="see-also"></a>Vea también  
 [Implementar una extensión de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensiones de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
