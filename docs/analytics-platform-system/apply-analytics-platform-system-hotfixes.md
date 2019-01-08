---
title: Aplicar revisiones de Analytics Platform System | Microsoft Docs
description: En este artículo se describe cómo aplicar las revisiones para el software de Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: b4b72017bb23ae44da9c5884f0ebf2a8b099fd3e
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52531653"
---
# <a name="apply-analytics-platform-system-hotfixes"></a>Aplicación de las revisiones de Analytics Platform System
En este artículo se describe cómo aplicar las revisiones para el software de Analytics Platform System.  
  
## <a name="before-you-begin"></a>Antes de empezar  
  
> [!WARNING]  
> No intente aplicar una revisión de Analytics Platform System si su dispositivo o cualquier componente de dispositivo está desconectado o está en un error sobre el estado. En ese caso, póngase en contacto con soporte técnico para obtener ayuda.  
  
> [!WARNING]  
> No aplique una revisión de Analytics Platform System mientras el dispositivo está en uso. Aplicar una revisión para hacer que los nodos del dispositivo se reinicie. La revisión se debe aplicar durante una ventana de mantenimiento cuando no se usa el dispositivo.  
  
### <a name="prerequisites"></a>Requisitos previos  
Para llevar a cabo estos pasos, necesitará:  
  
-   Un inicio de sesión de Analytics Platform System con permisos para tener acceso a la consola de administración para supervisar el estado del dispositivo. <!-- MISSING LINKS See [Grant Permissions to Use the Admin Console &#40;SQL Server PDW&#41;](../sqlpdw/grant-permissions-to-use-the-admin-console-sql-server-pdw.md).  -->  
  
-   Conocimiento de la cuenta de administrador de dominio del tejido para conectarse a la _< nombreDeDominio >_**-HST01** nodo.  
  
## <a name="HowToInstallPDW"></a>Para aplicar una revisión de Analytics Platform System  
A diferencia de las actualizaciones de Microsoft, las revisiones para el software de Analytics Platform System no se controlan a través de WSUS. Tienen un flujo de trabajo diferentes y se instalan mediante la ejecución de un paquete de revisión.  
  
1.  **Compruebe los indicadores de estado del dispositivo.**  
  
    1.  Abra la consola de administración y navegue a la página de estado del dispositivo. Para obtener más información, consulte [supervisar el dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
    2.  Todos los indicadores rojos o amarillos se deben resolver antes de continuar con el paso siguiente. Dos excepciones a esto son:  
  
        -   Si hay errores de disco, use la página de alertas de la consola de administrador para comprobar que no más de un error de disco en cada servidor o una matriz de SAN. Si se produce un error de no más de un disco en cada servidor o una matriz de SAN, puede continuar con el paso siguiente antes de corregir los errores de disco. Asegúrese de ponerse en contacto con soporte técnico de Microsoft para corregir los errores de disco tan pronto como sea posible.  
  
        -   Si se produce un error de volumen de disco (amarillo) no críticas que no está en la unidad C:\, puede continuar con el paso siguiente antes de resolver el error de volumen de disco.  
  
2.  **Instale la revisión de Analytics Platform System**  
  
    1.  Inicie sesión en el <*appliance_domain*>-nodo HST01 como administrador del dominio.  
  
    2.  Use la **ejecutar como administrador** opción para abrir un símbolo del sistema.  
  
    3.  Ejecute el siguiente comando, reemplazando *<HotfixPackageName>* con el nombre del paquete ejecutable de la revisión y reemplazando los demás elementos de marcador de posición *< >* con la información adecuada.  
  
        ```  
        <HotfixPackageName> /DomainAdminPassword="<password>"  
        ```  
  
    4.  Siga los pasos tal como se presenta el paquete de revisión.  
  
## <a name="see-also"></a>Vea también  
[Descargue y aplique las actualizaciones de Microsoft &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)  
[Desinstalar las actualizaciones de Microsoft &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
[Desinstalar las revisiones de Analytics Platform System &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
[Mantenimiento de software &#40;Analytics Platform System&#41;](software-servicing.md)  
  
