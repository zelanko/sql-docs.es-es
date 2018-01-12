---
title: Configurar el contenedor de SQL Server en Kubernetes para alta disponibilidad | Documentos de Microsoft
description: "Este tutorial muestra cómo implementar una solución de alta disponibilidad de SQL Server con Kubernetes en el servicio de contenedor de Azure."
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.date: 01/10/2018
ms.topic: tutorial
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: mvc
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: 5055a5956ce83dadae3cef13f0855db02a61d01b
ms.sourcegitcommit: 06131936f725a49c1364bfcc2fccac844d20ee4d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/12/2018
---
# <a name="configure-sql-server-container-in-kubernetes-for-high-availability"></a>Configurar el contenedor de SQL Server en Kubernetes para alta disponibilidad

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Siga este artículo para configurar una instancia de SQL Server en Kubernetes en el servicio de contenedor de Azure (AKS) con el almacenamiento persistente para lograr alta disponibilidad. La solución ofrece resistencia. Si se produce un error en la instancia de SQL Server, Kubernetes automáticamente vuelve a crear en un nuevo conjunto pod. AKS proporciona resistencia frente a un error de nodo Kubernetes. 

Este tutorial muestra cómo configurar una instancia de SQL Server de alta disponibilidad en contenedores con AKS. 

> [!div class="checklist"]
> * Crear contraseña
> * Crear un almacenamiento
> * Crear implementación
> * Conectar con SQL Server Management Studio (SSMS)
> * Comprobar errores y recuperaciones

### <a name="ha-solution-using-kubernetes-running-in-azure-container-service"></a>Solución de alta disponibilidad mediante Kubernetes que se ejecuta en el servicio de contenedor de Azure

Kubernetes 1.6 + es compatible con [clases de almacenamiento](http://kubernetes.io/docs/concepts/storage/storage-classes/), [persistente de volumen de notificaciones](http://kubernetes.io/docs/concepts/storage/storage-classes/#persistentvolumeclaims)y el [controlador de volumen de disco de Azure](http://github.com/Azure/azurefile-dockervolumedriver). Puede crear y administrar las instancias de SQL Server forma nativa en Kubernetes. El ejemplo de este artículo muestra cómo crear un [implementación](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) para lograr una configuración de alta disponibilidad similar a la instancia de clúster de conmutación por error de disco compartido. En esta configuración, Kubernetes desempeña un papel del organizador de clúster. Cuando se produce un error en una instancia de SQL Server en un contenedor, el orchestrator ejecuta un bootstrap otra instancia del contenedor al que se adjunta al mismo almacenamiento persistente.

![Clúster de servidores de SQL Kubernetes](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql.png)

En el diagrama anterior, `mssql-server` es un contenedor en un [pod](http://kubernetes.io/docs/concepts/workloads/pods/pod/). Kubernetes organiza los recursos del clúster. A [conjunto de réplicas](http://kubernetes.io/docs/concepts/workloads/controllers/replicaset/) garantiza que el conjunto pod se recuperará automáticamente después de un error de nodo. Aplicaciones que se conectan al servicio. En este caso, el servicio representa un equilibrador de carga que hospeda una dirección IP que seguirá siendo la misma después de un error de la `mssql-server`.

En el diagrama siguiente, la `mssql-server` contenedor ha fallado. Como el orquestador Kubernetes garantiza el número correcto de instancias en buen estado de la réplica se establece e inicia un nuevo contenedor de acuerdo con la configuración. El orchestrator inicia un nuevo conjunto pod en el mismo nodo, y `mssql-server` se vuelve a conectar al mismo almacenamiento persistente. El servicio se conecta a la ha vuelto a crear `mssql-server`.

![Clúster de servidores de SQL Kubernetes después de](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-pod-fail.png)

En el diagrama siguiente, el nodo que hospeda el `mssql-server` contenedor ha fallado. El orchestrator inicia el nuevo conjunto pod en otro nodo, y `mssql-server` se vuelve a conectar al mismo almacenamiento persistente. El servicio se conecta a la ha vuelto a crear `mssql-server`.

![Clúster de servidores de SQL Kubernetes después de](media/tutorial-sql-server-containers-kubernetes/kubernetes-sql-after-node-fail.png)

## <a name="prerequisites"></a>Requisitos previos

* **Clúster Kubernetes**
   - El tutorial, necesita un clúster de Kubernetes. Utilizan los pasos [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), para administrar el clúster. 

   - Puede seguir las instrucciones en [implementar un clúster de servicio de contenedor de Azure (AKS)](http://docs.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-cluster) para crear y conectarse a un clúster de nodo único Kubernetes en AKS con `kubectl`. 

   >[!NOTE]
   >Para protegerse frente a errores de nodo, un clúster de Kubernetes requiere más de un nodo.

* **CLI de Azure 2.0.23**
   - Las instrucciones que aparecen en este tutorial se ha validado en Azure CLI 2.0.23.

## <a name="create-sa-password"></a>Crear contraseña

Crear una contraseña de SA en el clúster Kubernetes. Kubernetes pueden administrar la información de configuración confidencial como contraseñas como [secretos](http://kubernetes.io/docs/concepts/configuration/secret/).

El siguiente comando crea una contraseña para la cuenta SA:

   ```azurecli
   kubectl create secret generic mssql --from-literal=SA_PASSWORD="MyC0m9l&xP@ssw0rd"
   ```  

   Reemplace `MyC0m9l&xP@ssw0rd` con una contraseña compleja.

   Para crear un secreto en Kubernetes denominado `mssql` que contiene el valor `MyC0m9l&xP@ssw0rd` para el `SA_PASSWORD`, ejecute el comando.


## <a name="create-storage"></a>Crear un almacenamiento

Configurar un [volumen persistente](http://kubernetes.io/docs/concepts/storage/persistent-volumes/), y [volumen persistente notificación](http://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistent-volume-claim-protection) en el clúster Kubernetes. Complete los pasos siguientes: 

1. Cree un manifiesto para definir la clase de almacenamiento y el volumen persistente notificación.  El manifiesto especifica el aprovisionador de almacenamiento, parámetros y el [reclamar directiva](http://kubernetes.io/docs/concepts/storage/persistent-volumes/#reclaiming). El clúster de Kubernetes utiliza este manifiesto para crear el almacenamiento persistente. 

   El siguiente ejemplo de yaml define una clase de almacenamiento y la notificación de volumen persistente. Es el aprovisionador de clase de almacenamiento `azure-disk` porque este clúster Kubernetes está en Azure. El tipo de cuenta de almacenamiento es `Standard_LRS`. La notificación de volumen persistente se denomina `mssql-data`. Los metadatos de la notificación de volumen persistentes incluyen una anotación para conectarse de nuevo a la clase de almacenamiento. 

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

   Guarde el archivo, por ejemplo **pvc.yaml**.

1. Cree la notificación de volumen persistente en Kubernetes.

   ```azurecli
   kubectl apply -f <Path to pvc.yaml file>
   ```

   * `<Path to pvc.yaml file>`
      * La ubicación donde guardó el archivo.

   El volumen persistente automáticamente se crea como una cuenta de almacenamiento de Azure y enlazado a la notificación de volumen persistente. 

    ![Comando de notificación de volumen persistente](media/tutorial-sql-server-containers-kubernetes/02_pvc_cmd.png)

1. Compruebe la notificación de volumen persistente.

   ```azurecli
   kubectl describe pvc <PersistentVolumeClaim>
   ```

   * `<PersistentVolumeClaim>`
      * El nombre de la notificación de volumen persistente.

    En el paso anterior, la notificación de volumen persistente se denomina `mssql-data`. Para ver los metadatos acerca de la notificación de volumen persistente, ejecute el siguiente comando:

    ```azurecli
    kubectl describe pvc mssql-data
    ```

    Los metadatos devueltos incluyen un valor denominado `Volume`. Este valor se asigna al nombre del blob.

    ![Se describen los volúmenes](media/tutorial-sql-server-containers-kubernetes/describe-volume.png)

    El valor de volumen, coincide con parte del nombre del blob en la siguiente imagen del portal de Azure: 

    ![Describir el portal de volumen](media/tutorial-sql-server-containers-kubernetes/describe-volume-portal.png)

1. Compruebe el volumen persistente.

   ```azurecli
   kubectl describe pv
   ```

   `kubectl`Devuelve los metadatos sobre el volumen persistente que se crea automáticamente y se enlazan a la notificación de volumen persistente. 

## <a name="create-the-deployment"></a>Crear la implementación

En este ejemplo, el contenedor que aloja la instancia de SQL Server se describe como un objeto de implementación de Kubernetes. La implementación crea un conjunto de réplicas. El conjunto de réplica crea el conjunto pod. 

En este paso, creará un manifiesto para describir el contenedor en función de Microsoft SQL Server [mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/) imagen de Docker. El manifiesto hace referencia a la `mssql-server` notificación de volumen persistente y el `mssql` secreto que ya ha aplicado al clúster Kubernetes. El manifiesto también describe una [servicio](http://kubernetes.io/docs/concepts/services-networking/service/). Este servicio es un equilibrador de carga. El equilibrador de carga garantiza que la dirección IP se conserve después de que se recupera la instancia de SQL Server. 

1. Cree un manifiesto: un archivo yaml - para describir la implementación. En el ejemplo siguiente se describe una implementación incluido un contenedor en función de la imagen de contenedor de SQL Server.

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
           image: microsoft/mssql-server-linux
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

   Copie el código anterior en un nuevo archivo denominado `sqldeployment.yaml`. Actualice los siguientes valores: 

   * `value: "Developer"`
     * Establece el contenedor para ejecutar SQL Server Developer edition. Edición Developer no tiene licencia para los datos de producción. Si la implementación es para su uso en producción, establezca la edición adecuada. Puede ser uno de `Enterprise`, `Standard`, o `Express`. 

      >[!NOTE]
      >Para obtener más información, consulte [licencias de SQL Server](http://www.microsoft.com/sql-server/sql-server-2017-pricing).

   * `persistentVolumeClaim`
     * Este valor requiere una entrada para `claimName:` que se asigna para el nombre utilizado para la notificación de volumen persistente. Este artículo usa `mssql-data`. 

   * `name: SA_PASSWORD`
      * Configura la imagen del contenedor para establecer la contraseña de SA, tal como se define en esta sección.

      ```yaml
      valueFrom:
        secretKeyRef:
          name: mssql
          key: SA_PASSWORD 
      ```

       Cuando Kubernetes implementa el contenedor, que hace referencia el secreto denominado `mssql` para obtener el valor de la contraseña. 

   >[!NOTE]
   >Mediante el uso de la `LoadBalancer` tipo de servicio, la instancia de SQL Server está accesible de forma remota (a través de internet) en el puerto 1433.

    Guarde el archivo, por ejemplo **sqldeployment.yaml**.

1. Crear la implementación.

   ```azurecli
   kubectl apply -f <Path to sqldeployment.yaml file>
   ```

   * `<Path to sqldeployment.yaml file>`
      * La ubicación donde guardó el archivo.

   ![Comando de implementación](media/tutorial-sql-server-containers-kubernetes/04_deploy_cmd.png)

   Se crean la implementación y el servicio. La instancia de SQL Server está en un contenedor - conectado al almacenamiento persistente.

   Para ver el estado de la pod, escriba `kubectl get pod`.

   ![Obtener pod, comando](media/tutorial-sql-server-containers-kubernetes/05_get_pod_cmd.png)

   >[!NOTE]
   >Una vez creada la implementación, puede tardar unos minutos antes de que el conjunto pod sea visible. El retraso es porque el clúster necesita extraer el [mssql-server-linux](https://hub.docker.com/r/microsoft/mssql-server-linux/) imagen de Docker hub. Una vez que se extrae la primera vez, las implementaciones posteriores pueden ser más rápidas - si la implementación está en un nodo que ya tiene la imagen almacenada en ella. 

1. Compruebe que los servicios se estén ejecutando. Ejecute el siguiente comando:

   ```azurecli
   kubectl get services 
   ```

   Este comando devuelve los servicios que se ejecutan, así como las direcciones IP internas y externas de los servicios. Tenga en cuenta la dirección IP externa para el `mssql-deployment` service.  Usar esta dirección IP para conectarse a SQL Server. 

   ![Obtener comandos de servicio](media/tutorial-sql-server-containers-kubernetes/06_get_service_cmd.png)

   Para obtener información adicional sobre el estado de los objetos en el clúster Kubernetes, ejecute:

   ```azurecli
   az aks browse --resource-group <MyResourceGroup> --name <MyKubernetesClustername>
   ```  

## <a name="connect-to-the-sql-server-instance"></a>Conéctese a la instancia de SQL Server

Si ha configurado el contenedor, como se describe, puede conectar con una aplicación desde fuera de la red virtual de Azure. Use la `sa` cuenta y la dirección IP externa de direcciones para el servicio. Utilice la contraseña que ha configurado como el secreto de Kubernetes. 

Puede usar las siguientes aplicaciones para conectarse a la instancia de SQL Server. 

* [SSMS](http://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-ssms)

* [SSDT](http://docs.microsoft.com/en-us/sql/linux/sql-server-linux-develop-use-ssdt)

* SQLCMD para conectarse con `sqlcmd`, ejecute el siguiente comando:

   ```cmd
   sqlcmd -S <External IP Address> -U sa -P "MyC0m9l&xP@ssw0rd"
   ```

   Reemplace los valores siguientes:
      - `<External IP Address>`con la dirección IP para el `mssql-deployment` servicio 
      - `MyC0m9l&xP@ssw0rd`con la contraseña

## <a name="verify-failure-and-recovery"></a>Comprobar errores y recuperaciones

Para comprobar los errores y recuperaciones puede eliminar el conjunto pod. Realice los pasos siguientes:

1. Enumerar el conjunto de pod que ejecuta SQL Server.

   ```azurecli
   kubectl get pods
   ```

   Tenga en cuenta el nombre de la pod que ejecuta SQL Server.

1. Eliminar el conjunto pod.

   ```azurecli
   kubectl delete pod mssql-deployment-0
   ```
   `mssql-deployment-0`es el valor devuelto desde el paso anterior para el nombre del conjunto pod. 

Kubernetes automáticamente vuelve a crear el conjunto de pod para recuperar una instancia de SQL Server y conéctese al almacenamiento persistente. Utilice `kubectl get pods` para comprobar que se ha implementado un nuevo conjunto pod. Utilice `kubectl get services` para comprobar que la dirección IP para el nuevo contenedor es el mismo. 

## <a name="summary"></a>Resumen

En este tutorial, aprendió a implementar contenedores de SQL Server en un clúster de Kubernetes para lograr alta disponibilidad. 

> [!div class="checklist"]
> * Crear contraseña
> * Crear un almacenamiento
> * Crear implementación
> * Conectar con SQL Server Management Studio (SSMS)
> * Comprobar errores y recuperaciones

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
>[Introducción - Kubernetes](http://docs.microsoft.com/en-us/azure/aks/intro-kubernetes)
