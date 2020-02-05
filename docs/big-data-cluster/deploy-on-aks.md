---
title: Configurar Azure Kubernetes Service
titleSuffix: SQL Server Big Data Clusters
description: Obtenga información sobre cómo configurar Azure Kubernetes Service (AKS) para las implementaciones del [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)].
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.metadata: seo-lt-2019
ms.date: 12/13/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 10e46d39d312f47fa327d79523a2613ef4b80634
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "75251198"
---
# <a name="configure-azure-kubernetes-service-for-sql-server-big-data-cluster-deployments"></a>Configurar Azure Kubernetes Service para implementaciones de clúster de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo, se describe cómo configurar Azure Kubernetes Service (AKS) para las implementaciones del [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)].

Con AKS, es fácil crear, configurar y administrar un clúster de máquinas virtuales preconfiguradas con un clúster de Kubernetes para ejecutar aplicaciones en contenedores. Esto le permite usar sus aptitudes existentes o aprovechar un amplio y creciente grupo de expertos de la comunidad para implementar y administrar aplicaciones basadas en contenedor en Microsoft Azure.

En este artículo, se describen los pasos para implementar Kubernetes en AKS con la CLI de Azure. Si no tiene una suscripción de Azure, cree una cuenta gratuita antes de empezar.

> [!TIP]
> También puede crear un script de la implementación de AKS y un clúster de macrodatos en un único paso. Para obtener más información, vea cómo realizar este procedimiento en un [script de Python](quickstart-big-data-cluster-deploy.md) o en un [cuaderno](deploy-notebooks.md) de Azure Data Studio.

## <a name="prerequisites"></a>Prerequisites

- [Implementar las herramientas de macrodatos de SQL Server 2019](deploy-big-data-tools.md):
   - **Kubectl**
   - **Azure Data Studio**
   - **Extensión de SQL Server 2019**
   - **CLI de Azure**

- Versión mínima 1.13 para el servidor de Kubernetes. Para AKS, necesita usar el parámetro `--kubernetes-version` para especificar una versión distinta de la predeterminada.

- Para garantizar una implementación correcta y una experiencia óptima al validar escenarios básicos en AKS, puede usar un solo nodo o un clúster de AKS de varios nodos, con estos recursos disponibles:
   - 8 CPU virtuales en todos los nodos
   - 64 GB de memoria por VM
   - 24 o más discos conectados en todos los nodos

   > [!TIP]
   > La infraestructura de Azure ofrece varias opciones de tamaño para máquinas virtuales; [aquí](https://docs.microsoft.com/azure/virtual-machines/windows/sizes) puede ver varias opciones en la región donde tenga previsto realizar la implementación.

## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Un grupo de recursos de Azure es un grupo lógico en el que se implementan y administran recursos de Azure. Siga este procedimiento para iniciar sesión en Azure y crear un grupo de recursos para el clúster de AKS.

1. En el símbolo del sistema, ejecute el comando siguiente y siga las indicaciones para iniciar sesión en su suscripción de Azure:

    ```azurecli
    az login
    ```

1. Si tiene varias suscripciones, puede verlas todas si ejecuta el comando siguiente:

   ```azurecli
   az account list
   ```

1. Si quiere cambiar a otra suscripción, ejecute este comando:

   ```azurecli
   az account set --subscription <subscription id>
   ```

1. Para crear un grupo de recursos, use el comando **az group create**. En el ejemplo siguiente, se crea un grupo de recursos denominado `sqlbdcgroup` en la ubicación `westus2`.

   ```azurecli
   az group create --name sqlbdcgroup --location westus2
   ```

## <a name="verify-available-kubernetes-versions"></a>Verificar las versiones de Kubernetes disponibles

Use la versión más reciente disponible de Kubernetes. La versión disponible más reciente depende de la ubicación donde vaya a implementar el clúster. El comando siguiente muestra las versiones de Kubernetes disponibles en una ubicación específica.

Antes de ejecutar el comando, actualice el script. Reemplace `<Azure data center>` por la ubicación del clúster.

   **bash**

   ```bash
   az aks get-versions \
   --location <Azure data center> \
   --query orchestrators \
   --o table
   ```

   **PowerShell**

   ```powershell
   az aks get-versions `
   --location <Azure data center> `
   --query orchestrators `
   --o table
   ```

Seleccione la versión disponible más reciente para el clúster. Anote el número de versión. Lo usará en el paso siguiente.

## <a name="create-a-kubernetes-cluster"></a>Creación de un clúster de Kubernetes

1. Para crear un clúster de Kubernetes en AKS, use el comando [az aks create](https://docs.microsoft.com/cli/azure/aks). En el ejemplo siguiente, se crea un clúster de Kubernetes denominado *kubcluster* con un nodo de agente de Linux del tamaño **Standard_L8s**.

   Antes de ejecutar el script, reemplace `<version number>` por el número de versión que ha identificado en el paso anterior.

   Asegúrese de crear el clúster de AKS en el mismo grupo de recursos que ha usado en las secciones anteriores.

   **bash:**

   ```bash
   az aks create --name kubcluster \
   --resource-group sqlbdcgroup \
   --generate-ssh-keys \
   --node-vm-size Standard_L8s \
   --node-count 1 \
   --kubernetes-version <version number>
   ```

   **PowerShell:**

   ```powershell
   az aks create --name kubcluster `
   --resource-group sqlbdcgroup `
   --generate-ssh-keys `
   --node-vm-size Standard_L8s `
   --node-count 1 `
   --kubernetes-version <version number>
   ```

   Puede incrementar o disminuir el número de nodos del agente de Kubernetes; para hacerlo, cambie `--node-count <n>`, donde `<n>` es el número de nodos de agente que quiere usar. Esto no incluye el nodo de Kubernetes maestro, que se administra en segundo plano mediante AKS. En el ejemplo anterior, se usa un solo nodo con fines de evaluación.

   En unos minutos, terminará de ejecutarse el comando, que devuelve información con formato JSON sobre el clúster.

   > [!TIP]
   > Si se muestran errores al crear el clúster en AKS, vea la [sección de solución de problemas](#troubleshoot) de este artículo.

1. Guarde el resultado en formato JSON del comando anterior para su uso posterior.

## <a name="connect-to-the-cluster"></a>Conectarse al clúster

1. Para configurar kubectl con el fin de conectarse a su clúster de Kubernetes, ejecute el comando [az aks get-credentials](https://docs.microsoft.com/cli/azure/aks?view=azure-cli-latest#az-aks-get-credentials). Este paso descarga las credenciales y configura la CLI de kubectl para usarlas.

   ```azurecli
   az aks get-credentials --resource-group=sqlbdcgroup --name kubcluster
   ```

1. Para comprobar la conexión al clúster, use el comando [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) para devolver una lista de los nodos del clúster.  En el ejemplo siguiente, se muestra el resultado si necesita tener un nodo maestro y tres nodos de agente.

   ```bash
   kubectl get nodes
   ```

## <a id="troubleshoot"></a> Solucionar problemas

Si tiene problemas para crear una instancia de Azure Kubernetes Service con los comandos anteriores, pruebe las soluciones siguientes:

- Asegúrese de que ha instalado la versión más reciente de la [CLI de Azure](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).
- Pruebe los mismos pasos con otro grupo de recursos y nombre de clúster.

## <a name="next-steps"></a>Pasos siguientes

Con los pasos de este artículo, ha configurado un clúster de Kubernetes en AKS. El paso siguiente es implementar un clúster de macrodatos de SQL Server 2019 en el clúster de Kubernetes de AKS. Para obtener más información sobre cómo implementar clústeres de macrodatos, vea el artículo siguiente:

[Implementación de [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] en Kubernetes](deployment-guidance.md)
