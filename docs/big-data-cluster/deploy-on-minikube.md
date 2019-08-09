---
title: Configuración de Minikube
titleSuffix: SQL Server big data clusters
description: Aprenda a configurar Minikube para implementaciones de clústeres de macrodatos de SQL Server 2019 (versión preliminar) en un solo equipo.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6c2261b5cfbbe590c76ce410da4b95ee678a20b5
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67958473"
---
# <a name="configure-minikube-for-sql-server-big-data-cluster-deployments"></a>Configuración de Minikube para implementaciones de clústeres de macrodatos de SQL Server

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se explica cómo configurar **Minikube** en un solo equipo para implementaciones de clústeres de macrodatos de SQL Server 2019 (versión preliminar). Minikube es una herramienta que facilita la ejecución de Kubernetes en un solo equipo, por ejemplo uno portátil o de escritorio. Minikube ejecuta un clúster de Kubernetes de un solo nodo dentro de una máquina virtual del equipo portátil para los usuarios que quieren probar Kubernetes o desarrollar con él cada día. 

## <a name="prerequisites"></a>Prerequisites

- 32 GB de memoria (se recomiendan 64 GB).

- Si el equipo solo tiene la memoria mínima recomendada, configure la implementación del clúster para que tenga una sola instancia de grupo de proceso, una instancia de grupo de datos y una instancia de bloque de almacenamiento. Esta configuración solo se debe usar para entornos de evaluación en los que la durabilidad y disponibilidad de los datos no importan. Vea la [documentación de implementación](deployment-guidance.md#configfile) para obtener más información sobre las variables de entorno que se deben establecer para configurar el número de réplicas de los grupos de datos, grupos de proceso y bloques de almacenamiento.

- La virtualización VT-x o AMD-v debe estar habilitada en el BIOS del equipo.

## <a name="install-dependencies"></a>Instalar dependencias

1. Instale [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

1. Instale Python 3:
   - Si falta pip, descargue [get-clspip.py](https://bootstrap.pypa.io/get-pip.py) y ejecute `python get-pip.py`.
   - Instale el paquete de solicitudes mediante `python -m pip install requests`.

1. Si aún no tiene un hipervisor instalado, instale uno ahora.
   - En OS X, instale [xhyve driver](https://git.k8s.io/minikube/docs/drivers.md), [VirtualBox](https://www.virtualbox.org/wiki/Downloads) o [VMware Fusion](https://www.vmware.com/products/fusion).
   - En Linux, instale [VirtualBox](https://www.virtualbox.org/wiki/Downloads) o [KVM](https://www.linux-kvm.org/).
   - En Windows, instale [VirtualBox](https://www.virtualbox.org/wiki/Downloads) o [Hyper-V](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_install). Si no tiene un conmutador externo configurado en Hyper-V, cree uno con acceso de red externo.  Vea cómo [crear un conmutador externo en Hyper-V para Minikube](https://blogs.msdn.microsoft.com/wasimbloch/2017/01/23/setting-up-kubernetes-on-windows10-laptop-with-minikube/).

## <a name="install-minikube"></a>Instalación de Minikube

Instale Minikube conforme a las instrucciones de la [versión v0.28.2](https://github.com/kubernetes/minikube/releases/tag/v0.28.2). El clúster de macrodatos de SQL Server 2019 (versión preliminar) solo funciona con la versión v0.24.1 y posterior.

## <a name="create-a-minikube-cluster"></a>Creación de un clúster de Minikube

El comando siguiente crea un clúster de Minikube en una máquina virtual de Hyper-V con 8 CPU, 28 GB de memoria y un tamaño de disco de 100 GB. El tamaño de disco no es espacio reservado.  Aumenta a ese tamaño en disco según sea necesario.  Se recomienda no cambiar el espacio en disco a un valor inferior a 100 GB, ya que durante las pruebas se han experimentado problemas con eso. También especifica el conmutador de Hyper-V con acceso externo de forma explícita.

Cambie parámetros como **--memory** según sea necesario en función del hardware disponible y del hipervisor que se use.  Asegúrese de que el valor del parámetro de conmutador virtual **--hyper-v** coincida con el nombre usado al crear el conmutador virtual.

```bash
minikube start --vm-driver="hyperv" --cpus 8 --memory 28672 --disk-size 100g --hyperv-virtual-switch "External"
```

Si usa Minikube con VirtualBox, el comando tendría este aspecto:

```base
minikube start --cpus 8 --memory 28672 --disk-size 100g
```

## <a name="disable-automatic-checkpoint-with-hyper-v"></a>Deshabilitar el punto de comprobación automático con Hyper-V

En Windows 10, el punto de comprobación automático está habilitado en una máquina virtual. Ejecute el comando siguiente en PowerShell para deshabilitar el punto de comprobación automático en la máquina virtual.

```PowerShell
Set-VM -Name minikube -CheckpointType Disabled -AutomaticCheckpointsEnabled $false
```

## <a name="next-steps"></a>Pasos siguientes

En los pasos de este artículo se ha configurado un clúster de Minikube. El siguiente paso es implementar un clúster de macrodatos de SQL Server 2019. Para obtener instrucciones, vea el siguiente artículo:

[Implementación de clústeres de macrodatos de SQL Server 2019 en Kubernetes](deployment-guidance.md#deploy)
