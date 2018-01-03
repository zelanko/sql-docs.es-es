---
title: "Aplicar revisiones de sistema de plataforma de análisis (Analytics Platform System)"
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
ms.assetid: fca5eec9-86b8-4d20-b498-1678c367b5c8
caps.latest.revision: "25"
ms.openlocfilehash: 562d0ce41f5a1b12930fdedabd73214ddebd4e4e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="apply-analytics-platform-system-hotfixes"></a>Aplicar las revisiones del sistema de plataforma de análisis
En este tema se describe cómo aplicar las revisiones para el software del sistema de la plataforma de análisis.  
  
## <a name="before-you-begin"></a>Antes de comenzar  
  
> [!WARNING]  
> No intente aplicar una revisión de sistema de la plataforma de análisis si su aplicación o cualquier componente de dispositivo está desconectado o está en un error sobre el estado. En ese caso, póngase en contacto con soporte técnico para obtener ayuda.  
  
> [!WARNING]  
> No se aplica una revisión de sistema de la plataforma de análisis mientras el dispositivo está en uso. Aplicar una revisión para hacer que los nodos de dispositivo que se va a reiniciar. La revisión se debe aplicar durante una ventana de mantenimiento cuando el dispositivo no esté en uso.  
  
### <a name="prerequisites"></a>Prerequisites  
Para llevar a cabo estos pasos, necesitará:  
  
-   Un inicio de sesión de sistema de la plataforma de análisis con permisos para tener acceso a la consola de administración para supervisar el estado del dispositivo. <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   Conocimiento de la cuenta de administrador de dominio del tejido para conectarse a la *< nombreDeDominio >***-HST01** nodo.  
  
## <a name="HowToInstallPDW"></a>Para aplicar una revisión de sistema de la plataforma de análisis  
A diferencia de las actualizaciones de Microsoft, las revisiones para el software del sistema de la plataforma de análisis no se controlan a través de WSUS. Tienen un flujo de trabajo diferente y se instalan mediante la ejecución de un paquete de revisión.  
  
1.  **Compruebe los indicadores de estado de dispositivo.**  
  
    1.  Abra la consola de administración y vaya a la página de estado de dispositivo. Para obtener más información, vea [supervisar el dispositivo mediante la consola de administración &#40; Sistema de la plataforma de análisis &#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
    2.  Todos los indicadores de color rojo o amarillos se deben resolver antes de continuar con el paso siguiente. Algunas excepciones a esto son:  
  
        -   Si hay errores de disco, use la página de alertas de la consola de administrador para comprobar que hay no más de un error de disco en cada servidor o la matriz de SAN. Si se produce el error de no más de un disco en cada servidor o la matriz de SAN, puede continuar con el paso siguiente antes de corregir los errores de disco. Asegúrese de ponerse en contacto con soporte técnico de Microsoft para corregir los errores de disco tan pronto como sea posible.  
  
        -   Si se produce un error de volumen de disco (amarillo) no crítico que no está en la unidad C:\, puede continuar con el paso siguiente antes de resolver el error de volumen de disco.  
  
2.  **Instale la revisión de sistema de la plataforma de análisis**  
  
    1.  Inicie sesión en el <*appliance_domain*>-nodo HST01 como administrador del dominio.  
  
    2.  Use la **ejecutar como administrador** opción para abrir un símbolo del sistema.  
  
    3.  Ejecute el comando siguiente, reemplazando  *<HotfixPackageName>*  con el nombre del paquete ejecutable de la revisión y reemplazando los demás elementos de marcador de posición *< >* con la información adecuada.  
  
        ```  
        <HotfixPackageName> /DomainAdminPassword="<password>"  
        ```  
  
    4.  Siga los pasos tal como se presenta mediante el paquete de revisión.  
  
## <a name="see-also"></a>Vea también  
[Descargue y aplique las actualizaciones de Microsoft &#40; Sistema de la plataforma de análisis &#41;](download-and-apply-microsoft-updates.md)  
[Desinstalar las actualizaciones de Microsoft &#40; Sistema de la plataforma de análisis &#41;](uninstall-microsoft-updates.md)  
[Desinstalar las revisiones del sistema de plataforma de análisis &#40; Sistema de la plataforma de análisis &#41;](uninstall-analytics-platform-system-hotfixes.md)  
[Mantenimiento de software &#40; Sistema de la plataforma de análisis &#41;](software-servicing.md)  
  
