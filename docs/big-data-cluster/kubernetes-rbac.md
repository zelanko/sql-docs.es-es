---
title: RBAC de Kubernetes
titleSuffix: SQL Server big data clusters
description: En este artículo se describe cómo los Clústeres de macrodatos de SQL Server usan RBAC con Kubernetes.
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 5d2e3f379402f16f32020f9cd34103919f13a30c
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552980"
---
# <a name="kubernetes-rbac-model--impact-on-users-managing-bdc"></a>Modelo e impacto de RBAC de Kubernetes en los usuarios que administran BDC

En la siguiente sección se describen los permisos necesarios para los usuarios que administran clústeres de macrodatos.

> [!NOTE]
> Para obtener recursos adicionales sobre el modelo RBAC de Kubernetes, vea [Uso de la autorización de RBAC: Kubernetes](https://kubernetes.io/docs/reference/access-authn-authz/rbac/) y [Uso de RBAC para definir y aplicar permisos: OpenShift](https://docs.openshift.com/container-platform/4.4/authentication/using-rbac.html).

## <a name="role-required-for-deployment"></a>Rol necesario para la implementación

El BDC usa cuentas de servicio (como `sa-mssql-controller` o `master`) para orquestar el aprovisionamiento de los pods, servicios, alta disponibilidad y supervisión del clúster, entre otras cosas. La implementación del BDC (por ejemplo, `azdata bdc create`), `azdata` hace lo siguiente al iniciarse:

1. Comprueba si existe el espacio de nombres proporcionado.
2. Si no existe, se crea uno y se aplica la etiqueta `MSSQL_CLUSTER`.
3. Crea la cuenta de servicio de `sa-mssql-controller`.
4. Crea un rol de `<namespaced>-admin` con permisos completos en el espacio de nombres o en el proyecto, pero no en los permisos de nivel de clúster.
5. Crea una asignación de roles de esa cuenta de servicio para el rol.

Una vez completados estos pasos, se aprovisionan los pods de plano de control y la cuenta de servicio implementa el resto del clúster de macrodatos.  

Por consiguiente, el usuario de implementación debe tener permisos para lo siguiente:

- Enumerar los espacios de nombres en el clúster (1).
- Aplicar una revisión al espacio de nombres nuevo o existente con la etiqueta (2).
- Crear la cuenta de servicio de `sa-mssql-controller`, el rol de `<namespaced>-admin` y el enlace de rol (3-5).

El rol de `admin` predeterminado no tiene estos permisos, por lo que el usuario que implementa el clúster de macrodatos debe tener al menos permisos de administrador de nivel de espacio de nombres.

## <a name="cluster-role-required-for-pods-and-nodes-metrics-collection"></a>Rol de clúster necesario para la recopilación de métricas de pods y nodos

A partir de SQL Server 2019 CU5, Telegraf requiere una cuenta de servicio con permisos de rol en todo el clúster para recopilar las métricas de pods y nodos. Durante la implementación (o la actualización de las implementaciones existentes), se intenta crear la cuenta de servicio y el rol de clúster necesarios, pero si el usuario que implementa el clúster o realiza la actualización no tiene permisos suficientes, la implementación o la actualización continuará con una advertencia y se realizará correctamente. En este caso, no se recopilarán las métricas de pods y nodos. El usuario que implementa el clúster debe pedirle a un administrador que cree el rol y la cuenta de servicio (antes o después de la implementación o actualización). Una vez creados, BDC los usa. 

Este es un script que muestra cómo crear los artefactos necesarios:

```console
export CLUSTER_NAME=mssql-cluster
kubectl create -f - <<EOF
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: ${CLUSTER_NAME}:cr-mssql-metricsdc-reader
rules:
- apiGroups:
  - '*'
  resources:
  - pods
  - nodes/stats
  verbs:
  - get
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: ${CLUSTER_NAME}:crb-mssql-metricsdc-reader
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: ${CLUSTER_NAME}:cr-mssql-metricsdc-reader
subjects:
- kind: ServiceAccount
  name: sa-mssql-metricsdc-reader
  namespace: ${CLUSTER_NAME}
EOF
```

La cuenta de servicio, el rol de clúster y el enlace de rol de clúster se pueden crear antes o después de implementar el BDC. Kubernetes actualiza automáticamente el permiso para la cuenta de servicio de Telegraf. Si se crean como una implementación de pod, verá un retraso de unos minutos en el pod y se recopilarán las métricas de nodos.

> [!NOTE]
> SQL Server 2019 CU5 presenta dos modificadores de características para controlar la recopilación de métricas de pods y nodos. De forma predeterminada, estos parámetros se establecen en true en todos los destinos de entorno, excepto OpenShift, donde está invalidado el valor predeterminado. 

Se puede personalizar esta configuración en la sección de seguridad del archivo de configuración de implementación de `control.json`:

```json
  "security": {
    …
    "allowNodeMetricsCollection": false,
    "allowPodMetricsCollection": false
  }
```

Si esta configuración se establece en `false`, el flujo de trabajo de implementación del BDC no intentará crear la cuenta de servicio, el rol de clúster y el enlace para Telegraf.
