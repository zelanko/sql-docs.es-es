---
title: Aplicación de las revisiones de Analytics Platform System
description: En este artículo se describe cómo aplicar revisiones al software de sistema de la plataforma de análisis.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: fd62413ec8542aba9f3973d0e8483cb9c5c9128a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401374"
---
# <a name="apply-analytics-platform-system-hotfixes"></a>Aplicación de las revisiones de Analytics Platform System
En este artículo se describe cómo aplicar revisiones al software de sistema de la plataforma de análisis.  
  
## <a name="before-you-begin"></a>Antes de empezar  
  
> [!WARNING]  
> No intente aplicar una revisión del sistema de la plataforma de análisis si el dispositivo o cualquier componente del dispositivo está inactivo o en un estado de conmutación por error. En ese caso, póngase en contacto con soporte técnico para obtener ayuda.  
  
> [!WARNING]  
> No aplique una revisión de Analytics Platform System mientras el dispositivo esté en uso. La aplicación de una revisión puede hacer que los nodos del dispositivo se reinicien. La revisión debe aplicarse durante una ventana de mantenimiento cuando no se usa el dispositivo.  
  
### <a name="prerequisites"></a>Prerrequisitos  
Para realizar estos pasos, necesitará:  
  
-   Un inicio de sesión de System Analytics Platform con permisos para tener acceso a la consola de administración para supervisar el estado del dispositivo. <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   Conocimiento de la cuenta de administrador de dominio de tejido para conectarse al _<domain_name nodo>_ **-HST01** .  
  
## <a name="to-apply-a-analytics-platform-system-hotfix"></a><a name="HowToInstallPDW"></a>Para aplicar una revisión del sistema de análisis de plataforma  
A diferencia de las actualizaciones de Microsoft, las revisiones del software de sistema de la plataforma de análisis no se controlan a través de WSUS. Tienen un flujo de trabajo diferente y se instalan mediante la ejecución de un paquete de revisiones.  
  
1.  **Compruebe los indicadores de estado del dispositivo.**  
  
    1.  Abra la consola de administración de y vaya a la página estado del dispositivo. Para más información, consulte [supervisión del dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
    2.  Antes de continuar con el paso siguiente, debe resolver todos los indicadores rojos o amarillos. Hay un par de excepciones a esto:  
  
        -   Si hay errores de disco, use la página de alertas de la consola de administración para comprobar que no haya más de un error de disco dentro de cada matriz de servidores o SAN. Si no hay más de un error de disco dentro de cada matriz de servidores o SAN, puede continuar con el paso siguiente antes de corregir los errores de disco. Asegúrese de ponerse en contacto con el soporte técnico de Microsoft para corregir los errores de disco lo antes posible.  
  
        -   Si hay un error de volumen de disco no crítico (amarillo) que no está en el C:\ , puede continuar con el paso siguiente antes de resolver el error de volumen de disco.  
  
2.  **Instalación de la revisión de Analytics Platform System**  
  
    1.  Inicie sesión en el <*appliance_domain* nodo>-HST01 como administrador del dominio.  
  
    2.  Use la opción **Ejecutar como administrador** para abrir un símbolo del sistema.  
  
    3.  Ejecute el comando siguiente, reemplazando *<HotfixPackageName>* por el nombre del paquete ejecutable de la revisión y reemplazando los demás elementos del marcador de posición *<  >* por la información adecuada.  
  
        ```  
        <HotfixPackageName> /DomainAdminPassword="<password>"  
        ```  
  
    4.  Siga los pasos que presenta el paquete de revisiones.  
  
## <a name="see-also"></a>Consulte también  
[Descargar y aplicar actualizaciones de Microsoft &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)  
[Desinstale Microsoft Updates &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[Desinstalación de las revisiones de Analytics Platform System &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[Servicio de software &#40;Analytics Platform System&#41;](software-servicing.md)  
  
