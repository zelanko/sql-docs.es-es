---
title: "Desinstalar las revisiones de sistema de plataforma de análisis (Analytics Platform System)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c9ab596d-3f5a-48e2-bce7-c9be99b8c23b
caps.latest.revision: "21"
ms.openlocfilehash: 32d733f2e05855eb361095d23d6c34acefd343dc
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>Desinstalar las revisiones del sistema de plataforma de análisis
Los pasos siguientes describen cómo desinstalar una revisión Analytics Platform System instalada previamente.  
  
## <a name="before-you-begin"></a>Antes de comenzar  
  
### <a name="prerequisites"></a>Prerequisites  
Para llevar a cabo estos pasos, necesitará:  
  
-   Un inicio de sesión de sistema de la plataforma de análisis con permisos para tener acceso a la consola de administración para supervisar el dispositivo.  
  
-   La cuenta de administrador de dominio para iniciar sesión en el *< appliance_domain >***-HST01** nodo.  
  
-   Número de artículo de Knowledge Base para la revisión para desinstalar.  
  
## <a name="HowToUninstallPDW"></a>Para desinstalar una revisión de SQL Server PDW  
  
1.  Inicie sesión en el *< appliance_domain >***-HST01** nodo como el administrador del dominio de tejido.  
  
2.  Usar la ejecución como opción de administrador para abrir un símbolo del sistema.  
  
3.  Cambie los directorios a `C:\PDWINST\Patches\<kbarticle>\media` donde  *<kbarticle>*  es el número de artículo de Knowledge Base para la revisión para desinstalar.  
  
    ```  
    cd /d c:\PDWINST\Patches\<kbarticle>\media  
    ```  
  
4.  Para quitar la revisión, ejecute el siguiente comando.  
  
    ```  
    setup.exe /action="removepatch" /DomainAdminPassword="<password>"  
    ```  
  
## <a name="see-also"></a>Vea también  
[Descargue y aplique las actualizaciones de Microsoft &#40; Sistema de la plataforma de análisis &#41;](download-and-apply-microsoft-updates.md)  
[Desinstalar las actualizaciones de Microsoft &#40; Sistema de la plataforma de análisis &#41;](uninstall-microsoft-updates.md)  
[Aplicar las revisiones del sistema de plataforma de análisis &#40; Sistema de la plataforma de análisis &#41;](apply-analytics-platform-system-hotfixes.md)  
[Mantenimiento de software &#40; Sistema de la plataforma de análisis &#41;](software-servicing.md)  
  
