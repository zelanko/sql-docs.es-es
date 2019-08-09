---
title: Conexión a un grupo de disponibilidad AlwaysOn de SQL Server en un clúster de Kubernetes
description: En este artículo se explica cómo conectarse a un grupo de disponibilidad AlwaysOn.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f05bc51f587723414d3b0a4090fe2b27ad5fb837
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67952604"
---
# <a name="connect-to-a-sql-server-always-on-availability-group-on-kubernetes"></a>Conexión a un grupo de disponibilidad AlwaysOn de SQL Server en Kubernetes

Para conectarse a instancias de SQL Server en contenedores de un clúster de Kubernetes, cree un [servicio de equilibrador de carga](https://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer). El equilibrador de carga es un punto de conexión. Contiene una dirección IP y reenvía las solicitudes de esa dirección IP al pod que ejecuta la instancia de SQL Server.

Para conectarse a una réplica de grupo de disponibilidad, cree un servicio para diferentes tipos de réplica. Puede ver ejemplos de servicios para diferentes tipos de réplicas en [sql-server-samples/ag-services.yaml](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/high%20availability/Kubernetes/sample-manifest-files).

* `ag1-primary` apunta a la réplica principal.
* `ag1-secondary` apunta a cualquier réplica secundaria.

Si hay más de una réplica secundaria, Kubernetes enruta la conexión a las distintas réplicas de modo round robin.

## <a name="create-a-load-balancer-service"></a>Creación de un servicio de equilibrador de carga

Para crear servicios de equilibrador de carga para las réplicas principal y secundarias, copie [`ag1-services.yaml`](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml) desde [sql-server-samples](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-file) y actualícelo para el grupo de disponibilidad.

El siguiente comando aplica la configuración del archivo `.yaml` al clúster:

```kubectl
kubectl apply -f ag1-services.yaml --namespace ag1
```

## <a name="get-the-ip-address-for-your-load-balancer-service"></a>Obtención de la dirección IP del servicio de equilibrador de carga

Para obtener la dirección IP del equilibrador de carga del servicio de equilibrador de carga, ejecute

```kubectl
kubectl get services
```

Identifique la dirección IP del servicio al que quiere conectarse.

## <a name="connect-to-primary-replica"></a>Conexión a la réplica principal

Para conectarse a la réplica principal con autenticación de SQL, use la cuenta `sa`, el valor de `sapassword` del secreto que ha creado y esta dirección IP.

Por ejemplo:

```cmd
sqlcmd -S <0.0.0.0> -U sa -P "<MyC0m9l&xP@ssw0rd>"
```

## <a name="next-steps"></a>Pasos siguientes

[Administración de un grupo de disponibilidad de SQL Server en un clúster de Kubernetes](sql-server-linux-kubernetes-manage.md)

[Grupo de disponibilidad AlwaysOn en clúster de Kubernetes](sql-server-ag-kubernetes.md)
