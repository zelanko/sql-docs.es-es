---
title: Conectarse a SQL Server grupo de disponibilidad AlwaysOn en un clúster de Kubernetes
description: En este artículo se explica cómo conectarse a un grupo de disponibilidad AlwaysOn
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
ms.openlocfilehash: d13f89a1297d21c882075821a681886dc95c4c76
ms.sourcegitcommit: df21af652d0906ade8cc9ca3985a7ba5569f0db6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2018
ms.locfileid: "47049595"
---
# <a name="connect-to-a-sql-server-always-on-availability-group-on-kubernetes"></a>Conectarse a un servidor SQL Server Always On Availability Group en Kubernetes

Para conectarse a instancias de SQL Server en contenedores en un clúster de Kubernetes, cree un [servicio del equilibrador de carga](http://kubernetes.io/docs/concepts/services-networking/service/#loadbalancer). El equilibrador de carga reenvía las solicitudes para la dirección IP en el pod que ejecuta la instancia de SQL Server.

Para conectarse a una réplica del grupo de disponibilidad, cree un servicio para los tipos de otra réplica. Puede ver ejemplos de servicios para diferentes tipos de réplicas en [ejemplos de sql server](https://github.com/Microsoft/sql-server-samples/blob/master/samples/features/high%20availability/Kubernetes/sample-manifest-files/ag-services.yaml).

* `ag1-primary` apunta a la réplica principal.
* `ag1-secondary-sync` apunta a la réplica secundaria sincrónica.
* `ag1-secondary-async` apunta a una réplica secundaria asincrónica.

Si existe más de una réplica secundaria del mismo tipo, Kubernetes enruta la conexión a las diferentes réplicas en un modo round-robin.

## <a name="create-a-load-balancer-service"></a>Crear un servicio del equilibrador de carga

Para crear un servicio del equilibrador de carga para la réplica principal, copie `ag1-primary.yaml` desde [ejemplos de sql server]()y actualícelo para el grupo de disponibilidad.

El siguiente comando aplica el archivo .yaml a su clúster:

```kubectl
kubectl apply -f ag1-primary.yaml
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