---
title: Software antivirus - Analytics Platform System | Microsoft Docs
description: Si su centro de datos requiere un software antivirus, use estas instrucciones para instalar el software antivirus en Analytics Platform System. Se recomienda no instalar el software antivirus a menos que sea un requisito firme de su centro de datos.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2bf94fb04bd6f96de019c7e8543b8a626cebe439
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51699133"
---
# <a name="antivirus-software-for-analytics-platform-system"></a>Software antivirus para Analytics Platform System
Si su centro de datos requiere un software antivirus, use estas instrucciones para instalar el software antivirus en Analytics Platform System. Se recomienda no instalar el software antivirus a menos que sea un requisito firme de su centro de datos.  
  
> [!WARNING]  
> Se recomienda encarecidamente que evaluar individualmente el riesgo de seguridad para cada equipo y Analytics Platform System, como un todo, y que seleccione las herramientas que son adecuadas para el nivel de riesgo de seguridad de cada equipo. Además, se recomienda que antes de implementar cualquier proyecto de protección contra virus, probar todo el sistema bajo una carga completa para medir los cambios en la estabilidad y rendimiento.  
>   
> Software antivirus requiere algunos recursos del sistema para ejecutar. Debe realizar pruebas antes y después de instalar el software antivirus para determinar si hay cualquier impacto en el sistema de plataforma de análisis de rendimiento.  
  
En este tema se basa en las instrucciones de [cómo elegir software antivirus se ejecuten en equipos que ejecutan SQL Server](https://support.microsoft.com/kb/309422) y [961804 de artículo de KB](https://support.microsoft.com/kb/961804/en-us).  
  
## <a name="exclusion-list-for-physical-hosts"></a>Lista de exclusión para Hosts físicos  
Para instalar el software antivirus en los hosts físicos, excluya la siguiente lista de directorios y procesos. No se explorará el software antivirus.  
  
**Excluir estos directorios:**  
  
-   C:\ProgramData\Microsoft\Windows\Hyper-V - directorio de configuración de máquina Virtual  
  
-   Discos duros C:\Users\Public\Documents\Hyper-V\Virtual - directorio predeterminado de la unidad de disco duro virtual  
  
-   C:\clusterStorage - directorios de la unidad de disco duro Virtual  
  
**Excluir estos procesos:**  
  
-   Administración de máquinas virtuales (Vmms.exe)  
  
-   Procesos de trabajo de máquina virtual (Vmwp.exe)  
  
## <a name="exclusion-list-for-virtual-machines-vms"></a>Lista de exclusión para máquinas virtuales (VM)  
Para instalar el software antivirus en las máquinas virtuales, excluya la siguiente lista de directorios y archivos. No se explorará el software antivirus.  
  
***PDW_region *-CTL01**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
***appliance_domain *-AD01** y ***appliance_domain *-AD02**  
  
-   Sin restricciones  
  
**Máquinas virtuales de nodo de proceso**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
***appliance_domain*-VMM**  
  
-   Sin restricciones  
  
***appliance_domain*-WDS**  
  
-   Sin restricciones  
  
***appliance_domain*-ISCSI01**  
  
-   C:\iscsitarget  
  
## <a name="see-also"></a>Vea también  
[Tareas de administración de dispositivo &#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
