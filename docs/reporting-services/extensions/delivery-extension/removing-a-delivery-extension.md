---
title: Quitar una extensión de entrega | Microsoft Docs
description: Obtenga información sobre cómo quitar una extensión de entrega de Reporting Services para que el servidor de informes no la muestre como disponible y desactive las suscripciones que la usen.
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- removing delivery extensions
- deleting delivery extensions
- delivery extensions [Reporting Services], removing
ms.assetid: dcb7caf2-d19a-4bc5-afb3-2b61ad11cac5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6f4f23d58836dbadb9393be49dd34425c89a15c3
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529491"
---
# <a name="removing-a-delivery-extension"></a>Quitar una extensión de entrega
  Para quitar una extensión de entrega de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], basta con quitar el elemento **Extension** para la extensión de entrega del archivo de configuración. Después de quitar la información de configuración, la extensión de entrega deja de estar disponible en el servidor de informes.  
  
 Cuando el elemento **Extension** correspondiente de la extensión de entrega se quita del archivo de configuración, ya no está registrado en el servidor de informes. El servidor de informes quita la entrada de la lista de extensiones de entrega y desactiva cualquier suscripción que use esa extensión de entrega. Cuando una extensión de entrega se quita, los usuarios ya no pueden seleccionarla como un método de notificación.  
  
## <a name="see-also"></a>Consulte también  
 [Implementar una extensión de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensiones de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
