---
title: Desinstalar actualizaciones de Microsoft (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: df61570a-210d-4154-822f-98acd721f075
caps.latest.revision: "19"
ms.openlocfilehash: c801918cbac5d0762384a0cd3adcca9ddf8f346a
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="uninstall-microsoft-updates"></a>Desinstalar actualizaciones de Microsoft
En este tema se describe cómo desinstalar una actualización de Microsoft instalada previamente en el dispositivo de sistema de la plataforma de análisis.  
  
## <a name="before-you-begin"></a>Antes de comenzar  
  
### <a name="prerequisites"></a>Requisitos previos  
Para llevar a cabo estos pasos, necesitará:  
  
-   Un inicio de sesión de sistema de la plataforma de análisis con permisos para tener acceso a la consola de administración para supervisar el dispositivo.  
  
-   Conocimiento de la cuenta de administrador de dominio del tejido que inicie sesión en el  *<Fabric Domain>*  **-HST01** nodo.  
  
## <a name="HowToUninstallMSFT"></a>Para desinstalar las actualizaciones de Microsoft  
  
1.  Inicie sesión en el  *<Fabric Domain>*  **-HST01** nodo como el administrador del dominio de tejido.  
  
2.  Para desinstalar todas las actualizaciones que están aprobadas para que WSUS desinstalar, abra una ventana del símbolo del sistema y escriba el siguiente comando. Reemplace los elementos de marcador de posición *< >* con la información adecuada.  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="see-also"></a>Vea también  
[Descargue y aplique las actualizaciones de Microsoft &#40; Sistema de la plataforma de análisis &#41;](download-and-apply-microsoft-updates.md)  
[Aplicar las revisiones del sistema de plataforma de análisis &#40; Sistema de la plataforma de análisis &#41;](apply-analytics-platform-system-hotfixes.md)  
[Desinstalar las revisiones del sistema de plataforma de análisis &#40; Sistema de la plataforma de análisis &#41;](uninstall-analytics-platform-system-hotfixes.md)  
[Mantenimiento de software &#40; Sistema de la plataforma de análisis &#41;](software-servicing.md)  
  
