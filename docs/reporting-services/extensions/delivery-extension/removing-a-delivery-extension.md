---
title: "Quitar una extensión de entrega | Documentos de Microsoft"
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
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- removing delivery extensions
- deleting delivery extensions
- delivery extensions [Reporting Services], removing
ms.assetid: dcb7caf2-d19a-4bc5-afb3-2b61ad11cac5
caps.latest.revision: 31
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: e0d806bd57750b4e260ce0ba9fe48e86ac6d7386
ms.contentlocale: es-es
ms.lasthandoff: 08/12/2017

---
# <a name="removing-a-delivery-extension"></a>Quitar una extensión de entrega
  Para quitar un [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] extensión de entrega, basta con quitar el **extensión** (elemento) para la extensión de entrega del archivo de configuración. Después de quitar la información de configuración, la extensión de entrega deja de estar disponible en el servidor de informes.  
  
 Una vez que una extensión de entrega correspondiente a la **extensión** elemento se quita del archivo de configuración, ya no está registrado con el servidor de informes. El servidor de informes quita la entrada de la lista de extensiones de entrega y desactiva cualquier suscripción que use esa extensión de entrega. Cuando una extensión de entrega se quita, los usuarios ya no pueden seleccionarla como un método de notificación.  
  
## <a name="see-also"></a>Vea también  
 [Implementar una extensión de entrega](../../../reporting-services/extensions/delivery-extension/implementing-a-delivery-extension.md)   
 [Biblioteca de extensión de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
