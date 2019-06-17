---
title: Desinstalar actualizaciones de Microsoft - Analytics Platform System | Microsoft Docs"
description: Desinstalar actualizaciones de Microsoft Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 4739d05b1878c8b7fc9f66f2e0b8145ff1044e54
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63243824"
---
# <a name="uninstall-microsoft-updates-in-analytics-platform-system"></a>Desinstalar actualizaciones de Microsoft en Analytics Platform System
En este artículo se describe cómo desinstalar una actualización de Microsoft instalada previamente en el dispositivo de Analytics Platform System.  
  
## <a name="before-you-begin"></a>Antes de empezar  
  
### <a name="prerequisites"></a>Requisitos previos  
Para llevar a cabo estos pasos, necesitará:  
  
-   Un inicio de sesión de Analytics Platform System con permisos para tener acceso a la consola de administración para supervisar el dispositivo.  
  
-   Conocimiento de la cuenta de administrador del tejido dominio iniciar sesión en el <em> <Fabric Domain> </em> **-HST01** nodo.  
  
## <a name="HowToUninstallMSFT"></a>Para desinstalar las actualizaciones de Microsoft  
  
1.  Inicie sesión en el <em> <Fabric Domain> </em> **-HST01** nodo como el Administrador de dominio de Fabric.  
  
2.  Para desinstalar todas las actualizaciones aprobadas desinstalar WSUS, abra una ventana del símbolo del sistema y escriba el siguiente comando. Reemplace el marcador de posición elementos *< >* con la información adecuada.  
  
    ```  
    C:\pdwinst\media\setup.exe /action="RemoveMicrosoftUpdate" /DomainAdminPasswords="<password>"  
    ```  
  
## <a name="next-steps"></a>Pasos siguientes
Para obtener más información, vea:
- [Descargue y aplique las actualizaciones de Microsoft &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md) 
- [Aplicar las revisiones de Analytics Platform System &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
- [Desinstalar las revisiones de Analytics Platform System &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
- [Mantenimiento de software &#40;Analytics Platform System&#41;](software-servicing.md)  
  
