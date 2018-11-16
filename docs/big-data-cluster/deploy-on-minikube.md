---
title: Configuración de Minikube para las implementaciones de clústeres de SQL Server 2019 macrodatos | Microsoft Docs
description: Obtenga información sobre cómo configurar Minikube para las implementaciones de clústeres (versión preliminar) de macrodatos de 2019 de SQL Server en un solo equipo.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/06/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 9b6902057c3bf5da706de8832b33c959ed285a9b
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51702353"
---
# <a name="configure-minikube-for-sql-server-2019-big-data-cluster-deployments"></a>Configuración de Minikube para las implementaciones de clústeres de macrodatos de SQL Server 2019

En este artículo se describe cómo configurar **minikube** en una única máquina para las implementaciones de clústeres (versión preliminar) de datos de gran tamaño de SQL Server 2019. Minikube es una herramienta que facilita la tarea Ejecutar Kubernetes en un único equipo como un equipo portátil o un equipo de escritorio. Minikube ejecuta un clúster de Kubernetes de nodo único dentro de una máquina virtual en el equipo portátil para los usuarios que desean probar Kubernetes o desarrollar con ella diarias. 

## <a name="prerequisites"></a>Requisitos previos

- Para ejecutar un clúster de Minikube para 2019 CTP 2.1 de SQL Server en una configuración de clúster de macrodatos SQL, se recomienda que la máquina tenga al menos 32 GB de RAM.

   > [!TIP] 
   > Si el equipo tiene solo el mínimo de memoria recomendado, a continuación, configurar la implementación de clúster tenga la instancia del grupo de 1 almacenamiento, 1 instancia del grupo de datos y solo 1 instancia de grupo de proceso. Esta configuración solo debe usar para entornos de evaluación donde la durabilidad y disponibilidad de los datos no son importantes. Consulte la [documentación de implementación](deployment-guidance.md#define-environment-variables) para obtener más información sobre las variables de entorno para establecer el número de réplicas para grupos de datos de configuración, calcular los grupos y grupos de almacenamiento.

- Virtualización AMD-v o VT-x debe habilitarse en el BIOS del equipo.

## <a name="install-dependencies"></a>Instale las dependencias

1. Si aún no está instalado, instale localmente en git [Windows](https://git-for-windows.github.io/), [Linux o Mac](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

1. Instalar [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

1. Instale Python 3:
   - Si falta pip, a continuación, descargue [get clspip.py](https://bootstrap.pypa.io/get-pip.py) y ejecute `python get-pip.py`.
   - Las solicitudes de instalación del paquete mediante `python -m pip install requests`.

1. Si no dispone de un hipervisor instalado, instalar una ahora.
   - Para OS X, instalar [xhyve controlador](https://git.k8s.io/minikube/docs/drivers.md), [VirtualBox](https://www.virtualbox.org/wiki/Downloads), o [VMware Fusion](https://www.vmware.com/products/fusion).
   - Para Linux, instale [VirtualBox](https://www.virtualbox.org/wiki/Downloads) o [KVM](https://www.linux-kvm.org/).
   - Para Windows, instale [VirtualBox](https://www.virtualbox.org/wiki/Downloads) o [Hyper-V](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install). Si no tiene un conmutador externo configurado en hyper-v, a continuación, cree uno que tenga acceso a la red externa.  Vea cómo [crear conmutador externo de hyper-v para minikube](https://blogs.msdn.microsoft.com/wasimbloch/2017/01/23/setting-up-kubernetes-on-windows10-laptop-with-minikube/).

## <a name="install-minikube"></a>Instalar Minikube

Instalar Minikube según las instrucciones para la [v0.28.2 versión](https://github.com/kubernetes/minikube/releases/tag/v0.28.2). El clúster de SQL Server de 2019 CTP 2.1 macrodatos solo funciona con la versión v0.24.1 y posteriores.

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

[Implementar SQL Server 2019 CTP 2.1 en Kubernetes](deployment-guidance.md#deploy)
