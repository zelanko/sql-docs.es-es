---
title: Alta disponibilidad de sistema de la plataforma de análisis
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: Describe cómo Analytics Platform System (APS) se ha diseñado para lograr alta disponibilidad.
ms.date: 10/20/2016
ms.topic: article
ms.assetid: 5ab245e9-0316-4d25-a626-4745ce856925
caps.latest.revision: 9
ms.openlocfilehash: 9fd057a4cd673f06034e0093ca93be7ceaf345ea
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="analytics-platform-system-high-availability"></a>Alta disponibilidad de sistema de la plataforma de análisis
Describe cómo Analytics Platform System (APS) se ha diseñado para lograr alta disponibilidad.  
  
## <a name="high-availability-architecture"></a>Arquitectura de alta disponibilidad  
![La arquitectura del dispositivo](media/appliance-architecture.png "la arquitectura del dispositivo")  
  
## <a name="network"></a>Red  
Disponibilidad de la red, el dispositivo de APS tiene dos redes InfiniBand. Si una de las redes InfiniBand deja de funcionar, el otro se sigue estando disponible. Además, Active Directory ha replicado los controladores de dominio para resolver las solicitudes entrantes a la red InfiniBand correcta.  
  
Para obtener más información, consulte [adaptadores de red InfiniBand configurar](configure-infiniband-network-adapters.md).  
  
## <a name="storage"></a>Almacenamiento  
Para conservar los datos seguros, APS utiliza RAID 1 para mantener dos copias de todos los datos de usuario de creación de reflejo. Cuando se produce un error en un disco, el sistema de hardware vuelve a generar los datos en un disco de repuesto y establece una alerta que hay un error de disco.  
  
Para mantener los datos disponibles en línea, APS usa espacios de almacenamiento de Windows y volúmenes compartidos de clúster para administrar los discos de datos de usuario en el almacenamiento de conexión directa. Hay un grupo de almacenamiento por unidad de escala de datos que se organizan en volúmenes compartidos de clúster que están disponibles para los hosts de nodo de proceso a través de puntos de montaje.  
  
Para asegurarse de que el bloque de almacenamiento permanece en línea, cada host en la unidad de escala de datos tiene una máquina virtual ISCSI que no lo hará. Esta arquitectura es importante porque si se produce un error en un host, los datos aún están accesibles a través de los otros hosts en la unidad de escala de datos.  
  
## <a name="hosts"></a>Hosts  
Disponibilidad de host, todos los hosts se configuran en un clúster de conmutación por error de Windows. Cada bastidor tiene un host pasivo. Opcionalmente, el primer bastidor, que controla el almacenamiento de datos paralelos (PDW) de SQL Server y el tejido de dispositivo, puede tener un segundo host pasivo. Si se produce un error en un host, máquinas virtuales que están configuradas para la conmutación por error, conmutará por error a un host disponible pasivo.  
  
## <a name="pdw-nodes-and-appliance-fabric"></a>Nodos PDW y el tejido de dispositivo  
Para lograr alta disponibilidad de los nodos PDW y del tejido de dispositivo, APS utiliza la virtualización. Cada uno de los componentes del tejido PDW y la aplicación se ejecute en una máquina virtual.  
  
Cada máquina virtual se define como un rol en el clúster de conmutación por error de Windows. Cuando se produce un error en una máquina virtual, el clúster reinicia en un host disponible pasivo. Las máquinas virtuales se implementan mediante System Center Virtual Machine Manager. Cuando se produce una conmutación por error, la máquina virtual que se ejecuta en el host pasivo es todavía puede tener acceso a sus datos de usuario a través de la red InfiniBand.  
  
El nodo de Control y máquinas virtuales de nodo de proceso se configuran como un clúster de nodo único. El clúster de nodo único administra las redes InfiniBand como recurso de clúster para asegurarse de que el clúster siempre usa la active InfiniBand dirección IP. El clúster de nodo único administra los procesos PDW que se ejecutan dentro de la máquina virtual. Por ejemplo, el clúster de nodo único tiene SQL Server y servicio de movimiento de datos (DMS) como recursos de modo que puede iniciar en el orden correcto. El nodo de Control de máquina virtual también controla el orden de inicio para las máquinas virtuales que se ejecutan en el host de orquestación.  
  
