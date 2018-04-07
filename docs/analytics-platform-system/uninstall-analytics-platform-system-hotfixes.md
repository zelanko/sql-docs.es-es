---
title: Desinstalar las revisiones de sistema de plataforma de análisis (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c9ab596d-3f5a-48e2-bce7-c9be99b8c23b
caps.latest.revision: 21
ms.openlocfilehash: 56c6731d5a39741574999d94532b9505adaf6380
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>Desinstalar las revisiones del sistema de plataforma de análisis
Los pasos siguientes describen cómo desinstalar una revisión Analytics Platform System instalada previamente.  
  
## <a name="before-you-begin"></a>Antes de comenzar  
  
### <a name="prerequisites"></a>Requisitos previos  
Para llevar a cabo estos pasos, necesitará:  
  
-   Un inicio de sesión de sistema de la plataforma de análisis con permisos para tener acceso a la consola de administración para supervisar el dispositivo.  
  
-   La cuenta de administrador de dominio para iniciar sesión en el *< appliance_domain > ***-HST01** nodo.  
  
-   Número de artículo de Knowledge Base para la revisión para desinstalar.  
  
## <a name="HowToUninstallPDW"></a>Para desinstalar una revisión de SQL Server PDW  
  
1.  Inicie sesión en el *< appliance_domain > ***-HST01** nodo como el administrador del dominio de tejido.  
  
2.  Usar la ejecución como opción de administrador para abrir un símbolo del sistema.  
  
3.  Cambie los directorios a `C:\PDWINST\Patches\<kbarticle>\media` donde *<kbarticle>* es el número de artículo de Knowledge Base para la revisión para desinstalar.  
  
    ```  
    cd /d c:\PDWINST\Patches\<kbarticle>\media  
    ```  
  
4.  Para quitar la revisión, ejecute el siguiente comando.  
  
    ```  
    setup.exe /action="removepatch" /DomainAdminPassword="<password>"  
    ```  
  
## <a name="see-also"></a>Vea también  
[Descargue y aplique las actualizaciones de Microsoft &#40;sistema de la plataforma de análisis&#41;](download-and-apply-microsoft-updates.md)  
[Desinstalar actualizaciones de Microsoft &#40;sistema de la plataforma de análisis&#41;](uninstall-microsoft-updates.md)  
[Aplicar las revisiones del sistema de plataforma de análisis &#40;sistema de la plataforma de análisis&#41;](apply-analytics-platform-system-hotfixes.md)  
[Mantenimiento de software &#40;sistema de la plataforma de análisis&#41;](software-servicing.md)  
  
