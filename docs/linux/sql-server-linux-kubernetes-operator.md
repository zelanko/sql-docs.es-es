---
title: SQL Server Always On grupo Kubernetes operador globales requisitos de disponibilidad
description: En este artículo se explica los parámetros para el SQL Server Kubernetes Always On grupo operador globales requisitos de disponibilidad
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 187517c79f14ddcbf08ffa644e65558fa0a85b38
ms.sourcegitcommit: 4832ae7557a142f361fbf0a4e2d85945dbf8fff6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/03/2018
ms.locfileid: "48252003"
---
# <a name="sql-server-always-on-availability-group-kubernetes-operator-parameters"></a>SQL Server Always On grupo Kubernetes operador los parámetros de disponibilidad

Un grupo de disponibilidad Always On en Kubernetes requiere un operador. Un manifiesto describe el operador. El manifiesto es un `.yaml` archivo. Ver un ejemplo de la especificación en [grupos de disponibilidad de Always On para los contenedores de SQL Server](sql-server-ag-kubernetes.md).

En este artículo se explica las variables de entorno globales de operador.

## <a name="example"></a>Ejemplo

En el ejemplo siguiente se describe una implementación para el `mssql-operator`.

## <a name="global-environment-variables"></a>Variables de entorno globales

* `MSSQL_K8S_POD_NAMESPACE` 
  * Obligatorio
  * **Descripción**: Kubernetes el espacio de nombres del operador.

* `MSSQL_K8S_SQL_WRITE_LEASE_PERIOD_SECONDS`
  * Opcional
  * **Descripción**: la duración de la concesión de escritura de sql server. Se usa para mantener el servidor sql server puede escribir y evitar escenarios de cerebro divididos. Las réplicas secundarias se espere a que este número de segundos después de seleccionar un nuevo líder.

* `MSSQL_K8S_MONITOR_PERIOD_SECONDS`
  * Opcional
  * **Descripción**: el período para supervisar el estado del grupo de disponibilidad. Determina la rapidez con las réplicas se agregan y eliminan. Debe ser menor que `MSSQL_K8S_SQL_WRITE_LEASE_PERIOD_SECONDS`.
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
