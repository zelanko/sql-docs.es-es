---
title: Propiedades de configuración de la instancia maestra de SQL Server
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para las propiedades de configuración de la instancia maestra de SQL Server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: rahul.ajmera
ms.date: 08/04/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 60888246623796d9b4d17c498da47ab4b6557cf2
ms.sourcegitcommit: 6ab28d954f3a63168463321a8bc6ecced099b247
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/05/2020
ms.locfileid: "87790476"
---
# <a name="sql-server-master-instance-configuration-properties"></a>Propiedades de configuración de la instancia maestra de SQL Server

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

## <a name="properties"></a>Propiedades

Puede configurar las siguientes opciones de SQL Server para la instancia maestra en el momento de la implementación.

|Propiedad|Opciones|
| --- | --- |
|`[sqlagent]`|`enabled = { true | false }` |
|`[telemetry]`|`customerfeedback = { true | false }` |
|`[telemetry]`|`userRequestedLocalAuditDirectory = </path/file>`|
|`[licensing]`| `pid = { Enterprise | Developer }`|
|`[traceflag]`|` traceflag<#> = <####>`|

### <a name="examples"></a>Ejemplos

En el siguiente ejemplo se habilita el Agente SQL y la telemetría, se establece un PID para Enterprise Edition y se habilita la marca de seguimiento 1204:

```
[sqlagent]
enabled=true

[telemetry]
customerfeedback=true
userRequestedLocalAuditDirectory = /tmp/audit

[licensing]
pid = Enterprise

[traceflag]
traceflag0 = 1204
```

Para ver las instrucciones, consulte [Configuración de una instancia maestra de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](configure-sql-server-master-instance.md).

## <a name="next-steps"></a>Pasos siguientes

[Configuración de una instancia maestra de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](configure-sql-server-master-instance.md)
