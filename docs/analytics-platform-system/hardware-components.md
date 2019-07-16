---
title: 'Componentes de hardware: Analytics Platform System | Microsoft Docs'
description: Analytics Platform System (APS) usa componentes escalables para que la cantidad adecuada de procesamiento y almacenamiento, puede comprar según sus requisitos empresariales. Cuando el pedido de APS, necesitará una combinación de estos componentes de hardware principales.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 0f7f3bd8f4d5500a59675d40ff7f50d1afd9a199
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960887"
---
# <a name="hardware-components-for-analytics-platform-system"></a>Componentes de hardware para Analytics Platform System

Analytics Platform System (APS) usa componentes escalables para que la cantidad adecuada de procesamiento y almacenamiento, puede comprar según sus requisitos empresariales. Cuando el pedido de APS, necesitará una combinación de estos componentes de hardware principales. Fabricantes de hardware específico podrían usar las convenciones de nomenclatura diferentes o tiene componentes adicionales.  
 
  
## <a name="rackandnetwork"></a>Bastidor y red 
 
Componentes de puntos de acceso se almacenan en uno o varios bastidores que encajan en su centro de datos. Cada bastidor incluye unidades de distribución de energía (PDU), los dos conmutadores de InfiniBand y dos conmutadores de Ethernet.  
  
![Bastidor y red](media/rack-and-network.png "APS en bastidor y red")  
  
## <a name="datascaleunit"></a>Unidad de escalado de datos
 
Una unidad de escalado de datos contiene los hosts de datos y almacenamiento de conexión directa (DAS) para el procesamiento y almacenamiento de datos de usuario. Para agregar la capacidad de agregar unidades de escalado de datos según las configuraciones que son compatibles con el fabricante del hardware. A medida que crece el número de unidades de escala de datos, deberá agregar bastidor adicional & componentes de red, según sea necesario, para proporcionar más de alimentación, red y la infraestructura en bastidor.  
  
### <a name="data-host"></a>Host de datos  

Un host de datos es un servidor dedicado a procesar los datos de usuario. Almacenamiento de datos paralelos (PDW) se ejecuta un nodo de proceso en cada host de datos. Para dispositivos HPE, la unidad de escalado de datos tiene dos hosts de datos. Dell y cuantos dispositivos, la unidad de escalado de datos tiene tres hosts de datos.  
  
### <a name="direct-attached-storage"></a>Almacenamiento de conexión directa
 
El almacenamiento de conexión directa (DAS) es un grupo de discos conectados a los hosts de datos. Todos los hosts de datos pueden tener acceso a ninguno de los discos. Como parte de la nada compartido arquitectura, los nodos de proceso que se ejecutan en los hosts de datos no comparten los discos individuales. Sin embargo, para lograr alta disponibilidad, se comparte el acceso de almacenamiento y cada uno de los hosts de datos puede tener acceso a ninguno de los discos.  
  
### <a name="data-scale-unit-architecture---dell-and-quanta"></a>Arquitectura de unidad de escala datos - cuantos y DELL
  
![Unidad de escalabilidad](media/scalability-unit-dell.png "unidad de escalabilidad de Dell")  
  
### <a name="data-scale-unit-architecture---hpe"></a>Arquitectura de unidad de escalado de datos - HPE 
 
![Unidad de escalabilidad de HPE](media/scalability-unit-hpe.png "unidad HPE escalabilidad")  
  
### <a name="data-scale-unit-description"></a>Descripción de la unidad de datos de escalado

Una unidad de escalado de datos tiene un servidor (host) para cada nodo de proceso y una conexión directa de discos que se adjunta con Serial Attached SCSI (SAS). En el contenedor de almacenamiento, la matriz de discos se divide en dos mitades cada uno con fuentes de alimentación redundantes. Espacios de almacenamiento de Windows Server administra los datos de usuario mediante la desduplicación de datos a través de pares de disco reflejado RAID 1. Los discos en cada par de disco se almacenan en mitades diferentes de la matriz de discos.  
  
La matriz de discos también contiene discos de reserva activa y un disco del sistema. Si se produce un error en un disco, espacios de almacenamiento utiliza la copia correcta de los datos en el disco funcionando para volver a generar una copia duplicada de los datos en una reserva activa. Se trata de una importante capacidad de recuperación automática que ayuda a proteger contra la pérdida de datos.  
  
El número total de discos para los nodos de proceso:  
  
-   DELL tiene 96 discos = (3 servidores) * (16 discos por servidor) \* (2 discos redundantes).  
  
-   HPE tiene 64 discos = (2 servidores) * (16 discos por servidor) \* (2 discos redundantes).  
  
-   Además, cada matriz de discos tiene discos de reserva activa y un disco del sistema.  
  
**Para lograr alta disponibilidad**, cuando un nodo de proceso conmuta por error, puede acceder a los datos de usuario a través de otro host en la unidad de escalado de datos y siguen funcionando. Al menos uno de los hosts físicos conectados directos debe funcionar o se pierde el acceso de datos al almacenamiento.  
  
**Para tamaños de disco**, el almacenamiento conectado directo puede tener 1, 2 o 3 unidades de disco de Terabyte. Todas las unidades de escala de datos deben tener los discos del mismo tamaño.  
  
## <a name="basescaleunit"></a>Unidad de escala base 
 
La unidad de escalado de Base contiene el número mínimo de cerebro power hosts, hosts de datos y almacenamiento de conexión directa que se requiere para el dispositivo. Incluye los siguientes componentes. 
  
### <a name="orchestration-host"></a>Host de orquestación  
Este servidor ejecuta el cerebro de PDW.
  
### <a name="passive-host"></a>Host pasivo  
Este servidor proporciona alta disponibilidad. Está conectado y listo para ejecutar trabajos en caso de que hay un error en la orquestación o un host de datos. El host de orquestación, pasivo host y servidores de la unidad de escala de datos se configuran como un clúster de conmutación por error de Windows. Cada bastidor en el dispositivo requiere un host pasivo.  
  
### <a name="optional-passive-host"></a>Host pasivo opcional  
Para agregar aún más la redundancia, tiene la opción para agregar un segundo host pasivo a la unidad de escalado de Base.  
  
### <a name="data-scale-unit"></a>Unidad de escalado de datos  
La unidad de escalado de Base incluye una unidad de escalado de datos que se coloca en la parte inferior del bastidor.  
  
Este diagrama muestra la unidad de escalado de Base más el bastidor y red. Se trata de la configuración mínima para un dispositivo de Analytics Platform System.  
  
![Unidad de escala base](media/base-scale-unit.png "unidad de escalado de Base")  
 
