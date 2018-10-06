---
title: Configurar Minikube para las implementaciones de SQL Server de 2019 CTP 2.0 | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/05/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: 1f20f2adc916a456e4a1975804fac1640ee95f69
ms.sourcegitcommit: 8aecafdaaee615b4cd0a9889f5721b1c7b13e160
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2018
ms.locfileid: "48818053"
---
# <a name="configure-minikube-for-sql-server-2019-ctp-20"></a>Configurar Minikube para SQL Server de 2019 CTP 2.0

Minikube es una herramienta que facilita la tarea Ejecutar Kubernetes en un único equipo como un equipo portátil o un equipo de escritorio. Minikube ejecuta un clúster de Kubernetes de nodo único dentro de una máquina virtual en el equipo portátil para los usuarios que desean probar Kubernetes o desarrollar con ella diarias. 

## <a name="prerequisites"></a>Requisitos previos

- Para ejecutar un clúster de Minikube para SQL Server de 2019 CTP 2.0 en una configuración de clúster de SQL Big Data, se recomienda que la máquina tenga al menos 32 GB de RAM.

   > [!TIP] 
   > Si la máquina no tiene suficiente memoria, a continuación, modificar la configuración del clúster tal que se crean solo 3 instancias: una instancia de maestra y dos instancias de proceso.

- Virtualización AMD-v o VT-x debe habilitarse en el BIOS del equipo.

## <a name="install-dependencies"></a>Instale las dependencias

1. Si aún no está instalado, instale localmente en git [Windows](https://git-for-windows.github.io/), [Linux o Mac](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

1. Instalar [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

1. Instale Python 3:
   - Si falta pip, a continuación, descargue [get clspip.py](https://bootstrap.pypa.io/get-pip.py) y ejecute `python get-pip.py`.
   - Las solicitudes de instalación del paquete mediante `python -m pip install requests`.

1. Si no dispone de un hipervisor instalado, instalar una ahora.
   - Para OS X, instalar [xhyve controlador](https://git.k8s.io/minikube/docs/drivers.md), [VirtualBox](https://www.virtualbox.org/wiki/Downloads), o [VMware Fusion](https://www.vmware.com/products/fusion).
   - Para Linux, instale [VirtualBox](https://www.virtualbox.org/wiki/Downloads) o [KVM](http://www.linux-kvm.org/).
   - Para Windows, instale [VirtualBox](https://www.virtualbox.org/wiki/Downloads) o [Hyper-V](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install). Si no tiene un conmutador externo configurado en hyper-v, a continuación, cree uno que tenga acceso a la red externa.  Vea cómo [crear conmutador externo de hyper-v para minikube](https://blogs.msdn.microsoft.com/wasimbloch/2017/01/23/setting-up-kubernetes-on-windows10-laptop-with-minikube/).

## <a name="install-minikube"></a>Instalar Minikube

Instalar Minikube según las instrucciones para la [v0.28.2 versión](https://github.com/kubernetes/minikube/releases/tag/v0.28.2). El clúster de macrodatos de SQL Server de 2019 CTP 2.0 sólo funciona con la versión v0.24.1 y posteriores.

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

Los pasos descritos en este artículo, configuran un clúster de Minikube. El siguiente paso es implementar SQL Server 2019 CTP 2.0 en el clúster.

[Implementar 2019 CTP 2.0 de SQL Server en Kubernetes](deployment-guidance.md#deploy)
