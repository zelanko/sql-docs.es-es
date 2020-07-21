---
title: Desinstalación de las actualizaciones de Microsoft
description: Desinstale las actualizaciones de Microsoft en Analytics Platform System (APS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: a5ebe1ee911f7500505cdbd1962d28c35461a635
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "74399465"
---
# <a name="uninstall-microsoft-updates-in-analytics-platform-system"></a>Desinstalación de actualizaciones de Microsoft en Analytics Platform System
En este artículo se describe cómo desinstalar una actualización de Microsoft instalada previamente en el dispositivo Analytics Platform System.  
  
## <a name="before-you-begin"></a>Antes de empezar  
  
### <a name="prerequisites"></a>Prerrequisitos  
Para realizar estos pasos, necesitará:  
  
-   Un inicio de sesión de System Analytics Platform con permisos para tener acceso a la consola de administración para supervisar el dispositivo.  
  
-   Conocimiento de la cuenta de administrador de dominio de tejido para iniciar <em> <Fabric Domain> </em>sesión en el nodo **-HST01** .  
  
## <a name="to-uninstall-microsoft-updates"></a><a name="HowToUninstallMSFT"></a>Para desinstalar las actualizaciones de Microsoft  
  
1.  Inicie sesión en el <em> <Fabric Domain> </em>nodo **-HST01** como administrador del dominio del tejido.  
  
2.  Para desinstalar todas las actualizaciones aprobadas para que WSUS se desinstale, abra una ventana del símbolo del sistema y escriba el siguiente comando. Reemplace los elementos del marcador de posición *<  >* por la información adecuada.  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="next-steps"></a>Pasos siguientes
Para más información, consulte:
- [Descargar y aplicar actualizaciones de Microsoft &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md) 
- [Aplicación de revisiones de Analytics Platform System &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
- [Desinstalación de las revisiones de Analytics Platform System &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
- [Servicio de software &#40;Analytics Platform System&#41;](software-servicing.md)  
  
