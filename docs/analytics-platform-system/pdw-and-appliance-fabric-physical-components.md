---
title: Componentes físicos del dispositivo
description: Nombres y descripciones de los componentes físicos de PDW y Appliance fabric.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 5cbed66f53189668518e04848002ae69adb8c614
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400922"
---
# <a name="appliance-physical-components---analytics-platform-system"></a>Componentes físicos del dispositivo: Analytics Platform System
Nombres y descripciones de los componentes físicos de PDW y Appliance fabric. 
  
<!-- MISSING LINKS See also [HDInsight Physical Components &#40;Analytics Platform System&#41;](hdinsight-physical-components.md).  -->  
  
## <a name="diagrams"></a>Diagramas de componentes  
Esto muestra los nombres de los componentes físicos y dónde se encuentran en el primer bastidor de un dispositivo de seis nodos de proceso.  
  
![Nombres de componente de región PDW, HP](./media/pdw-and-appliance-fabric-physical-components/APS_HW_ComponentNames-HP.png "APS_HW_ComponentNames-HP")  
  
El nombre real de los componentes de PDW es el nombre de la región de PDW, seguido de un guión, seguido del nombre del componente. Por ejemplo, si el nombre de la región de PDW es PDW123, los nombres reales son **PDW123-CTL01**, **PDW123-CMP01**, etc.  
  
Del mismo modo, el nombre real de los componentes del tejido del dispositivo es el dominio de la aplicación, seguido de un guión, seguido del nombre del componente. Por ejemplo, si el dominio del dispositivo es FSW123, las máquinas virtuales del tejido de aplicación son **FSW123-WDS**, **FSW123-AD01**, **FSW123-VMM**, etc.  
  
Esta es una vista consolidada de una región de PDW con seis nodos de proceso.  
  
![Nombre de componente PDW](./media/pdw-and-appliance-fabric-physical-components/APS_HW_Names.png "APS_HW_Names")  
  
## <a name="pdw"></a>Componentes de PDW  
Las máquinas virtuales de PDW forman parte de la región de PDW.  
  
*PDW_region*CTL01  
Una máquina virtual que ejecuta el nodo de control. Se ejecuta en HST01 y puede conmutar por error a HST02.  
  
> [!WARNING]  
> PDW de SQL Server no admite la creación de una instantánea de la máquina virtual CTL01 mediante el administrador de Hyper-V. Las instantáneas se basan en el almacenamiento local, lo que provocará errores si la máquina virtual intenta conmutar por error a su copia de seguridad. La creación de una instantánea también puede provocar problemas de confiabilidad con las demás máquinas virtuales que conmutan por error al servidor pasivo.  
  
*PDW_region*-CMP01 a *PDW_Region*-CMP06  
Una máquina virtual que ejecuta el nodo de proceso. En este diagrama de seis nodos de proceso, el hospeda HSA01 a través de HSA06 ejecutar máquinas virtuales de nodo de proceso CMP01 a CMP06, respectivamente.  
  
## <a name="fabric"></a>Componentes del tejido del dispositivo  
Estos componentes forman parte del tejido del dispositivo.  
  
### <a name="virtual-machines"></a>Virtual Machines  
*appliance_domain*-WDS  
Esta máquina virtual hospeda servicios de implementación de Windows (WDS), que usa el sistema de plataforma de análisis para implementar sistemas operativos Windows a través de la red del dispositivo. También aloja el servicio DHCP, que permite que los hosts del dispositivo se unan a la red del dispositivo sin tener una dirección IP configurada previamente.  
  
La máquina virtual *appliance_domain*-WDS se ejecuta en HST01 y puede conmutar por error a HST02. La máquina virtual de WDS y la máquina virtual de VMM implementan Windows en los hosts físicos durante la instalación del dispositivo. Durante el ciclo de vida del dispositivo, WDS y VMM realizan operaciones como reemplazar un host.  
  
*appliance_domain*-VMM  
El Virtual Machine Manager (VMM) se ejecuta en una máquina virtual y puede conmutar por error a HST02. VMM hospeda System Center para implementar el sistema operativo en los hosts físicos. VMM también proporciona Windows Server Update Services (WSUS) para aplicar o quitar actualizaciones de Windows en todos los hosts y máquinas virtuales.  
  
*appliance_domain*-AD01, *appliance_domain*-AD02  
Active Directory Domain Services, que contiene el sistema de nombres de dominio (DNS), se ejecuta en una máquina virtual tanto en HST01 como en HST02. Para lograr una alta disponibilidad del dispositivo, AD01 y AD02 son controladores de dominio replicados y no realizan la conmutación por error. Si se produce un error en uno, el otro ya está disponible con los datos correctos.  
  
*appliance_domain*ISCSI01  
Una máquina virtual ISCSI se ejecuta en cada uno de los hosts con almacenamiento conectado (HSA01-HSA06). Esta máquina virtual no realiza la conmutación por error.  
  
### <a name="hosts"></a>Hosts  
*appliance_domain*-HST01 a *appliance_domain*-HST06  
Los hosts para el nodo de control de PDW y las máquinas virtuales de fabric de dispositivo. HST03 es un host pasivo opcional.  
  
*appliance_domain*-HSA01 a *appliance_domain*-HSA08  
Los hosts con almacenamiento conectado (HSA). Cada una de ellas tiene un host que ejecuta una máquina virtual de nodo de proceso y una máquina virtual ISCSI.  
  
### <a name="cluster-for-pdw"></a>Clúster para PDW  
*appliance_domain*WFOHST01  
El clúster de PDW se denomina WFOHST01. Administra todos los hosts físicos y las máquinas virtuales que pertenecen a PDW.  
  
### <a name="direct-attached-storage"></a>Almacenamiento con conexión directa  
*appliance_domain*-DAS01 a *appliance_domain*-DAS03  
Este es el almacenamiento de conexión directa que está conectado a los nodos de proceso. HP tiene un DAS por cada dos nodos de proceso. Dell y cuantos tienen un DAS por cada tres nodos de proceso.  
  
## <a name="see-also"></a>Consulte también  
<!-- MISSING LINKS [Hardware Configurations &#40;Analytics Platform System&#41;](../architecture/hardware-configurations.md)  -->  
[Configuración del dispositivo &#40;Analytics Platform System&#41;](appliance-configuration.md)  
[Tareas de administración de dispositivos &#40;Analytics Platform System&#41;](appliance-management-tasks.md)  
  
