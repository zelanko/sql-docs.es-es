---
title: Use kubectl para solucionar problemas de monitor /
titleSuffix: SQL Server big data clusters
description: En este artículo se proporcionan comandos de kubectl útil para la supervisión y solución de problemas de un clúster de macrodatos de 2019 de SQL Server (versión preliminar).
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 8b9be0566725822e0241c65c7f8324b153cca072
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860376"
---
# <a name="kubectl-commands-for-monitoring-and-troubleshooting-sql-server-big-data-clusters"></a>Comandos de Kubectl para la supervisión y solución de problemas de clústeres de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe varios comandos útiles de Kubernetes que puede usar para supervisar y solucionar problemas de un clúster de macrodatos de 2019 de SQL Server (versión preliminar). Este artículo tratan las tareas comunes, como copiar archivos a o desde un contenedor que ejecuta uno de los servicios de clúster de macrodatos de SQL Server. También muestra cómo ver información detallada de un pod u otros artefactos de Kubernetes que se encuentran en el clúster de macrodatos.

## <a name="kubectl-command-examples"></a>Ejemplos de comandos de Kubectl

Ejecute el siguiente **kubectl** comandos en un equipo cliente de Linux (bash) o Windows (cmd o PS). Requiere autenticación anterior en el clúster y ejecutar en un contexto de clúster. Por ejemplo, para un clúster AKS creado previamente puede ejecutar `az aks get-credentials --name <aks_cluster_name> --resource-group <azure_resource_group_name>` para descargar el archivo de configuración de clúster de Kubernetes y establecer el contexto de clúster.

## <a name="get-status-of-pods"></a>Obtener estado de pods

Puede usar el `kubectl get pods` comando para obtener el estado de pods del clúster para todos los espacios de nombres o el espacio de nombres de clúster de macrodatos. Las secciones siguientes muestran ejemplos de ambos.

### <a name="show-status-of-all-pods-in-the-kubernetes-cluster"></a>Mostrar el estado de todos los pods del clúster de Kubernetes

Ejecute el comando siguiente para obtener todos los pods y sus Estados, incluidos los pods que forman parte del espacio de nombres que SQL Server se crean los pods del clúster de macrodatos en:

```bash
kubectl get pods --all-namespaces
```

### <a name="show-status-of-all-pods-in-the-sql-server-big-data-cluster"></a>Mostrar el estado de todos los pods en el clúster de macrodatos de SQL Server

Use el `-n` parámetro para especificar un espacio de nombres específico. Tenga en cuenta que se crean los pods del clúster de macrodatos en un nuevo espacio de nombres que se crea en tiempo de arranque del clúster de SQL Server se basa en el nombre de clúster especificado en el `mssqlctl cluster create --name <cluster_name>` comando.

```bash
kubectl get pods -n <namespace_name>
```

Por ejemplo, el siguiente comando muestra el estado de pods en un clúster de macrodatos denominado `big_data_cluster`:

```bash
kubectl get pods -n big_data_cluster
```

## <a name="get-pod-details"></a>Obtener detalles de pod

Ejecute el siguiente comando para obtener una descripción detallada de un pod específico en la salida del formato json. Incluye detalles como el nodo actual de Kubernetes que se coloca el pod, los contenedores que se ejecutan en el pod y la imagen que se utiliza para arrancar los contenedores. También se muestran otros detalles, como etiquetas, estado y conserva las notificaciones de los volúmenes que están asociadas con el pod.

```bash
kubectl describe pod  <pod_name> -n <namespace_name>
```

El ejemplo siguiente muestra los detalles de la `mssql-data-pool-master-0` pod en un clúster de macrodatos denominado `big_data_cluster`:

```bash
kubectl describe pod  mssql-data-pool-master-0 -n big_data_cluster
```

## <a name="get-status-of-services"></a>Obtener el estado de servicios

Ejecute el siguiente comando para obtener detalles de los servicios de clúster de macrodatos. Estos detalles incluyen su tipo y las direcciones IP asociadas con puertos y los servicios correspondientes. Tenga en cuenta que los servicios de clúster de macrodatos de SQL Server se crean en un espacio de nombres nuevo creado en tiempo de arranque del clúster según el nombre de clúster especificado en el `mssqlctl cluster create --name <cluster_name>` comando.

```bash
kubectl get svc -n <namespace_name>
```

En el ejemplo siguiente se muestra el estado de los servicios en un clúster de macrodatos denominado `big_data_cluster`:

```bash
kubectl get svc -n big_data_cluster
```

## <a name="get-service-details"></a>Obtener detalles de servicio

Ejecute este comando para obtener una descripción detallada de un servicio en la salida del formato json. Se incluyen detalles como etiquetas, selector, IP, external-IP (si el servicio es de tipo de equilibrador de carga), el puerto, etcetera.
```
kubectl describe pod  <pod_name> -n <namespace_name>
```

Ejemplo:
```
kubectl describe pod  mssql-data-pool-master-0 -n big_data_cluster
```

## <a name="run-commands-in-a-container"></a>Ejecute los comandos en un contenedor

Si las herramientas existentes o la infraestructura no permite realizar una tarea determinada sin ser realmente en el contexto del contenedor, puede iniciar sesión en el contenedor mediante `kubectl exec` comando. Por ejemplo, es posible que deba Compruebe si existe un archivo específico, o si es posible que deba reiniciar los servicios en el contenedor. 

Para usar el `kubectl exec` de comandos, use la sintaxis siguiente:

```bash
kubectl exec -it <pod_name>  -c <container_name> -n <namespace_name> -- /bin/bash <command name> 
```

Las dos secciones siguientes proporcionan dos ejemplos de ejecutar un comando en un contenedor específico.

### <a id="restartsql"></a> Inicie sesión en un contenedor específico y reinicie el proceso de SQL Server

El ejemplo siguiente muestra cómo reiniciar el proceso de SQL Server en el `mssql-server` contenedor en el `mssql-master-pool-0` pod:

```bash
kubectl exec -it mssql-master-pool-0  -c mssql-server -n big_data_cluster -- /bin/bash 
supervisorctl restart mssql
```

### <a id="restartservices"></a> Inicie sesión en un contenedor específico y reiniciar los servicios en un contenedor
 
El ejemplo siguiente muestra cómo reiniciar todos los servicios administrados por **supervisord**: 

```bash
kubectl exec -it mssql-master-pool-0  -c mssql-server -n big_data_cluster -- /bin/bash 
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
kubectl cp mssql-master-pool-0:/var/opt/mssql/log -c mssql-server -n big_data_cluster ~/tmp/sqlserverlogs
```

### <a id="copyinto"></a> Copie los archivos de contenedor

Las copias de ejemplo siguiente la **AdventureWorks2016CTP3.bak** archivo desde el equipo local en el contenedor de la instancia principal de SQL Server (`mssql-server`) en el `mssql-master-pool-0` pod. El archivo se copia en el `/tmp` directorio en el contenedor. 

```bash
kubectl cp ~/Downloads/AdventureWorks2016CTP3.bak mssql-master-pool-0:/tmp -c mssql-server -n big_data_cluster
```

## <a id="forcedelete"></a> Forzar la eliminación un pod
 
No se recomienda para forzar la eliminación de un pod. Pero para las pruebas de disponibilidad, resistencia o persistencia de datos, se puede eliminar un pod para simular un error de pod con el `kubectl delete pods` comando.

```bash
kubectl delete pods <pod_name> -n <namespace_name> --grace-period=0 --force
```

En el ejemplo siguiente se elimina el pod del grupo de almacenamiento, `mssql-storage-pool-default-0`:

```bash
kubectl delete pods mssql-storage-pool-default-0 -n big_data_cluster --grace-period=0 --force
```

## <a id="getip"></a> Obtener dirección IP de pod
 
Para solucionar problemas, deberá obtener la dirección IP del nodo que se está ejecutando actualmente en un pod. Para obtener la dirección IP, utilice el `kubectl get pods` comando con la sintaxis siguiente:

```bash
kubectl get pods <pod_name> -o yaml -n <namespace_name> | grep hostIP
```

En el ejemplo siguiente se obtiene la dirección IP del nodo que la `mssql-master-pool-0` pod se ejecuta en:

```bash
kubectl get pods mssql-master-pool-0 -o yaml -n big_data_cluster | grep hostIP
```

## <a name="start-the-kubernetes-dashboard"></a>Iniciar el panel de Kubernetes

Puede iniciar el panel de Kubernetes para obtener más información sobre el clúster. Las siguientes secciones explican cómo iniciar el panel de Kubernetes en AKS y de Kubernetes kubeadm de arrancar.
 
### <a name="start-dashboard-when-cluster-is-running-in-aks"></a>Iniciar panel cuando el clúster se ejecuta en AKS

Para iniciar el panel de Kubernetes que ejecute:
 
```bash
az aks browse --resource-group <azure_resource_group> --name <aks_cluster_name>
```

> [!Note]
> Si recibe el error siguiente: *No se puede escuchar en el puerto 8001: Todos los agentes de escucha no se pudo crear con los siguientes errores: No se puede crear el agente de escucha: Error escuchar tcp4 127.0.0.1:8001: > enlazar: Normalmente se permite un solo uso de cada dirección de socket (dirección de red Protocolo/puerto). No se puede crear el agente de escucha: Error escuchar tcp6: dirección [[:: 1]]: 8001: falta el puerto en > error de dirección: No se puede escuchar en cualquiera de los puertos solicitados: [{8001 9090}]*, asegúrese de que no se inició el panel ya desde otra ventana.

Al iniciar el panel del explorador, podría obtener advertencias permiso debido a que se está habilitado de forma predeterminada en los clústeres de AKS de RBAC y la cuenta de servicio usada por el panel no tiene permisos suficientes para tener acceso a todos los recursos (por ejemplo,  *está prohibido Pods: Usuario "del sistema: serviceaccount:kube-kubernetes: sistema-panel" no se pueden enumerar los pods en el espacio de nombres "predeterminado"*). Ejecute el comando siguiente para conceder los permisos necesarios para `kubernetes-dashboard`y, a continuación, reinicie el panel:

```
kubectl create clusterrolebinding kubernetes-dashboard -n kube-system --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
```

### <a name="start-dashboard-when-kubernetes-cluster-is-bootstrapped--using-kubeadm"></a>Iniciar panel cuando se arranca un clúster de Kubernetes mediante kubeadm

Para obtener instrucciones detalladas para implementar y configurar el panel en el clúster de Kubernetes, consulte [la documentación de Kubernetes](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/). Para iniciar el panel de Kubernetes, ejecute este comando:

```
kubectl proxy
```

## <a name="next-steps"></a>Pasos siguientes

Para la supervisión y solución de problemas que es específica de SQL Server macrodatos clústeres, consulte el [portal de administración de clúster](cluster-admin-portal.md).