---
title: Grupos de disponibilidad Always On para contenedores que ejecuten Linux
titleSuffix: SQL Server
description: En este artículo, se proporciona información general sobre los grupos de disponibilidad en contenedores de SQL Server.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 3910c74be803b7fc63c8bf560fc637387e06ee15
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67910475"
---
# <a name="always-on-availability-groups-for-sql-server-containers"></a>Grupos de disponibilidad Always On para contenedores de SQL Server

SQL Server 2019 admite grupos de disponibilidad en contenedores de un clúster de Kubernetes. En los grupos de disponibilidad, implemente el [operador de Kubernetes](https://coreos.com/blog/introducing-operators.html) de SQL Server en el clúster de Kubernetes. El operador ayuda a empaquetar, implementar y administrar un grupo de disponibilidad en un clúster.

![Grupo de disponibilidad en contenedor de Kubernetes](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

En la imagen anterior, un clúster de Kubernetes de cuatro nodos hospeda un grupo de disponibilidad con tres réplicas. En la solución, se incluyen los componentes siguientes:

* Una [*implementación*](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) de Kubernetes. En la implementación, se incluyen el operador y un mapa de configuración. Se proporciona la imagen del contenedor, el software y las instrucciones necesarias para implementar instancias de SQL Server para el grupo de disponibilidad.

* Tres nodos, cada uno de los cuales hospeda un [*StatefulSet*](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/). StatefulSet contiene un [*pod*](https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/). Cada pod contiene:
  * Un contenedor de SQL Server que ejecuta una instancia de SQL Server.
  * Un agente de grupos de disponibilidad. 

* Dos [*ConfigMaps*](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/) relacionados con el grupo de disponibilidad. ConfigMaps proporciona información sobre:
  * La implementación para el operador.
  * Grupo de disponibilidad.

 * Los [*volúmenes persistentes*](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) son elementos de almacenamiento. Una *reclamación de volumen persistente* (PVC) es una solicitud de almacenamiento realizada por un usuario. Cada contenedor está asociado a una PVC para el almacenamiento de registros y datos. En Azure Kubernetes Service (AKS), [creará una reclamación de volumen persistente](https://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv) para aprovisionar forma automática el almacenamiento basándose en una clase de almacenamiento.


Además, el clúster almacena [*secretos*](https://kubernetes.io/docs/concepts/configuration/secret/) de contraseñas, certificados, claves y otra información confidencial.

## <a name="deploy-the-availability-group-in-kubernetes"></a>Implementar el grupo de disponibilidad en Kubernetes

Para implementar un grupo de disponibilidad en Kubernetes:

1. Crear el clúster de Kubernetes

   Para un grupo de disponibilidad, cree como mínimo tres nodos para SQL Server, además de un nodo para la instancia maestra.

1. Implementar el operador

1. Configurar el almacenamiento

1. Implementar StatefulSet

   El operador escucha en espera de instrucciones para implementar StatefulSet. Crea automáticamente las instancias de SQL Server en tres nodos separados y configura el grupo de disponibilidad con un administrador de clústeres externo.

1. Crear las bases de datos y asociarlas al grupo de disponibilidad

Para obtener más información sobre los pasos, vea [Grupos de disponibilidad Always On para contenedores de SQL Server](sql-server-ag-kubernetes.md).

## <a name="sql-server-kubernetes-operator"></a>Operador de SQL Server Kubernetes

Después de implementar el operador, registrará un recurso de SQL Server personalizado. Use el operador para implementar este recurso.  Cada recurso se corresponde con una instancia de SQL Server e incluye propiedades específicas, como `sapassword` y `monitoring policy`. El operador analizar el recurso e implementa StatefulSet de Kubernetes.

StatfulSet contiene lo siguiente:

* contenedor de mssql-server

* contenedor de mssql-ha-supervisor

El código del operador, el supervisor de alta disponibilidad y SQL Server se empaquetan en una imagen de Docker llamada `mcr.microsoft.com/mssql/ha`. Esta imagen contiene los siguientes archivos binarios:

* `mssql-operator`

    Este proceso se implementa como una implementación de Kubernetes independiente. Registra el [recurso personalizado de Kubernetes](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) denominado `SqlServer` (sqlservers.mssql.microsoft.com). Después, escucha para comprobar si esos recursos se crean o actualizan en el clúster de Kubernetes. Por cada evento, crea o actualiza los recursos de Kubernetes para la instancia correspondiente (por ejemplo, StatefulSet o un trabajo de `mssql-server-k8s-init-sql`).

* `mssql-server-k8s-health-agent`

    Este servidor web sirve [sondeos de ejecución](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/) de Kubernetes para determinar el estado de una instancia de SQL Server. Para supervisar el estado de la instancia de SQL Server local, llama a `sp_server_diagnostics` y compara los resultados con la directiva de supervisión.

* `mssql-ha-supervisor`

   Mantiene el punto de conexión y el certificado del grupo de disponibilidad. 

* `mssql-server-k8s-ag-agent`
  
    Este proceso supervisa el estado de una réplica de grupo de disponibilidad en una única instancia de SQL Server y realiza conmutaciones por error.

    También mantiene la elección del líder.

* `mssql-server-k8s-init-sql`
  
    El [trabajo](https://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/) de Kubernetes aplica la configuración de estado que prefiera en una instancia de SQL Server. El operador crea el trabajo cada vez que se crea o actualiza un recurso de SqlServer. Garantiza que la instancia de SQL Server de destino que se corresponde con el recurso personalizado tenga la configuración que prefiera que se describe en el recurso.

    Por ejemplo, si alguna de las siguientes opciones de configuración es obligatoria, la completa:
  * Actualiza la contraseña del administrador del sistema.
  * Crea el inicio de sesión de SQL para los agentes.
  * Crea el punto de conexión de DBM.

* `mssql-server-k8s-rotate-creds`
  
    Este trabajo de Kubernetes implementa la tarea de rotación de credenciales. Cree este trabajo para solicitar actualizaciones en la contraseña del administrador del sistema, la contraseña de inicio de sesión del agente SQL, el certificado de DBM, etc. La contraseña del administrador del sistema se especifica como los parámetros del trabajo. El resto se genera automáticamente.

* `mssql-server-k8s-failover`

   Un trabajo de Kubernetes que implementa el flujo de trabajo de conmutación por error manual.

### <a name="notes"></a>Notas

Independientemente de la configuración del grupo de disponibilidad, el operador siempre implementará el supervisor de alta disponibilidad. Si en el recurso SqlServer no se muestra ningún grupo de disponibilidad, el operador seguirá implementando el contenedor.

La versión de la imagen del operador es idéntica a la versión de la imagen de SQL Server.

## <a name="next-steps"></a>Pasos siguientes

> [Contenedor de SQL Server en Kubernetes](tutorial-sql-server-containers-kubernetes.md)
