---
title: Software antivirus
description: Si el centro de datos requiere un software antivirus, siga estas instrucciones para instalar el software antivirus en Analytics Platform System (APS). Se recomienda no instalar el software antivirus a menos que sea un requisito firme de su centro de datos.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/24/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: c3687b839e52e64350591402c3aa19e9c2c54ac7
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401470"
---
# <a name="antivirus-software-for-analytics-platform-system-aps"></a>Software antivirus para Analytics Platform System (APS)
Si el centro de datos requiere un software antivirus, siga estas instrucciones para instalar el software antivirus en Analytics Platform System. Se recomienda no instalar el software antivirus a menos que sea un requisito firme de su centro de datos.  
  
> [!WARNING]  
> Le recomendamos encarecidamente que evalúe individualmente el riesgo de seguridad para cada equipo y para el sistema de plataforma de análisis en su conjunto y que seleccione las herramientas adecuadas para el nivel de riesgo de seguridad de cada equipo. Además, se recomienda que antes de implementar cualquier proyecto de protección antivirus, pruebe todo el sistema con una carga completa para medir los cambios de estabilidad y rendimiento.  
>   
> El software de protección antivirus requiere que se ejecuten algunos recursos del sistema. Debe realizar pruebas antes y después de instalar el software antivirus para determinar si hay algún efecto de rendimiento en el sistema Analytics Platform System.  
  
Este tema se basa en las instrucciones de [Cómo elegir el software antivirus que se va a ejecutar en los equipos que ejecutan SQL Server](https://support.microsoft.com/kb/309422) y el [artículo de KB 961804](https://support.microsoft.com/kb/961804/en-us).  
  
## <a name="exclusion-list-for-physical-hosts"></a>Lista de exclusión para hosts físicos  
Para instalar el software antivirus en los hosts físicos, excluya la siguiente lista de directorios y procesos. No se deben analizar mediante el software antivirus.  
  
**Excluya estos directorios:**  
  
-   C:\ProgramData\Microsoft\Windows\Hyper-V: directorio de configuración de máquina virtual  
  
-   C:\Users\Public\Documents\Hyper-V\Virtual discos duros-directorio de unidad de disco duro virtual predeterminado  
  
-   C:\clusterStorage: directorios de unidad de disco duro virtual  
  
**Excluya estos procesos:**  
  
-   Administración de máquinas virtuales (vMMS. exe)  
  
-   Procesos de trabajo de las máquinas virtuales (VMWP. exe)  
  
## <a name="exclusion-list-for-virtual-machines-vms"></a>Lista de exclusión para Virtual Machines (VM)  
Para instalar el software antivirus en las máquinas virtuales, excluya la siguiente lista de directorios y archivos. No se deben analizar mediante el software antivirus.  
  
**_PDW_region_CTL01**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
**_appliance_domain_-AD01** y ** _appliance_domain_-AD02**  
  
-   Sin restricciones  
  
**Máquinas virtuales de nodo de proceso**  
  
-   C:\windows\cluster\  
  
-   G:\  
  
**_appliance_domain_-VMM**  
  
-   Sin restricciones  
  
**_appliance_domain_-WDS**  
  
-   Sin restricciones  
  
**_appliance_domain_ISCSI01**  
  
-   C:\iscsitarget  
  
## <a name="see-also"></a>Véase también  
[Tareas de administración de dispositivos &#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
