---
title: SQL Server Always On grupo Kubernetes operador globales requisitos de disponibilidad
description: En este artículo se explica los parámetros para el SQL Server Kubernetes Always On grupo operador globales requisitos de disponibilidad
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2d5699ae16a02346f9dded732180b16615087d16
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2018
ms.locfileid: "46715394"
---
# <a name="sql-server-always-on-availability-group-kubernetes-operator-parameters"></a>SQL Server Always On grupo Kubernetes operador los parámetros de disponibilidad

Un grupo de disponibilidad Always On en Kubernetes requiere un operador. Se describe el operador en un archivo .yaml.  Ver un ejemplo de la especificación en [este tutorial](tutorial-sql-server-ag-kubernetes.md).

En este artículo se explica las variables de entorno globales de operador.

## <a name="example"></a>Ejemplo

En el ejemplo siguiente se describe una implementación para el `mssql-operator`.

## <a name="global-environment-variables"></a>Variables de entorno globales

* `MSSQL_K8S_POD_NAMESPACE` 
  * Obligatorio
  * **Descripción**: el espacio de nombres de Kubernetes del operador.

* `MSSQL_K8S_SQL_WRITE_LEASE_PERIOD_SECONDS`
  * Opcional
  * **Descripción**: la duración de sql server externa escribir concesión para mantener el servidor sql server puede escribir y evitar escenarios de cerebro divididos. Las réplicas secundarias se esperan a que esta expiración después de elegir a un líder nuevo.

* `MSSQL_K8S_MONITOR_PERIOD_SECONDS`
  * Opcional
  * **Descripción**: el período para supervisar si el estado del grupo de disponibilidad. Determina la rapidez con las réplicas se agregan y eliminan. Debe ser menor que `MSSQL_K8S_SQL_WRITE_LEASE_PERIOD_SECONDS`.
  * **Default**: 1

* `MSSQL_K8S_LEASE_DURATION_SECONDS`
  * Opcional
  * **Descripción**: duración de concesión de líder de grupo de disponibilidad. Determina cuánto tiempo esperar antes de volver a elegir si la réplica principal se ha bloqueado las réplicas secundarias. Esto es diferente de la concesión de escritura de SQL Server. 
  * **Default**: 10
  
  >[!NOTE]
  >Otros valores de configuración calculan automáticamente según `MSSQL_K8S_LEASE_DURATION_SECONDS`.

* `MSSQL_K8S_RENEW_DEADLINE_SECONDS`
  * Opcional
  * **Descripción**: duración de la réplica principal actúa vuelve a intentar actualizar liderazgo antes de desistir. Debe ser menor que `MSSQL_K8S_LEASE_DURATION_SECONDS`.
  * **Default**:  `MSSQL_K8S_LEASE_DURATION_SECONDS` /2

* `MSSQL_K8S_RETRY_PERIOD_SECONDS`
  * Opcional
  * **Descripción**: duración activo [maestro](http://kubernetes.io/docs/concepts/architecture/master-node-communication/) esperará antes de renovar la concesión líder. Debe ser menor que `MSSQL_K8S_LEASE_DURATION_SECONDS`.
  * **Default**:  `MSSQL_K8S_RENEW_DEADLINE_SECONDS` /2

* `MSSQL_K8S_ACQUIRE_PERIOD_SECONDS` 
  * Opcional
  * **Descripción**: período de las réplicas secundarias sondean si la concesión líder ha expirado. 
  * **Default**: 1


  ## <a name="next-steps"></a>Pasos siguientes

[Grupo de disponibilidad de SQL Server en clúster de Kubernetes](sql-server-ag-kubernetes.md)