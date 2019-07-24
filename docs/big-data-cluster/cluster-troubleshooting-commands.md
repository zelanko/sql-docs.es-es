---
title: Supervisión y solución de problemas
titleSuffix: SQL Server big data clusters
description: En este artículo se proporcionan comandos útiles para supervisar y solucionar problemas de un clúster de macrodatos SQL Server 2019 (versión preliminar).
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 272249b7bd6c22895b7d10e7fbce4a20cb647a49
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419483"
---
# <a name="monitoring-and-troubleshoot-sql-server-big-data-clusters"></a>Supervisión y solución de problemas de clústeres de macrodatos SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describen varios comandos de Kubernetes útiles que puede usar para supervisar y solucionar problemas de un clúster de macrodatos SQL Server 2019 (versión preliminar). Muestra cómo ver detalles detallados de un pod u otros artefactos de Kubernetes que se encuentran en el clúster de Big Data. En este artículo también se tratan las tareas habituales, como copiar archivos en un contenedor o desde uno de los servicios de clúster de macrodatos de SQL Server.

> [!TIP]
> Ejecute los siguientes comandos de **kubectl** en un equipo cliente Windows (CMD o PS) o Linux (Bash). Requieren la autenticación anterior en el clúster y un contexto de clúster con el que ejecutarse. Por ejemplo, para un clúster de AKS creado anteriormente, puede `az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>` ejecutar para descargar el archivo de configuración del clúster de Kubernetes y establecer el contexto del clúster.

## <a name="get-status-of-pods"></a>Obtención del estado de pods

Puede usar el `kubectl get pods` comando para obtener el estado de pods en el clúster para todos los espacios de nombres o para el espacio de nombres del clúster de Big Data. En las secciones siguientes se muestran ejemplos de ambos.

### <a name="show-status-of-all-pods-in-the-kubernetes-cluster"></a>Mostrar el estado de todos los pods en el clúster de Kubernetes

Ejecute el siguiente comando para obtener todos los pods y sus Estados, incluidos los pods que forman parte del espacio de nombres en el que se crean SQL Server pods de clúster de Big Data:

```bash
kubectl get pods --all-namespaces
```

### <a name="show-status-of-all-pods-in-the-sql-server-big-data-cluster"></a>Mostrar el estado de todos los pods en el SQL Server clúster de Big Data

Use el `-n` parámetro para especificar un espacio de nombres concreto. Tenga en cuenta que SQL Server los pods de clúster de macrodatos se crean en un nuevo espacio de nombres creado en el momento del arranque del clúster basado en el nombre del clúster especificado en el archivo de configuración de implementación. El nombre predeterminado, `mssql-cluster`, se utiliza aquí.

```bash
kubectl get pods -n mssql-cluster
```

Debería ver un resultado similar a la lista siguiente para un clúster de Big Data en ejecución:

```output
PS C:\> kubectl get pods -n mssql-cluster
NAME              READY   STATUS    RESTARTS   AGE
appproxy-f2qqt    2/2     Running   0          110m
compute-0-0       3/3     Running   0          110m
control-zlncl     4/4     Running   0          118m
data-0-0          3/3     Running   0          110m
data-0-1          3/3     Running   0          110m
gateway-0         2/2     Running   0          109m
logsdb-0          1/1     Running   0          112m
logsui-jtdnv      1/1     Running   0          112m
master-0          7/7     Running   0          110m
metricsdb-0       1/1     Running   0          112m
metricsdc-shv2f   1/1     Running   0          112m
metricsui-9bcj7   1/1     Running   0          112m
mgmtproxy-x6gcs   2/2     Running   0          112m
nmnode-0-0        1/1     Running   0          110m
storage-0-0       7/7     Running   0          110m
storage-0-1       7/7     Running   0          110m
```

> [!NOTE]
> Durante la implementación, los pods con un **Estado** de **ContainerCreating** siguen apareciendo. Si la implementación se bloquea por cualquier motivo, le puede dar una idea de dónde puede ser el problema. Fíjese también en la columna **listo** . Esto indica cuántos contenedores se han iniciado en el POD. Tenga en cuenta que las implementaciones pueden tardar 30 minutos o más, en función de la configuración y la red. Gran parte de este tiempo se dedica a la descarga de imágenes de contenedor para diferentes componentes.

## <a name="get-pod-details"></a>Obtención de detalles del Pod

Ejecute el siguiente comando para obtener una descripción detallada de un pod específico en la salida de formato JSON. Incluye detalles, como el nodo Kubernetes actual en el que se coloca el POD, los contenedores que se ejecutan dentro del Pod y la imagen que se usa para arrancar los contenedores. También se muestran otros detalles, como las etiquetas, el estado y las notificaciones de volúmenes persistentes que están asociadas con el POD.

```bash
kubectl describe pod  <pod_name> -n <namespace_name>
```

En el ejemplo siguiente se muestran los detalles `master-0` del Pod en un clúster de Big `mssql-cluster`Data denominado:

```bash
kubectl describe pod  master-0 -n mssql-cluster
```

Si se ha producido algún error, a veces puede ver el error en los eventos recientes del Pod.

## <a name="get-pod-logs"></a>Obtención de registros Pod

Puede recuperar los registros de los contenedores que se ejecutan en un pod. El siguiente comando recupera los registros de todos los contenedores que se ejecutan en `master-0` el POD denominado y los envía a `master-0-pod-logs.txt`un nombre de archivo:

```bash
kubectl logs master-0 --all-containers=true -n mssql-cluser > master-0-pod-logs.txt
```

## <a id="services"></a>Obtener el estado de los servicios

Ejecute el siguiente comando para obtener detalles de los servicios de clúster de Big Data. Estos detalles incluyen su tipo y las direcciones IP asociadas a los servicios y puertos correspondientes. Tenga en cuenta que SQL Server los servicios de clúster de macrodatos se crean en un nuevo espacio de nombres creado en el momento del arranque del clúster basado en el nombre del clúster especificado en el archivo de configuración de implementación.

```bash
kubectl get svc -n <namespace_name>
```

En el ejemplo siguiente se muestra el estado de los servicios en un clúster `mssql-cluster`de Big Data denominado:

```bash
kubectl get svc -n mssql-cluster
```

Los siguientes servicios admiten conexiones externas al clúster de Big Data:

| Servicio | Descripción |
|---|---|
| **master-svc-external** | Proporciona acceso a la instancia maestra.<br/>(**External-IP, 31433** y el usuario **SA** ) |
| **controller-svc-external** | Admite herramientas y clientes que administran el clúster. |
| **gateway-svc-external** | Proporciona acceso a la puerta de enlace HDFS/Spark.<br/>(**External-IP** y el usuario **raíz** ) |
| **appproxy-svc-external** | Compatibilidad con escenarios de implementación de aplicaciones. |

> [!TIP]
> Se trata de una manera de ver los servicios con **kubectl**, pero también es posible usar `azdata bdc endpoint list` el comando para ver estos puntos de conexión. Para más información, consulte [obtención de puntos de conexión de clúster de Big Data](deployment-guidance.md#endpoints).

## <a name="get-service-details"></a>Obtener detalles del servicio

Ejecute este comando para obtener una descripción detallada de un servicio en la salida de formato JSON. Se incluirán detalles como las etiquetas, el selector, la dirección IP, la dirección IP externa (si el servicio es de tipo LoadBalancer), el puerto, etc.

```bash
kubectl describe service <service_name> -n <namespace_name>
```

En el ejemplo siguiente se recuperan los detalles del servicio **Master-SVC-external** :

```bash
kubectl describe service master-svc-external -n mssql-cluster
```

## <a name="run-commands-in-a-container"></a>Ejecutar comandos en un contenedor

Si las herramientas o la infraestructura existentes no le permiten realizar una tarea determinada sin estar realmente en el contexto del contenedor, puede iniciar sesión en el contenedor mediante `kubectl exec` el comando. Por ejemplo, puede que tenga que comprobar si existe un archivo específico o puede que necesite reiniciar los servicios del contenedor. 

Para usar el `kubectl exec` comando, use la siguiente sintaxis:

```bash
kubectl exec -it <pod_name>  -c <container_name> -n <namespace_name> -- /bin/bash <command name> 
```

En las dos secciones siguientes se proporcionan dos ejemplos de ejecución de un comando en un contenedor específico.

### <a id="restartsql"></a>Iniciar sesión en un contenedor específico y reiniciar SQL Server proceso

En el ejemplo siguiente se muestra cómo reiniciar el proceso de SQL Server `mssql-server` en el contenedor `master-0` del Pod:

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl restart mssql
```

### <a id="restartservices"></a>Iniciar sesión en un contenedor específico y reiniciar los servicios en un contenedor
 
En el ejemplo siguiente se muestra cómo reiniciar todos los servicios administrados por el **supervisor**: 

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl -c /opt/supervisor/supervisord.conf reload
```

## <a id="copy"></a>Copiar archivos

Si necesita copiar archivos del contenedor en el equipo local, use `kubectl cp` el comando con la siguiente sintaxis:

```bash
kubectl cp <pod_name>:<source_file_path> -c <container_name> -n <namespace_name> <target_local_file_path>
```

Del mismo modo, puede `kubectl cp` usar para copiar archivos del equipo local en un contenedor específico.

```bash
kubectl cp <source_local_file_path> <pod_name>:<target_container_path> -c <container_name>  -n <namespace_name>
```

### <a id="copyfrom"></a>Copiar archivos de un contenedor

En el ejemplo siguiente se copian los archivos de registro de SQL Server `~/temp/sqlserverlogs` del contenedor a la ruta de acceso en el equipo local (en este ejemplo, el equipo local es un cliente Linux):

```bash
kubectl cp master-0:/var/opt/mssql/log -c mssql-server -n mssql-cluster ~/tmp/sqlserverlogs
```

### <a id="copyinto"></a>Copiar archivos en un contenedor

En el ejemplo siguiente se copia el archivo **AdventureWorks2016CTP3. bak** del equipo local en el contenedor de la instancia`mssql-server`principal de SQL Server `master-0` () en el POD. El archivo se copia en el `/tmp` directorio del contenedor. 

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak master-0:/tmp -c mssql-server -n mssql-cluster
```

## <a id="forcedelete"></a>Forzar la eliminación de un pod
 
No se recomienda forzar la eliminación de un pod. Pero para probar la disponibilidad, la resistencia o la persistencia de datos, puede eliminar un POD para simular un error Pod con `kubectl delete pods` el comando.

```bash
kubectl delete pods <pod_name> -n <namespace_name> --grace-period=0 --force
```

En el ejemplo siguiente se elimina el POD del bloque `storage-0-0`de almacenamiento,:

```bash
kubectl delete pods storage-0-0 -n mssql-cluster --grace-period=0 --force
```

## <a id="getip"></a>Obtención de IP Pod
 
Para solucionar problemas, es posible que tenga que obtener la dirección IP del nodo en el que se está ejecutando actualmente un pod. Para obtener la dirección IP, use el `kubectl get pods` comando con la siguiente sintaxis:

```bash
kubectl get pods <pod_name> -o yaml -n <namespace_name> | grep hostIP
```

En el ejemplo siguiente se obtiene la dirección IP del nodo en `master-0` el que se ejecuta el POD:

```bash
kubectl get pods master-0 -o yaml -n mssql-cluster | grep hostIP
```

## <a name="kubernetes-dashboard"></a>Panel de Kubernetes

Puede iniciar el panel de Kubernetes para obtener información adicional sobre el clúster. En las secciones siguientes se explica cómo iniciar el panel de Kubernetes en AKS y para el arranque de Kubernetes con kubeadm.
 
### <a name="start-dashboard-when-cluster-is-running-in-aks"></a>Iniciar el panel cuando el clúster se está ejecutando en AKS

Para iniciar el panel de Kubernetes, ejecute:

```bash
az aks browse --resource-group <azure_resource_group> --name <aks_cluster_name>
```

> [!Note]
> Si recibe el siguiente error: *No se puede escuchar en el puerto 8001: No se pudieron crear todos los agentes de escucha con los siguientes errores: No se puede crear el agente de escucha: Error de escucha tcp4 127.0.0.1:8001: > enlace: Normalmente se permite un uso de cada dirección de socket (protocolo/dirección de red/puerto). No se puede crear el agente de escucha: Error de escucha de tcp6: dirección [[:: 1]]: 8001: falta el puerto en > error de dirección: No se puede escuchar en ninguno de los puertos solicitados: [{8001 9090*}]. Asegúrese de que no inició el panel ya desde otra ventana.

Al iniciar el panel en el explorador, es posible que obtenga advertencias de permisos debido a que el RBAC está habilitado de forma predeterminada en los clústeres de AKS, y la cuenta de servicio usada por el panel no tiene permisos suficientes para  *tener acceso a todos los recursos (por ejemplo, pods está prohibido: El usuario "System: ServiceAccount: Kube-System: kubernetes-Dashboard" no puede enumerar los pods en el*espacio de nombres "default"). Ejecute el siguiente comando para conceder los permisos necesarios `kubernetes-dashboard`a y, a continuación, reinicie el panel:

```bash
kubectl create clusterrolebinding kubernetes-dashboard -n kube-system --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
```

### <a name="start-dashboard-when-kubernetes-cluster-is-bootstrapped--using-kubeadm"></a>Iniciar el panel cuando se arranque el clúster de Kubernetes con kubeadm

Para obtener instrucciones detalladas sobre cómo implementar y configurar el panel en el clúster de Kubernetes, consulte [la documentación de Kubernetes](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/). Para iniciar el panel de Kubernetes, ejecute este comando:

```bash
kubectl proxy
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre los clústeres de Big Data, consulte [¿Qué son](big-data-cluster-overview.md)los clústeres de macrodatos SQL Server.
