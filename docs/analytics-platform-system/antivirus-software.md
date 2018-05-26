---
title: El software antivirus - Analytics Platform System | Documentos de Microsoft
description: Si su centro de datos requiere el software antivirus, siga estas instrucciones para instalar el software antivirus en el sistema de la plataforma de análisis. Se recomienda no instalar el software antivirus a menos que sea un requisito estricto de su centro de datos.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5d9ff6848d2df43408613d41dc7a0e6f8c1b0b8c
ms.sourcegitcommit: fc3cd23685c6b9b6972d6a7bab2cc2fc5ebab5f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/25/2018
---
# <a name="antivirus-software-for-analytics-platform-system"></a>Software antivirus para Analytics Platform System
Si su centro de datos requiere el software antivirus, siga estas instrucciones para instalar el software antivirus en el sistema de la plataforma de análisis. Se recomienda no instalar el software antivirus a menos que sea un requisito estricto de su centro de datos.  
  
> [!WARNING]  
> Se recomienda encarecidamente que individualmente evaluar el riesgo de seguridad para cada equipo y de sistema de la plataforma de análisis como un todo, y seleccionar las herramientas adecuadas para el nivel de riesgo para la seguridad de cada equipo. Además, se recomienda que antes de implementar cualquier proyecto de protección antivirus, probar todo el sistema soporta una carga completa para medir los cambios en la estabilidad y rendimiento.  
>   
> Software de protección antivirus requiere algunos recursos del sistema para ejecutar. Debe realizar pruebas antes y después de instalar el software antivirus para determinar si hay cualquier impacto en el sistema de la plataforma de análisis de rendimiento.  
  
En este tema se basa en las instrucciones de [cómo elegir el software antivirus para que se ejecute en equipos que ejecutan SQL Server](http://support.microsoft.com/kb/309422) y [961804 de artículo de KB](http://support.microsoft.com/kb/961804/en-us).  
  
## <a name="exclusion-list-for-physical-hosts"></a>Lista de exclusión para Hosts físicos  
Para instalar el software antivirus en los hosts físicos, excluya la siguiente lista de directorios y procesos. No se explorará mediante el software antivirus.  
  
**Excluir estos directorios:**  
  
-   C:\ProgramData\Microsoft\Windows\Hyper-V - directorio de configuración de máquina Virtual  
  
-   Discos duros C:\Users\Public\Documents\Hyper-V\Virtual - directorio predeterminado de la unidad de disco duro virtual  
  
-   C:\clusterStorage - directorios de la unidad de disco duro Virtual  
  
**Excluir estos procesos:**  
  
-   Administración de máquinas virtuales (Vmms.exe)  
  
-   Procesos de trabajo de máquina virtual (Vmwp.exe)  
  
## <a name="exclusion-list-for-virtual-machines-vms"></a>Lista de exclusión para máquinas virtuales (VM)  
Para instalar el software antivirus en las máquinas virtuales, excluya la siguiente lista de directorios y archivos. No se explorará mediante el software antivirus.  
  
***PDW_region *-CTL01**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
***appliance_domain *-AD01** y ***appliance_domain *-AD02**  
  
-   Sin restricciones  
  
**Máquinas virtuales de nodos de proceso**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
***appliance_domain*-VMM**  
  
-   Sin restricciones  
  
***appliance_domain*-WDS**  
  
-   Sin restricciones  
  
***appliance_domain*-ISCSI01**  
  
-   C:\iscsitarget  
  
## <a name="see-also"></a>Vea también  
[Tareas de administración de dispositivo &#40;sistema de la plataforma de análisis&#41;](appliance-management-tasks.md)  
  
