---
title: Alta disponibilidad
description: Obtenga información sobre cómo Analytics Platform System (APS) está diseñado para lograr alta disponibilidad.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 6246ed25909a2e366d8bbafcd912a4fd923cc84a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401102"
---
# <a name="analytics-platform-system-high-availability"></a>Alta disponibilidad de Analytics Platform System
Obtenga información sobre cómo Analytics Platform System (APS) está diseñado para lograr alta disponibilidad.  
  
## <a name="high-availability-architecture"></a>Arquitectura de alta disponibilidad  
![Arquitectura del dispositivo](media/appliance-architecture.png "Arquitectura del dispositivo")  
  
## <a name="network"></a>Red  
En cuanto a la disponibilidad de la red, el dispositivo APS tiene dos redes InfiniBand. Si una de las redes InfiniBand deja de funcionar, la otra sigue estando disponible. Además, Active Directory ha replicado controladores de dominio para resolver las solicitudes entrantes en la red InfiniBand correcta.  
  
Para obtener más información, consulte [configuración de adaptadores de red InfiniBand](configure-infiniband-network-adapters.md).  
  
## <a name="storage"></a>Storage  
Para mantener la seguridad de los datos, APS utiliza la creación de reflejo RAID 1 para mantener dos copias de todos los datos de usuario. Cuando se produce un error en un disco, el sistema de hardware vuelve a generar los datos en un disco de reserva y establece una alerta que indica que hay un error de disco.  
  
Para mantener los datos disponibles en línea, APS usa espacios de almacenamiento de Windows y volúmenes compartidos en clúster para administrar los discos de datos del usuario en el almacenamiento de conexión directa. Hay un grupo de almacenamiento por unidad de escala de datos organizados en volúmenes compartidos de clúster que están disponibles para los hosts del nodo de proceso a través de puntos de montaje.  
  
Para asegurarse de que el grupo de almacenamiento permanece en línea, cada host de la unidad de escalado de datos tiene una máquina virtual ISCSI que no realiza la conmutación por error. Esta arquitectura es importante porque, si se produce un error en un host, todavía se puede obtener acceso a los datos a través de los otros hosts de la unidad de escala de datos.  
  
## <a name="hosts"></a>Hosts  
Para la disponibilidad del host, todos los hosts se configuran en un clúster de conmutación por error de Windows. Cada bastidor tiene un host pasivo. Opcionalmente, el primer bastidor, que controla SQL Server almacenamiento de datos paralelo (PDW) y el tejido del dispositivo, puede tener un segundo host pasivo. Si se produce un error en un host, las máquinas virtuales configuradas para la conmutación por error se conmutarán por error a un host pasivo disponible.  
  
## <a name="pdw-nodes-and-appliance-fabric"></a>Nodos de PDW y fabric de dispositivo  
Para lograr una alta disponibilidad de los nodos PDW y el tejido del dispositivo, APS usa la virtualización. Cada uno de los componentes de PDW y de fabric de dispositivo se ejecuta en una máquina virtual.  
  
Cada máquina virtual se define como un rol en el clúster de conmutación por error de Windows. Cuando se produce un error en una máquina virtual, el clúster la reinicia en un host pasivo disponible. Las máquinas virtuales se implementan mediante System Center Virtual Machine Manager. Cuando se produce una conmutación por error, la máquina virtual que se ejecuta en el host pasivo sigue pudiendo acceder a sus datos de usuario a través de la red InfiniBand.  
  
Las máquinas virtuales de nodo de control y de nodo de proceso se configuran como un clúster de un solo nodo. El clúster de un solo nodo administra las redes InfiniBand como un recurso de clúster para asegurarse de que el clúster siempre usa la dirección IP de InfiniBand activa. El clúster de un solo nodo administra los procesos de PDW que se ejecutan dentro de la máquina virtual. Por ejemplo, el clúster de un solo nodo tiene SQL Server y el servicio de movimiento de datos (DMS) como recursos para que pueda iniciarlos en el orden adecuado. La VM de nodo de control también controla el orden de inicio de las otras máquinas virtuales que se ejecutan en el host de orquestación.  
  
