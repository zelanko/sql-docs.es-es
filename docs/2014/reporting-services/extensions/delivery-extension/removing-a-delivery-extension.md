---
title: Quitar una extensión de entrega | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- removing delivery extensions
- deleting delivery extensions
- delivery extensions [Reporting Services], removing
ms.assetid: dcb7caf2-d19a-4bc5-afb3-2b61ad11cac5
caps.latest.revision: 30
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 249d54aba50465d7732595d2c8e3c90a2de0225f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202455"
---
# <a name="removing-a-delivery-extension"></a>Quitar una extensión de entrega
  Para quitar una extensión de entrega de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], basta con quitar el elemento **Extension** para la extensión de entrega del archivo de configuración. Después de quitar la información de configuración, la extensión de entrega deja de estar disponible en el servidor de informes.  
  
 Cuando el elemento **Extension** correspondiente de la extensión de entrega se quita del archivo de configuración, ya no está registrado en el servidor de informes. El servidor de informes quita la entrada de la lista de extensiones de entrega y desactiva cualquier suscripción que use esa extensión de entrega. Cuando una extensión de entrega se quita, los usuarios ya no pueden seleccionarla como un método de notificación.  
  
## <a name="see-also"></a>Vea también  
 [Implementar una extensión de entrega](implementing-a-delivery-extension.md)   
 [Biblioteca de extensiones de Reporting Services](../reporting-services-extension-library.md)  
  
  