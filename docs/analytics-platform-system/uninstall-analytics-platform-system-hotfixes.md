---
title: Desinstalar revisiones
description: Desinstale las revisiones de Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ef6929aeb06c9472eb3ff210de016117a9636ded
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "74399766"
---
# <a name="uninstall-analytics-platform-system-hotfixes"></a>Desinstalación de las revisiones de Analytics Platform System 
En los pasos siguientes se describe cómo desinstalar una revisión del sistema de análisis de plataforma previamente instalada.  
  
## <a name="before-you-begin"></a>Antes de empezar  
  
### <a name="prerequisites"></a>Prerrequisitos  
Para realizar estos pasos, necesitará:  
  
-   Un inicio de sesión de System Analytics Platform con permisos para tener acceso a la consola de administración para supervisar el dispositivo.  
  
-   La cuenta de administrador de dominio para iniciar sesión en el <em><appliance_domain nodo></em> **-HST01** .  
  
-   El número de artículo de Knowledge base de la revisión que se va a desinstalar.  
  
## <a name="to-uninstall-a-sql-server-pdw-hotfix"></a><a name="HowToUninstallPDW"></a>Para desinstalar una revisión PDW de SQL Server  
  
1.  Inicie sesión en el <em><appliance_domain nodo></em> **-HST01** como administrador del dominio del tejido.  
  
2.  Use la opción ejecutar como administrador para abrir un símbolo del sistema.  
  
3.  Cambie los directorios `C:\PDWINST\Patches\<kbarticle>\media` a *<kbarticle>* , donde es el número de artículo de Knowledge base de la revisión que se va a desinstalar.  
  
    ```  
    cd /d c:\PDWINST\Patches\<kbarticle>\media  
    ```  
  
4.  Para quitar la revisión, ejecute el siguiente comando.  
  
    ```  
    setup.exe /action="removepatch" /DomainAdminPassword="<password>"  
    ```  
  
## <a name="see-also"></a>Consulte también  
[Descargar y aplicar actualizaciones de Microsoft &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)  
[Desinstale Microsoft Updates &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[Aplicación de revisiones de Analytics Platform System &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
[Servicio de software &#40;Analytics Platform System&#41;](software-servicing.md)  
  
