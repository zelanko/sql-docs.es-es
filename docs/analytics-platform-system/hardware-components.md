---
title: Componentes de hardware
description: Analytics Platform System (APS) usa componentes escalables para que pueda comprar la cantidad adecuada de procesamiento y almacenamiento según sus requisitos empresariales. Cuando se ordenan los APS, se necesita una combinación de estos componentes de hardware básicos.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: db9966315d60fd4de1de7ae6805620d3f2144e6f
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401145"
---
# <a name="hardware-components-for-analytics-platform-system"></a>Componentes de hardware para Analytics Platform System

Analytics Platform System (APS) usa componentes escalables para que pueda comprar la cantidad adecuada de procesamiento y almacenamiento según sus requisitos empresariales. Cuando se ordenan los APS, se necesita una combinación de estos componentes de hardware básicos. Los proveedores de hardware específicos podrían usar distintas convenciones de nomenclatura o tener componentes adicionales.  
 
  
## <a name="rackandnetwork"></a>Bastidor y red 
 
Todos los componentes de APS se almacenan en uno o varios bastidores que caben en el centro de datos. Cada bastidor incluye unidades de distribución de energía (PDU), dos conmutadores InfiniBand y dos conmutadores Ethernet.  
  
![Bastidor y red](media/rack-and-network.png "Bastidor y red de APS")  
  
## <a name="datascaleunit"></a>Unidad de escalado de datos
 
Una unidad de escalado de datos contiene los hosts de datos y el almacenamiento de conexión directa (DAS) para procesar y almacenar los datos de usuario. Para agregar capacidad, agregue unidades de escalado de datos según las configuraciones admitidas por el proveedor de hardware. A medida que aumenta el número de unidades de escalado de datos, debe agregar más componentes de red & bastidor, según sea necesario, para proporcionar más energía, red e infraestructura de bastidor.  
  
### <a name="data-host"></a>Host de datos  

Un host de datos es un servidor dedicado a procesar los datos de usuario. El almacenamiento de datos paralelos (PDW) ejecuta un nodo de proceso en cada host de datos. En el caso de los dispositivos HPE, la unidad de escalado de datos tiene dos hosts de datos. En el caso de los dispositivos Dell y Quanta, la unidad de escalado de datos tiene tres hosts de datos.  
  
### <a name="direct-attached-storage"></a>Almacenamiento con conexión directa
 
El almacenamiento de conexión directa (DAS) es un grupo de discos conectados a los hosts de datos. Todos los hosts de datos pueden tener acceso a cualquiera de los discos. Como parte de la arquitectura de nada compartida, los nodos de proceso que se ejecutan en los hosts de datos no comparten discos individuales. Sin embargo, para lograr alta disponibilidad, se comparte el acceso al almacenamiento y cada uno de los hosts de datos puede tener acceso a cualquiera de los discos.  
  
### <a name="data-scale-unit-architecture---dell-and-quanta"></a>Arquitectura de unidad de escalado de datos (DELL y cuantos)
  
![Unidad de escalabilidad](media/scalability-unit-dell.png "Unidad de escalabilidad de Dell")  
  
### <a name="data-scale-unit-architecture---hpe"></a>Arquitectura de unidad de escalado de datos: HPE 
 
![Unidad de escalabilidad de HPE](media/scalability-unit-hpe.png "Unidad de escalabilidad de HPE")  
  
### <a name="data-scale-unit-description"></a>Descripción de la unidad de escalado de datos

Una unidad de escalado de datos tiene un servidor (host) para cada nodo de proceso y una matriz de discos de conexión directa que está conectada con el SCSI conectado en serie (SAS). Dentro del contenedor de almacenamiento, la matriz de discos se divide en dos mitades que tienen fuentes de alimentación redundantes. Los espacios de almacenamiento de Windows Server administran datos de usuario mediante la duplicación de datos entre pares de discos reflejados RAID 1. Los discos de cada par de discos se almacenan en las mitades diferentes de la matriz de discos.  
  
La matriz de discos también contiene discos de reserva activa y un disco del sistema. Si se produce un error en un disco, espacios de almacenamiento usa la copia correcta de los datos en el disco en funcionamiento para recompilar una copia duplicada de los datos en una reserva activa. Se trata de una funcionalidad importante de recuperación automática que ayuda a proteger contra la pérdida de datos.  
  
El número total de discos para los nodos de proceso:  
  
-   DELL tiene 96 discos = (3 servidores) * (16 discos por servidor) \* (2 para discos redundantes).  
  
-   HPE tiene 64 discos = (2 servidores) * (16 discos por servidor) \* (2 para discos redundantes).  
  
-   Además, cada matriz de discos tiene discos de reserva activa y un disco del sistema.  
  
**Para lograr una alta disponibilidad**, cuando un nodo de proceso conmuta por error, puede seguir funcionando y obtener acceso a sus datos de usuario a través del otro host en la unidad de escala de datos. Al menos uno de los hosts físicos de conexión directa debe estar funcionando o se perderá el acceso a los datos del almacenamiento.  
  
**En el caso de los tamaños de disco**, el almacenamiento con conexión directa puede tener una unidad de disco de 1, 2 o 3 terabytes. Todas las unidades de escalado de datos deben tener discos del mismo tamaño.  
  
## <a name="basescaleunit"></a>Unidad de escala base 
 
La unidad de escala base contiene el número mínimo de hosts de potencia de cerebro, hosts de datos y almacenamiento conectado directo que se requiere para el dispositivo. Incluye los componentes siguientes. 
  
### <a name="orchestration-host"></a>Host de orquestación  
Este servidor ejecuta el cerebro de PDW.
  
### <a name="passive-host"></a>Host pasivo  
Este servidor proporciona alta disponibilidad. Está en línea y listo para ejecutar trabajos en caso de que se produzca un error en la orquestación o el host de datos. El host de orquestación, el host pasivo y los servidores de unidad de escala de datos están configurados como un clúster de conmutación por error de Windows. Cada bastidor del dispositivo requiere un host pasivo.  
  
### <a name="optional-passive-host"></a>Host pasivo opcional  
Para agregar más redundancia, tiene la opción de agregar un segundo host pasivo a la unidad de escala base.  
  
### <a name="data-scale-unit"></a>Unidad de escalado de datos  
La unidad de escala base incluye una unidad de escalado de datos que se coloca en la parte inferior del bastidor.  
  
Este diagrama muestra la unidad de escala base más el bastidor y la red. Esta es la configuración mínima para un dispositivo de sistema de plataforma de análisis.  
  
![Unidad de escala base](media/base-scale-unit.png "Unidad de escala base")  
 
