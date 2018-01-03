---
title: "Componentes físicos de PDW y el tejido de dispositivo (Analytics Platform System)"
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
ms.assetid: 7748d3da-0b7c-4ec6-9c22-4897758ba573
caps.latest.revision: "17"
ms.openlocfilehash: 95e80aaa641b04391d96b55f7491e21f1a30b6d1
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="pdw-and-appliance-fabric-physical-components"></a>Componentes físicos PDW y el tejido de dispositivo
Nombres y descripciones para los componentes físicos del tejido PDW y dispositivo. La región de PDW contiene todos estos componentes.  
  
<!-- MISSING LINKS See also [HDInsight Physical Components &#40;Analytics Platform System&#41;](hdinsight-physical-components.md).  -->  
  
## <a name="diagrams"></a>Diagramas de componentes  
Muestra los nombres de los componentes físicos y donde se encuentran en el primer bastidor de un dispositivo de nodo de proceso de 6.  
  
![Nombre de componente de región PDW - HP](./media/pdw-and-appliance-fabric-physical-components/APS_HW_ComponentNames-HP.png "APS_HW_ComponentNames HP")  
  
El nombre real para los componentes PDW es el nombre de región PDW, seguido por un guión, seguido por el nombre del componente. Por ejemplo, si el nombre de la región de PDW es PDW123, los nombres reales son **PDW123 CTL01**, **PDW123 CMP01**, etcetera.  
  
De forma similar, el nombre real de los componentes del tejido de dispositivo es el dominio del equipo, seguido por un guión, seguido por el nombre del componente. Por ejemplo, si el dominio del equipo es FSW123, el tejido de dispositivo las máquinas virtuales son **FSW123 WDS**, **FSW123 AD01**, **FSW123 VMM**, etcetera.  
  
Esta es una vista consolidada de una región PDW con 6 nodos de ejecución.  
  
![Los nombres de componente PDW](./media/pdw-and-appliance-fabric-physical-components/APS_HW_Names.png "APS_HW_Names")  
  
## <a name="pdw"></a>Componentes PDW  
Las máquinas virtuales PDW son parte de la región de PDW.  
  
*PDW_region*-CTL01  
Una máquina virtual que ejecuta el nodo de Control. Esto se ejecuta en HST01 y puede conmutar por error a HST02.  
  
> [!WARNING]  
> PDW de SQL Server no admite la creación de una instantánea de la máquina virtual de CTL01 mediante el Administrador de Hyper-V. Las instantáneas se basan en almacenamiento local, lo que provocará errores si trata de la máquina virtual conmute por error a su copia de seguridad. Crear una instantánea también puede causar problemas de confiabilidad con otra VM que conmutan por error en el servidor pasivo.  
  
*PDW_region*-CMP01 a través de *PDW_Region*-CMP06  
Una máquina virtual que ejecuta el nodo de proceso. En este diagrama de nodos de proceso de 6, los hosts HSA01 a través de HSA06 Ejecutar proceso nodo CMP01 de máquinas virtuales a través de CMP06 respectivamente.  
  
## <a name="fabric"></a>Componentes del tejido de dispositivo  
Estos componentes forman parte del tejido de dispositivo.  
  
### <a name="virtual-machines"></a>Máquinas virtuales  
*appliance_domain*- WDS  
Este hosts de máquina virtual de servicios de implementación de Windows (WDS), que utiliza el sistema de la plataforma de análisis de implementación sistemas operativos Windows a través de la red del dispositivo. También hospeda el servicio DHCP, que permite a los hosts de dispositivo para unirse a la red de dispositivo sin necesidad de una dirección IP configurada previamente.  
  
El *appliance_domain*máquina virtual de - WDS se ejecuta en HST01 y puede conmutar por error a HST02. La máquina virtual WDS y la máquina virtual VMM, debe implementar Windows en los hosts físicos durante la instalación del dispositivo. Durante el ciclo de vida del dispositivo, WDS y VMM realizar operaciones como el reemplazo de un host.  
  
*appliance_domain*- VMM  
Virtual Machine Manager (VMM) se ejecuta en una máquina virtual y puede conmutar por error a HST02. VMM hospeda System Center para implementar el sistema operativo en los hosts físicos. VMM también proporciona servicios de Windows Server Update Services (WSUS) para aplicar o quitar las actualizaciones de Windows en todos los hosts y máquinas virtuales.  
  
*appliance_domain*-AD01, *appliance_domain*-AD02  
Servicios de dominio de Active Directory, contiene el sistema de nombres de dominio (DNS), se ejecuta en una máquina virtual en HST01 y HST02. Para lograr alta disponibilidad del dispositivo, AD01 y AD02 son controladores de dominio replicados y lo hacen no conmutación por error. Si se produce un error en uno, el otro se ya está disponible con los datos correctos.  
  
*appliance_domain*-ISCSI01  
Una máquina virtual ISCSI se ejecuta en cada uno de los hosts con almacenamiento conectado (HSA01 HSA06). Esta máquina virtual no lo hará.  
  
### <a name="hosts"></a>Hosts  
*appliance_domain*-HST01 a través de *appliance_domain*-HST06  
Los hosts para las máquinas virtuales PDW Control nodo y la aplicación fabric. HST03 es un host pasivo opcional.  
  
*appliance_domain*-HSA01 a través de *appliance_domain*-HSA08  
Los hosts con almacenamiento conectado (HSA). Cada nodo de ejecución una máquina virtual de HAS host se ejecuta y otra VM ISCSI.  
  
### <a name="cluster-for-pdw"></a>Clúster de PDW  
*appliance_domain*-WFOHST01  
El clúster PDW se denomina WFOHST01. Administra todos los hosts físicos y máquinas virtuales que pertenecen a PDW.  
  
### <a name="direct-attached-storage"></a>Almacenamiento con conexión directa  
*appliance_domain*-DAS01 a través de *appliance_domain*-DAS03  
Esto es el almacenamiento de conexión directa que está conectado a los nodos de proceso. HP tiene uno DAS para cada dos nodos de proceso. Dell y cuantos tienen uno DAS para cada tres nodos de proceso.  
  
## <a name="see-also"></a>Vea también  
<!-- MISSING LINKS [Hardware Configurations &#40;Analytics Platform System&#41;](../architecture/hardware-configurations.md)  -->  
[Configuración de dispositivo &#40; Sistema de la plataforma de análisis &#41;](appliance-configuration.md)  
[Tareas de administración de dispositivo &#40; Sistema de la plataforma de análisis &#41;](appliance-management-tasks.md)  
  
