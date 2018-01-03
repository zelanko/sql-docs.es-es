---
title: Software de servicio (Analytics Platform System)
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
ms.assetid: cec4d924-c88f-470c-84bb-0af3e21aabf1
caps.latest.revision: "33"
ms.openlocfilehash: 8435291233a9486632f3d26ecae90c4bf1be8e21
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="software-servicing"></a>Mantenimiento de software
En esta sección resume lo requisitos para dispositivos de sistema de la plataforma de análisis, incluidas las revisiones de WSUS y de sistema de la plataforma de análisis de mantenimiento de software.  
  
## <a name="Basics"></a>Conceptos básicos de mantenimiento de software  
**WSUS:** su dispositivo Analytics Platform System debe configurarse para recibir actualizaciones de Windows Server Update Services (WSUS). Estas actualizaciones incluyen cambios importantes en el software del dispositivo. Después de que se configuraron, muchas actualizaciones se instalarán automáticamente y no requieren ninguna administración práctica. Normalmente, se configuran las actualizaciones WSUS durante la [configurar Windows Server Update Services &#40; WSUS &#41; &#40; Sistema de la plataforma de análisis &#41; ](configure-windows-server-update-services-wsus.md) paso se realiza durante la nueva configuración de dispositivo. De lo contrario, este paso de configuración puede realizarse más adelante. Para obtener información sobre WSUS, consulte la [sitio Web de WSUS guía](http://go.microsoft.com/fwlink/?LinkId=202417).  
  
**Revisiones:** Además, puede que necesite aplicar las revisiones del sistema de la plataforma de análisis. A *revisión* es una actualización de software que se crea para que un cliente específico resolver un problema con el software del sistema de la plataforma de análisis. Todas las revisiones es un archivo ejecutable que instala la corrección del problema específico del cliente. Todas las revisiones también contiene una acumulación de todas las actualizaciones de software publicadas anteriormente para Windows, SQL Server y Analytics Platform System. Si necesita instalar una revisión, soporte técnico de Microsoft le proporcionará la revisión e instrucciones.  
  
**Ámbito de las actualizaciones:** aplicar una revisión o un service pack a Analytics Platform System debe desconectar el dispositivo completo. Es decir, se verán afectadas las regiones PDW tanto de HDInsight.  
  
**Adaptador de destino de SSIS y las herramientas de cliente:** al aplicar una revisión que incluye cambios en el adaptador de MSI SSIS destino o MSI de herramientas de cliente, los archivos MSI se actualizarán en el **C:\PDWINST\ClientTools** directorio en el nodo de Control. La revisión no instala automáticamente los componentes de los archivos MSI actualizados. Para actualizar estos componentes, el cliente debe desinstalar las versiones anteriores de los componentes e instalar las nuevas versiones de los archivos MSI actualizados. Cuando se desinstala una revisión que incluye cambios en el adaptador de MSI SSIS destino o MSI de herramientas de cliente, los archivos MSI para dichos componentes se revertirán a las versiones anteriores. Para revertir los componentes a una versión anterior, el cliente debe desinstalar las versiones existentes (más recientes) de los componentes y vuelva a instalar las versiones anteriores de los archivos MSI revertidas.  
  
## <a name="software-servicing-topics"></a>Temas de mantenimiento de software  
Los temas siguientes describen cómo administrar el mantenimiento de software en el dispositivo:  
  
-   [Descargue y aplique las actualizaciones de Microsoft &#40; Sistema de la plataforma de análisis &#41;](download-and-apply-microsoft-updates.md)  
  
-   [Desinstalar las actualizaciones de Microsoft &#40; Sistema de la plataforma de análisis &#41;](uninstall-microsoft-updates.md)  
  
-   [Aplicar las revisiones del sistema de plataforma de análisis &#40; Sistema de la plataforma de análisis &#41;](apply-analytics-platform-system-hotfixes.md)  
  
-   [Desinstalar las revisiones del sistema de plataforma de análisis &#40; Sistema de la plataforma de análisis &#41;](uninstall-analytics-platform-system-hotfixes.md)  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
