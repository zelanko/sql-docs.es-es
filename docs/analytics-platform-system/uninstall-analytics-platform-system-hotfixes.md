---
title: Desinstalar las revisiones del sistema de la plataforma de análisis en | Documentos de Microsoft
description: Desinstalar las revisiones del sistema de la plataforma de análisis.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 83e57a676ee0eff21eb3a736484d8e286cdeee01
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>Desinstalar las revisiones del sistema de la plataforma de análisis 
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
  
