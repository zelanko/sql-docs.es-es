---
title: Compatibilidad con la GPU y TensorFlow
titleSuffix: SQL Server big data clusters
description: Implementar un clúster de macrodatos con compatibilidad con GPU y usar TensorFlow en Azure Data Studio blocs de notas.
author: inchiosa
ms.author: marinch
ms.reviewer: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 4913526270e919e95c2ff6dad73fa4b67693a038
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/24/2019
ms.locfileid: "63473309"
---
# <a name="deploy-a-big-data-cluster-with-gpu-support-and-run-tensorflow"></a>Implementar un clúster de macrodatos con compatibilidad con GPU y ejecutar TensorFlow

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se muestra cómo implementar un clúster de macrodatos en Azure Kubernetes Service (AKS) que admite grupos de nodos basados en GPU para las cargas de trabajo de proceso intensivo. A continuación, ejecutar cuadernos de ejemplo en Azure Data Studio que realizan la clasificación de imágenes con TensorFlow para GPU.

## <a name="prerequisites"></a>Requisitos previos

- [Herramientas de macrodatos](deploy-big-data-tools.md):
  - **mssqlctl**
  - **kubectl**
  - **Azure Data Studio**
  - **Extensión de SQL Server 2019**
  - **Azure CLI**

[!INCLUDE [Limited public preview note](../includes/big-data-cluster-preview-note.md)]

## <a name="create-an-aks-cluster"></a>Crear un clúster de AKS

Los pasos siguientes usan la CLI de Azure para crear un clúster de AKS que admite GPU.

1. En el símbolo del sistema, ejecute el siguiente comando y siga las indicaciones para iniciar sesión en su suscripción de Azure:

    ```azurecli
    az login
    ```

1. Crear un grupo de recursos con el **crear grupo az** comando. En el ejemplo siguiente se crea un grupo de recursos denominado `sqlbigdatagroupgpu` en el `eastus` ubicación.

   ```azurecli
   az group create --name sqlbigdatagroupgpu --location eastus
   ```

1. Crear un clúster de Kubernetes en AKS con la [crear az aks](https://docs.microsoft.com/cli/azure/aks) comando. En el ejemplo siguiente se crea un clúster de Kubernetes denominado `gpucluster` en el `sqlbigdatagroupgpu` grupo de recursos.

   ```azurecli
   az aks create --name gpucluster --resource-group sqlbigdatagroupgpu --generate-ssh-keys --node-vm-size Standard_NC6 --node-count 3 --node-osdisk-size 50 --kubernetes-version 1.11.9 --location eastus
   ```

   > [!NOTE]
   > Este clúster usa la **Standard_NC6** [tamaño de VM optimizadas para GPU](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-gpu), que es una de las máquinas virtuales especializadas disponibles con una o varias GPU de NVIDIA. Para obtener más información, consulte [uso de GPU para cargas de trabajo de proceso intensivo en Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/gpu-cluster).

1. Para configurar kubectl para conectarse al clúster de Kubernetes, ejecute el [az aks get-credentials](https://docs.microsoft.com/cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials) comando.

   ```azurecli
   az aks get-credentials --overwrite-existing --resource-group=sqlbigdatagroupgpu --name gpucluster
   ```

## <a name="apply-yaml-manifest"></a>Aplicar el manifiesto YAML

1. Use **kubectl** para crear un espacio de nombres de Kubernetes denominado `gpu-resources`.

   ```
   kubectl create namespace gpu-resources
   ```

1. Guardar el contenido del siguiente archivo de YAML a un archivo denominado **nvidia-dispositivo-plugin-ds.yaml**. Guardar en el directorio de trabajo en el equipo que se está ejecutando **kubectl** desde.

   Actualización de la `image: nvidia/k8s-device-plugin:1.11` mitad de camino hacia abajo el manifiesto para que coincida con su versión de Kubernetes. Por ejemplo, si el clúster de AKS ejecuta Kubernetes versión 1.12, actualice la etiqueta a `image: nvidia/k8s-device-plugin:1.12`.

   ```yaml
   apiVersion: extensions/v1beta1
   kind: DaemonSet
   metadata:
     labels:
       kubernetes.io/cluster-service: "true"
     name: nvidia-device-plugin
     namespace: gpu-resources
   spec:
     template:
       metadata:
         # Mark this pod as a critical add-on; when enabled, the critical add-on scheduler
         # reserves resources for critical add-on pods so that they can be rescheduled after
         # a failure.  This annotation works in tandem with the toleration below.
         annotations:
           scheduler.alpha.kubernetes.io/critical-pod: ""
         labels:
           name: nvidia-device-plugin-ds
       spec:
         tolerations:
         # Allow this pod to be rescheduled while the node is in "critical add-ons only" mode.
         # This, along with the annotation above marks this pod as a critical add-on.
         - key: CriticalAddonsOnly
           operator: Exists
         containers:
         - image: nvidia/k8s-device-plugin:1.11 # Update this tag to match your Kubernetes version
           name: nvidia-device-plugin-ctr
           securityContext:
             allowPrivilegeEscalation: false
             capabilities:
               drop: ["ALL"]
           volumeMounts:
             - name: device-plugin
               mountPath: /var/lib/kubelet/device-plugins
         volumes:
           - name: device-plugin
             hostPath:
               path: /var/lib/kubelet/device-plugins
         nodeSelector:
           beta.kubernetes.io/os: linux
           accelerator: nvidia
   ```

1. Ahora, use el kubectl aplicar el comando para crear el DaemonSet. **NVIDIA-dispositivo-plugin-ds.yaml** debe estar en el directorio de trabajo cuando se ejecute el siguiente comando:

   ```
   kubectl apply -f nvidia-device-plugin-ds.yaml
   ```

## <a name="deploy-the-big-data-cluster"></a>Implementar el clúster de macrodatos

Para implementar un clúster de macrodatos de 2019 de SQL Server (versión preliminar) que admite GPU, debe implementar desde un registro de docker específico y un repositorio. En concreto, usa valores diferentes para **DOCKER_REGISTRY**, **DOCKER_REPOSITORY**, **DOCKER_USERNAME**, **DOCKER_PASSWORD**, y **DOCKER_EMAIL**. Las secciones siguientes proporcionan ejemplos de cómo establecer las variables de entorno. Use secciones de Windows o Linux según la plataforma del cliente que se usa para implementar el clúster de macrodatos.

### <a name="windows"></a>Windows

   1. Con una ventana CMD (no PowerShell), configure las siguientes variables de entorno. No utilice comillas alrededor de los valores.

      ```cmd
      SET ACCEPT_EULA=yes
      SET CLUSTER_PLATFORM=aks

      SET CONTROLLER_USERNAME=<controller_admin_name - can be anything>
      SET CONTROLLER_PASSWORD=<controller_admin_password - can be anything, password complexity compliant>
      SET KNOX_PASSWORD=<knox_password - can be anything, password complexity compliant>
      SET MSSQL_SA_PASSWORD=<sa_password_of_master_sql_instance, password complexity compliant>

      SET DOCKER_REGISTRY=marinchcreus3.azurecr.io
      SET DOCKER_REPOSITORY=ctp24-8-0-61-gpu
      SET DOCKER_USERNAME=<your username, gpu-specific credentials provided by Microsoft>
      SET DOCKER_PASSWORD=<your password, gpu-specific credentials provided by Microsoft>
      SET DOCKER_EMAIL=<your email address>
      SET DOCKER_PRIVATE_REGISTRY=1
      SET STORAGE_SIZE=10Gi
      ```

   1. Implementar el clúster de macrodatos:

      ```cmd
      mssqlctl cluster create --name gpubigdatacluster
      ```

### <a name="linux"></a>Linux

   1. Inicialice las variables de entorno siguientes. En bash, puede usar comillas alrededor de cada valor.

      ```bash
      export ACCEPT_EULA=yes
      export CLUSTER_PLATFORM="aks"

      export CONTROLLER_USERNAME="<controller_admin_name - can be anything>"
      export CONTROLLER_PASSWORD="<controller_admin_password - can be anything, password complexity compliant>"
      export KNOX_PASSWORD="<knox_password - can be anything, password complexity compliant>"
      export MSSQL_SA_PASSWORD="<sa_password_of_master_sql_instance, password complexity compliant>"

      export DOCKER_REGISTRY="marinchcreus3.azurecr.io"
      export DOCKER_REPOSITORY="ctp24-8-0-61-gpu"
      export DOCKER_USERNAME="<your username, gpu-specific credentials provided by Microsoft>"
      export DOCKER_PASSWORD="<your password, gpu-specific credentials provided by Microsoft>"
      export DOCKER_EMAIL="<your email address>"
      export DOCKER_PRIVATE_REGISTRY="1"
      export STORAGE_SIZE="10Gi"
      ```

   1. Implementar el clúster de macrodatos:

      ```bash
      mssqlctl cluster create --name gpubigdatacluster
      ```

## <a name="run-the-tensorflow-example"></a>Ejecutar el ejemplo de TensorFlow

Los cuadernos de dos ejemplos siguientes muestran entrenar modelos de clasificación de dos imágenes en un único nodo del clúster Spark mediante TensorFlow para GPU.

| Descarga del cuaderno | Descripción |
|---|---|
| [**tf-cuda8.ipynb**](https://aka.ms/AA4jdgd) | Usa 8 CUDA, CUDNN 6 y TensorFlow 1.4.0.  |
| [**tf-cuda9.ipynb**](https://aka.ms/AA4ixzr) | Usa TensorFlow 1.12.0, CUDA 9 y CUDNN 7. |

Coloque el archivo de Bloc de notas adecuado en el equipo local y, a continuación, abra y ejecutarla en Azure Data Studio con el kernel PySpark3. A menos que tenga una necesidad concreta para una versión anterior de TensorFlow o de CUDA, elija CUDA 9 y CUDNN 7/TensorFlow 1.12.0. Para obtener más información acerca de cómo usar cuadernos con clústeres de datos de gran tamaño, vea [para usar cuadernos en versión preliminar de SQL Server 2019](notebooks-guidance.md).

> [!NOTE]
> Tenga en cuenta que los cuadernos de instalación software en las ubicaciones del sistema. Esto es posible porque actualmente ejecutan blocs de notas con privilegios raíz en CTP 2.4.

Después de instalar las bibliotecas de GPU de NVIDIA y TensorFlow para GPU, los cuadernos de lista de dispositivos GPU disponibles. Que, a continuación, ajustarán y evaluación un modelo de TensorFlow para reconocer con el conjunto de datos MNIST de dígitos escritos a mano. Después de comprobar el espacio en disco disponible, descargue y ejecute el ejemplo de clasificación de imágenes de CIFAR 10 desde [ https://github.com/tensorflow/models.git ](https://github.com/tensorflow/models.git). Al ejecutar el ejemplo de CIFAR 10 en clústeres con distintas GPU, puede observar el aumento de velocidad ofrecida por cada generación de GPU disponible en Azure.

## <a name="clean-up-resources"></a>Limpiar recursos

Para eliminar el clúster de macrodatos, use el siguiente comando:

```
mssqlctl cluster delete --name gpubigdatacluster
```

El comando anterior no elimina el clúster de AKS. Para eliminar el clúster de AKS y los recursos asociados con él, use el siguiente comando:

```azurecli
az group delete -n sqlbigdatagroupgpu
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de los clústeres de macrodatos de 2019 de SQL Server (versión preliminar), consulte [¿cuáles son los clústeres de SQL Server 2019 macrodatos?](big-data-cluster-overview.md).
