---
title: Configurar el servicio de Kubernetes de Azure
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo configurar Azure Kubernetes Service (AKS) para las implementaciones de clústeres (versión preliminar) de datos de gran tamaño de SQL Server 2019.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
manager: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: c5860e4c26008cf94b9ec168bb6a705f15ae7cd1
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/10/2019
ms.locfileid: "67728921"
---
# <a name="configure-azure-kubernetes-service-for-sql-server-big-data-cluster-deployments"></a>Configuración de Azure Kubernetes Service para las implementaciones de clústeres de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe cómo configurar Azure Kubernetes Service (AKS) para las implementaciones de clústeres (versión preliminar) de datos de gran tamaño de SQL Server 2019.

AKS simplifica crear, configurar y administrar un clúster de máquinas virtuales que están preconfiguradas con un clúster de Kubernetes para ejecutar aplicaciones en contenedores. Esto permite usar sus conocimientos o recurrir a un gran Corpus creciente de expertos comunitarios, implementar y administrar aplicaciones basadas en contenedores en Microsoft Azure.

En este artículo se describe los pasos para implementar en Kubernetes en AKS mediante la CLI de Azure. Si no tiene una suscripción de Azure, cree una cuenta gratuita antes de comenzar.

> [!TIP] 
> Para un script de python de ejemplo que implementa el clúster de macrodatos AKS y SQL Server, vea [inicio rápido: Implementar SQL Server en Azure Kubernetes Service (AKS) del clúster de macrodatos](quickstart-big-data-cluster-deploy.md).

## <a name="prerequisites"></a>Requisitos previos

- [Implementar las herramientas de datos de gran tamaño de SQL Server 2019](deploy-big-data-tools.md):
   - **kubectl**
   - **Azure Data Studio**
   - **Extensión de SQL Server 2019**
   - **CLI de Azure**

- Versión mínima 1.10 para servidor de Kubernetes. Para AKS, deberá usar `--kubernetes-version` parámetro para especificar una versión distinta de la predeterminada.

- Para obtener una experiencia óptima al validar escenarios básicos en AKS, use:
   - 8 vCPU en todos los nodos
   - 32 GB de memoria por máquina virtual
   - 24 o conectados más discos en todos los nodos

   > [!TIP]
   > Infraestructura de Azure ofrece varias opciones de tamaño para máquinas virtuales, consulte [aquí](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) selecciones en la región que se va a implementar.

## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Un grupo de recursos de Azure es un grupo lógico de Azure que se implementan y administran los recursos. Los pasos siguientes, se inicia sesión en Azure y creación un grupo de recursos para el clúster de AKS.

1. En el símbolo del sistema, ejecute el siguiente comando y siga las indicaciones para iniciar sesión en su suscripción de Azure:

    ```azurecli
    az login
    ```

1. Si tiene varias suscripciones, puede ver todas las suscripciones, ejecute el comando siguiente:

   ```azurecli
   az account list
   ```

1. Si desea cambiar a otra suscripción puede ejecutar este comando:

   ```azurecli
   az account set --subscription <subscription id>
   ```

1. Crear un grupo de recursos con el **crear grupo az** comando. En el ejemplo siguiente se crea un grupo de recursos denominado `sqlbdcgroup` en el `westus2` ubicación.

   ```azurecli
   az group create --name sqlbdcgroup --location westus2
   ```

## <a name="create-a-kubernetes-cluster"></a>Crear un clúster de Kubernetes

1. Crear un clúster de Kubernetes en AKS con la [crear az aks](https://docs.microsoft.com/cli/azure/aks) comando. En el ejemplo siguiente se crea un clúster de Kubernetes denominado *kubcluster* con un nodo de agente de Linux de tamaño **Standard_L8s**. Asegúrese de que crear el clúster de AKS en el mismo grupo de recursos que usó en las secciones anteriores.

   **bash:**

   ```bash
   az aks create --name kubcluster \
   --resource-group sqlbdcgroup \
   --generate-ssh-keys \
   --node-vm-size Standard_L8s \
   --node-count 1 \
   --kubernetes-version 1.12.8
   ```

   **PowerShell:**

   ```powershell
   az aks create --name kubcluster `
   --resource-group sqlbdcgroup `
   --generate-ssh-keys `
   --node-vm-size Standard_L8s `
   --node-count 1 `
   --kubernetes-version 1.12.8
   ```

   Puede aumentar o disminuir el número de nodos de agente de Kubernetes cambiando el `--node-count <n>` donde `<n>` es el número de nodos de agente que desea usar. Esto no incluye el nodo maestro de Kubernetes, que se administra en segundo plano mediante AKS. El ejemplo anterior utiliza sólo un único nodo para fines de evaluación.

   Después de varios minutos, el comando se completa y devuelve información sobre el clúster en formato JSON.

   > [!TIP]
   > Si obtiene errores al crear el clúster de AKS, consulte el [sección Solución de problemas](#troubleshoot) de este artículo.

1. Guarde la salida JSON desde el comando anterior para su uso posterior.

## <a name="connect-to-the-cluster"></a>Conéctese al clúster

1. Para configurar kubectl para conectarse al clúster de Kubernetes, ejecute el [az aks get-credentials](https://docs.microsoft.com/cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials) comando. Este paso descarga las credenciales y configura la CLI para usarlos de kubectl.

   ```azurecli
   az aks get-credentials --resource-group=sqlbdcgroup --name kubcluster
   ```

1. Para comprobar la conexión con el clúster, use la [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) comando para devolver una lista de los nodos del clúster.  El ejemplo siguiente muestra la salida si fuera a tener 1 maestro y 3 nodos de agente.

   ```bash
   kubectl get nodes
   ```

## <a id="troubleshoot"></a> Solucionar problemas

Si tiene problemas al crear un servicio de Kubernetes de Azure con los comandos anteriores, pruebe las soluciones siguientes:

- Asegúrese de que ha instalado el [CLI de Azure más reciente](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).
- Pruebe lo mismo pasos con un nombre de clúster y del grupo de recursos diferentes.

## <a name="next-steps"></a>Pasos siguientes

Los pasos descritos en este artículo, configuran un clúster de Kubernetes en AKS. El siguiente paso es implementar un clúster de macrodatos de 2019 de SQL Server en el clúster de Kubernetes de AKS. Para obtener más información sobre cómo implementar clústeres de datos de gran tamaño, consulte el artículo siguiente:

[Cómo implementar clústeres de macrodatos de SQL Server en Kubernetes](deployment-guidance.md)
