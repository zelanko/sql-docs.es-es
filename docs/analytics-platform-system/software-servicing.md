---
title: Servicio de software
description: Servicio de software en Analytics Platform System (APS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4325dfa9c16edba12c2bba694b47c1b0875c7c6f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "74400315"
---
# <a name="software-servicing-in-analytics-platform-system"></a>Servicio de software en Analytics Platform System
En esta sección se resumen los requisitos de servicio de software para los dispositivos de sistema de plataforma de análisis, incluidas las revisiones de WSUS y análisis de plataforma de la plataforma.  
  
## <a name="software-servicing-basics"></a><a name="Basics"></a>Aspectos básicos del servicio de software  
**WSUS:** El dispositivo de análisis de plataforma de Analytics debe configurarse para recibir actualizaciones de Windows Server Update Services (WSUS). Estas actualizaciones incluyen cambios importantes en el software del dispositivo. Una vez configuradas, muchas actualizaciones se instalarán automáticamente y no requieren la administración práctica. Normalmente, las actualizaciones de WSUS se configuran durante el paso [configurar Windows Server Update Services &#40;wsus&#41; &#40;Analytics Platform System&#41;](configure-windows-server-update-services-wsus.md) realizada durante la configuración de la nueva aplicación. Si no es así, este paso de configuración se puede realizar más adelante. Para obtener información sobre WSUS, consulte la [Guía del sitio web de WSUS](https://go.microsoft.com/fwlink/?LinkId=202417).  
  
**Revisiones:** Además, es posible que tenga que aplicar revisiones de Analytics Platform System. Una *revisión* es una actualización de software que se crea para un cliente específico con el fin de resolver un problema con el software de sistema de la plataforma de análisis. Cada revisión es un archivo ejecutable que instala la corrección para el problema específico del cliente. Cada revisión también contiene una acumulación de todas las actualizaciones de software publicadas anteriormente para Windows, SQL Server y Analytics Platform System. Si necesita instalar una revisión, el soporte técnico de Microsoft le proporcionará la revisión y las instrucciones.  
  
**Ámbito de las actualizaciones:** La aplicación de una revisión o Service Pack al sistema de análisis de plataforma debe desconectar todo el dispositivo.  
  
**Adaptador de destino de SSIS y herramientas de cliente:** Al aplicar una revisión que incluye los cambios en el MSI del adaptador de destino de SSIS o en las herramientas de cliente, los archivos MSI se actualizarán en el directorio **C:\PDWINST\ClientTools** del nodo de control. La revisión no instala automáticamente los componentes de los archivos MSI actualizados. Para actualizar esos componentes, el cliente debe desinstalar las versiones anteriores de los componentes e instalar las nuevas versiones desde los archivos MSI actualizados. Al desinstalar una revisión que incluye cambios en el MSI del adaptador de destino de SSIS o en las herramientas de cliente MSI, los archivos MSI para esos componentes se revertirán a las versiones anteriores. Para revertir los componentes a una versión anterior, el cliente debe desinstalar las versiones existentes (más recientes) de los componentes y volver a instalar las versiones anteriores de los archivos MSI revertidos.  
  
## <a name="software-servicing-topics"></a>Temas de servicio de software  
En los temas siguientes se describe cómo administrar el servicio de mantenimiento de software en el dispositivo:  
  
-   [Descargar y aplicar actualizaciones de Microsoft &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)  
  
-   [Desinstale Microsoft Updates &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
  
-   [Aplicación de revisiones de Analytics Platform System &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
  
-   [Desinstalación de las revisiones de Analytics Platform System &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
