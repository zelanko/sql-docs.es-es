---
title: Configuración de Kubernetes con kubeadm
titleSuffix: SQL Server big data clusters
description: Aprenda a configurar Kubernetes en varias máquinas Ubuntu 16,04 o 18,04 (físicas o virtuales) para [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] implementaciones.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: eb9971d326948715fa68e2eb1d3e9e8d73e06558
ms.sourcegitcommit: 823d7bdfa01beee3cf984749a8c17888d4c04964
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/26/2019
ms.locfileid: "70030289"
---
# <a name="configure-kubernetes-on-multiple-machines-for-sql-server-big-data-cluster-deployments"></a>Configuración de Kubernetes en varios equipos para implementaciones de clústeres de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se proporciona un ejemplo de cómo usar **kubeadm** para configurar Kubernetes en varios equipos [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] para implementaciones. En este ejemplo, el destino son varios equipos Ubuntu 16.04 o 18.04 LTS (físicos o virtuales). Si va a implementar en otra plataforma de Linux, debe modificar algunos de los comandos para que coincidan con el sistema.  

> [!TIP] 
> Para obtener scripts de ejemplo que configuran Kubernetes, vea [Creación de un clúster de Kubernetes con Kubeadm en Ubuntu 16.04 LTS o 18.04 LTS](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm).
Vea también [este](deployment-script-single-node-kubeadm.md) tema para obtener un script de ejemplo que automatiza una implementación de kubeadm de un solo nodo en una máquina virtual y luego implementa una configuración predeterminada del clúster de macrodatos.

## <a name="prerequisites"></a>Requisitos previos

- Un mínimo de tres equipos físicos o virtuales Linux
- Configuración recomendada por equipo:
   - 8 CPU
   - 64 GB de memoria
   - 100 GB de almacenamiento

## <a name="prepare-the-machines"></a>Preparar los equipos

En cada equipo hay varios requisitos previos imprescindibles. En un terminal de Bash, ejecute los siguientes comandos en cada equipo:

1. Agregue el equipo actual al archivo `/etc/hosts`:

   ```bash
   echo $(hostname -i) $(hostname) | sudo tee -a /etc/hosts
   ```

1. Deshabilite el intercambio en todos los dispositivos.

   ```bash
   sudo sed -i "/ swap / s/^/#/" /etc/fstab
   sudo swapoff -a
   ```

1. Importe las claves y registre el repositorio de Kubernetes.

   ```bash
   sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
   echo 'deb http://apt.kubernetes.io/ kubernetes-xenial main' | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
   ```

1. Configure los requisitos previos de Docker y Kubernetes en el equipo.

   ```bash
   KUBE_DPKG_VERSION=1.15.0-00
   sudo apt-get update && \
   sudo apt-get install -y ebtables ethtool && \
   sudo apt-get install -y docker.io && \
   sudo apt-get install -y apt-transport-https && \
   sudo apt-get install -y kubelet=$KUBE_DPKG_VERSION kubeadm=$KUBE_DPKG_VERSION kubectl=$KUBE_DPKG_VERSION && \
   curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash
   ```
 
1. Establezca `net.bridge.bridge-nf-call-iptables=1`. En Ubuntu 18.04, los siguientes comandos primero habilitan `br_netfilter`.

   ```bash
   . /etc/os-release
   if [ "$VERSION_CODENAME" == "bionic" ]; then sudo modprobe br_netfilter; fi
   sudo sysctl net.bridge.bridge-nf-call-iptables=1
   ```

## <a name="configure-the-kubernetes-master"></a>Configurar el maestro de Kubernetes

Después de ejecutar los comandos anteriores en cada equipo, elija uno de ellos como maestro de Kubernetes. Luego ejecute los siguientes comandos en cada equipo.

1. En primer lugar, cree un archivo rbac.yaml en el directorio actual con el siguiente comando. 

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

1. Inicialice el maestro de Kubernetes en este equipo. Debería ver en la salida que el maestro de Kubernetes se ha inicializado correctamente.

   ```bash
   KUBE_VERSION=1.11.3
   sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --kubernetes-version=$KUBE_VERSION
   ```

1. Anote el comando `kubeadm join` que debe usar en los otros servidores para unirse al clúster de Kubernetes. Cópielo para su uso posterior.

   ![kubeadm join](./media/deploy-with-kubeadm/kubeadm-join.png)

1. Defina un archivo de configuración de Kubernetes en el directorio particular.

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

## <a name="configure-the-kubernetes-agents"></a>Configurar los agentes de Kubernetes

Los demás equipos actúan como agentes de Kubernetes en el clúster. 

En cada uno de los otros equipos, ejecute el comando `kubeadm join` que ha copiado en la sección anterior.

![Agentes de kubeadm join](./media/deploy-with-kubeadm/kubeadm-join-agents.png)

## <a name="view-the-cluster-status"></a>Ver el estado del clúster

Para comprobar la conexión al clúster, use el comando [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) para devolver una lista de los nodos del clúster.

```bash
kubectl get nodes
```

## <a name="next-steps"></a>Pasos siguientes

En los pasos de este artículo se ha configurado un clúster de Kubernetes en varios equipos Ubuntu. El siguiente paso es implementar un clúster de macrodatos de SQL Server 2019. Para obtener instrucciones, vea el siguiente artículo:

[Implementación de SQL Server en Kubernetes](deployment-guidance.md#deploy)
