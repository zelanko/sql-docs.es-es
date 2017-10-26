---
title: "Transacciones - Grupos de disponibilidad AlwaysOn y creación de reflejo de la base de datos | Microsoft Docs"
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- cross-database transactions [SQL Server]
- transactions [database mirroring]
- Availability Groups [SQL Server], interoperability
- troubleshooting [SQL Server], cross-database transactions
ms.assetid: 9f7ed895-ad65-43e3-ba08-00d7bff1456d
caps.latest.revision: 33
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bc86ef8e495bacaaaebf2470306b25d38d5158e5
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="transactions---availability-groups-and-database-mirroring"></a>Transacciones - Grupos de disponibilidad y creación de reflejo de la base de datos
[!INCLUDE[tsql-appliesto-ssvnxt-xxxx-xxxx-xxx](../../../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

En este tema se describe la compatibilidad de las transacciones entre bases de datos y distribuidas para la creación de reflejo de la base de datos y grupos de disponibilidad AlwaysOn.  

## <a name="support-for-distributed-transactions"></a>Compatibilidad con transacciones distribuidas

SQL Server 2017 admite las transacciones distribuidas de bases de datos en los grupos de disponibilidad. Esto engloba tanto las bases de datos que hay en la misma instancia de SQL Server como las bases de datos en distintas instancias de SQL Server. Las transacciones distribuidas no son posibles con bases de datos configuradas para la creación de reflejo de base de datos.

>[!NOTE]
>[!INCLUDE[SQL Server 2016]](../../../includes/sssql15-md.md)] incluía compatibilidad limitada con las transacciones distribuidas en bases de datos de grupos de disponibilidad. Las transacciones distribuidas en las que se usan bases de datos de un grupo de disponibilidad se admitían siempre y cuando no hubiera más bases de datos de la transacción en la misma instancia de SQL Server. Para más información, vea [SQL Server 2016 DTC Support In Availability Groups](http://blogs.technet.microsoft.com/dataplatform/2016/01/25/sql-server-2016-dtc-support-in-availability-gr) (Compatibilidad con SQL Server 2016 DTC en grupos de disponibilidad).

Para configurar un grupo de disponibilidad para transacciones distribuidas, vea [Configurar un grupo de disponibilidad para las transacciones distribuidas](configure-availability-group-for-distributed-transactions.md).

Obtenga más información en:

- [DTC Administration Guide](http://msdn.microsoft.com/library/ms681291.aspx) (Guía de administración de DTC)
- [DTC Developers Guide](http://msdn.microsoft.com/library/ms679938.aspx) (Guía de desarrolladores de DTC)
- [DTC Programmers Reference](http://msdn.microsoft.com/library/ms686108.aspx) (Referencia de programadores de DTC)

## <a name="sql-server-2016-and-before-support-for-cross-database-transactions-within-the-same-sql-server-instance"></a>SQL Server 2016 y versiones anteriores: compatibilidad con transacciones entre bases de datos en la misma instancia de SQL Server  

En SQL Server 2016 y versiones anteriores, las transacciones entre bases de datos en la misma instancia de SQL Server no son compatibles con los grupos de disponibilidad. Esto significa que la misma instancia de SQL Server no puede hospedar dos bases de datos en una transacción entre bases de datos. Esto ocurre incluso si esas bases de datos forman parte del mismo grupo de disponibilidad.  
  
Las transacciones entre bases de datos tampoco se admiten para la creación de reflejo de la base de datos.  
  
##  <a name="dtcsupport"></a> SQL Server 2016: compatibilidad con transacciones distribuidas  
Las transacciones distribuidas son compatibles con los grupos de disponibilidad. Esto se aplica a las transacciones distribuidas entre bases de datos hospedadas en dos instancias diferentes de SQL Server. También se aplica a las transacciones distribuidas entre SQL Server y otro servidor compatible con DTC.  
 
Coordinador de transacciones distribuidas de Microsoft (MSDTC o DTC) es un servicio de Windows que proporciona infraestructura de transacciones para sistemas distribuidos. MSDTC permite que las aplicaciones cliente incluyan varios orígenes de datos en una transacción que luego se confirma en todos los servidores incluidos en la transacción. Por ejemplo, puede usar MSDTC para coordinar transacciones que abarcan varias bases de datos en servidores diferentes.

SQL Server 2016 ofrece la posibilidad de usar transacciones distribuidas en las que una o varias de las bases de datos de la transacción se encuentran en un grupo de disponibilidad. Antes de SQL Server 2016, no se admitían las transacciones distribuidas para bases de datos de grupos de disponibilidad. SQL Server 2016 puede registrar un administrador de recursos por base de datos. Esta nueva funcionalidad es la razón por la que las transacciones distribuidas pueden incluir bases de datos de grupos de disponibilidad.
  
 Se deben cumplir los requisitos siguientes:  
  
-   Los grupos de disponibilidad deben ejecutarse en Windows Server 2016 o Windows Server 2012 R2. Para Windows Server 2012 R2, debe instalar la actualización de KB3090973 disponible en [https://support.microsoft.com/es-es/kb/3090973](https://support.microsoft.com/en-us/kb/3090973).  
  
-   Availability groups must be created with the **CREATE AVAILABILITY GROUP** y la cláusula **WITH DTC_SUPPORT = PER_DB** . Actualmente no se puede modificar un grupo de disponibilidad existente.  

- Todas las instancias de SQL Server que participarán en el grupo de disponibilidad deben ser de SQL Server 2016 o posterior.
 
 ## <a name="non-support-for-distributed-transactions"></a>Sin compatibilidad con las transacciones distribuidas
 Los casos concretos en que no se admiten transacciones distribuidas incluyen:
 
 - En SQL Server 2016 y versiones anteriores, si hay más de una base de datos implicada en la transacción en el mismo grupo de disponibilidad.
 
 - En SQL Server 2016 y versiones anteriores, si al menos una base de datos se encuentra en un grupo de disponibilidad y otra base de datos se encuentra en la misma instancia de SQL Server. 
 
 - Si el grupo de disponibilidad no se ha creado con la transacción distribuida habilitada.
 
 - Creación de reflejo de base de datos.
 
 > [!IMPORTANT]
 > Determine la salida predeterminada apropiada de las transacciones que DTC no puede resolver para el entorno.  Para información sobre cómo configurar la salida predeterminada, consulte [in-doubt xact resolution (opción de configuración del servidor)](../../../database-engine/configure-windows/in-doubt-xact-resolution-server-configuration-option.md).
  
## <a name="example-scenario-with-database-mirroring"></a>Escenario de ejemplo con la creación de reflejo de base de datos  
 En el siguiente ejemplo de creación de reflejo de la base de datos se muestra cómo podría producirse una incoherencia lógica. En este ejemplo, una aplicación utiliza una transacción entre bases de datos para insertar dos filas de datos: una fila se inserta en una tabla de una base de datos reflejada, A, y la otra fila se inserta en una tabla de otra base de datos, B. La base de datos A se está reflejando en modo de alta seguridad con conmutación automática por error. Mientras la transacción se confirma, la base de datos A deja de estar disponible y la sesión de creación de reflejo se conmuta por error automáticamente al reflejo de la base de datos A.  
  
 Después de la conmutación por error, la transacción entre bases de datos podría confirmarse correctamente en la base de datos B, pero no en la base de datos conmutada por error. Esto se produciría si el servidor principal original de la base de datos A no hubiese enviado el registro de transacciones entre bases de datos al servidor reflejado antes del error. Después de la conmutación por error, esa transacción no existiría en el nuevo servidor principal. Las bases de datos A y B se volverían incoherentes porque los datos insertados en la base de datos B se mantienen intactos, pero los datos insertados en la base de datos A se pierden.  
  
 Su puede producir un escenario similar cuando se usa una transacción de MS DTC. Por ejemplo, después de la conmutación por error, el nuevo servidor principal contacta con MS DTC. Sin embargo, MS DTC.no tiene conocimiento del nuevo servidor principal y termina las transacciones que están "preparadas para confirmar" y que otras bases de datos consideran confirmadas.  
  
> [!NOTE]  
>  No se puede usar la creación de reflejo de la base de datos con DTC ni usar los grupos de disponibilidad con DTC de formas no aprobadas en este tema.  Esto no implica que los aspectos del producto no relacionados con DTC sean incompatibles; no obstante, no se admitirán los problemas derivados del uso incorrecto de las transacciones distribuidas.  
  
## <a name="see-also"></a>Vea también  
 [Always On availability groups: Interoperability &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)  
  
  

