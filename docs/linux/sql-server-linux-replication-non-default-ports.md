---
title: Configurar recursos compartidos de instantáneas carpeta replicación de SQL Server en Linux | Microsoft Docs
description: En este artículo se describe cómo configurar la replicación de SQL Server de los recursos compartidos de carpeta de instantáneas en Linux.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 9/24/2018
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: ''
ms.workload: On Demand
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6dd5887f4db97ae4d8f52103fd29403e7eb4c51e
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2018
ms.locfileid: "46715470"
---
# <a name="configure-replication-with-non-default-ports"></a>Configurar la replicación con puertos no predeterminados

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Puede configurar la replicación con SQL Server en las instancias de Linux para escuchar en cualquier puerto configurado con los parámetros de network.tcpport mssql-conf. El puerto se debe anexar al nombre del servidor durante la configuración si se cumplen las condiciones siguientes:

1. Configuración de replicación implica una instancia de SQL Server en Linux
2. Cualquier instancia (Windows o Linux) está escuchando en un puerto no predeterminado. 

El nombre de una instancia del servidor puede encontrarse ejecutando @@servername en la instancia.

## <a name="examples"></a>Ejemplos

'Server1' escucha en el puerto 1500 en Linux. Para configurar 'Server1' para la distribución, ejecute `sp_adddistributor` con `@distributor`. Por ejemplo: 

```sql
exec sp_adddistributor @distributor = 'Server1,1500'
```

'Server1' escucha en el puerto 1500 en Linux. Para configurar un publicador para el distribuidor, ejecute `sp_adddistpublisher` con `@publisher`. Por ejemplo:

```sql
exec sp_adddistpublisher @publisher = 'Server1,1500' ,  ,  
```

'Server2' escucha en el puerto 6549 en Linux. Para configurar 'Server2' como suscriptor, ejecute `sp_addsubscription` con `@subscriber`. Por ejemplo:

```sql
exec sp_addsubscription @subscriber = 'Server2,6549' ,  ,  
```

'Server3' escucha en el puerto 6549 en Windows con el nombre del servidor de Server3 y nombre de instancia de MSSQL2017. Para configurar 'Server3' como suscriptor, ejecute el `sp_addsubscription` con `@subscriber`. Por ejemplo:

```sql
exec sp_addsubscription @subscriber = 'Server3/MSSQL2017,6549',  ,  
```

## <a name="next-steps"></a>Pasos siguientes

[Conceptos: Replicación SQL Server en Linux](sql-server-linux-replication.md)

[Procedimientos almacenados de replicación](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).

