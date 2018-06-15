---
title: Desinstalar actualizaciones de Microsoft - Analytics Platform System | Documentos de Microsoft"
description: Desinstalar actualizaciones de Microsoft Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 57d0eb3616cf3567f63d75029f79cea6709ed955
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
ms.locfileid: "31538555"
---
# <a name="uninstall-microsoft-updates-in-analytics-platform-system"></a>Desinstalar actualizaciones de Microsoft en el sistema de la plataforma de análisis
En este artículo se describe cómo desinstalar una actualización de Microsoft instalada previamente en el dispositivo de sistema de la plataforma de análisis.  
  
## <a name="before-you-begin"></a>Antes de comenzar  
  
### <a name="prerequisites"></a>Requisitos previos  
Para llevar a cabo estos pasos, necesitará:  
  
-   Un inicio de sesión de sistema de la plataforma de análisis con permisos para tener acceso a la consola de administración para supervisar el dispositivo.  
  
-   Conocimiento de la cuenta de administrador de dominio del tejido para iniciar sesión en el  *<Fabric Domain>***-HST01** nodo.  
  
## <a name="HowToUninstallMSFT"></a>Para desinstalar las actualizaciones de Microsoft  
  
1.  Inicie sesión en el  *<Fabric Domain>***-HST01** nodo como el administrador del dominio de tejido.  
  
2.  Para desinstalar todas las actualizaciones que están aprobadas para que WSUS desinstalar, abra una ventana del símbolo del sistema y escriba el siguiente comando. Reemplace los elementos de marcador de posición *< >* con la información adecuada.  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea:
- [Descargue y aplique las actualizaciones de Microsoft &#40;sistema de la plataforma de análisis&#41;](download-and-apply-microsoft-updates.md) 
- [Aplicar las revisiones del sistema de plataforma de análisis &#40;sistema de la plataforma de análisis&#41;](apply-analytics-platform-system-hotfixes.md)  
- [Desinstalar las revisiones del sistema de plataforma de análisis &#40;sistema de la plataforma de análisis&#41;](uninstall-analytics-platform-system-hotfixes.md)  
- [Mantenimiento de software &#40;sistema de la plataforma de análisis&#41;](software-servicing.md)  
  
