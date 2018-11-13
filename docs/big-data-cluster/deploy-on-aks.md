---
title: Configuración de Azure Kubernetes Service para las implementaciones de clústeres de SQL Server 2019 macrodatos | Microsoft Docs
description: Obtenga información sobre cómo configurar Azure Kubernetes Service (AKS) para las implementaciones de clústeres (versión preliminar) de datos de gran tamaño de SQL Server 2019.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/06/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 07ee0ac0db742eca9a55decfcd78cb76b75e0160
ms.sourcegitcommit: cb73d60db8df15bf929ca17c1576cf1c4dca1780
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2018
ms.locfileid: "51221661"
---
# <a name="configure-azure-kubernetes-service-for-sql-server-2019-preview-deployments"></a>Configurar Azure Kubernetes Service para las implementaciones de SQL Server 2019 (versión preliminar)

En este artículo se describe cómo configurar Azure Kubernetes Service (AKS) para las implementaciones de clústeres (versión preliminar) de datos de gran tamaño de SQL Server 2019. 

AKS simplifica crear, configurar y administrar un clúster de máquinas virtuales que están preconfiguradas con un clúster de Kubernetes para ejecutar aplicaciones en contenedores. Esto permite usar sus conocimientos o recurrir a un gran Corpus creciente de expertos comunitarios, implementar y administrar aplicaciones basadas en contenedores en Microsoft Azure.

En este artículo se describe los pasos para implementar en Kubernetes en AKS mediante la CLI de Azure. Si no tiene una suscripción de Azure, cree una cuenta gratuita antes de comenzar.

> [!TIP] 
> Para un script de python de ejemplo que implementa el clúster de macrodatos AKS y SQL Server, vea [implementar un clúster de macrodatos en Azure Kubernetes Service (AKS) de SQL Server](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/aks).

## <a name="prerequisites"></a>Requisitos previos

- Para un entorno de AKS, para una experiencia óptima al validar escenarios básicos, se recomienda al menos tres agente las máquinas virtuales (principal), con al menos 4 vCPU y 32 GB de memoria cada. Infraestructura de Azure ofrece varias opciones de tamaño para máquinas virtuales, consulte [aquí](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sizes) selecciones en la región que se va a implementar.
  
- En esta sección tiene que estar ejecutando la CLI de Azure versión 2.0.4 o posterior. Si necesita instalarla o actualizarla, consulte [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli). Ejecute `az --version` para buscar la versión si es necesario.

- Instalar [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) con un mínimo de versión 1.10 para el servidor y cliente. Si desea instalar una versión específica en el cliente kubectl, consulte [instalar kubectl binario mediante curl](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl). Para AKS, deberá usar `--kubernetes-version` parámetro para especificar una versión distinta de la predeterminada.

> [!NOTE]
Tenga en cuenta que la versión de cliente/servidor que es sesgar admite es +/-1 versión secundaria. La documentación de Kubernetes se afirma que "un cliente debe ser la sesgados no más de una versión secundaria del servidor maestro, pero puede provocar al maestro de hasta una versión secundaria. Por ejemplo, un patrón v1.3 debería funcionar con v1.1, v1.2 y v1.3 nodos y debe funcionar con v1.2, v1.3 y clientes v1.4." Para obtener más información, consulte [Kubernetes admite versiones y componente sesgo](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/release/versioning.md#supported-releases-and-component-skew).

Además, tenga en cuenta que `az aks kubernetes install-cli` se instalará el cliente kubectl con una versión inferior que el 1.10 necesarios. Siga por encima de las instrucciones para instalar la versión correcta del cliente de kubectl.

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

1. Crear un clúster de Kubernetes en AKS con la [crear az aks](https://docs.microsoft.com/cli/azure/aks) comando. En el ejemplo siguiente se crea un clúster de Kubernetes denominado *kubcluster* con Linux de un nodo maestro y dos nodos de agente de Linux. Asegúrese de que crear el clúster de AKS en el mismo grupo de recursos que usó en las secciones anteriores.

    ```bash
   az aks create --name kubcluster \
    --resource-group sqlbigdatagroup \
    --generate-ssh-keys \
    --node-vm-size Standard_E4s_v3 \
    --node-count 3 \
    --kubernetes-version 1.10.8
    ```

    Puede aumentar o disminuir el número de agentes predeterminado cambiando el `--node-count <n>` donde `<n>` es el número de nodos de agente que desea tener.

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

Los pasos descritos en este artículo, configuran un clúster de Kubernetes en AKS. El siguiente paso es implementar datos de gran tamaño 2019 de SQL Server en el clúster.

[Inicio rápido: Implementación de clúster de macrodatos de SQL Server en Azure Kubernetes Service (AKS)](quickstart-big-data-cluster-deploy.md)
