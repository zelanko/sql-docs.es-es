---
title: Configuración de Kubernetes con kubeadm
titleSuffix: SQL Server big data clusters
description: Aprenda a configurar Kubernetes en varias máquinas Ubuntu 16,04 o 18,04 (físicas o virtuales) para implementaciones de clúster de macrodatos de SQL Server 2019 (versión preliminar).
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 07/24/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: ea79503869e7d403e4d3f4f960de9c95760eda0f
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419447"
---
# <a name="configure-kubernetes-on-multiple-machines-for-sql-server-big-data-cluster-deployments"></a>Configuración de Kubernetes en varios equipos para implementaciones de clúster de macrodatos SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se proporciona un ejemplo de cómo usar **kubeadm** para configurar Kubernetes en varios equipos para implementaciones de SQL Server 2019 Big Data cluster (versión preliminar). En este ejemplo, varias máquinas LTS de Ubuntu 16,04 o 18,04 (físicas o virtuales) son el destino. Si va a implementar en una plataforma de Linux diferente, debe modificar algunos de los comandos para que coincidan con el sistema.  

> [!TIP] 
> Para obtener scripts de ejemplo que configuran Kubernetes, consulte [creación de un clúster de Kubernetes con Kubeadm en Ubuntu 16,04 LTS o 18,04 LTS](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm).

## <a name="prerequisites"></a>Requisitos previos

- Mínimo de 3 máquinas físicas o máquinas virtuales Linux
- Configuración recomendada por máquina:
   - 8 CPU
   - 64 GB de memoria
   - 100 GB de almacenamiento

## <a name="prepare-the-machines"></a>Preparar las máquinas

En cada equipo, hay varios requisitos previos necesarios. En un terminal de Bash, ejecute los siguientes comandos en cada máquina:

1. Agregue el equipo actual al `/etc/hosts` archivo:

   ```bash
   echo $(hostname -i) $(hostname) | sudo tee -a /etc/hosts
   ```

1. Deshabilite el intercambio en todos los dispositivos.

   ```bash
   sudo sed -i "/ swap / s/^/#/" /etc/fstab
   sudo swapoff -a
   ```

1. Importe las claves y registre el repositorio para Kubernetes.

   ```bash
   sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
   echo 'deb http://apt.kubernetes.io/ kubernetes-xenial main' | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
   ```

1. Configure los requisitos previos de Docker y Kubernetes en la máquina.

   ```bash
   KUBE_DPKG_VERSION=1.11.3-00
   sudo apt-get update && /
   sudo apt-get install -y ebtables ethtool && /
   sudo apt-get install -y docker.io && /
   sudo apt-get install -y apt-transport-https && /
   sudo apt-get install -y kubelet=$KUBE_DPKG_VERSION kubeadm=$KUBE_DPKG_VERSION kubectl=$KUBE_DPKG_VERSION && /
   curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash
   ```
 
1. Establezca `net.bridge.bridge-nf-call-iptables=1`. En Ubuntu 18,04, primero se habilitan `br_netfilter`los siguientes comandos.

   ```bash
   . /etc/os-release
   if [ "$VERSION_CODENAME" == "bionic" ]; then sudo modprobe br_netfilter; fi
   sudo sysctl net.bridge.bridge-nf-call-iptables=1
   ```

## <a name="configure-the-kubernetes-master"></a>Configuración del maestro de Kubernetes

Después de ejecutar los comandos anteriores en cada equipo, elija una de las máquinas para que sea su maestro de Kubernetes. A continuación, ejecute los siguientes comandos en esa máquina.

1. En primer lugar, cree un archivo RBAC. yaml en el directorio actual con el siguiente comando. 

   ```bash
   cat <<EOF > rbac.yaml
   apiVersion: rbac.authorization.k8s.io/v1beta1
   kind: ClusterRoleBinding
   metadata:
     name: default-rbac
   subjects:
   - kind: ServiceAccount
     name: default
     namespace: default
   roleRef:
     kind: ClusterRole
     name: cluster-admin
     apiGroup: rbac.authorization.k8s.io
   EOF
   ```

1. Inicialice el maestro de Kubernetes en este equipo. Debería ver la salida de que el maestro Kubernetes se ha inicializado correctamente.

   ```bash
   KUBE_VERSION=1.11.3
   sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --kubernetes-version=$KUBE_VERSION
   ```

1. Tenga en `kubeadm join` cuenta el comando que debe usar en los otros servidores para unirse al clúster de Kubernetes. Cópielo para su uso posterior.

   ![kubeadm join](./media/deploy-with-kubeadm/kubeadm-join.png)

1. Configure un archivo de configuración de Kubernetes en el directorio particular.

   ```bash
   mkdir -p $HOME/.kube
   sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
   sudo chown $(id -u):$(id -g) $HOME/.kube/config
   ```

1. Configure el clúster y el panel de Kubernetes.

   ```bash
   kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
   helm init
   kubectl apply -f rbac.yaml
   kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
   kubectl create clusterrolebinding kubernetes-dashboard --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
   ```

## <a name="configure-the-kubernetes-agents"></a>Configuración de los agentes de Kubernetes

Las demás máquinas actuarán como agentes Kubernetes en el clúster. 

En cada uno de los demás equipos, ejecute `kubeadm join` el comando que copió en la sección anterior.

![agentes de Unión kubeadm](./media/deploy-with-kubeadm/kubeadm-join-agents.png)

## <a name="view-the-cluster-status"></a>Ver el estado del clúster

Para comprobar la conexión al clúster, use el comando [kubectl Get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) para devolver una lista de los nodos de clúster.

```bash
kubectl get nodes
```

## <a name="next-steps"></a>Pasos siguientes

En los pasos de este artículo se configuró un clúster de Kubernetes en varios equipos Ubuntu. El siguiente paso es implementar SQL Server clúster de macrodatos de 2019. Para obtener instrucciones, consulte el artículo siguiente:

[Implementar SQL Server en Kubernetes](deployment-guidance.md#deploy)
