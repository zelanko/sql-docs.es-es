---
title: Desinstalar las revisiones de Analytics Platform System en | Microsoft Docs
description: Desinstalar revisiones de Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d7135972201fe8cce8a43cbd3c8fe547ce40248e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959903"
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>Desinstalar revisiones de Analytics Platform System 
Los pasos siguientes describen cómo desinstalar una revisión de Analytics Platform System instalada previamente.  
  
## <a name="before-you-begin"></a>Antes de empezar  
  
### <a name="prerequisites"></a>Requisitos previos  
Para llevar a cabo estos pasos, necesitará:  
  
-   Un inicio de sesión de Analytics Platform System con permisos para tener acceso a la consola de administración para supervisar el dispositivo.  
  
-   La cuenta de administrador de dominio iniciar sesión en el <em>< appliance_domain ></em> **-HST01** nodo.  
  
-   Número de artículo de Knowledge Base para la revisión para desinstalar.  
  
## <a name="HowToUninstallPDW"></a>Para desinstalar una revisión de SQL Server PDW  
  
1.  Inicie sesión en el <em>< appliance_domain ></em> **-HST01** nodo como el Administrador de dominio de Fabric.  
  
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
[Descargue y aplique las actualizaciones de Microsoft &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)  
[Desinstalar las actualizaciones de Microsoft &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[Aplicar las revisiones de Analytics Platform System &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
[Mantenimiento de software &#40;Analytics Platform System&#41;](software-servicing.md)  
  
