---
title: "Componentes de hardware del sistema de la plataforma de análisis"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "Analytics Platform System (APS) usa componentes escalables de forma que puede comprar la cantidad correcta de procesamiento y almacenamiento según sus requisitos empresariales."
ms.date: 10/20/2016
ms.topic: article
ms.assetid: aa1cdcc7-cfee-4658-bbce-7d319bfb7483
caps.latest.revision: "17"
ms.openlocfilehash: cd58b4a7afb2f69081b99a884d3b0f32b194097a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="analytics-platform-system-hardware-components"></a>Componentes de hardware del sistema de la plataforma de análisis

Analytics Platform System (APS) usa componentes escalables de forma que puede comprar la cantidad correcta de procesamiento y almacenamiento según sus requisitos empresariales. Cuando realice el pedido APS, necesitará una combinación de estos componentes principales del hardware. Fabricantes de hardware específicos pueden usar distintas convenciones de nomenclatura o tener componentes adicionales.  
 
  
## <a name="rackandnetwork"></a>Bastidor y red 
 
Todos los componentes de puntos de acceso se almacenan en uno o varios bastidores que caben en el centro de datos. Cada bastidor incluye dos conmutadores de Ethernet, dos conmutadores de InfiniBand y unidades de distribución de energía (PDU).  
  
![Bastidor y red](media/rack-and-network.png "AP bastidor y red")  
  
## <a name="datascaleunit"></a>Unidad de escala de datos
 
Una unidad de escala de datos contiene los hosts de datos y el almacenamiento de conexión directa (DAS) para procesar y almacenar los datos de usuario. Para agregar capacidad de agregar unidades de escala de datos según las configuraciones que son compatibles con el proveedor de hardware. A medida que aumenta el número de unidades de escala de datos, debe agregar bastidor adicional & componentes de red, según sea necesario, para proporcionar más energía, red y bastidor infraestructura.  
  
### <a name="data-host"></a>Host de datos  

Un host de datos es un servidor dedicado a procesar los datos de usuario. Almacenamiento de datos paralelo (PDW) se ejecuta uno de los nodos de proceso en cada host de datos. Para dispositivos de HPE, la unidad de escala de datos tiene dos hosts de datos. Para dispositivos de Dell y cuantos, la unidad de escala de datos tiene tres hosts de datos.  
  
### <a name="direct-attached-storage"></a>Almacenamiento de conexión directa
 
El almacenamiento de conexión directa (DAS) es un grupo de discos conectados a los hosts de datos. Todos los hosts de datos pueden tener acceso a cualquiera de los discos. Como parte de la nada compartido arquitectura, los nodos de proceso que se ejecuta en los hosts de datos no comparten discos individuales. Sin embargo, para lograr alta disponibilidad, el acceso de almacenamiento es compartido y cada uno de los hosts de datos puede tener acceso a cualquiera de los discos.  
  
### <a name="data-scale-unit-architecture---dell-and-quanta"></a>Arquitectura de unidad de escala datos - DELL y Quanta
  
![Unidad de escalabilidad](media/scalability-unit-dell.png "unidad de escalabilidad de Dell")  
  
### <a name="data-scale-unit-architecture---hpe"></a>Arquitectura de unidad de escala de datos - HPE 
 
![Unidad de escalabilidad de HPE](media/scalability-unit-hpe.png "unidad de escalabilidad HPE")  
  
### <a name="data-scale-unit-description"></a>Descripción de la unidad de datos escala

Una unidad de escala de datos tiene un servidor (host) para cada nodo de proceso y la matriz de un disco conectado directamente que está asociado con Serial Attached SCSI (SAS). En el contenedor de almacenamiento, la matriz de discos se divide en dos mitades cada uno con fuentes de alimentación redundantes. Espacios de almacenamiento de Windows Server para administrar datos de usuario, duplicar datos entre pares de disco reflejado RAID 1. Los discos en cada par de disco se almacenan en diferentes mitades de la matriz de discos.  
  
La matriz de discos también contiene discos de reserva activa y un disco del sistema. Si se produce un error en un disco, espacios de almacenamiento utiliza la copia en buen estado de los datos en el disco funcione para volver a generar una copia duplicada de los datos en una reserva activa. Se trata de una importante capacidad de reparación automática que ayuda a proteger contra la pérdida de datos.  
  
El número total de discos para los nodos de proceso:  
  
-   DELL tiene discos de 96 = (3 servidores) * (16 discos por servidor) \* (2 discos redundante).  
  
-   HPE tiene 64 discos = (2 servidores) * (16 discos por servidor) \* (2 discos redundante).  
  
-   Además, cada matriz de discos tiene discos de reserva activa y un disco del sistema.  
  
**Para lograr alta disponibilidad**, cuando un proceso se produce un error en el nodo sobre ella puede siguen funcionando y tener acceso a sus datos de usuario a través de lo otro host en la unidad de escala de datos. Al menos uno de los hosts físicos conectados directa debe funcionar o se pierde el acceso de datos en el almacenamiento.  
  
**Para tamaños de disco**, el almacenamiento de conexión directa puede tener 1, 2 ó 3 unidades de disco de Terabyte. Todas las unidades de escala de datos deben tener discos del mismo tamaño.  
  
## <a name="basescaleunit"></a>Unidad básica de escala 
 
La unidad de escala Base contiene el número mínimo de energía cerebro hosts, hosts de datos y almacenamiento de conexión directa que se requiere para el dispositivo. Incluye estos componentes.  
  
### <a name="orchestration-host"></a>host de orquestación  
Este servidor ejecuta el cerebro de PDW.
  
### <a name="passive-host"></a>host pasivo  
Este servidor proporciona alta disponibilidad. Es en línea y está listo para ejecutar trabajos en caso de que hay un error en la orquestación o un host de datos. El host de orquestación, pasivo host y servidores de la unidad de escala de datos se configuran como un clúster de conmutación por error de Windows. Cada bastidor en el dispositivo requiere un host pasivo.  
  
### <a name="optional-passive-host"></a>host pasivo opcional  
Para agregar más redundancia, tiene la opción para agregar un segundo host pasivo a la unidad de escala de Base.  
  
### <a name="data-scale-unit"></a>Unidad de escala de datos  
La unidad de escala Base incluye una unidad de escala de datos que se coloca en la parte inferior del bastidor.  
  
Este diagrama muestra la unidad de escala de Base más el bastidor y red. Se trata de la configuración mínima para un dispositivo de sistema de la plataforma de análisis.  
  
![Unidad básica de escala](media/base-scale-unit.png "unidad de escalado de Base")  
 
