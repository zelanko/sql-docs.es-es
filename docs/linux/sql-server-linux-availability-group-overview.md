---
title: Grupo de disponibilidad AlwaysOn para SQL Server en Linux | Documentos de Microsoft
description: 
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 06/14/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: e37742d4-541c-4d43-9ec7-a5f9b2c0e5d1
ms.workload: On Demand
ms.openlocfilehash: 2b9d80b92fd189340c5c15504ab37a8c0022df85
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="availability-groups-for-sql-server-on-linux"></a>Grupos de disponibilidad para SQL Server en Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Un grupo de disponibilidad AlwaysOn de SQL Server es una alta disponibilidad (HA), recuperación ante desastres (DR) y solución de escalado horizontal. Proporciona alta disponibilidad para los grupos de bases de datos de almacenamiento de conexión directa. Admite varias secundarias para alta disponibilidad integrada y recuperación ante desastres, la detección de errores automática, conmutación por error rápida transparente y equilibrio de carga de lectura. Este amplio conjunto de capacidades permite lograr una disponibilidad óptima SLA para las cargas de trabajo.

Grupos de disponibilidad de SQL Server se introdujeron en SQL Server 2012 y se han mejorado con cada versión. Esta característica está disponible en Linux. Para dar cabida a cargas de trabajo de SQL Server con los requerimientos de continuidad de negocio rigurosas, ejecutan grupos de disponibilidad en todos los admitidos [distribuciones de Linux OS](sql-server-linux-release-notes.md). Asimismo, todas las funcionalidades que forman una solución de recuperación ante desastres de alta disponibilidad flexible, integrada y eficaz de los grupos de disponibilidad también están disponibles en Linux. Estos incluyen: 

- **Conmutación por error de varias bases de datos** un grupo de disponibilidad admite un entorno de conmutación por error para un conjunto de bases de datos de usuario, conocidas como bases de datos de disponibilidad.
- **La rápida conmutación por error y la detección de errores** como un recurso en un clúster de alta disponibilidad, un grupo de disponibilidad se beneficia de inteligencia de clúster integrados para la detección de conmutación por error inmediata y la acción de conmutación por error.
- **Conmutación por error transparente mediante el recurso de IP virtual** cliente permite usar cadena de conexión única a principal en caso de conmutación por error. Requiere la integración con un administrador de clústeres.
- **Varias secundarias sincrónicas y asincrónicas** un grupo de disponibilidad admite hasta ocho réplicas secundarias. Espera a que la réplica principal con réplicas sincrónicas para confirmar la transacción de que la réplica principal espera a que las transacciones se escriban en el disco en el registro de transacciones. La réplica principal no espera para operaciones de escritura en las réplicas sincrónicas asincrónicas.  
- **Conmutación por error manual o automática** conmutación por error a una réplica secundaria sincrónica puede activarse automáticamente por el clúster o a petición mediante el Administrador de base de datos.
- **Secundarias activas disponibles para las cargas de trabajo de lecturas y copia de seguridad** una o varias réplicas secundarias pueden configurarse para admitir el acceso de solo lectura a bases de datos secundarias o para permitir que las copias de seguridad de bases de datos secundarias.
- **La propagación automática** SQL Server crea automáticamente las réplicas secundarias para cada base de datos del grupo de disponibilidad.
- **Enrutamiento de solo lectura** SQL Server enruta las conexiones entrantes a un agente de escucha del grupo de disponibilidad a una réplica secundaria que está configurada para permitir las cargas de trabajo de solo lectura. 
- **Desencadenador de conmutación por error y supervisión de estado de nivel de base de datos** supervisión del nivel de base de datos y diagnósticos mejorados. 
- **Las configuraciones de recuperación ante desastres** con grupos de disponibilidad distribuidos o la configuración del grupo de disponibilidad de varias subredes. 
- **Capacidades de escala de lectura** en SQL Server 2017 puede crear un grupo de disponibilidad con o sin alta disponibilidad para las operaciones de solo lectura de escalabilidad horizontal. 


Para obtener más información acerca de los grupos de disponibilidad de SQL Server, vea [grupos de disponibilidad de SQL Server Always On](http://msdn.microsoft.com/library/hh510230.aspx).

## <a name="availability-group-terminology"></a>Terminología de grupo de disponibilidad

Un grupo de disponibilidad admite un entorno de conmutación por error para un conjunto discreto de bases de datos de usuario - conocidas como bases de datos de disponibilidad - que conmutar por error conjuntamente. Un grupo de disponibilidad admite un conjunto de bases de datos principales de lectura y escritura y de uno a ocho conjuntos de bases de datos secundarias correspondientes. Opcionalmente, las bases de datos secundarias pueden estar disponibles para el acceso de solo lectura o para algunas operaciones de copia de seguridad. Un grupo de disponibilidad define un conjunto de dos o más asociados de conmutación por error, conocidos como réplicas de disponibilidad. Réplicas de disponibilidad son componentes del grupo de disponibilidad. Para obtener más información, consulte [información general de grupos de disponibilidad AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).

Los términos siguientes describen las partes principales de una solución de grupo de disponibilidad de SQL Server:

 grupo de disponibilidad  
 Contenedor para un conjunto de bases de datos, las *bases de datos de disponibilidad*, que conmutan por error juntas.  
  
 base de datos de disponibilidad  
 Base de datos que pertenece a un grupo de disponibilidad. Para cada base de datos de disponibilidad, el grupo de disponibilidad mantiene una sola copia de lectura y escritura (la *base de datos principal*) y de una a ocho copias de solo lectura (*bases de datos secundarias*).  
  
 base de datos principal  
 La copia de lectura y escritura de una base de datos de disponibilidad.  
  
 base de datos secundaria  
 Una copia de solo lectura de una base de datos de disponibilidad.  
  
 réplica de disponibilidad  
 Una instancia de un grupo de disponibilidad que se hospeda en una instancia específica de SQL Server y mantiene una copia local de cada base de datos de disponibilidad perteneciente al grupo de disponibilidad. Existen dos tipos de réplicas de disponibilidad: una sola *réplica principal* y de una a ocho *réplicas secundarias*.  
  
 réplica principal  
 La réplica de disponibilidad que hace que las bases de datos principales estén disponibles para las conexiones de lectura y escritura de clientes y, además, envía las entradas del registro de transacciones para cada base de datos principal a cada réplica secundaria.  
  
 réplica secundaria  
 Réplica de disponibilidad que mantiene una copia secundaria de cada base de datos de disponibilidad y actúa como posible destino de conmutación por error para el grupo de disponibilidad. Opcionalmente, una réplica secundaria puede admitir acceso de solo lectura a bases de datos secundarias y la creación de copias de seguridad de bases de datos secundarias.  
  
 agente de escucha de grupo de disponibilidad  
 Nombre de servidor al que los clientes pueden conectarse para tener acceso a una base de datos en una réplica principal o secundaria de un grupo de disponibilidad. Los agentes de escucha del grupo de disponibilidad dirigen las conexiones entrantes a la réplica principal o una réplica secundaria de solo lectura.  


## <a name="new-in-sql-server-2017-for-availability-groups"></a>Nuevo en SQL Server 2017 para grupos de disponibilidad

SQL Server 2017 presenta nuevas características para los grupos de disponibilidad.

**CLUSTER_TYPE** utilizar con `CREATE AVAILABILITY GROUP`. Identifica el tipo de administrador de clústeres de servidor que administra un grupo de disponibilidad. Puede ser uno de los siguientes tipos:

   - **WSFC** Winows clústeres de conmutación por error. En Windows, es el valor predeterminado de CLUSTER_TYPE.
   - **EXTERNO** un administrador de clústeres que es no conmutación por error clúster de Windows server: por ejemplo, en Linux con marcapasos.
   - **Ninguno** ningún administrador de clústeres. Se usa para un grupo de disponibilidad de la escala de lectura.

Para obtener más información acerca de estas opciones, consulte [CREATE AVAILABILITY GROUP](http://msdn.microsoft.com/library/ff878399.aspx) o [ALTER AVAILABILITY GROUP](http://msdn.microsoft.com/library/ff878601.aspx).

**Garantía de que se confirma en réplicas secundarias sincrónicas.**

Use `required_synchronized_secondaries_to_commit`with `CREATE AVAILABILITY GROUP` or `ALTER AVAILABILITY GROUP`. Cuando `required_synchronized_secondaries_to_commit` se establece en un valor mayor que 0, las transacciones en la réplica principal de bases de datos esperará hasta que la transacción se confirma en el número especificado de **elemento secundario sincrónico** registros de transacciones de base de datos de réplica. Si suficientes réplicas secundarias sincrónicas no están en línea, se rechazarán todas las conexiones a la réplica principal hasta que reanudar la comunicación con suficientes réplicas secundarias.

**Grupos de disponibilidad de la escala de lectura**

Crear un grupo de disponibilidad sin un clúster para admitir las cargas de trabajo de la escala de lectura. Vea [grupos de disponibilidad de la escala de lectura](../database-engine/availability-groups/windows/read-scale-availability-groups.md).

## <a name="next-steps"></a>Pasos siguientes

[Configurar grupo de disponibilidad para SQL Server en Linux](sql-server-linux-availability-group-configure-ha.md)

[Configurar grupo de disponibilidad de la escala de lectura para SQL Server en Linux](sql-server-linux-availability-group-configure-rs.md)

[Agregar grupo de disponibilidad recurso de clúster en RHEL](sql-server-linux-availability-group-cluster-rhel.md)

[Agregar grupo de disponibilidad recurso de clúster en SLES](sql-server-linux-availability-group-cluster-sles.md)

[Agregar grupo de disponibilidad recurso de clúster en Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)
