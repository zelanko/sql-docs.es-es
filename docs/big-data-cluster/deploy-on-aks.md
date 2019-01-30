---
title: Configurar el servicio de Kubernetes de Azure
titleSuffix: SQL Server 2019 big data clusters
description: Obtenga información sobre cómo configurar Azure Kubernetes Service (AKS) para las implementaciones de clústeres (versión preliminar) de datos de gran tamaño de SQL Server 2019.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 5e4ec4e6f0de497e3ec5d35293ad142696a19a46
ms.sourcegitcommit: 3a1e0b92cbe53ccf3b233faf8629d16bbf673b30
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/29/2019
ms.locfileid: "55229036"
---
# <a name="configure-azure-kubernetes-service-for-sql-server-2019-big-data-cluster-preview-deployments"></a>Configuración de Azure Kubernetes Service para las implementaciones de clústeres (versión preliminar) de datos de gran tamaño de SQL Server 2019

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

- Para un entorno de AKS, para una experiencia óptima al validar escenarios básicos, se recomienda al menos tres máquinas virtuales de agente con al menos 4 vCPU y 32 GB de memoria de cada uno. Infraestructura de Azure ofrece varias opciones de tamaño para máquinas virtuales, consulte [aquí](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) selecciones en la región que se va a implementar.

## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Un grupo de recursos de Azure es un grupo lógico de Azure que se implementan y administran los recursos. Los pasos siguientes, se inicia sesión en Azure y creación un grupo de recursos para el clúster de AKS.

> [!TIP]
> Si usa Windows, use PowerShell para el resto de los pasos.

1. En el símbolo del sistema, ejecute el siguiente comando y siga las indicaciones para iniciar sesión en su suscripción de Azure:

    ```bash
    az login
    ```

1. Si tiene varias suscripciones, puede ver todas las suscripciones, ejecute el comando siguiente:

   ```bash
   az account list
   ```

1. Si desea cambiar a otra suscripción puede ejecutar este comando:

   ```bash
   az account set --subscription <subscription id>
   ```

1. Crear un grupo de recursos con el **crear grupo az** comando. En el ejemplo siguiente se crea un grupo de recursos denominado `sqlbigdatagroup` en el `westus2` ubicación.

   ```bash
   az group create --name sqlbigdatagroup --location westus2
   ```

## <a name="create-a-kubernetes-cluster"></a>Crear un clúster de Kubernetes

1. Crear un clúster de Kubernetes en AKS con la [crear az aks](https://docs.microsoft.com/cli/azure/aks) comando. En el ejemplo siguiente se crea un clúster de Kubernetes denominado *kubcluster* con tres nodos de agente de Linux. Asegúrese de que crear el clúster de AKS en el mismo grupo de recursos que usó en las secciones anteriores.

    ```bash
   az aks create --name kubcluster \
    --resource-group sqlbigdatagroup \
    --generate-ssh-keys \
    --node-vm-size Standard_L4s \
    --node-count 3 \
    --kubernetes-version 1.10.9
    ```

   Puede aumentar o disminuir el número de nodos de agente de Kubernetes cambiando el `--node-count <n>` donde `<n>` es el número de nodos de agente que desea usar. Esto no incluye el nodo maestro de Kubernetes, que se administra en segundo plano mediante AKS. Por lo que en el ejemplo anterior, hay **3** máquinas virtuales de tamaño **Standard_L4s** usan para los nodos de agente del clúster de AKS.

   Después de varios minutos, el comando se completa y devuelve información sobre el clúster en formato JSON.

1. Guarde la salida JSON desde el comando anterior para su uso posterior.

## <a name="connect-to-the-cluster"></a>Conéctese al clúster

1. Para configurar kubectl para conectarse al clúster de Kubernetes, ejecute el [az aks get-credentials](https://docs.microsoft.com/cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials) comando. Este paso descarga las credenciales y configura la CLI para usarlos de kubectl.

   ```bash
   az aks get-credentials --resource-group=sqlbigdatagroup --name kubcluster
   ```

1. Para comprobar la conexión con el clúster, use la [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) comando para devolver una lista de los nodos del clúster.  El ejemplo siguiente muestra la salida si fuera a tener 1 maestro y 3 nodos de agente.

   ```bash
   kubectl get nodes
   ```

## <a name="next-steps"></a>Pasos siguientes

Los pasos descritos en este artículo, configuran un clúster de Kubernetes en AKS. El siguiente paso es implementar datos de gran tamaño 2019 de SQL Server en el clúster. Para obtener más información sobre cómo implementar clústeres de datos de gran tamaño, consulte el artículo siguiente:

[Cómo implementar clústeres de macrodatos de SQL Server en Kubernetes](deployment-guidance.md)
