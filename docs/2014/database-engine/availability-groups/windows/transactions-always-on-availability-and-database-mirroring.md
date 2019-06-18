---
title: Las transacciones entre bases de datos no compatibles para la creación de reflejo de base de datos o AlwaysOn grupos de disponibilidad (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- cross-database transactions [SQL Server]
- transactions [database mirroring]
- Availability Groups [SQL Server], interoperability
- troubleshooting [SQL Server], cross-database transactions
ms.assetid: 9f7ed895-ad65-43e3-ba08-00d7bff1456d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8c3616e40ff54c67d27902ddf9454084fb62e282
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62813660"
---
# <a name="cross-database-transactions-not-supported-for-database-mirroring-or-alwayson-availability-groups-sql-server"></a>Transacciones entre bases de datos no compatibles para la creación de reflejo de la base de datos o grupos de disponibilidad de AlwaysOn (SQL Server)
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] y la creación de reflejo de la base de datos no admiten las transacciones entre bases de datos ni las transacciones distribuidas. Esto se debe a que la integridad o la atomicidad de las transacciones no se puede garantizar por las siguientes razones:  
  
-   Para las transacciones entre bases de datos: Cada base de datos se confirma independientemente. Por consiguiente, incluso para las bases de datos de un solo grupo de disponibilidad, podría producirse una conmutación por error después de que una base de datos confirme una transacción, pero antes de que lo haga la otra. Para la creación de reflejo de la base de datos este problema puede agravarse porque, después de una conmutación por error, la base de datos reflejada está normalmente en una instancia del servidor diferente al de la otra base de datos, e incluso si ambas bases de datos se reflejan entre los dos mismos asociados, no existe ninguna garantía de que ambas bases de datos se conmutarán por error al mismo tiempo.  
  
-   Para las transacciones distribuidas: Después de una conmutación por error, el nuevo servidor principal/réplica principal es no puede conectarse al Coordinador de transacciones distribuidas en el anterior servidor principal/réplica principal. Por lo tanto, el nuevo servidor principal o la nueva réplica principal no puede obtener el estado de la transacción.  
  
 En el siguiente ejemplo de creación de reflejo de la base de datos se muestra cómo podría producirse una incoherencia lógica. En este ejemplo, una aplicación utiliza una transacción entre bases de datos para insertar dos filas de datos: una fila se inserta en una tabla de una base de datos reflejada, A, y la otra fila se inserta en una tabla de otra base de datos, B. La base de datos A se está reflejando en modo de alta seguridad con conmutación automática por error. Mientras la transacción se confirma, la base de datos A deja de estar disponible y la sesión de creación de reflejo se conmuta por error automáticamente al reflejo de la base de datos A.  
  
 Después de la conmutación por error, la transacción entre bases de datos podría confirmarse correctamente en la base de datos B, pero no en la base de datos conmutada por error. Esto se produciría si el servidor principal original de la base de datos A no hubiese enviado el registro de transacciones entre bases de datos al servidor reflejado antes del error. Después de la conmutación por error, esa transacción no existiría en el nuevo servidor principal. Las bases de datos A y B se volverían incoherentes porque los datos insertados en la base de datos B se mantienen intactos, pero los datos insertados en la base de datos A se pierden.  
  
 Su puede producir un escenario similar cuando se usa una transacción de MS DTC. Por ejemplo, después de la conmutación por error, el nuevo servidor principal contacta con MS DTC. Sin embargo, MS DTC.no tiene conocimiento del nuevo servidor principal y termina las transacciones que están "preparadas para confirmar" y que otras bases de datos consideran confirmadas.  
  
> [!IMPORTANT]  
>  El uso de creación de reflejo de la base de datos o de grupos de disponibilidad junto con DTC no da como resultado una instalación no admitida de SQL Server. Sin embargo, si una base de datos forma parte de una sesión de creación de reflejo de la base de datos o de un grupo de disponibilidad y también se usa DTC en la base de datos, Microsoft solo investigará los problemas de compatibilidad si no están relacionados con el uso combinado de creación de reflejo de la base de datos o de grupos de disponibilidad con DTC.  
  
  
