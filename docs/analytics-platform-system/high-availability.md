---
title: Alta disponibilidad en Analytics Platform System | Microsoft Docs
description: Obtenga información sobre cómo Analytics Platform System (APS) está diseñado para lograr alta disponibilidad.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: cdf1837bd3b3b1cdf8e189ae591cd6fbff58387a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960863"
---
# <a name="analytics-platform-system-high-availability"></a>Alta disponibilidad de Analytics Platform System
Obtenga información sobre cómo Analytics Platform System (APS) está diseñado para lograr alta disponibilidad.  
  
## <a name="high-availability-architecture"></a>Arquitectura de alta disponibilidad  
![Arquitectura del dispositivo](media/appliance-architecture.png "arquitectura del dispositivo")  
  
## <a name="network"></a>red  
Disponibilidad de la red, el dispositivo APS tiene dos redes InfiniBand. Si una de las redes InfiniBand deja de funcionar, el otro se sigue estando disponible. Además, Active Directory ha replicado los controladores de dominio para resolver las solicitudes entrantes a la red InfiniBand correcta.  
  
Para obtener más información, consulte [adaptadores de red InfiniBand configurar](configure-infiniband-network-adapters.md).  
  
## <a name="storage"></a>Almacenamiento  
Para mantener seguros los datos, puntos de acceso utiliza RAID 1 para mantener dos copias de todos los datos de usuario de creación de reflejo. Cuando se produce un error en un disco, el sistema de hardware regenera los datos en un disco de repuesto y establece una alerta que hay un error de disco.  
  
Para mantener los datos disponibles en línea, APS usa espacios de almacenamiento de Windows y volúmenes compartidos en clúster para administrar los discos de datos de usuario en el almacenamiento de conexión directa. Hay un grupo de almacenamiento por unidad de escalado de datos que se organizan en volúmenes compartidos de clúster que están disponibles para los hosts de nodo de proceso a través de puntos de montaje.  
  
Para asegurarse de que el bloque de almacenamiento permanece en línea, cada host en la unidad de escalado de datos tiene una máquina virtual de ISCSI que realiza la conmutación por error. Esta arquitectura es importante porque si se produce un error en un host, los datos están siendo accesibles a través de los otros hosts en la unidad de escalado de datos.  
  
## <a name="hosts"></a>Hosts  
Para la disponibilidad del host, todos los hosts se configuran en un clúster de conmutación por error de Windows. Cada bastidor tiene un host pasivo. El primer bastidor, que controla el almacenamiento de datos paralelos (PDW) de SQL Server y el tejido de dispositivo, puede tener opcionalmente un segundo host pasivo. Si se produce un error en un host, las máquinas virtuales que están configuradas para la conmutación por error, conmutará por error a un host disponible pasivo.  
  
## <a name="pdw-nodes-and-appliance-fabric"></a>Nodos PDW y el tejido de dispositivo  
Para la alta disponibilidad de los nodos PDW y el tejido del dispositivo APS utiliza la virtualización. Cada uno de los componentes del dispositivo y de PDW fabric se ejecute en una máquina virtual.  
  
Cada máquina virtual se define como un rol en el clúster de conmutación por error de Windows. Cuando se produce un error en una máquina virtual, el clúster reinicia en un host disponible pasivo. Las máquinas virtuales se implementan mediante System Center Virtual Machine Manager. Cuando se produce una conmutación por error, la máquina virtual que se ejecuta en el host pasivo es siguen teniendo acceso a sus datos de usuario a través de la red InfiniBand.  
  
El nodo de Control y las máquinas virtuales de nodo de proceso se configuran como un clúster de nodo único. El clúster de nodo único administra las redes InfiniBand como un recurso de clúster para asegurarse de que el clúster siempre usa la IP de InfiniBand active. El clúster de nodo único administra los procesos PDW que se ejecutan dentro de la máquina virtual. Por ejemplo, el clúster de nodo único tiene SQL Server y el servicio de movimiento de datos (DMS) como recursos de modo que puede iniciarlos en el orden correcto. El nodo de Control de máquina virtual también controla el orden de inicio para las máquinas virtuales que se ejecutan en el host de orquestación.  
  
