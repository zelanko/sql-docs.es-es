---
title: Implementar un contenedor de SQL Server en Kubernetes con Azure Kubernetes Services (AKS) | Microsoft Docs
description: Este tutorial muestra cómo implementar una solución de alta disponibilidad de SQL Server con Kubernetes en Azure Kubernetes Service.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 01/10/2018
ms.topic: tutorial
ms.prod: sql
ms.custom: sql-linux,mvc
ms.technology: linux
ms.openlocfilehash: 44f81a23d341e549243b8e99366fef435be04ffa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47808633"
---
# <a name="deploy-a-sql-server-container-in-kubernetes-with-azure-kubernetes-services-aks"></a>Implementar un contenedor de SQL Server en Kubernetes con Azure Kubernetes Services (AKS)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Obtenga información sobre cómo configurar una instancia de SQL Server en Kubernetes en Azure Kubernetes Service (AKS), con el almacenamiento persistente de alta disponibilidad (HA). La solución proporciona resistencia. Si se produce un error en la instancia de SQL Server, Kubernetes automáticamente vuelve a crearla en un pod nuevo. Kubernetes también proporciona resistencia frente a un error de nodo.

Este tutorial muestra cómo configurar una instancia de SQL Server de alta disponibilidad en un contenedor de AKS. También puede [crear un grupo de disponibilidad de SQL Server en Kubernetes](tutorial-sql-server-ag-kubernetes.md). Para comparar las dos soluciones diferentes de Kubernetes, consulte [alta disponibilidad para los contenedores de SQL Server](sql-server-linux-container-ha-overview.md).

> [!div class="checklist"]
> * Crear una contraseña de SA
> * Crear almacenamiento
> * Crear la implementación
> * Conectar con SQL Server Management Studio (SSMS)
> * Compruebe el error y recuperación

## <a name="ha-solution-on-kubernetes-running-in-azure-kubernetes-service"></a>Solución de alta disponibilidad en Kubernetes que se ejecuta en Azure Kubernetes Service

Kubernetes 1.6 y versiones posteriores es compatible con [clases de almacenamiento](http://kubernetes.io/docs/concepts/storage/storage-classes/), [notificaciones de volumen persistente](http://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims)y el [tipo de volumen de disco de Azure](https://github.com/kubernetes/examples/tree/master/staging/volumes/azure_disk). Puede crear y administrar las instancias de SQL Server de forma nativa en Kubernetes. El ejemplo de este artículo muestra cómo crear un [implementación](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) para lograr una configuración de alta disponibilidad similar a una instancia de clúster de conmutación por error de disco compartido. En esta configuración, Kubernetes desempeña la función del orquestador de clúster. Cuando se produce un error en una instancia de SQL Server en un contenedor, el orquestador arranca otra instancia del contenedor al que se adjunta al mismo almacenamiento persistente.

![Diagrama del clúster de Kubernetes SQL Server](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

En el diagrama anterior, `mssql-server` es un contenedor en un [pod](http://kubernetes.io/docs/concepts/workloads/pods/pod/). Kubernetes orquesta los recursos del clúster. Un [conjunto de réplicas](http://kubernetes.io/docs/concepts/workloads/controllers/replicaset/) garantiza que el pod se recupera automáticamente después de un error de nodo. Las aplicaciones se conectan al servicio. En este caso, el servicio representa un equilibrador de carga que hospeda una dirección IP que permanece igual después de un error de la `mssql-server`.

En el diagrama siguiente, la `mssql-server` contenedor ha producido un error. Como el orquestador, Kubernetes garantiza establece el recuento correcto de instancias en buen estado en la réplica e inicia un nuevo contenedor de acuerdo con la configuración. El orquestador inicia un nuevo conjunto pod en el mismo nodo, y `mssql-server` se vuelve a conectar al mismo almacenamiento persistente. El servicio se conecta a volver a crearse `mssql-server`.

![Diagrama del clúster de Kubernetes SQL Server](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-node-fail.png)

En el diagrama siguiente, el nodo que hospeda el `mssql-server` contenedor ha producido un error. El orquestador inicia el pod nuevo en un nodo diferente, y `mssql-server` se vuelve a conectar al mismo almacenamiento persistente. El servicio se conecta a volver a crearse `mssql-server`.

![Diagrama del clúster de Kubernetes SQL Server](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-pod-fail.png)

## <a name="prerequisites"></a>Requisitos previos

* **Clúster de Kubernetes**
   - El tutorial requiere un clúster de Kubernetes. Utilizan los pasos [kubectl](https://kubernetes.io/docs/user-guide/kubectl/) para administrar el clúster. 

   - Consulte [implementar un clúster de Azure Container Service (AKS)](http://docs.microsoft.com/azure/aks/tutorial-kubernetes-deploy-cluster) para crear y conectarse a un clúster de nodo único de Kubernetes en AKS con `kubectl`. 

   >[!NOTE]
   >Para protegerse frente a errores de nodo, un clúster de Kubernetes requiere más de un nodo.

* **CLI de Azure 2.0.23**
   - Las instrucciones de este tutorial se han validado con la CLI de Azure 2.0.23.

## <a name="create-an-sa-password"></a>Crear una contraseña de SA

Crear una contraseña de SA en el clúster de Kubernetes. Kubernetes puede administrar la información de configuración confidencial, como contraseñas como [secretos](http://kubernetes.io/docs/concepts/configuration/secret/).

El siguiente comando crea una contraseña para la cuenta SA:

   ```azurecli
   kubectl create secret generic mssql --from-literal=SA_PASSWORD="MyC0m9l&xP@ssw0rd"
   ```  

   Reemplace `MyC0m9l&xP@ssw0rd` con una contraseña compleja.

   Para crear un secreto de Kubernetes denominado `mssql` que contiene el valor `MyC0m9l&xP@ssw0rd` para el `SA_PASSWORD`, ejecute el comando.


## <a name="create-storage"></a>Crear almacenamiento

Configurar un [volumen persistente](http://kubernetes.io/docs/concepts/storage/persistent-volumes/) y [notificación de volumen persistente](http://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistent-volume-claim-protection) en el clúster de Kubernetes. Complete los pasos siguientes: 

1. Crear un manifiesto para definir la clase de almacenamiento y el volumen persistente de notificación.  El manifiesto especifica el aprovisionador de almacenamiento, parámetros, y [reclamar directiva](http://kubernetes.io/docs/concepts/storage/persistent-volumes/#reclaiming). El clúster de Kubernetes usa este manifiesto para crear el almacenamiento persistente. 

   El siguiente ejemplo de yaml define una clase de almacenamiento y la notificación de volumen persistente. Es el aprovisionador de clase de almacenamiento `azure-disk`, porque este clúster de Kubernetes en Azure. El tipo de cuenta de almacenamiento es `Standard_LRS`. La notificación de volumen persistente se denomina `mssql-data`. Los metadatos de la notificación de volumen persistente incluyen un nuevo a la clase de almacenamiento de la conexión de la anotación. 

   ```yaml
   kind: StorageClass
   apiVersion: storage.k8s.io/v1beta1
   metadata:
        name: azure-disk
   provisioner: kubernetes.io/azure-disk
   parameters:
     storageaccounttype: Standard_LRS
     kind: Managed
   ---
   kind: PersistentVolumeClaim
   apiVersion: v1
   metadata:
     name: mssql-data
     annotations:
       volume.beta.kubernetes.io/storage-class: azure-disk
   spec:
     accessModes:
     - ReadWriteOnce
     resources:
       requests:
         storage: 8Gi
   ```

   Guarde el archivo (por ejemplo, **pvc.yaml**).

1. Cree la notificación de volumen persistente de Kubernetes.

   ```azurecli
   kubectl apply -f <Path to pvc.yaml file>
   ```

   `<Path to pvc.yaml file>` es la ubicación donde guardó el archivo.

   El volumen persistente automáticamente se crea como una cuenta de almacenamiento de Azure y enlazado a la notificación de volumen persistente. 

    ![Captura de pantalla del comando de notificación de volumen persistente](media/tutorial-sql-server-containers-kubernetes/02_pvc_cmd.png)

1. Compruebe la notificación de volumen persistente.

   ```azurecli
   kubectl describe pvc <PersistentVolumeClaim>
   ```

   `<PersistentVolumeClaim>` es el nombre de la notificación de volumen persistente.

   En el paso anterior, se denomina la notificación de volumen persistente `mssql-data`. Para ver los metadatos acerca de la notificación de volumen persistente, ejecute el siguiente comando:

   ```azurecli
   kubectl describe pvc mssql-data
   ```

   Los metadatos devueltos incluyen un valor denominado `Volume`. Este valor se asigna al nombre del blob.

   ![Captura de pantalla de los metadatos devueltos, incluidos el volumen](media/tutorial-sql-server-containers-kubernetes/describe-volume.png)

   El valor de volumen coincide con la parte del nombre del blob en la siguiente imagen desde el portal de Azure: 

   ![Nombre de blob de portal de la captura de pantalla de Azure](media/tutorial-sql-server-containers-kubernetes/describe-volume-portal.png)

1. Compruebe el volumen persistente.

   ```azurecli
   kubectl describe pv
   ```

   `kubectl` Devuelve los metadatos de volumen persistente que se crea automáticamente y se enlazan a la notificación de volumen persistente. 

## <a name="create-the-deployment"></a>Crear la implementación

En este ejemplo, el contenedor que hospeda la instancia de SQL Server se describe como un objeto de implementación de Kubernetes. La implementación crea un conjunto de réplicas. El conjunto de réplicas, crea el pod. 

En este paso, creará un manifiesto para describir el contenedor en función del servidor SQL [mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/) imagen de Docker. Las referencias de manifiesto la `mssql-server` notificación de volumen persistente y el `mssql` secreto que ya ha aplicado al clúster de Kubernetes. El manifiesto también describe una [servicio](http://kubernetes.io/docs/concepts/services-networking/service/). Este servicio es un equilibrador de carga. El equilibrador de carga garantiza que la dirección IP se conserve después de que se recupera la instancia de SQL Server. 

1. Cree un manifiesto (un archivo YAML) para describir la implementación. El ejemplo siguiente describe una implementación, incluido un contenedor en función de la imagen de contenedor de SQL Server.

   ```yaml
   apiVersion: apps/v1beta1
   kind: Deployment
   metadata:
     name: mssql-deployment
   spec:
     replicas: 1
     template:
       metadata:
         labels:
           app: mssql
       spec:
         terminationGracePeriodSeconds: 10
         containers:
         - name: mssql
           image: mcr.microsoft.com/mssql/server/mssql-server-linux
           ports:
           - containerPort: 1433
           env:
           - name: ACCEPT_EULA
             value: "Y"
           - name: SA_PASSWORD
             valueFrom:
               secretKeyRef:
                 name: mssql
                 key: SA_PASSWORD 
           volumeMounts:
           - name: mssqldb
             mountPath: /var/opt/mssql
         volumes:
         - name: mssqldb
           persistentVolumeClaim:
             claimName: mssql-data
   ---
   apiVersion: v1
   kind: Service
   metadata:
     name: mssql-deployment
   spec:
     selector:
       app: mssql
     ports:
       - protocol: TCP
         port: 1433
         targetPort: 1433
     type: LoadBalancer
   ```

   Copie el código anterior en un nuevo archivo denominado `sqldeployment.yaml`. Actualice los valores siguientes: 

   * `value: "Developer"`: Establece el contenedor para la ejecución de SQL Server Developer edition. Edición para desarrolladores no tiene licencia para los datos de producción. Si la implementación es para su uso en producción, establezca la edición adecuada (`Enterprise`, `Standard`, o `Express`). 

      >[!NOTE]
      >Para obtener más información, consulte [licencias de SQL Server](http://www.microsoft.com/sql-server/sql-server-2017-pricing).

   * `persistentVolumeClaim`: Este valor requiere una entrada para `claimName:` que asigna el nombre utilizado para la notificación de volumen persistente. Este tutorial se usa `mssql-data`. 

   * `name: SA_PASSWORD`: Configura la imagen de contenedor para establecer la contraseña de SA, tal como se define en esta sección.

     ```yaml
     valueFrom:
       secretKeyRef:
         name: mssql
         key: SA_PASSWORD 
     ```

     Cuando implementa el contenedor en Kubernetes, hace referencia al secreto llamado `mssql` para obtener el valor de la contraseña. 

   >[!NOTE]
   >Mediante el uso de la `LoadBalancer` tipo de servicio, la instancia de SQL Server es accesible de forma remota (a través de internet) en el puerto 1433.

   Guarde el archivo (por ejemplo, **sqldeployment.yaml**).

1. Crear la implementación.

   ```azurecli
   kubectl apply -f <Path to sqldeployment.yaml file>
   ```

   `<Path to sqldeployment.yaml file>` es la ubicación donde guardó el archivo.

   ![Captura de pantalla del comando de implementación](media/tutorial-sql-server-containers-kubernetes/04_deploy_cmd.png)

   La implementación y el servicio se crean. La instancia de SQL Server está en un contenedor, conectado a un almacenamiento persistente.

   Para ver el estado de lo pod, escriba `kubectl get pod`.

   ![Captura de pantalla del comando de get pod](media/tutorial-sql-server-containers-kubernetes/05_get_pod_cmd.png)

   En la imagen anterior, el pod tiene un estado de `Running`. Este estado indica que el contenedor está listo. Esto puede tardar varios minutos.

   >[!NOTE]
   >Una vez creada la implementación, puede tardar unos minutos antes de que está visible el pod. El retraso sea porque el clúster extrae la [mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/) imagen desde Docker hub. Después de la imagen se extrae la primera vez, las implementaciones posteriores pueden ser más rápidas si la implementación es en un nodo que ya tiene la imagen almacenada en ella. 

1. Compruebe que se ejecutan los servicios. Ejecute el siguiente comando:

   ```azurecli
   kubectl get services 
   ```

   Este comando devuelve los servicios que se ejecutan, así como las direcciones IP internas y externas para los servicios. Tenga en cuenta la dirección IP externa para el `mssql-deployment` service. Use esta dirección IP para conectarse a SQL Server. 

   ![Captura de pantalla del comando get del servicio](media/tutorial-sql-server-containers-kubernetes/06_get_service_cmd.png)

   Para obtener más información sobre el estado de los objetos en el clúster de Kubernetes, ejecute:

   ```azurecli
   az aks browse --resource-group <MyResourceGroup> --name <MyKubernetesClustername>
   ```  

## <a name="connect-to-the-sql-server-instance"></a>Conéctese a la instancia de SQL Server

Si ha configurado el contenedor, como se describe, puede conectar con una aplicación desde fuera de la red virtual de Azure. Use la `sa` cuenta y la dirección IP externa de direcciones para el servicio. Use la contraseña que ha configurado como el secreto de Kubernetes. 

Puede usar las siguientes aplicaciones para conectarse a la instancia de SQL Server. 

* [SSMS](http://docs.microsoft.com/sql/linux/sql-server-linux-manage-ssms)

* [SSDT](http://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-ssdt)

* sqlcmd
   
   Para conectarse con `sqlcmd`, ejecute el siguiente comando:

   ```cmd
   sqlcmd -S <External IP Address> -U sa -P "MyC0m9l&xP@ssw0rd"
   ```

   Reemplace los valores siguientes:
      
    - `<External IP Address>` con la dirección IP para el `mssql-deployment` servicio 
    - `MyC0m9l&xP@ssw0rd` con la contraseña

## <a name="verify-failure-and-recovery"></a>Compruebe el error y recuperación

Para comprobar un error y recuperación, puede eliminar el pod. Realice los pasos siguientes:

1. Lista de lo pod que ejecuta SQL Server.

   ```azurecli
   kubectl get pods
   ```

   Tenga en cuenta el nombre del pod que ejecuta SQL Server.

1. Elimine el pod.

   ```azurecli
   kubectl delete pod mssql-deployment-0
   ```
   `mssql-deployment-0` es el valor devuelto en el paso anterior para el nombre del pod. 

Kubernetes automáticamente vuelve a crear el pod para recuperar una instancia de SQL Server y conéctese al almacenamiento persistente. Use `kubectl get pods` para comprobar que se ha implementado un nuevo conjunto pod. Use `kubectl get services` para comprobar que la dirección IP para el nuevo contenedor es el mismo. 

## <a name="summary"></a>Resumen

En este tutorial, aprendió a implementar contenedores de SQL Server en un clúster de Kubernetes para lograr alta disponibilidad. 

> [!div class="checklist"]
> * Crear una contraseña de SA
> * Crear almacenamiento
> * Crear la implementación
> * Conectar con SQL Server Management Studio (SSMS)
> * Compruebe el error y recuperación

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
>[Introducción a Kubernetes](http://docs.microsoft.com/azure/aks/intro-kubernetes)


