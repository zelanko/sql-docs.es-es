---
title: Grupos de disponibilidad de escalado de lectura | Microsoft Docs
ms.custom: 
ms.date: 04/11/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 9
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 6dfa046a07b9fd5a3eddbe474b5ea63c1163c26c
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="read-scale-availability-groups"></a>Grupos de disponibilidad de escalado de lectura
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

Aparte de que reúne lo mejor de las características de alta disponibilidad para SQL Server, un grupo de disponibilidad es una solución completa que proporciona también soluciones de escalado integradas. En una aplicación de base de datos típica, hay varios clientes que ejecutan diferentes tipos de cargas de trabajo y, a veces, esto puede provocar cuellos de botella debido a las restricciones de recursos. En este sentido, se pueden liberar recursos y lograr un mayor rendimiento de la carga de trabajo OLTP o proporcionar un mayor rendimiento y escalabilidad en las cargas de trabajo de solo lectura. Para conseguirlo, se puede usar la tecnología de replicación más rápida existente para SQL Server: crear un grupo de bases de datos replicadas para descargar las cargas de trabajo de informes y análisis en las réplicas de solo lectura. 

Con Grupos de disponibilidad, una o varias réplicas secundarias se pueden configurar para admitir el acceso de solo lectura a las bases de datos secundarias.

Las aplicaciones cliente que ejecutan cargas de trabajo de informes o análisis pueden conectarse directamente a las bases de datos secundarias. El cliente también puede configurar una lista de enrutamiento de solo lectura y conectarse a la réplica principal, que reenviará la solicitud de conexión a cada una de las réplicas secundarias de la lista de enrutamiento con el método round robin.

## <a name="read-scale-availability-groups-without-cluster"></a>Grupos de disponibilidad de escalado de lectura sin clúster

En [!INCLUDE[sssql15-md](..\..\..\includes\sssql15-md.md)] y versiones anteriores, todos los grupos de disponibilidad necesitaban un clúster. Ese clúster proporciona continuidad del negocio: alta disponibilidad y recuperación ante desastres (HADR). Además, las réplicas secundarias se podían configurar para operaciones de lectura. Configurar un clúster y ponerlo en funcionamiento acarreaba una enorme sobrecarga operativa cuando la alta disponibilidad no era el objetivo. SQL Server 2017 incluye los grupos de disponibilidad de escalado de lectura sin un clúster. 

Si el requisito empresarial es conservar los recursos para las cargas de trabajo más importantes que se ejecutan en la réplica principal, ahora puede usarse el enrutamiento de solo lectura o conectarse directamente a las réplicas secundarias legibles, sin depender de la integración con ninguna tecnología de agrupación en clústeres. Estas nuevas funciones están disponibles en sistemas SQL Server 2017 que se ejecutan en plataformas tanto Windows como Linux.

>[!IMPORTANT]
>Esto no es una configuración de alta disponibilidad; no hay ninguna infraestructura que supervise y coordine la detección de errores y la conmutación automática por error. Si hay usuarios que necesitan funciones de HADR, use un Administrador de clúster (WSFC en Windows o Pacemaker en Linux). 

## <a name="use-distributed-availability-groups-for-geographic-read-scale"></a>Usar grupos de disponibilidad distribuidos de escalado de lectura geográfico

Las soluciones separadas geográficamente pueden implementar soluciones de escalado de lectura con grupos de disponibilidad distribuidos. Esto permite descargar las cargas de trabajo de lectura desde la réplica principal en réplicas secundarias legibles que están más cerca del origen de las cargas de trabajo de lectura. Esto no solo reduce el uso de recursos en la réplica principal, sino que contribuye también a mejorar el rendimiento de lectura, ya que la latencia de red disminuye y se saca partido de los recursos dedicados.

Un único grupo de disponibilidad distribuido puede tener hasta 17 réplicas secundarias legibles. Para incrementar la capacidad de escalado, cree una cadena de margarita con varios grupos de disponibilidad y aumente el número de réplicas legibles más aún. También puede implementar dos grupos de disponibilidad distribuidos desde un mismo grupo de disponibilidad para las lecturas de baja latencia en entornos geográficamente dispersos.




## <a name="next-steps"></a>Pasos siguientes 

[Configure read-scale availability group on Linux](../../../linux/sql-server-linux-availability-group-configure-rs.md) (Configurar un grupo de disponibilidad de escalado de lectura en Linux)

## <a name="see-also"></a>Vea también  
 [Información general de los grupos de disponibilidad AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  

