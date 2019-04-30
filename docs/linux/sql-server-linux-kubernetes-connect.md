---
title: Conectarse a SQL Server grupo de disponibilidad AlwaysOn en un clúster de Kubernetes
description: En este artículo se explica cómo conectarse a un grupo de disponibilidad AlwaysOn
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6352fc7be129f485175b1144d14aa380b2d99e1f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63231171"
---
# <a name="connect-to-a-sql-server-always-on-availability-group-on-kubernetes"></a>Conectarse a un servidor SQL Server Always On Availability Group en Kubernetes

Para conectarse a instancias de SQL Server en contenedores en un clúster de Kubernetes, cree un [servicio del equilibrador de carga](https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer). El equilibrador de carga es un punto de conexión. Contiene una dirección IP y reenvía las solicitudes para la dirección IP en el pod que ejecuta la instancia de SQL Server.

Para conectarse a una réplica del grupo de disponibilidad, cree un servicio para los tipos de otra réplica. Puede ver ejemplos de servicios para diferentes tipos de réplicas en [sql-server-samples/ag-services.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files).

* `ag1-primary` apunta a la réplica principal.
* `ag1-secondary` puntos a cualquier réplica secundaria.

Si hay más de una réplica secundaria, Kubernetes enruta la conexión a las diferentes réplicas en un modo round-robin.

## <a name="create-a-load-balancer-service"></a>Crear un servicio del equilibrador de carga

Para crear servicios de equilibrador de carga para el principal y las réplicas, copie [ `ag1-services.yaml` ](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml) desde [ejemplos de sql server](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-file) y actualícelo para el grupo de disponibilidad.

El siguiente comando aplica la configuración de la `.yaml` archivos en clúster:

```kubectl
kubectl apply -f ag1-services.yaml --namespace ag1
```

## <a name="get-the-ip-address-for-your-load-balancer-service"></a>Obtenga la dirección IP para el servicio del equilibrador de carga

Para obtener la dirección IP del equilibrador de carga para el servicio del equilibrador de carga, ejecute

```kubectl
kubectl get services
```

Identificar la dirección IP del servicio en la que desea conectarse.

## <a name="connect-to-primary-replica"></a>Conéctese a la réplica principal

Para conectarse a la réplica principal con la autenticación de SQL, use la `sa` cuenta, el valor de `sapassword` desde el secreto que creó y esta dirección IP.

Por ejemplo:

```cmd
sqlcmd -S <0.0.0.0> -U sa -P "<MyC0m9l&xP@ssw0rd>"
```

## <a name="next-steps"></a>Pasos siguientes

[Administrar grupo de disponibilidad de SQL Server en clúster de Kubernetes](sql-server-linux-kubernetes-manage.md)

[Grupo de disponibilidad de SQL Server en clúster de Kubernetes](sql-server-ag-kubernetes.md)
