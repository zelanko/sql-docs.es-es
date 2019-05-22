---
title: Supervisión y solución de problemas
titleSuffix: SQL Server big data clusters
description: Este artículo proporciona comandos útiles para la supervisión y solución de problemas de un clúster de macrodatos de 2019 de SQL Server (versión preliminar).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 3914bc088ab8974c92a24131d69590b4353f068e
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2019
ms.locfileid: "65994088"
---
# <a name="monitoring-and-troubleshoot-sql-server-big-data-clusters"></a>Supervisión y solución de problemas de clústeres de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe varios comandos útiles de Kubernetes que puede usar para supervisar y solucionar problemas de un clúster de macrodatos de 2019 de SQL Server (versión preliminar). Muestra cómo ver información detallada de un pod u otros artefactos de Kubernetes que se encuentran en el clúster de macrodatos. Este artículo también tratan tareas comunes, como copiar archivos a o desde un contenedor que ejecuta uno de los servicios de clúster de macrodatos de SQL Server.

> [!TIP]
> Ejecute el siguiente **kubectl** comandos en un equipo cliente de Linux (bash) o Windows (cmd o PS). Requiere autenticación anterior en el clúster y ejecutar en un contexto de clúster. Por ejemplo, para un clúster AKS creado previamente puede ejecutar `az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>` para descargar el archivo de configuración de clúster de Kubernetes y establecer el contexto de clúster.

## <a name="get-status-of-pods"></a>Obtener estado de pods

Puede usar el `kubectl get pods` comando para obtener el estado de pods del clúster para todos los espacios de nombres o el espacio de nombres de clúster de macrodatos. Las secciones siguientes muestran ejemplos de ambos.

### <a name="show-status-of-all-pods-in-the-kubernetes-cluster"></a>Mostrar el estado de todos los pods del clúster de Kubernetes

Ejecute el comando siguiente para obtener todos los pods y sus Estados, incluidos los pods que forman parte del espacio de nombres que SQL Server se crean los pods del clúster de macrodatos en:

```bash
kubectl get pods --all-namespaces
```

### <a name="show-status-of-all-pods-in-the-sql-server-big-data-cluster"></a>Mostrar el estado de todos los pods en el clúster de macrodatos de SQL Server

Use el `-n` parámetro para especificar un espacio de nombres específico. Tenga en cuenta que los pods de clúster de macrodatos de SQL Server se crean en un espacio de nombres nuevo creado en tiempo de arranque del clúster según el nombre de clúster especificado en el archivo de configuración de implementación. El nombre predeterminado, `mssql-cluster`, se usa aquí.

```bash
kubectl get pods -n mssql-cluster
```

Debería ver resultados similares a la lista siguiente para un clúster de macrodatos funcionamiento:

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
> Durante la implementación, pods con un **estado** de **ContainerCreating** todavía próximamente. Si la implementación se bloquea por cualquier motivo, esto puede darle una idea donde podría ser el problema. Examine también el **listo** columna. Esto indica cuántos contenedores se han iniciado en el pod. Tenga en cuenta que las implementaciones pueden tardar 30 minutos o más dependiendo de su configuración y la red. Gran parte de este tiempo se dedica a descargar las imágenes de contenedor para los distintos componentes.

## <a name="get-pod-details"></a>Obtener detalles de pod

Ejecute el siguiente comando para obtener una descripción detallada de un pod específico en la salida del formato JSON. Incluye detalles como el nodo actual de Kubernetes que se coloca el pod, los contenedores que se ejecutan en el pod y la imagen que se utiliza para arrancar los contenedores. También se muestran otros detalles, como etiquetas, estado y conserva las notificaciones de los volúmenes que están asociadas con el pod.

```bash
kubectl describe pod  <pod_name> -n <namespace_name>
```

El ejemplo siguiente muestra los detalles de la `master-0` pod en un clúster de macrodatos denominado `mssql-cluster`:

```bash
kubectl describe pod  master-0 -n mssql-cluster
```

Si ha habido algún error, a veces puede ver el error en los eventos recientes para el pod.

## <a name="get-pod-logs"></a>Obtener registros del pod

Puede recuperar los registros de contenedores que se ejecutan en un pod. El comando siguiente recupera los registros para todos los contenedores que se ejecutan en el pod denominado `master-0` y la envía a un nombre de archivo `master-0-pod-logs.txt`:

```bash
kubectl logs master-0 --all-containers=true -n mssql-cluser > master-0-pod-logs.txt
```

## <a id="services"></a> Obtener el estado de servicios

Ejecute el siguiente comando para obtener detalles de los servicios de clúster de macrodatos. Estos detalles incluyen su tipo y las direcciones IP asociadas con puertos y los servicios correspondientes. Tenga en cuenta que los servicios de clúster de macrodatos de SQL Server se crean en un espacio de nombres nuevo creado en tiempo de arranque del clúster según el nombre de clúster especificado en el archivo de configuración de implementación.

```bash
kubectl get svc -n <namespace_name>
```

En el ejemplo siguiente se muestra el estado de los servicios en un clúster de macrodatos denominado `mssql-cluster`:

```bash
kubectl get svc -n mssql-cluster
```

Los siguientes servicios admiten conexiones externas al clúster de macrodatos:

| ssNoVersion | Descripción |
|---|---|
| **master-svc-external** | Proporciona acceso a la instancia maestra.<br/>(**EXTERNAL-IP, 31433** y **SA** usuario) |
| **controller-svc-external** | Es compatible con las herramientas y los clientes que administran el clúster. |
| **mgmtproxy-svc-external** | Proporciona acceso a la [Portal de administración de clúster](cluster-admin-portal.md).<br/>(https://**EXTERNAL-IP**:30777/portal) |
| **gateway-svc-external** | Proporciona acceso a la puerta de enlace de Spark o HDFS.<br/>(**EXTERNAL-IP** y **raíz** usuario) |
| **appproxy-svc-external** | Admite escenarios de implementación de la aplicación. |

> [!TIP]
> Se trata de una manera de ver los servicios con **kubectl**, pero también es posible usar `mssqlctl cluster endpoint list` comando para ver estos puntos de conexión. Para obtener más información, consulte [obtener puntos de conexión de clúster de macrodatos](deployment-guidance.md#endpoints).

## <a name="get-service-details"></a>Obtener detalles de servicio

Ejecute este comando para obtener una descripción detallada de un servicio en la salida del formato JSON. Se incluyen detalles como etiquetas, selector, IP, external-IP (si el servicio es de tipo de equilibrador de carga), el puerto, etcetera.

```bash
kubectl describe service <service_name> -n <namespace_name>
```

En el ejemplo siguiente se recuperan los detalles de la **master-svc-external** servicio:

```bash
kubectl describe service master-svc-external -n mssql-cluster
```

## <a name="run-commands-in-a-container"></a>Ejecute los comandos en un contenedor

Si las herramientas existentes o la infraestructura no permite realizar una tarea determinada sin ser realmente en el contexto del contenedor, puede iniciar sesión en el contenedor mediante `kubectl exec` comando. Por ejemplo, es posible que deba Compruebe si existe un archivo específico, o si es posible que deba reiniciar los servicios en el contenedor. 

Para usar el `kubectl exec` de comandos, use la sintaxis siguiente:

```bash
kubectl exec -it <pod_name>  -c <container_name> -n <namespace_name> -- /bin/bash <command name> 
```

Las dos secciones siguientes proporcionan dos ejemplos de ejecutar un comando en un contenedor específico.

### <a id="restartsql"></a> Inicie sesión en un contenedor específico y reinicie el proceso de SQL Server

El ejemplo siguiente muestra cómo reiniciar el proceso de SQL Server en el `mssql-server` contenedor en el `master-0` pod:

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl restart mssql
```

### <a id="restartservices"></a> Inicie sesión en un contenedor específico y reiniciar los servicios en un contenedor
 
El ejemplo siguiente muestra cómo reiniciar todos los servicios administrados por **supervisord**: 

```bash
kubectl exec -it master-0  -c mssql-server -n mssql-cluster -- /bin/bash 
supervisorctl -c /opt/supervisor/supervisord.conf reload
```

## <a id="copy"></a> Copiar archivos

Si tiene que copiar los archivos del contenedor en el equipo local, use `kubectl cp` comando con la sintaxis siguiente:

```bash
kubectl cp <pod_name>:<source_file_path> -c <container_name> -n <namespace_name> <target_local_file_path>
```

De forma similar, puede usar `kubectl cp` para copiar archivos desde el equipo local en un contenedor específico.

```bash
kubectl cp <source_local_file_path> <pod_name>:<target_container_path> -c <container_name>  -n <namespace_name>
```

### <a id="copyfrom"></a> Copiar archivos desde un contenedor

El siguiente ejemplo copia los archivos de registro de SQL Server desde el contenedor para el `~/temp/sqlserverlogs` ruta de acceso en el equipo local (en este ejemplo en el equipo local es un cliente Linux):

```bash
kubectl cp master-0:/var/opt/mssql/log -c mssql-server -n mssql-cluster ~/tmp/sqlserverlogs
```

### <a id="copyinto"></a> Copie los archivos de contenedor

Las copias de ejemplo siguiente la **AdventureWorks2016CTP3.bak** archivo desde el equipo local en el contenedor de la instancia principal de SQL Server (`mssql-server`) en el `master-0` pod. El archivo se copia en el `/tmp` directorio en el contenedor. 

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak master-0:/tmp -c mssql-server -n mssql-cluster
```

## <a id="forcedelete"></a> Forzar la eliminación un pod
 
No se recomienda para forzar la eliminación de un pod. Pero para las pruebas de disponibilidad, resistencia o persistencia de datos, se puede eliminar un pod para simular un error de pod con el `kubectl delete pods` comando.

```bash
kubectl delete pods <pod_name> -n <namespace_name> --grace-period=0 --force
```

En el ejemplo siguiente se elimina el pod del grupo de almacenamiento, `storage-0-0`:

```bash
kubectl delete pods storage-0-0 -n mssql-cluster --grace-period=0 --force
```

## <a id="getip"></a> Obtener dirección IP de pod
 
Para solucionar problemas, deberá obtener la dirección IP del nodo que se está ejecutando actualmente en un pod. Para obtener la dirección IP, utilice el `kubectl get pods` comando con la sintaxis siguiente:

```bash
kubectl get pods <pod_name> -o yaml -n <namespace_name> | grep hostIP
```

En el ejemplo siguiente se obtiene la dirección IP del nodo que la `master-0` pod se ejecuta en:

```bash
kubectl get pods master-0 -o yaml -n mssql-cluster | grep hostIP
```

## <a name="cluster-administration-portal"></a>Portal de administración de clústeres

Use la [portal de administración de clúster](cluster-admin-portal.md) para supervisar el estado del clúster de macrodatos. Por ejemplo, durante las implementaciones, puede usar el **implementación** ficha. Tendrá que esperar el **mgmtproxy-svc-external** que se inicie antes de acceder a este portal, por lo que no estará disponible al principio de una implementación de servicio.

## <a name="kubernetes-dashboard"></a>Panel de Kubernetes

Puede iniciar el panel de Kubernetes para obtener más información sobre el clúster. Las siguientes secciones explican cómo iniciar el panel de Kubernetes en AKS y de Kubernetes kubeadm de arrancar.
 
### <a name="start-dashboard-when-cluster-is-running-in-aks"></a>Iniciar panel cuando el clúster se ejecuta en AKS

Para iniciar el panel de Kubernetes que ejecute:

```bash
az aks browse --resource-group <azure_resource_group> --name <aks_cluster_name>
```

> [!Note]
> Si recibe el error siguiente: *No se puede escuchar en el puerto 8001: Todos los agentes de escucha no se pudo crear con los siguientes errores: No se puede crear el agente de escucha: Error escuchar tcp4 127.0.0.1:8001: > enlazar: Normalmente se permite un solo uso de cada dirección de socket (dirección de red Protocolo/puerto). No se puede crear el agente de escucha: Error escuchar tcp6: dirección [[:: 1]]: 8001: falta el puerto en > error de dirección: No se puede escuchar en cualquiera de los puertos solicitados: [{8001 9090}]*, asegúrese de que no se inició el panel ya desde otra ventana.

Al iniciar el panel del explorador, podría obtener advertencias permiso debido a que se está habilitado de forma predeterminada en los clústeres de AKS de RBAC y la cuenta de servicio usada por el panel no tiene permisos suficientes para tener acceso a todos los recursos (por ejemplo,  *está prohibido Pods: Usuario "del sistema: serviceaccount:kube-kubernetes: sistema-panel" no se pueden enumerar los pods en el espacio de nombres "predeterminado"*). Ejecute el comando siguiente para conceder los permisos necesarios para `kubernetes-dashboard`y, a continuación, reinicie el panel:

```bash
kubectl create clusterrolebinding kubernetes-dashboard -n kube-system --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
```

### <a name="start-dashboard-when-kubernetes-cluster-is-bootstrapped--using-kubeadm"></a>Iniciar panel cuando se arranca un clúster de Kubernetes mediante kubeadm

Para obtener instrucciones detalladas para implementar y configurar el panel en el clúster de Kubernetes, consulte [la documentación de Kubernetes](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/). Para iniciar el panel de Kubernetes, ejecute este comando:

```bash
kubectl proxy
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de datos de gran tamaño, vea [¿cuáles son los clústeres de SQL Server macrodatos](big-data-cluster-overview.md).
