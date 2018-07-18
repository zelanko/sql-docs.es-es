---
title: Mantenimiento de software - Analytics Platform System | Microsoft Docs
description: Software de mantenimiento en Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 79231b6e2867154bc4d826b83a0a4fd27487f438
ms.sourcegitcommit: 731c5aed039607a8df34c63e780d23a8fac937e1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/07/2018
ms.locfileid: "37909805"
---
# <a name="software-servicing-in-analytics-platform-system"></a>Mantenimiento de software en Analytics Platform System
En esta sección se resume el software de los requisitos para dispositivos de Analytics Platform System, incluidas las revisiones de WSUS y Analytics Platform System de mantenimiento.  
  
## <a name="Basics"></a>Conceptos básicos de mantenimiento de software  
**WSUS:** la aplicación Analytics Platform System debe configurarse para recibir actualizaciones de Windows Server Update Services (WSUS). Estas actualizaciones incluyen cambios importantes en el software del dispositivo. Una vez configurados, muchas actualizaciones, se instalarán automáticamente y no requieren administración práctica. Normalmente, se configuran las actualizaciones WSUS durante la [configurar Windows Server Update Services &#40;WSUS&#41; &#40;Analytics Platform System&#41; ](configure-windows-server-update-services-wsus.md) paso realizado durante la instalación de dispositivo nuevo. De lo contrario, se puede realizar este paso de configuración más adelante. Para obtener información acerca de WSUS, consulte el [sitio Web de WSUS guía](http://go.microsoft.com/fwlink/?LinkId=202417).  
  
**Revisiones:** Además, puede que necesite aplicar revisiones de Analytics Platform System. Un *revisión* es una actualización de software que se crea para que un cliente específico resolver un problema con el software de Analytics Platform System. Todas las revisiones es un archivo ejecutable que instala la corrección del problema específico del cliente. Todas las revisiones también contiene una acumulación de todas las actualizaciones de software publicadas anteriormente para Windows, SQL Server y Analytics Platform System. Si necesita instalar una revisión, soporte técnico de Microsoft le proporcionará la revisión e instrucciones.  
  
**Ámbito de las actualizaciones:** aplicar una revisión o service pack para el sistema Analytics Platform System debe desconectar el dispositivo completo.  
  
**Adaptador de destino de SSIS y herramientas de cliente:** al aplicar una revisión que incluye los cambios realizados en el adaptador de MSI SSIS destino o MSI de herramientas de cliente, se actualizarán los archivos MSI en la **C:\PDWINST\ClientTools** directorio en el nodo de Control. La revisión no instala automáticamente los componentes de los archivos actualizados de MSI. Para actualizar los componentes, el cliente debe desinstalar las versiones anteriores de los componentes e instalar las nuevas versiones de los archivos actualizados de MSI. Cuando se desinstala una revisión que incluye los cambios realizados en el adaptador de MSI SSIS destino o MSI de herramientas de cliente, los archivos MSI esos componentes, se revertirá a las versiones anteriores. Para revertir los componentes a una versión anterior, el cliente debe desinstalar las versiones existentes (más recientes) de los componentes y vuelva a instalar las versiones anteriores de los archivos MSI revertidas.  
  
## <a name="software-servicing-topics"></a>Temas de mantenimiento de software  
Los temas siguientes describen cómo administrar el mantenimiento de software en el dispositivo:  
  
-   [Descargue y aplique las actualizaciones de Microsoft &#40;Analytics Platform System&#41;](download-and-apply-microsoft-updates.md)  
  
-   [Desinstalar las actualizaciones de Microsoft &#40;Analytics Platform System&#41;](uninstall-microsoft-updates.md)  
  
-   [Aplicar las revisiones de Analytics Platform System &#40;Analytics Platform System&#41;](apply-analytics-platform-system-hotfixes.md)  
  
-   [Desinstalar las revisiones de Analytics Platform System &#40;Analytics Platform System&#41;](uninstall-analytics-platform-system-hotfixes.md)  
  
<!-- MISSING LINKS ## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
