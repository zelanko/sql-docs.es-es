---
title: Configurar minikube
titleSuffix: SQL Server big data clusters
description: Obtenga información sobre cómo configurar minikube para las implementaciones de clústeres (versión preliminar) de macrodatos de 2019 de SQL Server en un solo equipo.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: b091ec919c928f7c78eb37feca2543f06fe4f584
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860696"
---
# <a name="configure-minikube-for-sql-server-big-data-cluster-deployments"></a>Configurar minikube para las implementaciones de clústeres de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describe cómo configurar **minikube** en una única máquina para las implementaciones de clústeres (versión preliminar) de datos de gran tamaño de SQL Server 2019. Minikube es una herramienta que facilita la tarea Ejecutar Kubernetes en un único equipo como un equipo portátil o un equipo de escritorio. Minikube ejecuta un clúster de Kubernetes de nodo único dentro de una máquina virtual en el equipo portátil para los usuarios que desean probar Kubernetes o desarrollar con ella diarias. 

## <a name="prerequisites"></a>Requisitos previos

- 32 GB de memoria (64 GB recomendado).

- Si el equipo tiene solo el mínimo de memoria recomendado, a continuación, configurar la implementación de clúster tenga la instancia del grupo de 1 almacenamiento, 1 instancia del grupo de datos y solo 1 instancia de grupo de proceso. Esta configuración solo debe usar para entornos de evaluación donde la durabilidad y disponibilidad de los datos no son importantes. Consulte la [documentación de implementación](deployment-guidance.md#env) para obtener más información sobre las variables de entorno para establecer el número de réplicas para grupos de datos de configuración, calcular los grupos y grupos de almacenamiento.

- Virtualización AMD-v o VT-x debe habilitarse en el BIOS del equipo.

## <a name="install-dependencies"></a>Instale las dependencias

1. Instalar [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

1. Instale Python 3:
   - Si falta pip, a continuación, descargue [get clspip.py](https://bootstrap.pypa.io/get-pip.py) y ejecute `python get-pip.py`.
   - Las solicitudes de instalación del paquete mediante `python -m pip install requests`.

1. Si no dispone de un hipervisor instalado, instalar una ahora.
   - Para OS X, instalar [xhyve controlador](https://git.k8s.io/minikube/docs/drivers.md), [VirtualBox](https://www.virtualbox.org/wiki/Downloads), o [VMware Fusion](https://www.vmware.com/products/fusion).
   - Para Linux, instale [VirtualBox](https://www.virtualbox.org/wiki/Downloads) o [KVM](https://www.linux-kvm.org/).
   - Para Windows, instale [VirtualBox](https://www.virtualbox.org/wiki/Downloads) o [Hyper-V](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install). Si no tiene un conmutador externo configurado en hyper-v, a continuación, cree uno que tenga acceso a la red externa.  Vea cómo [crear conmutador externo de hyper-v para minikube](https://blogs.msdn.microsoft.com/wasimbloch/2017/01/23/setting-up-kubernetes-on-windows10-laptop-with-minikube/).

## <a name="install-minikube"></a>Instalar Minikube

Instalar Minikube según las instrucciones para la [v0.28.2 versión](https://github.com/kubernetes/minikube/releases/tag/v0.28.2). El clúster de macrodatos de 2019 de SQL Server (versión preliminar) solo funciona con la versión v0.24.1 y posteriores.

## <a name="create-a-minikube-cluster"></a>Crear un clúster de Minikube

El comando siguiente crea un clúster de minikube en una máquina virtual de Hyper-V con 8 CPU, 28 GB de memoria y el tamaño del disco de 100 GB. El tamaño del disco no es un espacio reservado.  Lo crece hasta que el tamaño en disco según sea necesario.  Se recomienda no cambiar el disco espacio a algo menos de 100 GB, tal como hemos tenido problemas con esto en las pruebas. También especifica el conmutador de hyper-v con acceso externo explícitamente.

Cambiar los parámetros como **--memoria** según sea necesario en función del hardware disponible y que usa el hipervisor.  Asegúrese de que el **--hyper-v** el valor del parámetro de conmutador virtual coincide con el nombre que utilizó al crear el conmutador virtual.

```bash
minikube start --vm-driver="hyperv" --cpus 8 --memory 28672 --disk-size 100g --hyperv-virtual-switch "External"
```

Si usas Minikube con VirtualBox el comando tendría este aspecto:

```base
minikube start --cpus 8 --memory 28672 --disk-size 100g
```

## <a name="disable-automatic-checkpoint-with-hyper-v"></a>Deshabilitar punto de comprobación automático con Hyper-V

En Windows 10, el punto de comprobación automático está habilitado en una máquina virtual. Ejecute el siguiente comando en PowerShell para deshabilitar un punto de comprobación automático en la máquina virtual.

```PowerShell
Set-VM -Name minikube -CheckpointType Disabled -AutomaticCheckpointsEnabled $false
```

## <a name="next-steps"></a>Pasos siguientes

Los pasos descritos en este artículo, configuran un clúster de Minikube. El siguiente paso es implementar el clúster de macrodatos de SQL Server 2019. Para obtener instrucciones, consulte el artículo siguiente:

[Implementar clústeres de SQL Server 2019 macrodatos en Kubernetes](deployment-guidance.md#deploy)
