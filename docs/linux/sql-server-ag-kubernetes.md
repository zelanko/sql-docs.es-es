---
title: Grupos de disponibilidad de Always On para los contenedores de SQL Server
description: En este artículo se describen los grupos de disponibilidad en los contenedores de SQL Server
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 08/09/2018
ms.topic: article
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cc5a96fd5efc4a2eb0e45a3034d17e98ae3c7172
ms.sourcegitcommit: 4832ae7557a142f361fbf0a4e2d85945dbf8fff6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/03/2018
ms.locfileid: "48251969"
---
# <a name="always-on-availability-groups-for-sql-server-containers"></a>Grupos de disponibilidad de Always On para los contenedores de SQL Server

SQL Server 2019 admite grupos de disponibilidad en los contenedores de un Kubernetes. Para los grupos de disponibilidad, implemente el servidor SQL Server [Kubernetes operador](http://coreos.com/blog/introducing-operators.html) al clúster de Kubernetes. El operador ayuda a paquete, implementar y administrar el grupo de disponibilidad en un clúster.

![Grupo de disponibilidad en el contenedor de Kubernetes](media/tutorial-sql-server-ag-containers-kubernetes/KubernetesCluster.png)

En la imagen anterior, los clústeres de cuatro nodos kubernetes hospedan un grupo de disponibilidad con tres réplicas. La solución incluye los siguientes componentes:

* Un Kubernetes [ *implementación*](http://kubernetes.io/docs/concepts/workloads/controllers/deployment/). La implementación incluye el operador y un mapa de la configuración. Proporcionan la imagen de contenedor, software y las instrucciones necesarias para implementar instancias de SQL Server para el grupo de disponibilidad.

* Tres nodos, cada hospeda un [ *StatefulSet*](http://kubernetes.io/docs/concepts/workloads/controllers/statefulset/). Contiene el StatefulSet un [ *pod*](http://kubernetes.io/docs/concepts/workloads/pods/pod-overview/). Cada pod contiene:
  * Un contenedor de SQL Server ejecuta una instancia de SQL Server.
  * Un agente de grupo de disponibilidad. 

* Dos [ *ConfigMaps* ](http://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/) relacionadas con el grupo de disponibilidad. El ConfigMaps proporcionan información acerca de:
  * La implementación del operador.
  * Grupo de disponibilidad.

 * [*Volúmenes persistentes* ](http://kubernetes.io/docs/concepts/storage/persistent-volumes/) son fragmentos de almacenamiento. Un *notificación de volumen persistente* (PVC) es una solicitud de almacenamiento por el usuario. Cada contenedor está afiliado a un circuito virtual permanente para el almacenamiento de datos y de registro. En Azure Kubernetes Service (AKS), [crear una notificación de volumen persistente](http://docs.microsoft.com/azure/aks/azure-disks-dynamic-pv) para aprovisionar automáticamente el almacenamiento basado en una clase de almacenamiento.


Además, el clúster almacena [ *secretos* ](http://kubernetes.io/docs/concepts/configuration/secret/) para las contraseñas, certificados, claves y otra información confidencial.

## <a name="deploy-the-availability-group-in-kubernetes"></a>Implementar el grupo de disponibilidad en Kubernetes

Para implementar un grupo de disponibilidad en Kubernetes:

1. Crear el clúster de Kubernetes

   Para un grupo de disponibilidad, cree al menos tres nodos para SQL Server además de un nodo del patrón.

1. Implementar el operador

1. Configurar el almacenamiento

1. Implementar el StatefulSet

   El operador realiza escuchas para que las instrucciones para implementar el StatefulSet. Automáticamente se crea las instancias de SQL Server en tres nodos independientes y se configura el grupo de disponibilidad con un administrador de clúster externo.

1. Crear las bases de datos y conéctelas al grupo de disponibilidad

Para obtener instrucciones detalladas, consulte [grupos de disponibilidad de Always On para los contenedores de SQL Server](sql-server-ag-kubernetes.md).

## <a name="sql-server-kubernetes-operator"></a>Operador de Kubernetes de SQL Server

Después de implementar el operador, registra un recurso personalizado de SQL Server. Use el operador para implementar este recurso.  Cada recurso corresponde a una instancia de SQL Server e incluye las propiedades específicas como `sapassword` y `monitoring policy`. El operador analiza el recurso e implementa Kubernetes StatefulSet.

Contiene el StatfulSet:

* contenedor MSSQL-server

* contenedor MSSQL-ha-supervisor

El código para el operador, el supervisor de alta disponibilidad y SQL Server se empaqueta en una imagen de Docker denominada `mcr.microsoft.com/mssql/ha`. Esta imagen contiene los siguientes archivos binarios:

* `mssql-operator`

    Este proceso se implementa como una implementación independiente de Kubernetes. Registra el [recurso personalizado de Kubernetes](http://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) llamado `SqlServer` (sqlservers.mssql.microsoft.com). A continuación, escucha estos recursos que se va a crear o actualizar en el clúster de Kubernetes. Para cada evento de este tipo, crea o actualiza los recursos de Kubernetes para la instancia correspondiente (por ejemplo el StatefulSet o `mssql-server-k8s-init-sql` trabajo).

* `mssql-server-k8s-health-agent`

    Este servidor web sirve Kubernetes [garantizan sondeos](http://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/) para determinar el estado de una instancia de SQL Server. Supervisa el estado de la instancia de SQL Server local mediante una llamada a `sp_server_diagnostics` y comparar los resultados con la directiva de supervisión.

* `mssql-ha-supervisor`

   Mantiene el certificado de grupo de disponibilidad y el punto de conexión. 

* `mssql-server-k8s-ag-agent`
  
    Este proceso supervisa el estado de una réplica de AG en una única instancia de SQL Server y realiza conmutaciones por error.

    También mantiene la elección de líder.

* `mssql-server-k8s-init-sql`
  
    Este Kubernetes [trabajo](http://kubernetes.io/docs/concepts/workloads/controllers/jobs-run-to-completion/) se aplica una configuración de estado deseado para una instancia de SQL Server. Cada vez que se crea o actualiza un recurso de SQL Server, se crea el trabajo por el operador. Se asegura de que la instancia de SQL Server de destino correspondiente al recurso personalizado tiene la configuración deseada que se describe en el recurso.

    Por ejemplo, si cualquiera de los valores siguientes son necesario, se completa ellos:
  * Actualizar la contraseña de SA
  * Crea el inicio de sesión SQL para los agentes
  * Crea el extremo DBM

* `mssql-server-k8s-rotate-creds`
  
    Este trabajo Kubernetes implementa la tarea de girar credenciales. Cree este trabajo para solicitar las actualizaciones de la contraseña de SA, contraseña de inicio de sesión del Agente SQL, cert DBM, etcetera. La contraseña de SA se especifica como los parámetros del trabajo. Los demás son generados automáticamente.

* `mssql-server-k8s-failover`

   Un trabajo de Kubernetes que implementa el flujo de trabajo de conmutación por error manual.

### <a name="notes"></a>Notas

Independientemente de la configuración de AG, el operador siempre implementará el supervisor de alta disponibilidad. Si el recurso de SQL Server no muestra ningún grupo de disponibilidad, el operador implementará este contenedor.

La versión de la imagen del operador es idéntica a la versión de la imagen de SQL Server.

## <a name="next-steps"></a>Pasos siguientes

> [Contenedor de SQL Server en Kubernetes](tutorial-sql-server-containers-kubernetes.md)
