---
title: Replicación de SQL Server en Linux | Microsoft Docs
description: En este artículo se describe la replicación de SQL Server en Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 03/20/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: ''
ms.workload: On Demand
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a6c4bad8947944d59208a0516e5950d36f64a84e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47734133"
---
# <a name="sql-server-replication-on-linux"></a>Replicación de SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] presenta la replicación de SQL Server para las instancias de SQL Server en Linux.

Configurar la replicación en Linux con SQL Server Management Studio (SSMS) [procedimientos almacenados de replicación](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).

Una instancia de SQL Server puede participar en cualquier rol de replicación:

* publicador
* Distribuidor
* Suscriptor

Un esquema de replicación puede mezclar y combinar las plataformas de sistema operativo. Por ejemplo, un esquema de replicación puede utilizar instancias de SQL Server en Linux para el publicador y el distribuidor y los suscriptores pueden incluir instancias de SQL Server en Windows.

Instancias de SQL Server en Linux pueden participar en cualquier tipo de replicación.

* Transaccional
* Mezcla
* Snapshot

Para obtener información detallada acerca de la replicación, vea [la documentación de SQL Server replication](../relational-databases/replication/sql-server-replication.md).

## <a name="supported-features"></a>Características admitidas

Para [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] se admiten las siguientes características de replicación:

* Replicación de instantáneas
* Replicación transaccional
* Replicación de mezcla
* Replicación punto a punto
* Replicación con puertos no predeterminados <!--Add link to explanation-->
* Replicación con la autenticación de Active Directory
* Configuraciones de replicación a través de Windows y Linux
* Actualizaciones inmediatas de la replicación transaccional

## <a name="limitations"></a>Limitaciones

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] no se admiten las siguientes características:

* Suscriptores de actualización inmediata

## <a name="next-steps"></a>Pasos siguientes

[Configurar la replicación de SQL Server en Linux](sql-server-linux-replication-tutorial-tsql.md)

[Ejemplo: Configurar la replicación de SQL Server en Linux](sql-server-linux-replication-configure.md)
