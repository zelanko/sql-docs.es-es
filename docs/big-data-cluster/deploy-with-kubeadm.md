---
title: Configuración de Kubernetes con kubeadm
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo configurar Kubernetes en varios Ubuntu 16.04 o 18.04 equipos (físicos o virtuales) para las implementaciones de clústeres (versión preliminar) de datos de gran tamaño de SQL Server 2019.
author: rothja
ms.author: jroth
manager: jroth
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: c48a8a8ad84a1378eed09727a3e51a51252b88c6
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66803069"
---
# <a name="configure-kubernetes-on-multiple-machines-for-sql-server-big-data-cluster-deployments"></a>Configuración de Kubernetes en varios equipos para las implementaciones de clústeres de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artículo proporciona un ejemplo de cómo usar **kubeadm** configuración de Kubernetes en varios equipos para las implementaciones de clústeres (versión preliminar) de datos de gran tamaño de SQL Server 2019. En este ejemplo, varias Ubuntu 16.04 o 18.04 máquinas LTS (físicas o virtuales) son el destino. Si va a implementar en una plataforma de Linux diferente, debe modificar algunos de los comandos para que coincida con el sistema.  

> [!TIP] 
> Para scripts de muestra que la configuración de Kubernetes, consulte [crear un clúster de Kubernetes mediante Kubeadm en Ubuntu 16.04 LTS o 18.04 LTS](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/deployment/kubeadm).

## <a name="prerequisites"></a>Requisitos previos

- Mínimo de 3 máquinas de Linux físicas o máquinas virtuales
- Configuración recomendada por máquina:
   - 8 CPU
   - 32 GB de memoria
   - 100 GB de almacenamiento

## <a name="prepare-the-machines"></a>Preparar las máquinas

En cada equipo, hay varios requisitos previos necesarios. En un terminal de bash, ejecute los comandos siguientes en cada máquina:

1. Agregar el equipo actual para el `/etc/hosts` archivo:

   ```bash
   echo $(hostname -i) $(hostname) | sudo tee -a /etc/hosts
   ```

1. Deshabilite el intercambio en todos los dispositivos.

   ```bash
   sudo sed -i "/ swap / s/^/#/" /etc/fstab
   sudo swapoff -a
   ```

1. Importe las claves y registrar el repositorio para Kubernetes.

   ```bash
   sudo curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
   echo 'deb http://apt.kubernetes.io/ kubernetes-xenial main' | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
   ```

1. Configurar requisitos previos de Kubernetes y docker en el equipo.

   ```bash
   KUBE_DPKG_VERSION=1.11.3-00
   sudo apt-get update && /
   sudo apt-get install -y ebtables ethtool && /
   sudo apt-get install -y docker.io && /
   sudo apt-get install -y apt-transport-https && /
   sudo apt-get install -y kubelet=$KUBE_DPKG_VERSION kubeadm=$KUBE_DPKG_VERSION kubectl=$KUBE_DPKG_VERSION && /
   curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get | bash
   ```
 
1. Establezca `net.bridge.bridge-nf-call-iptables=1`. En Ubuntu 18.04, habilite primero los siguientes comandos `br_netfilter`.

   ```bash
   . /etc/os-release
   if [ "$VERSION_CODENAME" == "bionic" ]; then sudo modprobe br_netfilter; fi
   sudo sysctl net.bridge.bridge-nf-call-iptables=1
   ```

## <a name="configure-the-kubernetes-master"></a>Configure el maestro de Kubernetes

Después de ejecutar los comandos anteriores en cada equipo, elija una de las máquinas que el servidor maestro de Kubernetes. A continuación, ejecute los siguientes comandos en esa máquina.

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

1. Inicializar al maestro de Kubernetes en este equipo. Debería ver la salida que el maestro de Kubernetes se inicializó correctamente.

   ```bash
   KUBE_VERSION=1.11.3
   sudo kubeadm init --pod-network-cidr=10.244.0.0/16 --kubernetes-version=$KUBE_VERSION
   ```

1. Tenga en cuenta el `kubeadm join` comando que se debe usar en los demás servidores a unirse al clúster de Kubernetes. Copie esto para su uso posterior.

   ![combinación de kubeadm](./media/deploy-with-kubeadm/kubeadm-join.png)

1. Configure su directorio particular de un archivo de configuración de Kubernetes.

   ```bash
   mkdir -p $HOME/.kube
   sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
   sudo chown $(id -u):$(id -g) $HOME/.kube/config
   ```

1. Configurar el clúster y el panel de Kubernetes.

   ```bash
   kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
   helm init
   kubectl apply -f rbac.yaml
   kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/master/src/deploy/recommended/kubernetes-dashboard.yaml
   kubectl create clusterrolebinding kubernetes-dashboard --clusterrole=cluster-admin --serviceaccount=kube-system:kubernetes-dashboard
   ```

## <a name="configure-the-kubernetes-agents"></a>Configurar a los agentes de Kubernetes

Las otras máquinas actuará como agentes de Kubernetes en el clúster. 

En cada una de las otras máquinas, ejecute el `kubeadm join` comando que ha copiado en la sección anterior.

![agentes de combinación kubeadm](./media/deploy-with-kubeadm/kubeadm-join-agents.png)

## <a name="view-the-cluster-status"></a>Ver el estado del clúster

Para comprobar la conexión con el clúster, use la [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands) comando para devolver una lista de los nodos del clúster.

```bash
kubectl get nodes
```

## <a name="next-steps"></a>Pasos siguientes

Los pasos descritos en este artículo, configura un clúster de Kubernetes en varios equipos de Ubuntu. El siguiente paso es implementar el clúster de macrodatos de SQL Server 2019. Para obtener instrucciones, consulte el artículo siguiente:

[Implementar SQL Server en Kubernetes](deployment-guidance.md#deploy)
