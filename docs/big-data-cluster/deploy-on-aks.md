---
title: Configurar el servicio de Kubernetes de Azure
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo configurar Azure Kubernetes Service (AKS) para las implementaciones de clústeres (versión preliminar) de datos de gran tamaño de SQL Server 2019.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: ddf14cf97fc72acb4a7c44bbc123f171e31c20a2
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59935232"
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
   - **Azure CLI**

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

1. Crear un grupo de recursos con el **crear grupo az** comando. En el ejemplo siguiente se crea un grupo de recursos denominado `sqlbigdatagroup` en el `westus2` ubicación.

   ```azurecli
   az group create --name sqlbigdatagroup --location westus2
   ```

## <a name="create-a-kubernetes-cluster"></a>Crear un clúster de Kubernetes

1. Crear un clúster de Kubernetes en AKS con la [crear az aks](https://docs.microsoft.com/cli/azure/aks) comando. En el ejemplo siguiente se crea un clúster de Kubernetes denominado *kubcluster* con un nodo de agente de Linux de tamaño **Standard_L8s**. Asegúrese de que crear el clúster de AKS en el mismo grupo de recursos que usó en las secciones anteriores.

    ```azurecli
   az aks create --name kubcluster \
    --resource-group sqlbigdatagroup \
    --generate-ssh-keys \
    --node-vm-size Standard_L8s \
    --node-count 1 \
    --kubernetes-version 1.12.6
    ```

   Puede aumentar o disminuir el número de nodos de agente de Kubernetes cambiando el `--node-count <n>` donde `<n>` es el número de nodos de agente que desea usar. Esto no incluye el nodo maestro de Kubernetes, que se administra en segundo plano mediante AKS. El ejemplo anterior utiliza sólo un único nodo para fines de evaluación.

   Después de varios minutos, el comando se completa y devuelve información sobre el clúster en formato JSON.

1. Guarde la salida JSON desde el comando anterior para su uso posterior.

## <a name="connect-to-the-cluster"></a>Conéctese al clúster

1. Para configurar kubectl para conectarse al clúster de Kubernetes, ejecute el [az aks get-credentials](https://docs.microsoft.com/cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials) comando. Este paso descarga las credenciales y configura la CLI para usarlos de kubectl.

   ```azurecli
   az aks get-credentials --resource-group=sqlbigdatagroup --name kubcluster
   ```

1. Para comprobar la conexión con el clúster, use la [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) comando para devolver una lista de los nodos del clúster.  El ejemplo siguiente muestra la salida si fuera a tener 1 maestro y 3 nodos de agente.

   ```
   kubectl get nodes
   ```

## <a name="next-steps"></a>Pasos siguientes

Los pasos descritos en este artículo, configuran un clúster de Kubernetes en AKS. El siguiente paso es implementar datos de gran tamaño 2019 de SQL Server en el clúster. Para obtener más información sobre cómo implementar clústeres de datos de gran tamaño, consulte el artículo siguiente:

[Cómo implementar clústeres de macrodatos de SQL Server en Kubernetes](deployment-guidance.md)
