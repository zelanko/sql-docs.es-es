---
title: Replicación de SQL Server en Linux
description: En este artículo se describe la replicación de SQL Server en Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 10/17/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b049866d9752485cb1b9eb609404a3bd86f28a41
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68065194"
---
# <a name="sql-server-replication-on-linux"></a>Replicación de SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] presenta Replicación de SQL Server para instancias de SQL Server en Linux.

Configure la replicación en Linux con [procedimientos almacenados de replicación](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md) de SQL Server Management Studio (SSMS).

Una instancia de SQL Server puede participar en cualquier rol de replicación:

* publicador
* Distribuidor
* Suscriptor

Un esquema de replicación puede mezclar y hacer coincidir plataformas de sistema operativo. Por ejemplo, un esquema de replicación puede incluir una instancia de SQL Server en Linux para el publicador y el distribuidor, y los suscriptores incluir instancias de SQL Server en Windows y Linux.

Las instancias de SQL Server en Linux pueden participar en cualquier tipo de replicación.

* Transaccional
* Mezcla
* Snapshot

Para obtener información detallada sobre la replicación, vea la [documentación sobre replicación de SQL Server](../relational-databases/replication/sql-server-replication.md).

## <a name="supported-features"></a>Características admitidas

En [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] se admiten las características de replicación siguientes:

* Replicación de instantáneas
* Replicación transaccional
* Replicación de mezcla
* Replicación punto a punto
* Replicación con puertos no predeterminados <!--Add link to explanation-->
* Replicación con autenticación de AD
* Configuraciones de replicación en Windows y Linux
* Actualizaciones inmediatas para la replicación transaccional

## <a name="limitations"></a>Limitaciones

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] no admite las siguientes características:

* Suscriptores de actualización inmediata
* Publicación de Oracle

## <a name="next-steps"></a>Pasos siguientes

[Configuración de la replicación de SQL Server en Linux](sql-server-linux-replication-tutorial-tsql.md)

[Ejemplo: Configuración de la replicación de SQL Server en Linux](sql-server-linux-replication-configure.md)
